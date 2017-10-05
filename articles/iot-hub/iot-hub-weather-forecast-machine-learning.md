---
title: "Azure Machine Learning을 사용하여 IoT Hub 데이터로 일기 예보 | Microsoft Docs"
description: "Azure Machine Learning을 사용하여 IoT Hub가 센서에서 수집한 온도 및 습도 데이터를 기반으로 하여 강우 확률을 예측합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "일기 예보 기계 학습"
ms.assetid: 8ba7d9e7-699c-4448-b353-0f3e1429d198
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 50ae54b9476c49b80236e295c0bf244df8236cff
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="weather-forecast-using-the-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a><span data-ttu-id="7b200-104">Azure Machine Learning에서 IoT Hub의 센서 데이터를 사용한 일기 예보</span><span class="sxs-lookup"><span data-stu-id="7b200-104">Weather forecast using the sensor data from your IoT hub in Azure Machine Learning</span></span>

![종단 간 다이어그램](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="7b200-106">기계 학습은 컴퓨터에서 기존 데이터로부터 학습하여 미래 동작, 결과 및 추세를 예측하는 데 유용한 데이터 과학 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-106">Machine learning is a technique of data science that helps computers learn from existing data to forecast future behaviors, outcomes, and trends.</span></span> <span data-ttu-id="7b200-107">Azure Machine Learning은 예측 모델을 신속하게 만들고 분석 솔루션으로 배포할 수 있게 해주는 클라우드 예측 분석 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-107">Azure Machine Learning is a cloud predictive analytics service that makes it possible to quickly create and deploy predictive models as analytics solutions.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="7b200-108">학습 내용</span><span class="sxs-lookup"><span data-stu-id="7b200-108">What you learn</span></span>

<span data-ttu-id="7b200-109">Azure Machine Learning을 사용하여 Azure IoT Hub의 온도 및 습도 데이터를 통해 일기 예보(강우 확률)를 수행하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-109">You learn how to use Azure Machine Learning to do weather forecast (chance of rain) using the temperature and humidity data from your Azure IoT hub.</span></span> <span data-ttu-id="7b200-110">강우 확률은 준비된 날씨 예측 모델의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-110">The chance of rain is the output of a prepared weather prediction model.</span></span> <span data-ttu-id="7b200-111">모델에서는 기록 데이터를 기반으로 하여 온도 및 습도에 따라 강우 확률을 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-111">The model is built upon historic data to forecast chance of rain based on temperature and humidity.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="7b200-112">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="7b200-112">What you do</span></span>

- <span data-ttu-id="7b200-113">날씨 예측 모델을 웹 서비스로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-113">Deploy the weather prediction model as a web service.</span></span>
- <span data-ttu-id="7b200-114">소비자 그룹을 추가하여 IoT Hub에서 데이터 액세스 준비</span><span class="sxs-lookup"><span data-stu-id="7b200-114">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="7b200-115">Stream Analytics 작업을 만들고 해당 작업을 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-115">Create a Stream Analytics job and configure the job to:</span></span>
  - <span data-ttu-id="7b200-116">IoT Hub에서 온도 및 습도 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-116">Read temperature and humidity data from your IoT hub.</span></span>
  - <span data-ttu-id="7b200-117">웹 서비스를 호출하여 강우 확률을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-117">Call the web service to get the rain chance.</span></span>
  - <span data-ttu-id="7b200-118">Azure Blob 저장소에 결과를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-118">Save the result to an Azure blob storage.</span></span>
- <span data-ttu-id="7b200-119">Microsoft Azure Storage 탐색기를 사용하여 일기 예보를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-119">Use Microsoft Azure Storage Explorer to view the weather forecast.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7b200-120">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="7b200-120">What you need</span></span>

- <span data-ttu-id="7b200-121">다음 요구 사항을 다루는 자습서 [장치 설정](iot-hub-raspberry-pi-kit-node-get-started.md) 완료:</span><span class="sxs-lookup"><span data-stu-id="7b200-121">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="7b200-122">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="7b200-122">An active Azure subscription.</span></span>
  - <span data-ttu-id="7b200-123">구독 중인 Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="7b200-123">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="7b200-124">메시지를 Azure IoT Hub로 보내는 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="7b200-124">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="7b200-125">Azure Machine Learning Studio 계정</span><span class="sxs-lookup"><span data-stu-id="7b200-125">An Azure Machine Learning Studio account.</span></span> <span data-ttu-id="7b200-126">[Machine Learning Studio 체험해 보기](https://studio.azureml.net/)</span><span class="sxs-lookup"><span data-stu-id="7b200-126">([Try Machine Learning Studio for free](https://studio.azureml.net/)).</span></span>

## <a name="deploy-the-weather-prediction-model-as-a-web-service"></a><span data-ttu-id="7b200-127">날씨 예측 모델을 웹 서비스로 배포</span><span class="sxs-lookup"><span data-stu-id="7b200-127">Deploy the weather prediction model as a web service</span></span>

1. <span data-ttu-id="7b200-128">[날씨 예측 모델 페이지](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-128">Go to the [weather prediction model page](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span></span>
1. <span data-ttu-id="7b200-129">Microsoft Azure Machine Learning Studio에서 **Studio에서 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-129">Click **Open in Studio** in Microsoft Azure Machine Learning Studio.</span></span>
   <span data-ttu-id="7b200-130">![Cortana Intelligence 갤러리에서 날씨 예측 모델 페이지 열기](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span><span class="sxs-lookup"><span data-stu-id="7b200-130">![Open the weather prediction model page in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span></span>
1. <span data-ttu-id="7b200-131">**실행**을 클릭하여 모델의 단계에 대한 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-131">Click **Run** to validate the steps in the model.</span></span> <span data-ttu-id="7b200-132">이 단계를 완료하는 데 2분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-132">This step might take 2 minutes to complete.</span></span>
   <span data-ttu-id="7b200-133">![Azure Machine Learning Studio에서 날씨 예측 모델 열기](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="7b200-133">![Open the weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="7b200-134">**웹 서비스 설정** > **예측형 웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-134">Click **SET UP WEB SERVICE** > **Predictive Web Service**.</span></span>
   <span data-ttu-id="7b200-135">![Azure Machine Learning Studio에 날씨 예측 모델 배포](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="7b200-135">![Deploy the weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="7b200-136">다이어그램에서 **웹 서비스 입력** 모듈을 **모델 점수 매기기** 모듈 근처로 끌어갑니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-136">In the diagram, drag the **Web service input** module somewhere near the **Score Model** module.</span></span>
1. <span data-ttu-id="7b200-137">**웹 서비스 입력** 모듈을 **모델 점수 매기기** 모듈에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-137">Connect the **Web service input** module to the **Score Model** module.</span></span>
   <span data-ttu-id="7b200-138">![Azure Machine Learning Studio에서 두 모듈 연결](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="7b200-138">![Connect two modules in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="7b200-139">**실행**을 클릭하여 모델의 단계에 대한 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-139">Click **RUN** to validate the steps in the model.</span></span>
1. <span data-ttu-id="7b200-140">**웹 서비스 배포**를 클릭하여 모델을 웹 서비스로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-140">Click **DEPLOY WEB SERVICE** to deploy the model as a web service.</span></span>
1. <span data-ttu-id="7b200-141">모델의 대시보드에서 **요청/응답**에 대한 **Excel 2010 또는 이전 통합 문서**를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-141">On the dashboard of the model, download the **Excel 2010 or earlier workbook** for **REQUEST/RESPONSE**.</span></span>

   > [!Note]
   > <span data-ttu-id="7b200-142">컴퓨터에서 최신 버전의 Excel을 실행하더라도 **Excel 2010 또는 이전 통합 문서**를 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-142">Ensure that you download the **Excel 2010 or earlier workbook** even if you are running a later version of Excel on your computer.</span></span>

   ![REQUEST RESPONSE 끝점에 대한 Excel 다운로드](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. <span data-ttu-id="7b200-144">Excel 통합 문서를 열고 **웹 서비스 URL** 및 **액세스 키**를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-144">Open the Excel workbook, make a note of the **WEB SERVICE URL** and **ACCESS KEY**.</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="7b200-145">Stream Analytics 작업 만들기, 구성 및 실행</span><span class="sxs-lookup"><span data-stu-id="7b200-145">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="7b200-146">Stream Analytics 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="7b200-146">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="7b200-147">[Azure Portal](https://ms.portal.azure.com/)에서 **새로 만들기** > **사물 인터넷** > **Stream Analytics 작업**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-147">In the [Azure portal](https://ms.portal.azure.com/), click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>
1. <span data-ttu-id="7b200-148">작업에 대한 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-148">Enter the following information for the job.</span></span>

   <span data-ttu-id="7b200-149">**작업 이름**: 작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-149">**Job name**: The name of the job.</span></span> <span data-ttu-id="7b200-150">이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-150">The name must be globally unique.</span></span>

   <span data-ttu-id="7b200-151">**리소스 그룹**: IoT Hub에서 사용하는 것과 동일한 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-151">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="7b200-152">**위치**: 리소스 그룹과 동일한 위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-152">**Location**: Use the same location as your resource group.</span></span>

   <span data-ttu-id="7b200-153">**대시보드에 고정**: 대시보드에서 IoT Hub에 쉽게 액세스하려면 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-153">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Azure에서 Stream Analytics 작업 만들기](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="7b200-155">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-155">Click **Create**.</span></span>

### <a name="add-an-input-to-the-stream-analytics-job"></a><span data-ttu-id="7b200-156">Stream Analytics 작업에 입력 추가</span><span class="sxs-lookup"><span data-stu-id="7b200-156">Add an input to the Stream Analytics job</span></span>

1. <span data-ttu-id="7b200-157">Stream Analytics 작업을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-157">Open the Stream Analytics job.</span></span>
1. <span data-ttu-id="7b200-158">**작업 토폴로지**에서 **입력**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-158">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="7b200-159">**입력** 창에서 **추가**를 클릭하고 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-159">In the **Inputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="7b200-160">**입력 별칭**: 입력에 대한 고유 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-160">**Input alias**: The unique alias for the input.</span></span>

   <span data-ttu-id="7b200-161">**원본**: **IoT Hub**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-161">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="7b200-162">**소비자 그룹**: 만든 소비자 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-162">**Consumer group**: Select the consumer group you created.</span></span>

   ![Azure에서 Stream Analytics 작업에 입력 추가](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. <span data-ttu-id="7b200-164">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-164">Click **Create**.</span></span>

### <a name="add-an-output-to-the-stream-analytics-job"></a><span data-ttu-id="7b200-165">Stream Analytics 작업에 출력 추가</span><span class="sxs-lookup"><span data-stu-id="7b200-165">Add an output to the Stream Analytics job</span></span>

1. <span data-ttu-id="7b200-166">**작업 토폴로지**에서 **출력**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-166">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="7b200-167">**출력** 창에서 **추가**를 클릭하고 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-167">In the **Outputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="7b200-168">**출력 별칭**: 출력에 대한 고유 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-168">**Output alias**: The unique alias for the output.</span></span>

   <span data-ttu-id="7b200-169">**싱크**: **Blob Storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-169">**Sink**: Select **Blob Storage**.</span></span>

   <span data-ttu-id="7b200-170">**저장소 계정**: Blob 저장소의 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-170">**Storage account**: The storage account for your blob storage.</span></span> <span data-ttu-id="7b200-171">저장소 계정을 만들거나 기존 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-171">You can create a storage account or use an existing one.</span></span>

   <span data-ttu-id="7b200-172">**컨테이너**: Blob이 저장되는 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-172">**Container**: The container where the blob is saved.</span></span> <span data-ttu-id="7b200-173">컨테이너를 만들거나 기존 컨테이너를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-173">You can create a container or use an existing one.</span></span>

   <span data-ttu-id="7b200-174">**이벤트 직렬화 형식**: **CSV**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-174">**Event serialization format**: Select **CSV**.</span></span>

   ![Azure에서 Stream Analytics 작업에 출력 추가](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. <span data-ttu-id="7b200-176">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-176">Click **Create**.</span></span>

### <a name="add-a-function-to-the-stream-analytics-job-to-call-the-web-service-you-deployed"></a><span data-ttu-id="7b200-177">Stream Analytics 작업에 배포된 웹 서비스를 호출하는 함수 추가</span><span class="sxs-lookup"><span data-stu-id="7b200-177">Add a function to the Stream Analytics job to call the web service you deployed</span></span>

1. <span data-ttu-id="7b200-178">**작업 토폴로지**에서 **함수** > **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-178">Under **Job Topology**, click **Functions** > **Add**.</span></span>
1. <span data-ttu-id="7b200-179">다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-179">Enter the following information:</span></span>

   <span data-ttu-id="7b200-180">**별칭 함수**: `machinelearning`을(를) 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-180">**Function Alias**: Enter `machinelearning`.</span></span>

   <span data-ttu-id="7b200-181">**함수 유형**: **Azure ML**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-181">**Function Type**: Select **Azure ML**.</span></span>

   <span data-ttu-id="7b200-182">**가져오기 옵션**: **다른 구독에서 가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-182">**Import option**: Select **Import from a different subscription**.</span></span>

   <span data-ttu-id="7b200-183">**URL**: Excel 통합 문서에서 기록해 둔 웹 서비스 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-183">**URL**: Enter the WEB SERVICE URL that you noted down from the Excel workbook.</span></span>

   <span data-ttu-id="7b200-184">**키**: Excel 통합 문서에서 기록해 둔 액세스 키를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-184">**Key**: Enter the ACCESS KEY that you noted down from the Excel workbook.</span></span>

   ![Azure에서 Stream Analytics 작업에 함수 추가](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. <span data-ttu-id="7b200-186">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-186">Click **Create**.</span></span>

### <a name="configure-the-query-of-the-stream-analytics-job"></a><span data-ttu-id="7b200-187">Stream Analytics 작업의 쿼리 구성</span><span class="sxs-lookup"><span data-stu-id="7b200-187">Configure the query of the Stream Analytics job</span></span>

1. <span data-ttu-id="7b200-188">**작업 토폴로지**에서 **쿼리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-188">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="7b200-189">기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-189">Replace the existing code with the following code:</span></span>

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   <span data-ttu-id="7b200-190">`[YourInputAlias]`를 작업의 입력 별칭으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-190">Replace `[YourInputAlias]` with the input alias of the job.</span></span>

   <span data-ttu-id="7b200-191">`[YourOutputAlias]`를 작업의 출력 별칭으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-191">Replace `[YourOutputAlias]` with the output alias of the job.</span></span>

1. <span data-ttu-id="7b200-192">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-192">Click **Save**.</span></span>

### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="7b200-193">스트림 분석 작업 실행</span><span class="sxs-lookup"><span data-stu-id="7b200-193">Run the Stream Analytics job</span></span>

<span data-ttu-id="7b200-194">Stream Analytics 작업에서 **시작** > **지금 시작** > **시작**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-194">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="7b200-195">작업이 성공적으로 시작되면 작업 상태가 **중지됨**에서 **실행 중**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-195">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span></span>

![스트림 분석 작업 실행](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-to-view-the-weather-forecast"></a><span data-ttu-id="7b200-197">Microsoft Azure Storage 탐색기를 사용하여 일기 예보 보기</span><span class="sxs-lookup"><span data-stu-id="7b200-197">Use Microsoft Azure Storage Explorer to view the weather forecast</span></span>

<span data-ttu-id="7b200-198">클라이언트 응용 프로그램을 실행하여 온도 및 습도 데이터를 수집하여 IoT Hub로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-198">Run the client application to start collecting and sending temperature and humidity data to your IoT hub.</span></span> <span data-ttu-id="7b200-199">Stream Analytics 작업에서는 IoT Hub에서 받은 각 메시지에 대해 일기 예보 웹 서비스를 호출하여 강우 확률을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-199">For each message that your IoT hub receives, the Stream Analytics job calls the weather forecast web service to produce the chance of rain.</span></span> <span data-ttu-id="7b200-200">그런 다음 Azure Blob 저장소에 결과를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-200">The result is then saved to your Azure blob storage.</span></span> <span data-ttu-id="7b200-201">Azure Storage 탐색기는 결과를 보는 데 사용할 수 있는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-201">Azure Storage Explorer is a tool that you can use to view the result.</span></span>

1. <span data-ttu-id="7b200-202">[Microsoft Azure Storage 탐색기를 다운로드하고 설치합니다](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="7b200-202">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
1. <span data-ttu-id="7b200-203">Azure Storage 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-203">Open Azure Storage Explorer.</span></span>
1. <span data-ttu-id="7b200-204">Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-204">Sign in to your Azure account.</span></span>
1. <span data-ttu-id="7b200-205">사용 중인 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-205">Select your subscription.</span></span>
1. <span data-ttu-id="7b200-206">구독> **저장소 계정** > 저장소 계정> **Blob 컨테이너**> 컨테이너를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-206">Click your subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span></span>
1. <span data-ttu-id="7b200-207">.csv 파일을 열어 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-207">Open a .csv file to see the result.</span></span> <span data-ttu-id="7b200-208">마지막 열은 강우 확률을 기록하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-208">The last column records the chance of rain.</span></span>

   ![Azure Machine Learning을 사용하여 일기 예보 결과 가져오기](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a><span data-ttu-id="7b200-210">요약</span><span class="sxs-lookup"><span data-stu-id="7b200-210">Summary</span></span>

<span data-ttu-id="7b200-211">Azure Machine Learning을 사용하여 IoT Hub에서 받은 온도 및 습도 데이터를 기반으로 하여 강우 확률을 생성했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b200-211">You’ve successfully used Azure Machine Learning to produce the chance of rain based on the temperature and humidity data that your IoT hub receives.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]