---
title: "IoT 실시간 데이터 스트림 및 Azure Stream Analytics | Microsoft Docs"
description: "스트림 분석 및 실시간 데이터 처리와 IoT 센서 태그 및 데이터 스트림"
keywords: "IoT 솔루션, IoT 시작"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 3e829055-75ed-469f-91f5-f0dc95046bdb
ms.service: stream-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3af5aaa833478ef35fb57664c573ebf22d7a4599
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-stream-analytics-to-process-data-from-iot-devices"></a><span data-ttu-id="f2186-104">IoT 장치에서 데이터를 처리하도록 Azure 스트림 분석 시작</span><span class="sxs-lookup"><span data-stu-id="f2186-104">Get started with Azure Stream Analytics to process data from IoT devices</span></span>
<span data-ttu-id="f2186-105">이 자습서에서는 IoT(사물 인터넷) 장치에서 데이터를 수집하기 위한 스트림 처리 논리를 만드는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-105">In this tutorial, you will learn how to create stream-processing logic to gather data from Internet of Things (IoT) devices.</span></span> <span data-ttu-id="f2186-106">실제, IoT(사물 인터넷) 사용 사례를 사용하여 솔루션을 신속하고 경제적으로 구축하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-106">We will use a real-world, Internet of Things (IoT) use case to demonstrate how to build your solution quickly and economically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2186-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f2186-107">Prerequisites</span></span>
* [<span data-ttu-id="f2186-108">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="f2186-108">Azure subscription</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* <span data-ttu-id="f2186-109">샘플 쿼리 및 데이터 파일은 [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot)</span><span class="sxs-lookup"><span data-stu-id="f2186-109">Sample query and data files downloadable from [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot)</span></span>

## <a name="scenario"></a><span data-ttu-id="f2186-110">시나리오</span><span class="sxs-lookup"><span data-stu-id="f2186-110">Scenario</span></span>
<span data-ttu-id="f2186-111">Contoso는 산업용 자동화 공간의 회사로, 제조 프로세스를 완전히 자동화했습니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-111">Contoso, which is a company in the industrial automation space, has completely automated its manufacturing process.</span></span> <span data-ttu-id="f2186-112">이 공장의 기계에는 실시간으로 데이터 스트림을 내보낼 수 있는 센서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-112">The machinery in this plant has sensors that are capable of emitting streams of data in real time.</span></span> <span data-ttu-id="f2186-113">이 시나리오에서 생산 작업장 관리자는 센서 데이터로부터 실시간으로 정보를 얻어 패턴을 파악하고 조치를 취하고 싶어합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-113">In this scenario, a production floor manager wants to have real-time insights from the sensor data to look for patterns and take actions on them.</span></span> <span data-ttu-id="f2186-114">센서 데이터에 대해 SAQL(Stream Analytics 쿼리 언어)를 사용하여 들어오는 스트림 데이터에서 주목할 만한 패턴을 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-114">We will use the Stream Analytics Query Language (SAQL) over the sensor data to find interesting patterns from the incoming stream of data.</span></span>

<span data-ttu-id="f2186-115">여기서 데이터는 Texas Instrument 센서 태그 장치에서 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-115">Here data is being generated from a Texas Instruments sensor tag device.</span></span>

![Texas Instruments 센서 태그](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-01.jpg)

<span data-ttu-id="f2186-117">데이터의 페이로드는 JSON 형식이며 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-117">The payload of the data is in JSON format and looks like the following:</span></span>

    {
        "time": "2016-01-26T20:47:53.0000000",  
        "dspl": "sensorE",  
        "temp": 123,  
        "hmdt": 34  
    }  

<span data-ttu-id="f2186-118">실제 시나리오에서는 이러한 센서가 수백 개 있으며 이벤트를 스트림으로 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-118">In a real-world scenario, you could have hundreds of these sensors generating events as a stream.</span></span> <span data-ttu-id="f2186-119">이상적으로 게이트웨이 장치는 이러한 이벤트를 [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) 또는 [Azure IoT Hubs](https://azure.microsoft.com/services/iot-hub/)로 푸시하는 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-119">Ideally, a gateway device would run code to push these events to [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) or [Azure IoT Hubs](https://azure.microsoft.com/services/iot-hub/).</span></span> <span data-ttu-id="f2186-120">스트림 분석 작업은 이벤트 허브에서 이러한 이벤트를 수집하고 스트림에 대해 실시간 분석 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-120">Your Stream Analytics job would ingest these events from Event Hubs and run real-time analytics queries against the streams.</span></span> <span data-ttu-id="f2186-121">[지원되는 출력](stream-analytics-define-outputs.md) 중 하나에 결과를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-121">Then, you could send the results to one of the [supported outputs](stream-analytics-define-outputs.md).</span></span>

<span data-ttu-id="f2186-122">사용 편의성을 위해 이 시작 가이드는 실제 센서 태그 장치에서 캡처된 샘플 데이터 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-122">For ease of use, this getting started guide provides a sample data file, which was captured from real sensor tag devices.</span></span> <span data-ttu-id="f2186-123">샘플 데이터에서 쿼리를 실행하고 결과를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-123">You can run queries on the sample data and see results.</span></span> <span data-ttu-id="f2186-124">이후 자습서에서는 작업을 입력 및 출력에 연결하고 이를 Azure 서비스에 배포하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-124">In subsequent tutorials, you will learn how to connect your job to inputs and outputs and deploy them to the Azure service.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="f2186-125">스트림 분석 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="f2186-125">Create a Stream Analytics job</span></span>
1. <span data-ttu-id="f2186-126">[Azure 포털](http://portal.azure.com)에서 더하기 기호를 클릭한 다음 오른쪽에 있는 텍스트 창에서 **Stream Analytics**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-126">In the [Azure portal](http://portal.azure.com), click the plus sign and then type **STREAM ANALYTICS** in the text window to the right.</span></span> <span data-ttu-id="f2186-127">그런 다음 결과 목록에서 **Stream Analytics 작업**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-127">Then select **Stream Analytics job** in the results list.</span></span>
   
    ![새 스트림 분석 작업 만들기](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-02.png)
2. <span data-ttu-id="f2186-129">고유한 작업 이름을 입력하고 해당 작업에 대한 구독이 유효한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-129">Enter a unique job name and verify the subscription is the correct one for your job.</span></span> <span data-ttu-id="f2186-130">그런 다음 새 리소스 그룹을 만들거나 구독에 속한 기존 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-130">Then either create a new resource group or select an existing one on your subscription.</span></span>
3. <span data-ttu-id="f2186-131">작업의 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-131">Then select a location for your job.</span></span> <span data-ttu-id="f2186-132">데이터 전송의 처리 속도와 비용 감소를 위해 리소스 그룹 및 의도한 저장소 계정으로 동일한 위치를 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-132">For speed of processing and reduction of cost in data transfer selecting the same location as the resource group and intended storage account is recommended.</span></span>
   
    ![새 Stream Analytics 작업 만들기 세부 정보](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03.png)
   
   > [!NOTE]
   > <span data-ttu-id="f2186-134">이 저장소 계정은 지역당 한 번만 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-134">You should create this storage account only once per region.</span></span> <span data-ttu-id="f2186-135">이 저장소는 해당 지역에 생성되는 모든 Stream Analytics 작업에서 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-135">This storage will be shared across all Stream Analytics jobs that are created in that region.</span></span>
   > 
   > 
4. <span data-ttu-id="f2186-136">대시보드에서 작업을 배치할 확인란을 선택한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-136">Check the box to place your job on your dashboard and then click **CREATE**.</span></span>
   
    ![진행 중인 작업 만들기](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03a.png)
5. <span data-ttu-id="f2186-138">'배포 시작...'이 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-138">You should see a 'Deployment started...'</span></span> <span data-ttu-id="f2186-139">브라우저 창의 오른쪽 상단에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-139">displayed in the top right of your browser window.</span></span> <span data-ttu-id="f2186-140">그리고는 곧 아래와 같이 완료된 창으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-140">Soon it will change to a completed window as shown below.</span></span>
   
    ![진행 중인 작업 만들기](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03b.png)

### <a name="create-an-azure-stream-analytics-query"></a><span data-ttu-id="f2186-142">Azure Stream Analytics 쿼리 만들기</span><span class="sxs-lookup"><span data-stu-id="f2186-142">Create an Azure Stream Analytics query</span></span>
<span data-ttu-id="f2186-143">작업이 만들어졌으면 이제는 해당 작업을 열고 쿼리를 빌드할 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-143">After your job is created it's time to open it and build a query.</span></span> <span data-ttu-id="f2186-144">작업의 타일을 클릭하면 해당 작업에 쉽게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-144">You can easily access your job by clicking the tile for it.</span></span>

![작업 타일](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-04.png)

<span data-ttu-id="f2186-146">**작업 토폴로지** 창에서 **쿼리** 상자를 클릭하여 쿼리 편집기로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-146">In the **Job Topology** pane click the **QUERY** box to go to the Query Editor.</span></span> <span data-ttu-id="f2186-147">**쿼리** 편집기에서는 들어오는 이벤트 데이터에 대해 변환을 수행하는 T-SQL 쿼리를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-147">The **QUERY** editor allows you to enter a T-SQL query that performs the transformation over the incoming event data.</span></span>

![쿼리 상자](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-05.png)

### <a name="query-archive-your-raw-data"></a><span data-ttu-id="f2186-149">쿼리: 원시 데이터 보관</span><span class="sxs-lookup"><span data-stu-id="f2186-149">Query: Archive your raw data</span></span>
<span data-ttu-id="f2186-150">가장 간단한 형태의 쿼리는 모든 입력 데이터를 지정된 출력에 보관하는 통과 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-150">The simplest form of query is a pass-through query that archives all input data to its designated output.</span></span> <span data-ttu-id="f2186-151">[GitHub](https://aka.ms/azure-stream-analytics-get-started-iot)에서 컴퓨터의 위치로 샘플 데이터 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-151">Download the sample data file from [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot) to a location on your computer.</span></span> 

1. <span data-ttu-id="f2186-152">PassThrough.txt 파일에서 쿼리를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-152">Paste the query from the PassThrough.txt file.</span></span> 
   
    ![입력 스트림 테스트](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06.png)
2. <span data-ttu-id="f2186-154">사용자의 입력 옆에 있는 점 세 개를 클릭하고 **파일에서 샘플 데이터 업로드** 상자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-154">Click the three dots next to your input and select **Upload sample data from file** box.</span></span>
   
    ![입력 스트림 테스트](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06a.png)
3. <span data-ttu-id="f2186-156">오른쪽에 열리는 결과 창에서 다운로드 위치에 있는 HelloWorldASA InputStream.json 데이터 파일을 선택하고 창 맨 아래의 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-156">A pane opens on the right as a result, in it select the HelloWorldASA-InputStream.json data file from your downloaded location and click **OK** at the bottom of the pane.</span></span>
   
    ![입력 스트림 테스트](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06b.png)
4. <span data-ttu-id="f2186-158">그런 다음 창의 왼쪽 위에 있는 **테스트** 기어를 클릭하여 샘플 데이터 집합에 대한 테스트 쿼리를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-158">Then click the **Test** gear in the top left area of the window and process your test query against the sample dataset.</span></span> <span data-ttu-id="f2186-159">처리가 완료되면 쿼리 아래에 결과 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-159">A results window will open below your query as the processing is complete.</span></span>
   
    ![테스트 결과](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-07.png)

### <a name="query-filter-the-data-based-on-a-condition"></a><span data-ttu-id="f2186-161">쿼리: 조건에 따라 데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="f2186-161">Query: Filter the data based on a condition</span></span>
<span data-ttu-id="f2186-162">조건에 따라 결과를 필터링해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-162">Let’s try to filter the results based on a condition.</span></span> <span data-ttu-id="f2186-163">"sensorA"에서 가져온 해당 이벤트에 대한 결과만 표시하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-163">We would like to show results for only those events that come from “sensorA.”</span></span> <span data-ttu-id="f2186-164">쿼리는 Filtering.txt 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-164">The query is in the Filtering.txt file.</span></span>

![데이터 스트림 필터링](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-08.png)

<span data-ttu-id="f2186-166">대/소문자를 구분하는 쿼리는 문자열 값을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-166">Note that the case-sensitive query compares a string value.</span></span> <span data-ttu-id="f2186-167">**테스트** 기어를 다시 클릭하여 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-167">Click the **Test** gear again to execute the query.</span></span> <span data-ttu-id="f2186-168">쿼리는 1860개 이벤트 중 389행만 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-168">The query should return 389 rows out of 1860 events.</span></span>

![쿼리 테스트의 두 번째 출력 결과](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-09.png)

### <a name="query-alert-to-trigger-a-business-workflow"></a><span data-ttu-id="f2186-170">쿼리: 비즈니스 워크플로를 트리거하는 경고</span><span class="sxs-lookup"><span data-stu-id="f2186-170">Query: Alert to trigger a business workflow</span></span>
<span data-ttu-id="f2186-171">쿼리를 더 자세히 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-171">Let's make our query more detailed.</span></span> <span data-ttu-id="f2186-172">모든 유형의 센서에 대해 30초 기간당 평균 온도를 모니터링하고 평균 온도가 100도를 초과하는 경우만 결과를 표시하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-172">For every type of sensor, we want to monitor average temperature per 30-second window and display results only if the average temperature is above 100 degrees.</span></span> <span data-ttu-id="f2186-173">다음 쿼리를 작성한 후 **테스트**를 클릭하여 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-173">We will write the following query and then click **Test** to see the results.</span></span> <span data-ttu-id="f2186-174">쿼리는 ThresholdAlerting.txt 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-174">The query is in the ThresholdAlerting.txt file.</span></span>

![30초 필터 쿼리](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-10.png)

<span data-ttu-id="f2186-176">이제 결과에서 245행 및 평균 온도가 100도를 넘는 센서의 이름을 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-176">You should now see results that contain only 245 rows and names of sensors where the average temperate is greater than 100.</span></span> <span data-ttu-id="f2186-177">이 쿼리는 이벤트의 스트림을 30초 동안의 **연속 창**에서 센서 이름인 **dspl**로 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-177">This query groups the stream of events by **dspl**, which is the sensor name, over a **Tumbling Window** of 30 seconds.</span></span> <span data-ttu-id="f2186-178">임시 쿼리는 시간을 진행할 방법을 명시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-178">Temporal queries must state how we want time to progress.</span></span> <span data-ttu-id="f2186-179">**TIMESTAMP BY** 절을 사용하여 모든 임시 계산과 시간을 연결하는 **OUTPUTTIME** 열을 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-179">By using the **TIMESTAMP BY** clause, we have specified the **OUTPUTTIME** column to associate times with all temporal calculations.</span></span> <span data-ttu-id="f2186-180">자세한 정보는 [시간 관리](https://msdn.microsoft.com/library/azure/mt582045.aspx) 및 [기간 이동 기능](https://msdn.microsoft.com/library/azure/dn835019.aspx)에 대한 MSDN 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2186-180">For detailed information, read the MSDN articles about [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing functions](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span></span>

### <a name="query-detect-absence-of-events"></a><span data-ttu-id="f2186-181">쿼리: 이벤트 부재 감지</span><span class="sxs-lookup"><span data-stu-id="f2186-181">Query: Detect absence of events</span></span>
<span data-ttu-id="f2186-182">이벤트의 부족을 찾기 위해 어떻게 쿼리를 작성할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="f2186-182">How can we write a query to find a lack of input events?</span></span> <span data-ttu-id="f2186-183">센서가 데이터를 전송한 다음 1분 동안 이벤트를 보내지 않은 마지막 시간을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-183">Let’s find the last time that a sensor sent data and then did not send events for the next minute.</span></span> <span data-ttu-id="f2186-184">쿼리는 AbsenseOfEvent.txt 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-184">The query is in the AbsenseOfEvent.txt file.</span></span>

![이벤트의 부재 감지](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-11.png)

<span data-ttu-id="f2186-186">여기서는 동일한 데이터 스트림에 대해 **왼쪽 외부** 조인을 사용합니다(자체 조인).</span><span class="sxs-lookup"><span data-stu-id="f2186-186">Here we use a **LEFT OUTER** join to the same data stream (self-join).</span></span> <span data-ttu-id="f2186-187">**내부** 조인의 경우 결과는 일치 항목이 있는 경우에만 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-187">For an **INNER** join, a result is returned only when a match is found.</span></span>  <span data-ttu-id="f2186-188">하지만 **왼쪽 외부** 조인의 경우 조인 왼쪽의 이벤트가 일치하지 않는 경우 오른쪽 행의 모든 열에 대해 NULL이 있는 행이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-188">For a **LEFT OUTER** join, if an event from the left side of the join is unmatched, a row that has NULL for all the columns of the right side is returned.</span></span> <span data-ttu-id="f2186-189">이 방법은 이벤트의 부재를 찾는 데 매우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-189">This technique is very useful to find an absence of events.</span></span> <span data-ttu-id="f2186-190">[조인](https://msdn.microsoft.com/library/azure/dn835026.aspx)에 대한 자세한 내용은 MSDN 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2186-190">See our MSDN documentation for more information about [JOIN](https://msdn.microsoft.com/library/azure/dn835026.aspx).</span></span>

## <a name="conclusion"></a><span data-ttu-id="f2186-191">결론</span><span class="sxs-lookup"><span data-stu-id="f2186-191">Conclusion</span></span>
<span data-ttu-id="f2186-192">이 자습서의 목적은 다른 Stream Analytics 쿼리 언어 쿼리를 작성하고 브라우저에서 결과를 확인하는 방법을 보여 주는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-192">The purpose of this tutorial is to demonstrate how to write different Stream Analytics Query Language queries and see results in the browser.</span></span> <span data-ttu-id="f2186-193">그러나 이 과정은 시작일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-193">However, this is just getting started.</span></span> <span data-ttu-id="f2186-194">Stream Analytics으로 많은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-194">You can do so much more with Stream Analytics.</span></span> <span data-ttu-id="f2186-195">Stream Analytics은 다양한 입력 및 출력을 지원하고 Azure Machine Learning에서 함수를 사용하여 데이터 스트림을 분석하는 강력한 도구로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-195">Stream Analytics supports a variety of inputs and outputs and can even use functions in Azure Machine Learning to make it a robust tool for analyzing data streams.</span></span> <span data-ttu-id="f2186-196">[학습 맵](https://azure.microsoft.com/documentation/learning-paths/stream-analytics/)을 사용하여 Stream Analytics에 대한 탐색을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2186-196">You can start to explore more about Stream Analytics by using our [learning map](https://azure.microsoft.com/documentation/learning-paths/stream-analytics/).</span></span> <span data-ttu-id="f2186-197">쿼리를 작성하는 방법에 대한 자세한 내용은 [일반적인 쿼리 패턴](stream-analytics-stream-analytics-query-patterns.md)에 대한 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2186-197">For more information about how to write queries, read the article about [common query patterns](stream-analytics-stream-analytics-query-patterns.md).</span></span>

