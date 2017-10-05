---
title: "Azure Stream Analytics 및 Machine Learning 통합 | Microsoft Azure"
description: "Stream Analytics 작업에서 사용자 정의 함수 및 Machine Learning을 사용하는 방법"
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
ms.openlocfilehash: 023033d5479fcf0e2dff168b6604431eef283d3b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a><span data-ttu-id="fad5e-103">Azure Stream Analytics 및 Azure Machine Learning을 사용한 감정 분석 수행</span><span class="sxs-lookup"><span data-stu-id="fad5e-103">Performing sentiment analysis by using Azure Stream Analytics and Azure Machine Learning</span></span>
<span data-ttu-id="fad5e-104">이 문서에서는 Azure Machine Learning을 통합하는 간단한 Azure Stream Analytics 작업을 신속하게 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-104">This article describes how to quickly set up a simple Azure Stream Analytics job that integrates Azure Machine Learning.</span></span> <span data-ttu-id="fad5e-105">Cortana Intelligence 갤러리의 Machine Learning 감정 분석 모델을 사용하여 실시간으로 스트리밍 텍스트 데이터를 분석하고 감정 점수를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-105">You use a Machine Learning sentiment analytics model from the Cortana Intelligence Gallery to analyze streaming text data and determine the sentiment score in real time.</span></span> <span data-ttu-id="fad5e-106">Cortana Intelligence Suite를 사용하면 감정 분석 모델 빌드에 대한 걱정없이 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-106">Using the Cortana Intelligence Suite lets you accomplish this task without worrying about the intricacies of building a sentiment analytics model.</span></span>

<span data-ttu-id="fad5e-107">문서에서 알아본 내용을 다음과 같은 시나리오에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-107">You can apply what you learn from this article to scenarios such as these:</span></span>

* <span data-ttu-id="fad5e-108">스트리밍 Twitter 데이터에 대한 실시간 감정 분석</span><span class="sxs-lookup"><span data-stu-id="fad5e-108">Analyzing real-time sentiment on streaming Twitter data.</span></span>
* <span data-ttu-id="fad5e-109">지원 담당자와 고객 채팅 레코드 분석</span><span class="sxs-lookup"><span data-stu-id="fad5e-109">Analyzing records of customer chats with support staff.</span></span>
* <span data-ttu-id="fad5e-110">포럼, 블로그 및 동영상에 대한 의견 평가</span><span class="sxs-lookup"><span data-stu-id="fad5e-110">Evaluating comments on forums, blogs, and videos.</span></span> 
* <span data-ttu-id="fad5e-111">기타 실시간 예측 점수 매기기 시나리오</span><span class="sxs-lookup"><span data-stu-id="fad5e-111">Many other real-time, predictive scoring scenarios.</span></span>

<span data-ttu-id="fad5e-112">실제 시나리오에서는 Twitter 데이터 스트림에서 직접 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-112">In a real-world scenario, you would get the data directly from a Twitter data stream.</span></span> <span data-ttu-id="fad5e-113">자습서를 단순화하기 Stream Analytics 작업이 Azure Blob Storage에서 CSV 파일의 트윗을 가져오도록 작성했습니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-113">To simplify the tutorial, we've written it so that the Streaming Analytics job gets tweets from a CSV file in Azure Blob storage.</span></span> <span data-ttu-id="fad5e-114">고유한 CSV 파일을 만들거나 다음 이미지에 나와 있는 것처럼 샘플 CSV 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-114">You can create your own CSV file, or you can use a sample CSV file, as shown in the following image:</span></span>

