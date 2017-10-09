---
title: "Azure IoT Hub-Power BI에서에서 센서 데이터의 타임 aaaReal 데이터 시각화 | Microsoft Docs"
description: "Power BI toovisualize 온도 및 습도 데이터를 사용 hello 센서에서 수집 되 고 tooyour Azure IoT 허브를 전송 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "실시간 데이터 시각화, 라이브 데이터 시각화, 센서 데이터 시각화"
ms.assetid: e67c9c09-6219-4f0f-ad42-58edaaa74f61
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: d79ce757a9f2ab7a4744e8a0c523106e0f72cecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a><span data-ttu-id="09ce6-104">Power BI를 사용하여 Azure IoT Hub에서 실시간 센서 데이터 시각화</span><span class="sxs-lookup"><span data-stu-id="09ce6-104">Visualize real-time sensor data from Azure IoT Hub using Power BI</span></span>

![종단 간 다이어그램](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="09ce6-106">학습 내용</span><span class="sxs-lookup"><span data-stu-id="09ce6-106">What you learn</span></span>

<span data-ttu-id="09ce6-107">배웁니다 어떻게 Power BI에서 Azure IoT hub 받는 toovisualize 센서 실시간 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-107">You learn how toovisualize real-time sensor data that your Azure IoT hub receives by Power BI.</span></span> <span data-ttu-id="09ce6-108">Tootry hello 데이터를 시각화 하려면 웹 앱과 IoT 허브에서를 참조 하세요 [Azure IoT 허브에서 사용 하 여 Azure 웹 앱 toovisualize 실시간 센서 데이터](iot-hub-live-data-visualization-in-web-apps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-108">If you want tootry visualize hello data in your IoT hub with Web Apps, please see [Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="09ce6-109">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="09ce6-109">What you do</span></span>

- <span data-ttu-id="09ce6-110">소비자 그룹을 추가하여 IoT Hub에서 데이터 액세스 준비</span><span class="sxs-lookup"><span data-stu-id="09ce6-110">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="09ce6-111">만들고 구성 하 고 IoT 허브 tooyour Power BI 계정에서에서 데이터 전송에 대 한 스트림 분석 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-111">Create, configure and run a Stream Analytics job for data transfer from your IoT hub tooyour Power BI account.</span></span>
- <span data-ttu-id="09ce6-112">만들고 Power BI 보고서 toovisualize hello 데이터를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-112">Create and publish a Power BI report toovisualize hello data.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="09ce6-113">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="09ce6-113">What you need</span></span>

- <span data-ttu-id="09ce6-114">자습서 [사용자 장치를 설정](iot-hub-raspberry-pi-kit-node-get-started.md) 완료는 hello 요구 사항에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-114">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="09ce6-115">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="09ce6-115">An active Azure subscription.</span></span>
  - <span data-ttu-id="09ce6-116">구독 중인 Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="09ce6-116">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="09ce6-117">메시지 tooyour Azure IoT 허브에서 전송 하는 클라이언트 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-117">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="09ce6-118">Power BI 계정</span><span class="sxs-lookup"><span data-stu-id="09ce6-118">A Power BI account.</span></span> <span data-ttu-id="09ce6-119">([Power BI를 무료로 사용해 보기](https://powerbi.microsoft.com/))</span><span class="sxs-lookup"><span data-stu-id="09ce6-119">([Try Power BI for free](https://powerbi.microsoft.com/))</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="09ce6-120">Stream Analytics 작업 만들기, 구성 및 실행</span><span class="sxs-lookup"><span data-stu-id="09ce6-120">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="09ce6-121">Stream Analytics 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="09ce6-121">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="09ce6-122">Hello Azure 포털에서 새로 만들기 > 사물 인터넷 > 스트림 분석 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-122">In hello Azure portal, click New > Internet of Things > Stream Analytics job.</span></span>
1. <span data-ttu-id="09ce6-123">Hello 다음 hello 작업에 대 한 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-123">Enter hello following information for hello job.</span></span>

   <span data-ttu-id="09ce6-124">**작업 이름**: hello 작업의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-124">**Job name**: hello name of hello job.</span></span> <span data-ttu-id="09ce6-125">hello 이름은 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-125">hello name must be globally unique.</span></span>

   <span data-ttu-id="09ce6-126">**리소스 그룹**: 동일 사용 하 여 hello IoT 허브를 사용 하는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-126">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="09ce6-127">**위치**: 사용 하 여 hello 동일한 리소스 그룹 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-127">**Location**: Use hello same location as your resource group.</span></span>

   <span data-ttu-id="09ce6-128">**Pin toodashboard**: hello 대시보드에서 쉽게 액세스할 수 있도록 tooyour IoT 허브에 대 한이 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-128">**Pin toodashboard**: Check this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Azure에서 Stream Analytics 작업 만들기](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="09ce6-130">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-130">Click **Create**.</span></span>

### <a name="add-an-input-toohello-stream-analytics-job"></a><span data-ttu-id="09ce6-131">입력된 toohello 스트림 분석 작업 추가</span><span class="sxs-lookup"><span data-stu-id="09ce6-131">Add an input toohello Stream Analytics job</span></span>

1. <span data-ttu-id="09ce6-132">열기 hello 스트림 분석 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-132">Open hello Stream Analytics job.</span></span>
1. <span data-ttu-id="09ce6-133">**작업 토폴로지**에서 **입력**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-133">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="09ce6-134">Hello에 **입력** 창에서 클릭 **추가**, hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-134">In hello **Inputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="09ce6-135">**입력된 별칭**: hello hello 입력에 대 한 고유 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-135">**Input alias**: hello unique alias for hello input.</span></span>

   <span data-ttu-id="09ce6-136">**원본**: **IoT Hub**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-136">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="09ce6-137">**소비자 그룹**: 방금 만든 선택 hello 소비자 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-137">**Consumer group**: Select hello consumer group you just created.</span></span>
1. <span data-ttu-id="09ce6-138">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-138">Click **Create**.</span></span>

   ![Azure에서 입력된 tooa 스트림 분석 작업 추가](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-toohello-stream-analytics-job"></a><span data-ttu-id="09ce6-140">출력 toohello 스트림 분석 작업 추가</span><span class="sxs-lookup"><span data-stu-id="09ce6-140">Add an output toohello Stream Analytics job</span></span>

1. <span data-ttu-id="09ce6-141">**작업 토폴로지**에서 **출력**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-141">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="09ce6-142">Hello에 **출력** 창에서 클릭 **추가**, hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-142">In hello **Outputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="09ce6-143">**출력 별칭**: hello hello 출력에 대 한 고유 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-143">**Output alias**: hello unique alias for hello output.</span></span>

   <span data-ttu-id="09ce6-144">**싱크**: **Power BI**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-144">**Sink**: Select **Power BI**.</span></span>
1. <span data-ttu-id="09ce6-145">**권한 부여**를 클릭한 다음 Power BI 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-145">Click **Authorize**, and then sign into your Power BI account.</span></span>
1. <span data-ttu-id="09ce6-146">에 게 권한이 부여 되 면 hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-146">Once authorized, enter hello following information:</span></span>

   <span data-ttu-id="09ce6-147">**그룹 작업 영역**: 대상 그룹 작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-147">**Group Workspace**: Select your target group workspace.</span></span>

   <span data-ttu-id="09ce6-148">**데이터 집합 이름**: 데이터 집합 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-148">**Dataset Name**: Enter a dataset name.</span></span>

   <span data-ttu-id="09ce6-149">**테이블 이름**: 테이블 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-149">**Table Name**: Enter a table name.</span></span>
1. <span data-ttu-id="09ce6-150">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-150">Click **Create**.</span></span>

   ![Azure에서 출력 tooa 스트림 분석 작업 추가](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a><span data-ttu-id="09ce6-152">Hello 스트림 분석 작업의 hello 쿼리 구성</span><span class="sxs-lookup"><span data-stu-id="09ce6-152">Configure hello query of hello Stream Analytics job</span></span>

1. <span data-ttu-id="09ce6-153">**작업 토폴로지**에서 **쿼리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-153">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="09ce6-154">대체 `[YourInputAlias]` hello 작업의 입력 hello 별칭으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-154">Replace `[YourInputAlias]` with hello input alias of hello job.</span></span>
1. <span data-ttu-id="09ce6-155">대체 `[YourOutputAlias]` hello 작업의 hello 출력 별칭 사용.</span><span class="sxs-lookup"><span data-stu-id="09ce6-155">Replace `[YourOutputAlias]` with hello output alias of hello job.</span></span>
1. <span data-ttu-id="09ce6-156">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-156">Click **Save**.</span></span>

   ![Azure의 쿼리 tooa 스트림 분석 작업 추가](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="09ce6-158">Hello 스트림 분석 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-158">Run hello Stream Analytics job</span></span>

<span data-ttu-id="09ce6-159">Hello Stream Analytics 작업에서 클릭 **시작** > **이제** > **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-159">In hello Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="09ce6-160">Hello 작업 상태에서 변경 hello 작업이 성공적으로 시작 되 면 **Stopped** 너무**실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-160">Once hello job successfully starts, hello job status changes from **Stopped** too**Running**.</span></span>

![Azure에서 Stream Analytics 작업 실행](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-toovisualize-hello-data"></a><span data-ttu-id="09ce6-162">만들기 및 Power BI 보고서 toovisualize hello 데이터 게시</span><span class="sxs-lookup"><span data-stu-id="09ce6-162">Create and publish a Power BI report toovisualize hello data</span></span>

1. <span data-ttu-id="09ce6-163">Hello 샘플 응용 프로그램 장치에서 실행 중인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-163">Ensure hello sample application is running on your device.</span></span> <span data-ttu-id="09ce6-164">아래 toohello 자습서를 참조 하면 그렇지 [사용자 장치를 설정](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started)합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-164">If not, you can refer toohello tutorials under [Setup your device](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span></span>
1. <span data-ttu-id="09ce6-165">Tooyour 로그인 [Power BI](https://powerbi.microsoft.com/en-us/) 계정.</span><span class="sxs-lookup"><span data-stu-id="09ce6-165">Sign in tooyour [Power BI](https://powerbi.microsoft.com/en-us/) account.</span></span>
1. <span data-ttu-id="09ce6-166">Hello 스트림 분석 작업에 대 한 hello 출력을 만들 때 설정한 toohello 그룹 작업 영역을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-166">Go toohello group workspace that you set when you created hello output for hello Stream Analytics job.</span></span>
1. <span data-ttu-id="09ce6-167">**스트리밍 데이터 집합**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-167">Click **Streaming datasets**.</span></span>

   <span data-ttu-id="09ce6-168">Hello hello 스트림 분석 작업에 대 한 출력을 만들 때 지정한 hello 나열 된 데이터 집합을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-168">You should see hello listed dataset that you specified when you created hello output for hello Stream Analytics job.</span></span>
1. <span data-ttu-id="09ce6-169">아래 **동작**, hello 첫 번째 아이콘 toocreate 보고서를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-169">Under **ACTIONS**, click hello first icon toocreate a report.</span></span>

   ![Microsoft Power BI 보고서 만들기](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. <span data-ttu-id="09ce6-171">시간이 지남에 따라 꺾은선형 차트 tooshow 실시간 온도를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-171">Create a line chart tooshow real-time temperature over time.</span></span>
   1. <span data-ttu-id="09ce6-172">Hello 보고서 만들기 페이지에는 꺾은선형 차트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-172">On hello report creation page, add a line chart.</span></span>
   1. <span data-ttu-id="09ce6-173">Hello에 **필드** 창 hello 스트림 분석 작업에 대 한 hello 출력을 만들 때 지정한 hello 테이블을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-173">On hello **Fields** pane, expand hello table that you specified when you created hello output for hello Stream Analytics job.</span></span>
   1. <span data-ttu-id="09ce6-174">끌기 **EventEnqueuedUtcTime** 너무**축** hello에 **시각화** 창.</span><span class="sxs-lookup"><span data-stu-id="09ce6-174">Drag **EventEnqueuedUtcTime** too**Axis** on hello **Visualizations** pane.</span></span>
   1. <span data-ttu-id="09ce6-175">끌기 **온도** 너무**값**합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-175">Drag **temperature** too**Values**.</span></span>

      <span data-ttu-id="09ce6-176">이제 꺾은선형 차트가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-176">Now a line chart is created.</span></span> <span data-ttu-id="09ce6-177">hello x 축 hello UTC 표준 시간대의 날짜 및 시간을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-177">hello x-axis displays date and time in hello UTC time zone.</span></span> <span data-ttu-id="09ce6-178">hello y 축 hello 센서의 온도 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-178">hello y-axis displays temperature from hello sensor.</span></span>

      ![온도 tooa Microsoft Power BI 보고서는 꺾은선형 차트를 추가 합니다.](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="09ce6-180">시간에 따라 다른 꺾은선형 차트 tooshow 실시간 습도를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-180">Create another line chart tooshow real-time humidity over time.</span></span> <span data-ttu-id="09ce6-181">toodo이 위의 프로세스를 같은 hello을 따르고 **EventEnqueuedUtcTime** hello x 축에 및 **습도** hello y 축에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-181">toodo this, follow hello same steps above and place **EventEnqueuedUtcTime** on hello x-axis and **humidity** on hello y-axis.</span></span>

   ![습도 tooa Microsoft Power BI 보고서는 꺾은선형 차트를 추가 합니다.](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="09ce6-183">클릭 **저장** toosave hello 보고서입니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-183">Click **Save** toosave hello report.</span></span>
1. <span data-ttu-id="09ce6-184">클릭 **파일** > **tooweb 게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-184">Click **File** > **Publish tooweb**.</span></span>
1. <span data-ttu-id="09ce6-185">**Embed 태그 만들기**를 클릭한 다음 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-185">Click **Create embed code**, and then click **Publish**.</span></span>

<span data-ttu-id="09ce6-186">블로그 또는 웹 사이트에 보고서 액세스에 대 한 모든 사용자와 코드 조각 toointegrate hello 보고서와 공유할 수 있는 hello 보고서 링크를 제공 하는.</span><span class="sxs-lookup"><span data-stu-id="09ce6-186">You're provided hello report link that you can share with anyone for report access and a code snippet toointegrate hello report into your blog or website.</span></span>

![Microsoft Power BI 보고서 게시](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

<span data-ttu-id="09ce6-188">Microsoft는 또한 hello 제공 [Power BI 모바일 앱](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) 보기 및 사용자 Power BI 대시보드 및 보고서 상호 작용에 대 한 모바일 장치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-188">Microsoft also offers hello [Power BI mobile apps](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) for viewing and interacting with your Power BI dashboards and reports on your mobile device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09ce6-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="09ce6-189">Next steps</span></span>

<span data-ttu-id="09ce6-190">Azure IoT 허브에서 Power BI toovisualize 실시간 센서 데이터를 성공적으로 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-190">You’ve successfully used Power BI toovisualize real-time sensor data from your Azure IoT hub.</span></span>
<span data-ttu-id="09ce6-191">다른 방법 toovisualize 데이터를 사용 하 여 Azure IoT Hub를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-191">There is an alternate way toovisualize data from Azure IoT Hub.</span></span> <span data-ttu-id="09ce6-192">참조 [Azure IoT 허브에서 사용 하 여 Azure 웹 앱 toovisualize 실시간 센서 데이터](iot-hub-live-data-visualization-in-web-apps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="09ce6-192">See [Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
