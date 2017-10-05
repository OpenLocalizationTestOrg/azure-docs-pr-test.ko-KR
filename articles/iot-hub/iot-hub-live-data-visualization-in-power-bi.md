---
title: "Azure IoT Hub에서 센서 데이터의 실시간 데이터 시각화 – Power BI | Microsoft Docs"
description: "Power BI를 사용하여 센서에서 수집하여 Azure IoT Hub로 보낸 온도 및 습도 데이터를 시각화합니다."
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
ms.openlocfilehash: b190fea06ffc2406d781c7edad091f097cca9c2d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a><span data-ttu-id="bb626-104">Power BI를 사용하여 Azure IoT Hub에서 실시간 센서 데이터 시각화</span><span class="sxs-lookup"><span data-stu-id="bb626-104">Visualize real-time sensor data from Azure IoT Hub using Power BI</span></span>

![종단 간 다이어그램](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="bb626-106">학습 내용</span><span class="sxs-lookup"><span data-stu-id="bb626-106">What you learn</span></span>

<span data-ttu-id="bb626-107">Azure IoT Hub에서 Power BI를 통해 받는 실시간 센서 데이터를 시각화하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-107">You learn how to visualize real-time sensor data that your Azure IoT hub receives by Power BI.</span></span> <span data-ttu-id="bb626-108">Web Apps를 사용하여 IoT Hub의 데이터를 시각화하려면 [Azure Web Apps를 사용하여 Azure IoT Hub의 실시간 센서 데이터 시각화](iot-hub-live-data-visualization-in-web-apps.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bb626-108">If you want to try visualize the data in your IoT hub with Web Apps, please see [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="bb626-109">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="bb626-109">What you do</span></span>

- <span data-ttu-id="bb626-110">소비자 그룹을 추가하여 IoT Hub에서 데이터 액세스 준비</span><span class="sxs-lookup"><span data-stu-id="bb626-110">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="bb626-111">IoT Hub에서 Power BI 계정으로의 데이터 전송을 위한 Stream Analytics 작업 만들기, 구성 및 실행</span><span class="sxs-lookup"><span data-stu-id="bb626-111">Create, configure and run a Stream Analytics job for data transfer from your IoT hub to your Power BI account.</span></span>
- <span data-ttu-id="bb626-112">Power BI 보고서를 만들고 게시하여 데이터 시각화</span><span class="sxs-lookup"><span data-stu-id="bb626-112">Create and publish a Power BI report to visualize the data.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bb626-113">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="bb626-113">What you need</span></span>

- <span data-ttu-id="bb626-114">다음 요구 사항을 다루는 자습서 [장치 설정](iot-hub-raspberry-pi-kit-node-get-started.md) 완료:</span><span class="sxs-lookup"><span data-stu-id="bb626-114">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="bb626-115">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="bb626-115">An active Azure subscription.</span></span>
  - <span data-ttu-id="bb626-116">구독 중인 Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="bb626-116">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="bb626-117">메시지를 Azure IoT Hub로 보내는 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="bb626-117">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="bb626-118">Power BI 계정</span><span class="sxs-lookup"><span data-stu-id="bb626-118">A Power BI account.</span></span> <span data-ttu-id="bb626-119">([Power BI를 무료로 사용해 보기](https://powerbi.microsoft.com/))</span><span class="sxs-lookup"><span data-stu-id="bb626-119">([Try Power BI for free](https://powerbi.microsoft.com/))</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="bb626-120">Stream Analytics 작업 만들기, 구성 및 실행</span><span class="sxs-lookup"><span data-stu-id="bb626-120">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="bb626-121">Stream Analytics 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="bb626-121">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="bb626-122">Azure Portal에서 새로 만들기 > 사물 인터넷 > Stream Analytics 작업을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-122">In the Azure portal, click New > Internet of Things > Stream Analytics job.</span></span>
1. <span data-ttu-id="bb626-123">작업에 대한 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-123">Enter the following information for the job.</span></span>

   <span data-ttu-id="bb626-124">**작업 이름**: 작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-124">**Job name**: The name of the job.</span></span> <span data-ttu-id="bb626-125">이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-125">The name must be globally unique.</span></span>

   <span data-ttu-id="bb626-126">**리소스 그룹**: IoT Hub에서 사용하는 것과 동일한 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-126">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="bb626-127">**위치**: 리소스 그룹과 동일한 위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-127">**Location**: Use the same location as your resource group.</span></span>

   <span data-ttu-id="bb626-128">**대시보드에 고정**: 대시보드에서 IoT Hub에 쉽게 액세스하려면 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-128">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Azure에서 Stream Analytics 작업 만들기](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="bb626-130">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-130">Click **Create**.</span></span>

### <a name="add-an-input-to-the-stream-analytics-job"></a><span data-ttu-id="bb626-131">Stream Analytics 작업에 입력 추가</span><span class="sxs-lookup"><span data-stu-id="bb626-131">Add an input to the Stream Analytics job</span></span>

1. <span data-ttu-id="bb626-132">Stream Analytics 작업을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-132">Open the Stream Analytics job.</span></span>
1. <span data-ttu-id="bb626-133">**작업 토폴로지**에서 **입력**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-133">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="bb626-134">**입력** 창에서 **추가**를 클릭하고 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-134">In the **Inputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="bb626-135">**입력 별칭**: 입력에 대한 고유 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-135">**Input alias**: The unique alias for the input.</span></span>

   <span data-ttu-id="bb626-136">**원본**: **IoT Hub**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-136">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="bb626-137">**소비자 그룹**: 방금 만든 소비자 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-137">**Consumer group**: Select the consumer group you just created.</span></span>
1. <span data-ttu-id="bb626-138">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-138">Click **Create**.</span></span>

   ![Azure에서 Stream Analytics 작업에 입력 추가](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-to-the-stream-analytics-job"></a><span data-ttu-id="bb626-140">Stream Analytics 작업에 출력 추가</span><span class="sxs-lookup"><span data-stu-id="bb626-140">Add an output to the Stream Analytics job</span></span>

1. <span data-ttu-id="bb626-141">**작업 토폴로지**에서 **출력**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-141">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="bb626-142">**출력** 창에서 **추가**를 클릭하고 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-142">In the **Outputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="bb626-143">**출력 별칭**: 출력에 대한 고유 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-143">**Output alias**: The unique alias for the output.</span></span>

   <span data-ttu-id="bb626-144">**싱크**: **Power BI**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-144">**Sink**: Select **Power BI**.</span></span>
1. <span data-ttu-id="bb626-145">**권한 부여**를 클릭한 다음 Power BI 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-145">Click **Authorize**, and then sign into your Power BI account.</span></span>
1. <span data-ttu-id="bb626-146">권한이 부여되면 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-146">Once authorized, enter the following information:</span></span>

   <span data-ttu-id="bb626-147">**그룹 작업 영역**: 대상 그룹 작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-147">**Group Workspace**: Select your target group workspace.</span></span>

   <span data-ttu-id="bb626-148">**데이터 집합 이름**: 데이터 집합 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-148">**Dataset Name**: Enter a dataset name.</span></span>

   <span data-ttu-id="bb626-149">**테이블 이름**: 테이블 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-149">**Table Name**: Enter a table name.</span></span>
1. <span data-ttu-id="bb626-150">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-150">Click **Create**.</span></span>

   ![Azure에서 Stream Analytics 작업에 출력 추가](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-the-query-of-the-stream-analytics-job"></a><span data-ttu-id="bb626-152">Stream Analytics 작업의 쿼리 구성</span><span class="sxs-lookup"><span data-stu-id="bb626-152">Configure the query of the Stream Analytics job</span></span>

1. <span data-ttu-id="bb626-153">**작업 토폴로지**에서 **쿼리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-153">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="bb626-154">`[YourInputAlias]`를 작업의 입력 별칭으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-154">Replace `[YourInputAlias]` with the input alias of the job.</span></span>
1. <span data-ttu-id="bb626-155">`[YourOutputAlias]`를 작업의 출력 별칭으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-155">Replace `[YourOutputAlias]` with the output alias of the job.</span></span>
1. <span data-ttu-id="bb626-156">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-156">Click **Save**.</span></span>

   ![Azure에서 Stream Analytics 작업에 쿼리 추가](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="bb626-158">스트림 분석 작업 실행</span><span class="sxs-lookup"><span data-stu-id="bb626-158">Run the Stream Analytics job</span></span>

<span data-ttu-id="bb626-159">Stream Analytics 작업에서 **시작** > **지금 시작** > **시작**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-159">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="bb626-160">작업이 성공적으로 시작되면 작업 상태가 **중지됨**에서 **실행 중**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-160">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span></span>

![Azure에서 Stream Analytics 작업 실행](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-to-visualize-the-data"></a><span data-ttu-id="bb626-162">Power BI 보고서를 만들고 게시하여 데이터 시각화</span><span class="sxs-lookup"><span data-stu-id="bb626-162">Create and publish a Power BI report to visualize the data</span></span>

1. <span data-ttu-id="bb626-163">응용 프로그램 예제가 사용자 장치에서 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-163">Ensure the sample application is running on your device.</span></span> <span data-ttu-id="bb626-164">그렇지 않은 경우 [사용자 장치 설정](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started)에 있는 자습서를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-164">If not, you can refer to the tutorials under [Setup your device](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span></span>
1. <span data-ttu-id="bb626-165">[Power BI](https://powerbi.microsoft.com/en-us/) 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-165">Sign in to your [Power BI](https://powerbi.microsoft.com/en-us/) account.</span></span>
1. <span data-ttu-id="bb626-166">Stream Analytics 작업에 대한 출력을 만들 때 설정한 그룹 작업 영역으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-166">Go to the group workspace that you set when you created the output for the Stream Analytics job.</span></span>
1. <span data-ttu-id="bb626-167">**스트리밍 데이터 집합**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-167">Click **Streaming datasets**.</span></span>

   <span data-ttu-id="bb626-168">Stream Analytics 작업에 대한 출력을 만들 때 지정한 나열된 데이터 집합이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-168">You should see the listed dataset that you specified when you created the output for the Stream Analytics job.</span></span>
1. <span data-ttu-id="bb626-169">**작업**에서 첫 번째 아이콘을 클릭하여 보고서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-169">Under **ACTIONS**, click the first icon to create a report.</span></span>

   ![Microsoft Power BI 보고서 만들기](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. <span data-ttu-id="bb626-171">시간이 지남에 따라 실시간 온도를 표시하는 꺾은선형 차트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-171">Create a line chart to show real-time temperature over time.</span></span>
   1. <span data-ttu-id="bb626-172">보고서 만들기 페이지에서 꺾은선형 차트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-172">On the report creation page, add a line chart.</span></span>
   1. <span data-ttu-id="bb626-173">**필드** 창에서 Stream Analytics 작업의 출력을 만들 때 지정한 테이블을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-173">On the **Fields** pane, expand the table that you specified when you created the output for the Stream Analytics job.</span></span>
   1. <span data-ttu-id="bb626-174">**시각화** 창에서 **EventEnqueuedUtcTime**을 **축**으로 끌어갑니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-174">Drag **EventEnqueuedUtcTime** to **Axis** on the **Visualizations** pane.</span></span>
   1. <span data-ttu-id="bb626-175">**온도**를 **값**으로 끌어갑니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-175">Drag **temperature** to **Values**.</span></span>

      <span data-ttu-id="bb626-176">이제 꺾은선형 차트가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-176">Now a line chart is created.</span></span> <span data-ttu-id="bb626-177">x축은 UTC 표준 시간대의 날짜와 시간을 표시하고,</span><span class="sxs-lookup"><span data-stu-id="bb626-177">The x-axis displays date and time in the UTC time zone.</span></span> <span data-ttu-id="bb626-178">y축은 센서의 온도를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-178">The y-axis displays temperature from the sensor.</span></span>

      ![온도에 대한 꺾은선형 차트를 Microsoft Power BI 보고서에 추가](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="bb626-180">시간이 지남에 따라 실시간 습도를 표시하는 꺾은선형 차트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-180">Create another line chart to show real-time humidity over time.</span></span> <span data-ttu-id="bb626-181">이렇게 하려면 위와 동일한 단계를 수행하고 **EventEnqueuedUtcTime**을 x축에, **습도**를 y축에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-181">To do this, follow the same steps above and place **EventEnqueuedUtcTime** on the x-axis and **humidity** on the y-axis.</span></span>

   ![습도에 대한 꺾은선형 차트를 Microsoft Power BI 보고서에 추가](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="bb626-183">**저장**을 클릭하여 보고서를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-183">Click **Save** to save the report.</span></span>
1. <span data-ttu-id="bb626-184">**파일** > **웹에 게시**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-184">Click **File** > **Publish to web**.</span></span>
1. <span data-ttu-id="bb626-185">**Embed 태그 만들기**를 클릭한 다음 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-185">Click **Create embed code**, and then click **Publish**.</span></span>

<span data-ttu-id="bb626-186">보고서 액세스를 위해 누구와도 공유할 수 있는 보고서 링크와 블로그 또는 웹 사이트에 보고서를 통합하는 코드 조각이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-186">You're provided the report link that you can share with anyone for report access and a code snippet to integrate the report into your blog or website.</span></span>

![Microsoft Power BI 보고서 게시](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

<span data-ttu-id="bb626-188">모바일 장치에서 Power BI 대시보드 및 보고서를 보고 상호 작용할 수 있는 [Power BI 모바일 앱](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/)도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-188">Microsoft also offers the [Power BI mobile apps](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) for viewing and interacting with your Power BI dashboards and reports on your mobile device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb626-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bb626-189">Next steps</span></span>

<span data-ttu-id="bb626-190">Power BI를 사용하여 Azure IoT Hub에서 실시간 센서 데이터를 시각화했습니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-190">You’ve successfully used Power BI to visualize real-time sensor data from your Azure IoT hub.</span></span>
<span data-ttu-id="bb626-191">Azure IoT Hub에서 데이터를 시각화하는 또 다른 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb626-191">There is an alternate way to visualize data from Azure IoT Hub.</span></span> <span data-ttu-id="bb626-192">[Azure Web Apps를 사용하여 Azure IoT Hub의 실시간 센서 데이터 시각화](iot-hub-live-data-visualization-in-web-apps.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bb626-192">See [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