![CSV 파일에서 샘플 트윗](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

<span data-ttu-id="fad5e-116">사용자가 만든 Stream Analytics 작업은 감정 분석 모델을 Blob Storage의 샘플 텍스트에 UDF(사용자 정의 함수)로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-116">The Streaming Analytics job that you create applies the sentiment analytics model as a user-defined function (UDF) on the sample text data from the blob store.</span></span> <span data-ttu-id="fad5e-117">출력(감정 분석의 결과)은 다른 CSV 파일에 있는 동일한 Blob Storage에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-117">The output (the result of the sentiment analysis) is written to the same blob store in a different CSV file.</span></span> 

<span data-ttu-id="fad5e-118">다음 그림은 이러한 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-118">The following figure demonstrates this configuration.</span></span> <span data-ttu-id="fad5e-119">언급한 대로 좀 더 현실적인 시나리오에서는 Blob Storage를 Azure Event Hubs 입력의 스트리밍 Twitter 데이터로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-119">As noted, for a more realistic scenario, you can replace blob storage with streaming Twitter data from an Azure Event Hubs input.</span></span> <span data-ttu-id="fad5e-120">또한 종합 정서의 [Microsoft Power BI](https://powerbi.microsoft.com/) 실시간 시각화를 빌드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-120">Additionally, you could build a [Microsoft Power BI](https://powerbi.microsoft.com/) real-time visualization of the aggregate sentiment.</span></span>    

![Stream Analytics Machine Learning 통합 개요](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a><span data-ttu-id="fad5e-122">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fad5e-122">Prerequisites</span></span>
<span data-ttu-id="fad5e-123">시작하기 전에 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-123">Before you start, make sure you have the following:</span></span>

* <span data-ttu-id="fad5e-124">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="fad5e-124">An active Azure subscription.</span></span>
* <span data-ttu-id="fad5e-125">데이터가 포함된 CSV 파일.</span><span class="sxs-lookup"><span data-stu-id="fad5e-125">A CSV file with some data in it.</span></span> <span data-ttu-id="fad5e-126">[GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv)에서 이전에 표시된 파일을 다운로드하거나 고유한 파일을 직접 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-126">You can download the file shown earlier from [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), or you can create your own file.</span></span> <span data-ttu-id="fad5e-127">이 문서의 경우 GitHub의 파일을 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-127">For this article, we assume that you're using the file from GitHub.</span></span>

<span data-ttu-id="fad5e-128">좀 더 높은 수준에서 이 문서에 설명된 작업을 완료하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-128">At a high level, to complete the tasks demonstrated in this article, you do the following:</span></span>

1. <span data-ttu-id="fad5e-129">Azure Storage 계정 및 Blob Storage 컨테이너를 만들고 컨테이너에 CSV로 포맷된 입력 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-129">Create an Azure storage account and a blob storage container, and upload a CSV-formatted input file to the container.</span></span>
3. <span data-ttu-id="fad5e-130">Cortana Intelligence 갤러리의 감정 분석 모델을 Azure Machine Learning 작업 영역에 추가하고 이 모델을 Azure Machine Learning 작업 영역의 웹 서비스로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-130">Add a sentiment analytics model from the Cortana Intelligence Gallery to your Azure Machine Learning workspace and deploy this model as a web service in the Machine Learning workspace.</span></span>
5. <span data-ttu-id="fad5e-131">텍스트 입력의 감정을 결정하기 위해 이 웹 서비스를 함수로 호출하는 Stream Analytics 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-131">Create a Stream Analytics job that calls this web service as a function in order to determine sentiment for the text input.</span></span>
6. <span data-ttu-id="fad5e-132">Stream Analytics 작업을 시작하고 출력을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-132">Start the Stream Analytics job and check the output.</span></span>

## <a name="create-a-storage-container-and-upload-the-csv-input-file"></a><span data-ttu-id="fad5e-133">저장소 컨테이너 만들기 및 CSV 입력 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="fad5e-133">Create a storage container and upload the CSV input file</span></span>
<span data-ttu-id="fad5e-134">이 단계의 경우 GitHub에서 사용할 수 있는 파일과 같은 모든 CSV 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-134">For this step, you can use any CSV file, such as the one available from GitHub.</span></span>

1. <span data-ttu-id="fad5e-135">Azure Portal에서 **새로 만들기** &gt; **저장소** &gt; **저장소 계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-135">In the Azure portal, click **New** &gt; **Storage** &gt; **Storage account**.</span></span>

   ![새 저장소 계정 만들기](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. <span data-ttu-id="fad5e-137">이름을 입력합니다(`samldemo` 예제에서).</span><span class="sxs-lookup"><span data-stu-id="fad5e-137">Provide a name (`samldemo` in the example).</span></span> <span data-ttu-id="fad5e-138">이름으로 소문자 및 숫자만 사용할 수 있으며 Azure 전체에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-138">The name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 

3. <span data-ttu-id="fad5e-139">기존 리소스 그룹을 지정하고 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-139">Specify an existing resource group and specify a location.</span></span> <span data-ttu-id="fad5e-140">위치의 경우 이 자습서에서 만든 모든 리소스가 동일한 위치를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-140">For location, we recommend that all the resources created in this tutorial use the same location.</span></span>

    ![저장소 계정 세부 정보 입력](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. <span data-ttu-id="fad5e-142">Azure Portal에서 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-142">In the Azure portal, select the storage account.</span></span> <span data-ttu-id="fad5e-143">저장소 계정 블레이드에서 **컨테이너**를 클릭하고 **+&nbsp;컨테이너**를 클릭하여 Blob Storage를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-143">In the storage account blade, click **Containers** and then click **+&nbsp;Container** to create blob storage.</span></span>

    ![Blob 컨테이너 만들기](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. <span data-ttu-id="fad5e-145">컨테이너에 이름(이 예에서 `azuresamldemoblob`)을 입력하고 **액세스 형식**이 **Blob**으로 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-145">Provide a name for the container (`azuresamldemoblob` in the example) and verify that **Access type** is set to **Blob**.</span></span> <span data-ttu-id="fad5e-146">완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-146">When you're done, click **OK**.</span></span>

    ![Blob 컨테이너 정보 지정](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. <span data-ttu-id="fad5e-148">**컨테이너** 블레이드에서 새 컨테이너를 선택합니다. 그러면 해당 컨테이너의 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-148">In the **Containers** blade, select the new container, which opens the blade for that container.</span></span>

7. <span data-ttu-id="fad5e-149">**업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-149">Click **Upload**.</span></span>

    ![컨테이너의 '업로드' 단추](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. <span data-ttu-id="fad5e-151">**Blob 업로드** 블레이드에서 이 자습서에 사용하려는 CSV 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-151">In the **Upload blob** blade, specify the CSV file that you want to use for this tutorial.</span></span> <span data-ttu-id="fad5e-152">**Blob 형식**에서 **블록 Blob**을 선택하고 블록 크기를 4MB로 설정합니다. 그러면 이 자습서에 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-152">For **Blob type**, select **Block blob** and set the block size to 4 MB, which is sufficient for this tutorial.</span></span>

    ![Blob 파일 업로드](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. <span data-ttu-id="fad5e-154">블레이드 맨 아래에 있는 **업로드** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-154">Click the **Upload** button at the bottom of the blade.</span></span>

## <a name="add-the-sentiment-analytics-model-from-the-cortana-intelligence-gallery"></a><span data-ttu-id="fad5e-155">Cortana Intelligence Gallery의 정서 분석 모델 추가</span><span class="sxs-lookup"><span data-stu-id="fad5e-155">Add the sentiment analytics model from the Cortana Intelligence Gallery</span></span>

<span data-ttu-id="fad5e-156">이제 Blob에 샘플 데이터가 있으므로 Cortana Intelligence Gallery에서 감정 분석 모델을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-156">Now that the sample data is in a blob, you can enable the sentiment analysis model in Cortana Intelligence Gallery.</span></span>

1. <span data-ttu-id="fad5e-157">Cortana Intelligence Gallery에서 [예측 감정 분석 모델](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-157">Go to the [predictive sentiment analytics model](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) page in the Cortana Intelligence Gallery.</span></span>  

2. <span data-ttu-id="fad5e-158">**Studio에서 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-158">Click **Open in Studio**.</span></span>  
   
   ![Stream Analytics Machine Learning, Machine Learning 스튜디오 열기](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. <span data-ttu-id="fad5e-160">로그인하여 작업 영역으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-160">Sign in to go to the workspace.</span></span> <span data-ttu-id="fad5e-161">위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-161">Select a location.</span></span>

4. <span data-ttu-id="fad5e-162">페이지 아래쪽에서 **실행** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-162">Click **Run** at the bottom of the page.</span></span> <span data-ttu-id="fad5e-163">프로세스가 실행되려면 약 1분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-163">The process runs, which takes about a minute.</span></span>

   ![Machine Learning Studio에서 실험 실행](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. <span data-ttu-id="fad5e-165">프로세스를 성공적으로 실행한 후에 페이지의 맨 아래에서 **웹 서비스 배포**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-165">After the process has run successfully, select **Deploy Web Service** at the bottom of the page.</span></span>

   ![Machine Learning Studio에서 실험을 웹 서비스로 배포](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. <span data-ttu-id="fad5e-167">감성 분석 모델을 사용할 수 있는지 유효성을 검사하려면 **테스트** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-167">To validate that the sentiment analytics model is ready to use, click the **Test** button.</span></span> <span data-ttu-id="fad5e-168">"I love Microsoft"와 같은 텍스트를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-168">Provide text input such as "I love Microsoft".</span></span> 

   ![Machine Learning Studio에서 실험 테스트](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    <span data-ttu-id="fad5e-170">테스트가 작동하면 다음 예제와 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-170">If the test works, you see a result similar to the following example:</span></span>

   ![Machine Learning Studio의 결과 테스트](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. <span data-ttu-id="fad5e-172">**앱** 열에서 **Excel 2010 또는 이전 통합 문서** 링크를 클릭하여 Excel 통합 문서를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-172">In the **Apps** column, click the **Excel 2010 or earlier workbook** link to download an Excel workbook.</span></span> <span data-ttu-id="fad5e-173">통합 문서는 나중에 Stream Analytics 작업을 설정하는 데 필요한 API 키와 URL을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-173">The workbook contains the an API key and the URL that you need later to set up the Stream Analytics job.</span></span>

    ![Stream Analytics Machine Learning, 간략 상태](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-the-machine-learning-model"></a><span data-ttu-id="fad5e-175">Machine Learning 모델을 사용하는 Stream Analytics 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="fad5e-175">Create a Stream Analytics job that uses the Machine Learning model</span></span>

<span data-ttu-id="fad5e-176">이제 CSV 파일에서 Blob Storage로의 샘플 트윗을 읽을 수 있는 Stream Analytics 작업을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-176">You can now create a Stream Analytics job that reads the sample tweets from the CSV file in blob storage.</span></span> 

### <a name="create-the-job"></a><span data-ttu-id="fad5e-177">작업 만들기</span><span class="sxs-lookup"><span data-stu-id="fad5e-177">Create the job</span></span>

1. <span data-ttu-id="fad5e-178">[Azure 포털](https://portal.azure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-178">Go to the [Azure portal](https://portal.azure.com).</span></span>  

2. <span data-ttu-id="fad5e-179">**새로 만들기** > **사물 인터넷** > **Stream Analytics 작업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-179">Click **New** > **Internet of Things** > **Stream Analytics job**.</span></span> 

   ![새 Stream Analytics 작업의 Azure Portal 경로](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. <span data-ttu-id="fad5e-181">`azure-sa-ml-demo`의 작업 이름을 지정하고, 구독을 지정하고, 기존 리소스 그룹을 지정하거나 새 리소스 그룹을 만들고, 작업의 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-181">Name the job `azure-sa-ml-demo`, specify a subscription, specify an existing resource group or create a new one, and select the location for the job.</span></span>

   ![새 Stream Analytics 작업의 설정 지정](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-the-job-input"></a><span data-ttu-id="fad5e-183">작업 입력 구성</span><span class="sxs-lookup"><span data-stu-id="fad5e-183">Configure the job input</span></span>
<span data-ttu-id="fad5e-184">작업은 이전에 업로드한 CSV 파일에서 Blob Storage로 해당 입력을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-184">The job gets its input from the CSV file that you uploaded earlier to blob storage.</span></span>

1. <span data-ttu-id="fad5e-185">작업이 만들어진 후에 작업 블레이드의 **작업 토폴로지** 아래에서 **입력** 상자를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-185">After the job has been created, under **Job Topology** in the job blade, click the **Inputs** box.</span></span>  
   
   ![Stream Analytics 작업 블레이드의 '입력' 상자](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. <span data-ttu-id="fad5e-187">**입력** 블레이드에서 **+ 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-187">In the **Inputs** blade, click **+ Add**.</span></span>

   ![Stream Analytics 작업에 입력을 추가하는 '추가' 단추](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. <span data-ttu-id="fad5e-189">다음과 같은 값으로 **새 입력** 블레이드를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-189">Fill out the **New input** blade with these values:</span></span>

    * <span data-ttu-id="fad5e-190">**입력 별칭**: 이름으로 `datainput`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-190">**Input alias**: Use the name `datainput`.</span></span>
    * <span data-ttu-id="fad5e-191">**원본 형식**: **데이터 스트림**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-191">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="fad5e-192">**원본**: **Blob Storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-192">**Source**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="fad5e-193">**가져오기 옵션**: **현재 구독의 Blob Storage 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-193">**Import option**: Select **Use blob storage from current subscription**.</span></span> 
    * <span data-ttu-id="fad5e-194">**저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="fad5e-194">**Storage account**.</span></span> <span data-ttu-id="fad5e-195">이전에 만든 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-195">Select the storage account you created earlier.</span></span>
    * <span data-ttu-id="fad5e-196">**컨테이너**.</span><span class="sxs-lookup"><span data-stu-id="fad5e-196">**Container**.</span></span> <span data-ttu-id="fad5e-197">앞에서 만든 컨테이너를 선택합니다(`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="fad5e-197">Select the container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="fad5e-198">**이벤트 직렬화 형식**</span><span class="sxs-lookup"><span data-stu-id="fad5e-198">**Event serialization format**.</span></span> <span data-ttu-id="fad5e-199">**CSV**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-199">Select **CSV**.</span></span>

    ![새 작업 입력의 설정](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. <span data-ttu-id="fad5e-201">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-201">Click **Create**.</span></span>

### <a name="configure-the-job-output"></a><span data-ttu-id="fad5e-202">작업 출력 구성</span><span class="sxs-lookup"><span data-stu-id="fad5e-202">Configure the job output</span></span>
<span data-ttu-id="fad5e-203">작업은 입력을 가져오는 동일한 Blob Storage에 결과를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-203">The job sends results to the same blob storage where it gets input.</span></span> 

1. <span data-ttu-id="fad5e-204">작업 블레이드의 **작업 토폴로지** 아래에서 **출력** 상자를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-204">Under **Job Topology** in the job blade, click the **Outputs** box.</span></span>  
  
   ![Streaming Analytics 작업에 대한 새 출력 만들기](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. <span data-ttu-id="fad5e-206">**출력** 블레이드에서 **+ 추가**를 클릭한 다음 `datamloutput` 별칭인 출력을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-206">In the **Outputs** blade, click **+ Add**, and then add an output with the alias `datamloutput`.</span></span> 

3. <span data-ttu-id="fad5e-207">**싱크**에서 **Blob Storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-207">For **Sink**, select **Blob storage**.</span></span> <span data-ttu-id="fad5e-208">그런 다음 입력을 위한 Blob Storage에 사용한 동일한 값을 사용하여 나머지 출력 설정을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-208">Then fill in the rest of the output settings using the same values that you used for the blob storage for input:</span></span>

    * <span data-ttu-id="fad5e-209">**저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="fad5e-209">**Storage account**.</span></span> <span data-ttu-id="fad5e-210">이전에 만든 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-210">Select the storage account you created earlier.</span></span>
    * <span data-ttu-id="fad5e-211">**컨테이너**.</span><span class="sxs-lookup"><span data-stu-id="fad5e-211">**Container**.</span></span> <span data-ttu-id="fad5e-212">앞에서 만든 컨테이너를 선택합니다(`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="fad5e-212">Select the container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="fad5e-213">**이벤트 직렬화 형식**</span><span class="sxs-lookup"><span data-stu-id="fad5e-213">**Event serialization format**.</span></span> <span data-ttu-id="fad5e-214">**CSV**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-214">Select **CSV**.</span></span>

   ![새 작업 출력의 설정](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. <span data-ttu-id="fad5e-216">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-216">Click **Create**.</span></span>   


### <a name="add-the-machine-learning-function"></a><span data-ttu-id="fad5e-217">Machine Learning 함수 추가</span><span class="sxs-lookup"><span data-stu-id="fad5e-217">Add the Machine Learning function</span></span> 
<span data-ttu-id="fad5e-218">이전에 웹 서비스에 Machine Learning 모델을 게시했습니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-218">Earlier you published a Machine Learning model to a web service.</span></span> <span data-ttu-id="fad5e-219">이 시나리오에서는 Stream Analysis 작업이 실행될 때 감정 분석에 대한 샘플을 입력에서 웹 서비스로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-219">In our scenario, when the Stream Analysis job runs, it sends each sample tweet from the input to the web service for sentiment analysis.</span></span> <span data-ttu-id="fad5e-220">Machine Learning 웹 서비스는 감정(`positive`, `neutral` 또는 `negative`) 및 긍정적인 트윗의 확률을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-220">The Machine Learning web service returns a sentiment (`positive`, `neutral`, or `negative`) and a probability of the tweet being positive.</span></span> 

<span data-ttu-id="fad5e-221">자습서의 이 섹션에서는 Stream Analysis 작업의 함수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-221">In this section of the tutorial, you define a function in the Stream Analysis job.</span></span> <span data-ttu-id="fad5e-222">웹 서비스에 트윗을 보내고 응답을 다시 가져오기 위해 함수를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-222">The function can be invoked to send a tweet to the web service and get the response back.</span></span> 

1. <span data-ttu-id="fad5e-223">Excel 통합 문서의 앞부분에서 다운로드한 웹 서비스 URL 및 API 키가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-223">Make sure you have the web service URL and API key that you downloaded earlier in the Excel workbook.</span></span>

2. <span data-ttu-id="fad5e-224">작업 개요 블레이드에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-224">Return to the job overview blade.</span></span>

3. <span data-ttu-id="fad5e-225">**설정** 아래에서 **함수**를 선택하고 **+ 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-225">Under **Settings**, select **Functions** and then click **+ Add**.</span></span>

   ![Stream Analytics 작업에 함수 추가](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. <span data-ttu-id="fad5e-227">`sentiment`를 함수 별칭으로 입력하고 다음과 같은 값을 사용하여 블레이드의 나머지 부분을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-227">Enter `sentiment` as the function alias and fill out the rest of the blade using these values:</span></span>

    * <span data-ttu-id="fad5e-228">**함수 유형**: **Azure ML**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-228">**Function type**: Select **Azure ML**.</span></span>
    * <span data-ttu-id="fad5e-229">**가져오기 옵션**: **다른 구독에서 가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-229">**Import option**: Select **Import from a different subscription**.</span></span> <span data-ttu-id="fad5e-230">이렇게 하면 URL과 키를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-230">This gives you a chance to enter the URL and key.</span></span>
    * <span data-ttu-id="fad5e-231">**URL**: 웹 서비스 URL에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-231">**URL**: Paste in the web service URL.</span></span>
    * <span data-ttu-id="fad5e-232">**키**: API 키에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-232">**Key**: Paste in the API key.</span></span>
  
    ![Stream Analytics 작업에 Machine Learning 함수를 추가하는 설정](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. <span data-ttu-id="fad5e-234">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-234">Click **Create**.</span></span>

### <a name="create-a-query-to-transform-the-data"></a><span data-ttu-id="fad5e-235">데이터를 변환하는 쿼리 만들기</span><span class="sxs-lookup"><span data-stu-id="fad5e-235">Create a query to transform the data</span></span>

<span data-ttu-id="fad5e-236">Stream Analytics는 선언적인 SQL 기반 쿼리를 사용하여 입력을 검사하고 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-236">Stream Analytics uses a declarative, SQL-based query to examine the input and process it.</span></span> <span data-ttu-id="fad5e-237">이 섹션에서는 입력의 트윗을 읽고 Machine Learning 함수를 호출하여 감정 분석을 수행하는 쿼리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-237">In this section, you create a query that reads each tweet from input and then invokes the Machine Learning function to perform sentiment analysis.</span></span> <span data-ttu-id="fad5e-238">그런 다음 쿼리는 정의한 출력으로 결과를 보냅니다(Blob Storage).</span><span class="sxs-lookup"><span data-stu-id="fad5e-238">The query then sends the result to the output that you defined (blob storage).</span></span>

1. <span data-ttu-id="fad5e-239">작업 개요 블레이드에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-239">Return to the job overview blade.</span></span>

2.  <span data-ttu-id="fad5e-240">**작업 토폴로지**에서 **쿼리** 상자를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-240">Under **Job Topology**, click the **Query** box.</span></span>

    ![Streaming Analytics 작업에 쿼리 만들기](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. <span data-ttu-id="fad5e-242">다음 쿼리를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-242">Enter the following query:</span></span>

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    <span data-ttu-id="fad5e-243">쿼리는 입력의 트윗에 대한 감정 분석을 수행하기 위해 앞에서 만든 함수를 호출합니다(`sentiment`).</span><span class="sxs-lookup"><span data-stu-id="fad5e-243">The query invokes the function you created earlier (`sentiment`) in order to perform sentiment analysis on each tweet in the input.</span></span> 

4. <span data-ttu-id="fad5e-244">**저장** 을 클릭하여 쿼리를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-244">Click **Save** to save the query.</span></span>


## <a name="start-the-stream-analytics-job-and-check-the-output"></a><span data-ttu-id="fad5e-245">Stream Analytics 작업을 시작하고 출력을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-245">Start the Stream Analytics job and check the output</span></span>

<span data-ttu-id="fad5e-246">이제 Stream Analytics 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-246">You can now start the Stream Analytics job.</span></span>

### <a name="start-the-job"></a><span data-ttu-id="fad5e-247">작업 시작</span><span class="sxs-lookup"><span data-stu-id="fad5e-247">Start the job</span></span>
1. <span data-ttu-id="fad5e-248">작업 개요 블레이드에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-248">Return to the job overview blade.</span></span>

2. <span data-ttu-id="fad5e-249">블레이드 위쪽에서 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-249">Click **Start** at the top of the blade.</span></span>

    ![Streaming Analytics 작업에 쿼리 만들기](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. <span data-ttu-id="fad5e-251">**작업 시작**에서 **사용자 지정**을 선택한 다음 Blob Storage에 CSV 파일을 업로드하기 하루 전날을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-251">In the **Start job**, select **Custom**, and then select one day prior to when you uploaded the CSV file to blob storage.</span></span> <span data-ttu-id="fad5e-252">완료되면 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-252">When you're done, click **Start**.</span></span>  


### <a name="check-the-output"></a><span data-ttu-id="fad5e-253">출력 파일 확인</span><span class="sxs-lookup"><span data-stu-id="fad5e-253">Check the output</span></span>
1. <span data-ttu-id="fad5e-254">**모니터링** 상자에서 작업을 확인할 때까지 몇 분 동안 작업을 실행하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-254">Let the job run for a few minutes until you see activity in the **Monitoring** box.</span></span> 

2. <span data-ttu-id="fad5e-255">일반적으로 Blob Storage의 내용을 검사하는 데 사용하는 도구가 있는 경우 해당 도구를 사용하여 `azuresamldemoblob` 컨테이너를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-255">If you have a tool that you normally use to examine the contents of blob storage, use that tool to examine the `azuresamldemoblob` container.</span></span> <span data-ttu-id="fad5e-256">또는 Azure Portal에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-256">Alternatively, do the following steps in the Azure portal:</span></span>

    1. <span data-ttu-id="fad5e-257">포털에서 `samldemo` 저장소 계정을 찾고 계정 내에서 `azuresamldemoblob` 컨테이너를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-257">In the portal, find the `samldemo` storage account, and within the account, find the `azuresamldemoblob` container.</span></span> <span data-ttu-id="fad5e-258">컨테이너에 두 개의 파일이 표시됩니다. 하나는 샘플 트윗을 포함하는 파일이고 다른 하나는 Stream Analytics 작업에 의해 생성된 CSV 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-258">You see two files in the container: the file that contains the sample tweets and a CSV file generated by the Stream Analytics job.</span></span>
    2. <span data-ttu-id="fad5e-259">생성된 파일을 마우스 오른쪽 단추로 클릭한 다음 **다운로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-259">Right-click the generated file and then select **Download**.</span></span> 

   ![Blob Storage에서 CSV 작업 출력 다운로드](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. <span data-ttu-id="fad5e-261">생성된 CSV 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-261">Open the generated CSV file.</span></span> <span data-ttu-id="fad5e-262">다음 예제와 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-262">You see something like the following example:</span></span>  
   
   ![Stream Analytics Machine Learning, CSV 보기](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a><span data-ttu-id="fad5e-264">메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="fad5e-264">View metrics</span></span>
<span data-ttu-id="fad5e-265">또한 Azure Machine Learning 함수 관련 메트릭도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-265">You also can view Azure Machine Learning function-related metrics.</span></span> <span data-ttu-id="fad5e-266">다음 함수 관련 메트릭은 작업 블레이드의 **모니터링** 상자에서 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-266">The following function-related metrics are displayed in the **Monitoring** box in the job blade:</span></span>

* <span data-ttu-id="fad5e-267">**함수 요청** 은 Machine Learning 웹 서비스로 전송되는 요청 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-267">**Function Requests** indicates the number of requests sent to a Machine Learning web service.</span></span>  
* <span data-ttu-id="fad5e-268">**함수 이벤트** 는 요청의 이벤트 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-268">**Function Events** indicates the number of events in the request.</span></span> <span data-ttu-id="fad5e-269">기본적으로 Machine Learning 웹 서비스에 대한 각 요청에는 최대 1,000개의 이벤트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="fad5e-269">By default, each request to a Machine Learning web service contains up to 1,000 events.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="fad5e-270">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fad5e-270">Next steps</span></span>

* [<span data-ttu-id="fad5e-271">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="fad5e-271">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="fad5e-272">Azure 스트림 분석 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="fad5e-272">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="fad5e-273">REST API 및 Machine Learning 통합</span><span class="sxs-lookup"><span data-stu-id="fad5e-273">Integrate REST API and Machine Learning</span></span>](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [<span data-ttu-id="fad5e-274">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="fad5e-274">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)



