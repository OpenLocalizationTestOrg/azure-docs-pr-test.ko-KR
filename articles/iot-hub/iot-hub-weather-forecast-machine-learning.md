---
title: "Azure 기계 학습을 사용 하 여 IoT 허브에서 데이터와 예측 aaaWeather | Microsoft Docs"
description: "Azure 기계 학습 hello 온도 및 습도에 따라 비 toopredict hello 가능성이 IoT 허브는 센서에서 수집 된 데이터를 사용 합니다."
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
ms.openlocfilehash: 04abe97558ccfc152bae2e0d435033433c0023dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="weather-forecast-using-hello-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a><span data-ttu-id="e57f5-104">IoT 허브에서 hello 센서 데이터를 사용 하 여 Azure 기계 학습에서 일기 예보</span><span class="sxs-lookup"><span data-stu-id="e57f5-104">Weather forecast using hello sensor data from your IoT hub in Azure Machine Learning</span></span>

![종단 간 다이어그램](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="e57f5-106">기계 학습에는 컴퓨터에서 기존 데이터 tooforecast 이후 동작, 결과 및 추세를 배울 도움이 되는 데이터 과학자의 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-106">Machine learning is a technique of data science that helps computers learn from existing data tooforecast future behaviors, outcomes, and trends.</span></span> <span data-ttu-id="e57f5-107">Azure 기계 학습은 클라우드 예측 분석 서비스를 이용 하 가능한 tooquickly 생성 하 고 분석 솔루션으로 예측 모델을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-107">Azure Machine Learning is a cloud predictive analytics service that makes it possible tooquickly create and deploy predictive models as analytics solutions.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="e57f5-108">학습 내용</span><span class="sxs-lookup"><span data-stu-id="e57f5-108">What you learn</span></span>

<span data-ttu-id="e57f5-109">어떻게 Azure IoT 허브에서 데이터를 온도 및 습도 hello toouse Azure 기계 학습 toodo 일기 예보 (비 가능성)를 사용 하 여 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-109">You learn how toouse Azure Machine Learning toodo weather forecast (chance of rain) using hello temperature and humidity data from your Azure IoT hub.</span></span> <span data-ttu-id="e57f5-110">비 hello 가능성은 준비 날씨 예측 모델의 hello 출력.</span><span class="sxs-lookup"><span data-stu-id="e57f5-110">hello chance of rain is hello output of a prepared weather prediction model.</span></span> <span data-ttu-id="e57f5-111">hello 모델 온도 및 습도에 따라 비 tooforecast 가능성이 기록 데이터를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-111">hello model is built upon historic data tooforecast chance of rain based on temperature and humidity.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="e57f5-112">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="e57f5-112">What you do</span></span>

- <span data-ttu-id="e57f5-113">웹 서비스로 hello 날씨 예측 모델을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-113">Deploy hello weather prediction model as a web service.</span></span>
- <span data-ttu-id="e57f5-114">소비자 그룹을 추가하여 IoT Hub에서 데이터 액세스 준비</span><span class="sxs-lookup"><span data-stu-id="e57f5-114">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="e57f5-115">스트림 분석 작업을 만들고 hello 작업을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-115">Create a Stream Analytics job and configure hello job to:</span></span>
  - <span data-ttu-id="e57f5-116">IoT Hub에서 온도 및 습도 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-116">Read temperature and humidity data from your IoT hub.</span></span>
  - <span data-ttu-id="e57f5-117">Hello 웹 서비스 tooget hello 비 기회를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-117">Call hello web service tooget hello rain chance.</span></span>
  - <span data-ttu-id="e57f5-118">Hello 결과 tooan Azure blob 저장소를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-118">Save hello result tooan Azure blob storage.</span></span>
- <span data-ttu-id="e57f5-119">Microsoft Azure 저장소 탐색기 tooview hello 일기 예보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-119">Use Microsoft Azure Storage Explorer tooview hello weather forecast.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e57f5-120">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="e57f5-120">What you need</span></span>

- <span data-ttu-id="e57f5-121">자습서 [사용자 장치를 설정](iot-hub-raspberry-pi-kit-node-get-started.md) 완료는 hello 요구 사항에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-121">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="e57f5-122">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="e57f5-122">An active Azure subscription.</span></span>
  - <span data-ttu-id="e57f5-123">구독 중인 Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="e57f5-123">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="e57f5-124">메시지 tooyour Azure IoT 허브에서 전송 하는 클라이언트 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-124">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="e57f5-125">Azure Machine Learning Studio 계정</span><span class="sxs-lookup"><span data-stu-id="e57f5-125">An Azure Machine Learning Studio account.</span></span> <span data-ttu-id="e57f5-126">[Machine Learning Studio 체험해 보기](https://studio.azureml.net/)</span><span class="sxs-lookup"><span data-stu-id="e57f5-126">([Try Machine Learning Studio for free](https://studio.azureml.net/)).</span></span>

## <a name="deploy-hello-weather-prediction-model-as-a-web-service"></a><span data-ttu-id="e57f5-127">웹 서비스로 hello 날씨 예측 모델을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-127">Deploy hello weather prediction model as a web service</span></span>

1. <span data-ttu-id="e57f5-128">Toohello 이동 [날씨 예측 모델 페이지](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1)합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-128">Go toohello [weather prediction model page](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span></span>
1. <span data-ttu-id="e57f5-129">Microsoft Azure Machine Learning Studio에서 **Studio에서 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-129">Click **Open in Studio** in Microsoft Azure Machine Learning Studio.</span></span>
   <span data-ttu-id="e57f5-130">![Cortana Intelligence 갤러리에서 열기 hello 날씨 예측 모델 페이지](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span><span class="sxs-lookup"><span data-stu-id="e57f5-130">![Open hello weather prediction model page in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span></span>
1. <span data-ttu-id="e57f5-131">클릭 **실행** toovalidate hello hello 모델의 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-131">Click **Run** toovalidate hello steps in hello model.</span></span> <span data-ttu-id="e57f5-132">이 단계는 2 분 toocomplete를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-132">This step might take 2 minutes toocomplete.</span></span>
   <span data-ttu-id="e57f5-133">![Azure 기계 학습 스튜디오에서 열기 hello 날씨 예측 모델](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="e57f5-133">![Open hello weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="e57f5-134">**웹 서비스 설정** > **예측형 웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-134">Click **SET UP WEB SERVICE** > **Predictive Web Service**.</span></span>
   <span data-ttu-id="e57f5-135">![Azure 기계 학습 스튜디오에서 hello 날씨 예측 모델 배포](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="e57f5-135">![Deploy hello weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="e57f5-136">Hello 다이어그램으로 끌어서 hello **웹 서비스 입력** hello 근처 어딘가에 모듈 **모델 점수 매기기** 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-136">In hello diagram, drag hello **Web service input** module somewhere near hello **Score Model** module.</span></span>
1. <span data-ttu-id="e57f5-137">Hello 연결 **웹 서비스 입력** 모듈 toohello **모델 점수 매기기** 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-137">Connect hello **Web service input** module toohello **Score Model** module.</span></span>
   <span data-ttu-id="e57f5-138">![Azure Machine Learning Studio에서 두 모듈 연결](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="e57f5-138">![Connect two modules in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="e57f5-139">클릭 **실행** toovalidate hello hello 모델의 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-139">Click **RUN** toovalidate hello steps in hello model.</span></span>
1. <span data-ttu-id="e57f5-140">클릭 **웹 서비스 배포** 웹 서비스로 toodeploy hello 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-140">Click **DEPLOY WEB SERVICE** toodeploy hello model as a web service.</span></span>
1. <span data-ttu-id="e57f5-141">Hello 모델의 hello 대시보드에서 hello 다운로드 **이전 통합 문서 또는 Excel 2010** 에 대 한 **요청/응답**합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-141">On hello dashboard of hello model, download hello **Excel 2010 or earlier workbook** for **REQUEST/RESPONSE**.</span></span>

   > [!Note]
   > <span data-ttu-id="e57f5-142">Hello를 다운로드 하는 확인 **이전 통합 문서 또는 Excel 2010** 컴퓨터에 Excel의 이후 버전을 실행 하는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-142">Ensure that you download hello **Excel 2010 or earlier workbook** even if you are running a later version of Excel on your computer.</span></span>

   ![Hello 요청 응답 끝점에 대 한 Excel hello 다운로드](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. <span data-ttu-id="e57f5-144">Hello Excel 통합 문서를 열고, hello 메모 **웹 서비스 URL** 및 **선택 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-144">Open hello Excel workbook, make a note of hello **WEB SERVICE URL** and **ACCESS KEY**.</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="e57f5-145">Stream Analytics 작업 만들기, 구성 및 실행</span><span class="sxs-lookup"><span data-stu-id="e57f5-145">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="e57f5-146">Stream Analytics 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="e57f5-146">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="e57f5-147">Hello에 [Azure 포털](https://ms.portal.azure.com/), 클릭 **새로** > **사물 인터넷** > **스트림 분석 작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-147">In hello [Azure portal](https://ms.portal.azure.com/), click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>
1. <span data-ttu-id="e57f5-148">Hello 다음 hello 작업에 대 한 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-148">Enter hello following information for hello job.</span></span>

   <span data-ttu-id="e57f5-149">**작업 이름**: hello 작업의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-149">**Job name**: hello name of hello job.</span></span> <span data-ttu-id="e57f5-150">hello 이름은 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-150">hello name must be globally unique.</span></span>

   <span data-ttu-id="e57f5-151">**리소스 그룹**: 동일 사용 하 여 hello IoT 허브를 사용 하는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-151">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="e57f5-152">**위치**: 사용 하 여 hello 동일한 리소스 그룹 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-152">**Location**: Use hello same location as your resource group.</span></span>

   <span data-ttu-id="e57f5-153">**Pin toodashboard**: hello 대시보드에서 쉽게 액세스할 수 있도록 tooyour IoT 허브에 대 한이 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-153">**Pin toodashboard**: Check this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Azure에서 Stream Analytics 작업 만들기](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="e57f5-155">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-155">Click **Create**.</span></span>

### <a name="add-an-input-toohello-stream-analytics-job"></a><span data-ttu-id="e57f5-156">입력된 toohello 스트림 분석 작업 추가</span><span class="sxs-lookup"><span data-stu-id="e57f5-156">Add an input toohello Stream Analytics job</span></span>

1. <span data-ttu-id="e57f5-157">열기 hello 스트림 분석 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-157">Open hello Stream Analytics job.</span></span>
1. <span data-ttu-id="e57f5-158">**작업 토폴로지**에서 **입력**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-158">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="e57f5-159">Hello에 **입력** 창에서 클릭 **추가**, hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-159">In hello **Inputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="e57f5-160">**입력된 별칭**: hello hello 입력에 대 한 고유 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-160">**Input alias**: hello unique alias for hello input.</span></span>

   <span data-ttu-id="e57f5-161">**원본**: **IoT Hub**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-161">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="e57f5-162">**소비자 그룹**: 만든 선택 hello 소비자 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-162">**Consumer group**: Select hello consumer group you created.</span></span>

   ![Azure에서 입력된 toohello 스트림 분석 작업 추가](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. <span data-ttu-id="e57f5-164">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-164">Click **Create**.</span></span>

### <a name="add-an-output-toohello-stream-analytics-job"></a><span data-ttu-id="e57f5-165">출력 toohello 스트림 분석 작업 추가</span><span class="sxs-lookup"><span data-stu-id="e57f5-165">Add an output toohello Stream Analytics job</span></span>

1. <span data-ttu-id="e57f5-166">**작업 토폴로지**에서 **출력**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-166">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="e57f5-167">Hello에 **출력** 창에서 클릭 **추가**, hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-167">In hello **Outputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="e57f5-168">**출력 별칭**: hello hello 출력에 대 한 고유 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-168">**Output alias**: hello unique alias for hello output.</span></span>

   <span data-ttu-id="e57f5-169">**싱크**: **Blob Storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-169">**Sink**: Select **Blob Storage**.</span></span>

   <span data-ttu-id="e57f5-170">**저장소 계정**: hello blob 저장소에 대 한 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-170">**Storage account**: hello storage account for your blob storage.</span></span> <span data-ttu-id="e57f5-171">저장소 계정을 만들거나 기존 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-171">You can create a storage account or use an existing one.</span></span>

   <span data-ttu-id="e57f5-172">**컨테이너**: hello 컨테이너 hello blob 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-172">**Container**: hello container where hello blob is saved.</span></span> <span data-ttu-id="e57f5-173">컨테이너를 만들거나 기존 컨테이너를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-173">You can create a container or use an existing one.</span></span>

   <span data-ttu-id="e57f5-174">**이벤트 직렬화 형식**: **CSV**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-174">**Event serialization format**: Select **CSV**.</span></span>

   ![Azure에서 출력 toohello 스트림 분석 작업 추가](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. <span data-ttu-id="e57f5-176">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-176">Click **Create**.</span></span>

### <a name="add-a-function-toohello-stream-analytics-job-toocall-hello-web-service-you-deployed"></a><span data-ttu-id="e57f5-177">함수 toohello 배포한 스트림 분석 작업 toocall hello 웹 서비스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-177">Add a function toohello Stream Analytics job toocall hello web service you deployed</span></span>

1. <span data-ttu-id="e57f5-178">**작업 토폴로지**에서 **함수** > **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-178">Under **Job Topology**, click **Functions** > **Add**.</span></span>
1. <span data-ttu-id="e57f5-179">Hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-179">Enter hello following information:</span></span>

   <span data-ttu-id="e57f5-180">**별칭 함수**: `machinelearning`을(를) 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-180">**Function Alias**: Enter `machinelearning`.</span></span>

   <span data-ttu-id="e57f5-181">**함수 유형**: **Azure ML**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-181">**Function Type**: Select **Azure ML**.</span></span>

   <span data-ttu-id="e57f5-182">**가져오기 옵션**: **다른 구독에서 가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-182">**Import option**: Select **Import from a different subscription**.</span></span>

   <span data-ttu-id="e57f5-183">**URL**: hello Excel 통합 문서에서 hello 아래로 기록한 웹 서비스 URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-183">**URL**: Enter hello WEB SERVICE URL that you noted down from hello Excel workbook.</span></span>

   <span data-ttu-id="e57f5-184">**키**: hello Excel 통합 문서에서 hello에 아래 표시 된 선택 키를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-184">**Key**: Enter hello ACCESS KEY that you noted down from hello Excel workbook.</span></span>

   ![Azure에서 함수 toohello 스트림 분석 작업 추가](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. <span data-ttu-id="e57f5-186">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-186">Click **Create**.</span></span>

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a><span data-ttu-id="e57f5-187">Hello 스트림 분석 작업의 hello 쿼리 구성</span><span class="sxs-lookup"><span data-stu-id="e57f5-187">Configure hello query of hello Stream Analytics job</span></span>

1. <span data-ttu-id="e57f5-188">**작업 토폴로지**에서 **쿼리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-188">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="e57f5-189">코드 다음 hello hello 기존 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-189">Replace hello existing code with hello following code:</span></span>

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   <span data-ttu-id="e57f5-190">대체 `[YourInputAlias]` hello 작업의 입력 hello 별칭으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-190">Replace `[YourInputAlias]` with hello input alias of hello job.</span></span>

   <span data-ttu-id="e57f5-191">대체 `[YourOutputAlias]` hello 작업의 hello 출력 별칭 사용.</span><span class="sxs-lookup"><span data-stu-id="e57f5-191">Replace `[YourOutputAlias]` with hello output alias of hello job.</span></span>

1. <span data-ttu-id="e57f5-192">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-192">Click **Save**.</span></span>

### <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="e57f5-193">Hello 스트림 분석 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-193">Run hello Stream Analytics job</span></span>

<span data-ttu-id="e57f5-194">Hello Stream Analytics 작업에서 클릭 **시작** > **이제** > **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-194">In hello Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="e57f5-195">Hello 작업 상태에서 변경 hello 작업이 성공적으로 시작 되 면 **Stopped** 너무**실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-195">Once hello job successfully starts, hello job status changes from **Stopped** too**Running**.</span></span>

![Hello 스트림 분석 작업을 실행 합니다.](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-tooview-hello-weather-forecast"></a><span data-ttu-id="e57f5-197">Microsoft Azure 저장소 탐색기 tooview hello 일기 예보를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e57f5-197">Use Microsoft Azure Storage Explorer tooview hello weather forecast</span></span>

<span data-ttu-id="e57f5-198">온도 및 습도 데이터 tooyour IoT 허브를 보내고 hello 클라이언트 응용 프로그램 toostart 수집을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-198">Run hello client application toostart collecting and sending temperature and humidity data tooyour IoT hub.</span></span> <span data-ttu-id="e57f5-199">IoT hub를 수신 하는 각 메시지에 대 한 hello 스트림 분석 작업 비 hello 일기 예보 웹 서비스 tooproduce hello 가능성이 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-199">For each message that your IoT hub receives, hello Stream Analytics job calls hello weather forecast web service tooproduce hello chance of rain.</span></span> <span data-ttu-id="e57f5-200">hello 결과 tooyour Azure blob 저장소를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-200">hello result is then saved tooyour Azure blob storage.</span></span> <span data-ttu-id="e57f5-201">Azure 저장소 탐색기는 tooview hello 결과 사용할 수 있는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-201">Azure Storage Explorer is a tool that you can use tooview hello result.</span></span>

1. <span data-ttu-id="e57f5-202">[Microsoft Azure Storage 탐색기를 다운로드하고 설치합니다](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="e57f5-202">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
1. <span data-ttu-id="e57f5-203">Azure Storage 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-203">Open Azure Storage Explorer.</span></span>
1. <span data-ttu-id="e57f5-204">Azure 계정 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-204">Sign in tooyour Azure account.</span></span>
1. <span data-ttu-id="e57f5-205">사용 중인 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-205">Select your subscription.</span></span>
1. <span data-ttu-id="e57f5-206">구독> **저장소 계정** > 저장소 계정> **Blob 컨테이너**> 컨테이너를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-206">Click your subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span></span>
1. <span data-ttu-id="e57f5-207">.Csv 파일 toosee hello 결과를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-207">Open a .csv file toosee hello result.</span></span> <span data-ttu-id="e57f5-208">마지막 열 레코드 hello hello 비 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-208">hello last column records hello chance of rain.</span></span>

   ![Azure Machine Learning을 사용하여 일기 예보 결과 가져오기](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a><span data-ttu-id="e57f5-210">요약</span><span class="sxs-lookup"><span data-stu-id="e57f5-210">Summary</span></span>

<span data-ttu-id="e57f5-211">IoT hub 받는 hello 온도 및 습도 데이터를 기반으로 하는 비 Azure 기계 학습 tooproduce hello 가능성을 성공적으로 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e57f5-211">You’ve successfully used Azure Machine Learning tooproduce hello chance of rain based on hello temperature and humidity data that your IoT hub receives.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]