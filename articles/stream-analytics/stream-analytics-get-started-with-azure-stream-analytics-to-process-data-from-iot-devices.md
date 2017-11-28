---
title: "aaaIoT 실시간 데이터 스트림 및 Azure 스트림 분석 | Microsoft Docs"
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
ms.openlocfilehash: 422e6b719d0289880aa7f17fdc585e2b768c63d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-stream-analytics-tooprocess-data-from-iot-devices"></a><span data-ttu-id="116eb-104">IoT 장치에서 Azure 스트림 분석 tooprocess 데이터 시작</span><span class="sxs-lookup"><span data-stu-id="116eb-104">Get started with Azure Stream Analytics tooprocess data from IoT devices</span></span>
<span data-ttu-id="116eb-105">이 자습서에서는 살펴보겠습니다 어떻게 toocreate 스트림 처리 논리 toogather 장치에서에서 데이터를 인터넷 IoT (사물).</span><span class="sxs-lookup"><span data-stu-id="116eb-105">In this tutorial, you will learn how toocreate stream-processing logic toogather data from Internet of Things (IoT) devices.</span></span> <span data-ttu-id="116eb-106">사용 하 여 실제, 인터넷 IoT (사물) 사용 하 여 사례 toodemonstrate 어떻게 toobuild 솔루션 신속 하 고 경제적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-106">We will use a real-world, Internet of Things (IoT) use case toodemonstrate how toobuild your solution quickly and economically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="116eb-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="116eb-107">Prerequisites</span></span>
* [<span data-ttu-id="116eb-108">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="116eb-108">Azure subscription</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* <span data-ttu-id="116eb-109">샘플 쿼리 및 데이터 파일은 [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot)</span><span class="sxs-lookup"><span data-stu-id="116eb-109">Sample query and data files downloadable from [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot)</span></span>

## <a name="scenario"></a><span data-ttu-id="116eb-110">시나리오</span><span class="sxs-lookup"><span data-stu-id="116eb-110">Scenario</span></span>
<span data-ttu-id="116eb-111">Hello 산업 자동화 공간에서 회사는 Contoso의 제조 프로세스 완전히 자동화 했습니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-111">Contoso, which is a company in hello industrial automation space, has completely automated its manufacturing process.</span></span> <span data-ttu-id="116eb-112">이 공장의 hello 기계 스트림을 실시간으로 데이터를 내보낼 수 있는 센서에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-112">hello machinery in this plant has sensors that are capable of emitting streams of data in real time.</span></span> <span data-ttu-id="116eb-113">이 시나리오는 프로덕션 floor 관리자 hello 센서 데이터 toolook에서 실시간 정보 toohave 서빙 직원을 위한 패턴 및에 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-113">In this scenario, a production floor manager wants toohave real-time insights from hello sensor data toolook for patterns and take actions on them.</span></span> <span data-ttu-id="116eb-114">데이터의 hello 들어오는 스트림에서 hello 센서 데이터 toofind 주목할 만한 패턴을 통해 스트림 분석 쿼리 언어 (SAQL) hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-114">We will use hello Stream Analytics Query Language (SAQL) over hello sensor data toofind interesting patterns from hello incoming stream of data.</span></span>

<span data-ttu-id="116eb-115">여기서 데이터는 Texas Instrument 센서 태그 장치에서 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-115">Here data is being generated from a Texas Instruments sensor tag device.</span></span>

![Texas Instruments 센서 태그](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-01.jpg)

<span data-ttu-id="116eb-117">hello 데이터 페이로드를 hello JSON 형식 이므로 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-117">hello payload of hello data is in JSON format and looks like hello following:</span></span>

    {
        "time": "2016-01-26T20:47:53.0000000",  
        "dspl": "sensorE",  
        "temp": 123,  
        "hmdt": 34  
    }  

<span data-ttu-id="116eb-118">실제 시나리오에서는 이러한 센서가 수백 개 있으며 이벤트를 스트림으로 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-118">In a real-world scenario, you could have hundreds of these sensors generating events as a stream.</span></span> <span data-ttu-id="116eb-119">이상적으로 게이트웨이 장치는 실행 코드 toopush 이러한 이벤트 너무[Azure 이벤트 허브](https://azure.microsoft.com/services/event-hubs/) 또는 [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/)합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-119">Ideally, a gateway device would run code toopush these events too[Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) or [Azure IoT Hubs](https://azure.microsoft.com/services/iot-hub/).</span></span> <span data-ttu-id="116eb-120">스트림 분석 작업 이벤트 허브에서 이러한 이벤트를 수집 하 고 hello 스트림에 대해 실시간 분석 쿼리를 실행할 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-120">Your Stream Analytics job would ingest these events from Event Hubs and run real-time analytics queries against hello streams.</span></span> <span data-ttu-id="116eb-121">Hello의 hello 결과 tooone를 보낼 수 있으며 그런 다음 [출력 지원](stream-analytics-define-outputs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-121">Then, you could send hello results tooone of hello [supported outputs](stream-analytics-define-outputs.md).</span></span>

<span data-ttu-id="116eb-122">사용 편의성을 위해 이 시작 가이드는 실제 센서 태그 장치에서 캡처된 샘플 데이터 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-122">For ease of use, this getting started guide provides a sample data file, which was captured from real sensor tag devices.</span></span> <span data-ttu-id="116eb-123">Hello 예제 데이터에서 쿼리를 실행 하 고 결과 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-123">You can run queries on hello sample data and see results.</span></span> <span data-ttu-id="116eb-124">이후 자습서에 설명 합니다 방법을 tooconnect 프로그램 tooinputs / 출력 작업 및 toohello Azure 서비스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-124">In subsequent tutorials, you will learn how tooconnect your job tooinputs and outputs and deploy them toohello Azure service.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="116eb-125">Stream Analytics 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="116eb-125">Create a Stream Analytics job</span></span>
1. <span data-ttu-id="116eb-126">Hello에 [Azure 포털](http://portal.azure.com)hello 더하기 기호를 클릭 한 다음 입력, **스트림 분석** hello 텍스트 창 toohello 오른쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-126">In hello [Azure portal](http://portal.azure.com), click hello plus sign and then type **STREAM ANALYTICS** in hello text window toohello right.</span></span> <span data-ttu-id="116eb-127">그런 다음 선택 **스트림 분석 작업** hello 결과 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-127">Then select **Stream Analytics job** in hello results list.</span></span>
   
    ![새 스트림 분석 작업 만들기](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-02.png)
2. <span data-ttu-id="116eb-129">고유한 작업 이름을 입력 하 고 hello 구독 작업에 적절 한 hello는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-129">Enter a unique job name and verify hello subscription is hello correct one for your job.</span></span> <span data-ttu-id="116eb-130">그런 다음 새 리소스 그룹을 만들거나 구독에 속한 기존 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-130">Then either create a new resource group or select an existing one on your subscription.</span></span>
3. <span data-ttu-id="116eb-131">작업의 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-131">Then select a location for your job.</span></span> <span data-ttu-id="116eb-132">처리 속도 hello를 선택 하는 데이터 전송에서 비용을 절감 하는 역할에 대 한 hello 리소스 그룹 및 의도 한 저장소 계정이 동일한 위치 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-132">For speed of processing and reduction of cost in data transfer selecting hello same location as hello resource group and intended storage account is recommended.</span></span>
   
    ![새 Stream Analytics 작업 만들기 세부 정보](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03.png)
   
   > [!NOTE]
   > <span data-ttu-id="116eb-134">이 저장소 계정은 지역당 한 번만 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-134">You should create this storage account only once per region.</span></span> <span data-ttu-id="116eb-135">이 저장소는 해당 지역에 생성되는 모든 Stream Analytics 작업에서 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-135">This storage will be shared across all Stream Analytics jobs that are created in that region.</span></span>
   > 
   > 
4. <span data-ttu-id="116eb-136">Hello 상자 tooplace 대시보드 작업을 확인 하 고 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-136">Check hello box tooplace your job on your dashboard and then click **CREATE**.</span></span>
   
    ![진행 중인 작업 만들기](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03a.png)
5. <span data-ttu-id="116eb-138">'배포 시작...'를 참조 해야 브라우저 창의 오른쪽 위 hello에에서 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-138">You should see a 'Deployment started...' displayed in hello top right of your browser window.</span></span> <span data-ttu-id="116eb-139">곧 아래와 같이 완료 tooa 창이 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-139">Soon it will change tooa completed window as shown below.</span></span>
   
    ![진행 중인 작업 만들기](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03b.png)

### <a name="create-an-azure-stream-analytics-query"></a><span data-ttu-id="116eb-141">Azure Stream Analytics 쿼리 만들기</span><span class="sxs-lookup"><span data-stu-id="116eb-141">Create an Azure Stream Analytics query</span></span>
<span data-ttu-id="116eb-142">후 작업을 만든 시간 tooopen 쿼리 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-142">After your job is created it's time tooopen it and build a query.</span></span> <span data-ttu-id="116eb-143">에 대 한 hello 타일을 클릭 하 여 작업을 쉽게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-143">You can easily access your job by clicking hello tile for it.</span></span>

![작업 타일](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-04.png)

<span data-ttu-id="116eb-145">Hello에 **작업 토폴로지** 창의 hello 클릭 **쿼리** toogo toohello 쿼리 편집기 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-145">In hello **Job Topology** pane click hello **QUERY** box toogo toohello Query Editor.</span></span> <span data-ttu-id="116eb-146">hello **쿼리** hello 들어오는 이벤트 데이터에 대해 hello 변환을 수행 하는 T-SQL tooenter 쿼리 편집기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-146">hello **QUERY** editor allows you tooenter a T-SQL query that performs hello transformation over hello incoming event data.</span></span>

![쿼리 상자](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-05.png)

### <a name="query-archive-your-raw-data"></a><span data-ttu-id="116eb-148">쿼리: 원시 데이터 보관</span><span class="sxs-lookup"><span data-stu-id="116eb-148">Query: Archive your raw data</span></span>
<span data-ttu-id="116eb-149">쿼리 hello 가장 간단한 형태는 출력을 지정 하는 모든 입력된 데이터 tooits 보관 하는 통과 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-149">hello simplest form of query is a pass-through query that archives all input data tooits designated output.</span></span> <span data-ttu-id="116eb-150">Hello 예제 데이터 파일의 다운로드 [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot) 컴퓨터에서 tooa 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-150">Download hello sample data file from [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot) tooa location on your computer.</span></span> 

1. <span data-ttu-id="116eb-151">Hello PassThrough.txt 파일에서 hello 쿼리를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-151">Paste hello query from hello PassThrough.txt file.</span></span> 
   
    ![입력 스트림 테스트](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06.png)
2. <span data-ttu-id="116eb-153">Hello 3 점 다음 tooyour 입력을 클릭 하 고 선택 **파일에서 샘플 데이터 업로드** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-153">Click hello three dots next tooyour input and select **Upload sample data from file** box.</span></span>
   
    ![입력 스트림 테스트](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06a.png)
3. <span data-ttu-id="116eb-155">결과 오른쪽으로 hello에는 창이 열립니다에 select hello HelloWorldASA InputStream.json 데이터 파일을 다운로드 한 위치에서 클릭 **확인** hello hello 창 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-155">A pane opens on hello right as a result, in it select hello HelloWorldASA-InputStream.json data file from your downloaded location and click **OK** at hello bottom of hello pane.</span></span>
   
    ![입력 스트림 테스트](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06b.png)
4. <span data-ttu-id="116eb-157">Hello 클릭 **테스트** hello 창의 왼쪽 hello 위에에서 기어를 hello 샘플 데이터 집합에 대해 테스트 쿼리를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-157">Then click hello **Test** gear in hello top left area of hello window and process your test query against hello sample dataset.</span></span> <span data-ttu-id="116eb-158">Hello 처리가 완료 될 때 쿼리 아래 결과 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-158">A results window will open below your query as hello processing is complete.</span></span>
   
    ![테스트 결과](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-07.png)

### <a name="query-filter-hello-data-based-on-a-condition"></a><span data-ttu-id="116eb-160">조건에 따라 hello 데이터를 필터링 하는 쿼리:</span><span class="sxs-lookup"><span data-stu-id="116eb-160">Query: Filter hello data based on a condition</span></span>
<span data-ttu-id="116eb-161">조건에 따라 toofilter hello 결과 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-161">Let’s try toofilter hello results based on a condition.</span></span> <span data-ttu-id="116eb-162">"SensorA"에서 제공 하는 이벤트에 대 한 tooshow 결과 같은</span><span class="sxs-lookup"><span data-stu-id="116eb-162">We would like tooshow results for only those events that come from “sensorA.”</span></span> <span data-ttu-id="116eb-163">hello 쿼리 hello Filtering.txt 파일에는입니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-163">hello query is in hello Filtering.txt file.</span></span>

![데이터 스트림 필터링](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-08.png)

<span data-ttu-id="116eb-165">Hello 대/소문자 구분 쿼리 하는 문자열 값을 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-165">Note that hello case-sensitive query compares a string value.</span></span> <span data-ttu-id="116eb-166">Hello 클릭 **테스트** 기어 다시 tooexecute hello 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-166">Click hello **Test** gear again tooexecute hello query.</span></span> <span data-ttu-id="116eb-167">hello 쿼리 389 행 1860 이벤트 밖으로 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-167">hello query should return 389 rows out of 1860 events.</span></span>

![쿼리 테스트의 두 번째 출력 결과](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-09.png)

### <a name="query-alert-tootrigger-a-business-workflow"></a><span data-ttu-id="116eb-169">쿼리: 경고 tootrigger 비즈니스 워크플로</span><span class="sxs-lookup"><span data-stu-id="116eb-169">Query: Alert tootrigger a business workflow</span></span>
<span data-ttu-id="116eb-170">쿼리를 더 자세히 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-170">Let's make our query more detailed.</span></span> <span data-ttu-id="116eb-171">모든 유형의 센서에 대 한 30 초 창당 toomonitor 평균 온도 원하는 म 고 hello 평균 온도 100 이상인 경우에 결과 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-171">For every type of sensor, we want toomonitor average temperature per 30-second window and display results only if hello average temperature is above 100 degrees.</span></span> <span data-ttu-id="116eb-172">Hello 다음 쿼리하고 클릭 작성 하 **테스트** toosee hello 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-172">We will write hello following query and then click **Test** toosee hello results.</span></span> <span data-ttu-id="116eb-173">hello 쿼리 hello ThresholdAlerting.txt 파일에는입니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-173">hello query is in hello ThresholdAlerting.txt file.</span></span>

![30초 필터 쿼리](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-10.png)

<span data-ttu-id="116eb-175">이제 표시 되어야만 245 행과 센서의 이름을 포함 하는 결과 온도 hello 평균이 100 보다 큰 합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-175">You should now see results that contain only 245 rows and names of sensors where hello average temperate is greater than 100.</span></span> <span data-ttu-id="116eb-176">이 쿼리로 이벤트의 hello 스트림을 그룹화 **dspl**는 hello 센서 이름을 초과 하는 한 **텀블 링 창** 30 초입니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-176">This query groups hello stream of events by **dspl**, which is hello sensor name, over a **Tumbling Window** of 30 seconds.</span></span> <span data-ttu-id="116eb-177">임시 쿼리 시간 tooprogress 원하는 라고 명시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-177">Temporal queries must state how we want time tooprogress.</span></span> <span data-ttu-id="116eb-178">Hello를 사용 하 여 **TIMESTAMP BY** 절 hello 앞서 지정한 **OUTPUTTIME** 열 tooassociate 시간이 모든 임시 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-178">By using hello **TIMESTAMP BY** clause, we have specified hello **OUTPUTTIME** column tooassociate times with all temporal calculations.</span></span> <span data-ttu-id="116eb-179">에 대 한 자세한 정보에 대 한 hello MSDN 문서를 읽을 [시간 관리](https://msdn.microsoft.com/library/azure/mt582045.aspx) 및 [창 작업 기능](https://msdn.microsoft.com/library/azure/dn835019.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-179">For detailed information, read hello MSDN articles about [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing functions](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span></span>

### <a name="query-detect-absence-of-events"></a><span data-ttu-id="116eb-180">쿼리: 이벤트 부재 감지</span><span class="sxs-lookup"><span data-stu-id="116eb-180">Query: Detect absence of events</span></span>
<span data-ttu-id="116eb-181">에서는 작성 방법을 쿼리 toofind 입력된 이벤트의 부족?</span><span class="sxs-lookup"><span data-stu-id="116eb-181">How can we write a query toofind a lack of input events?</span></span> <span data-ttu-id="116eb-182">센서 데이터를 전송 하 고 다음 다음 분 hello에 대 한 이벤트를 보내지 않은 hello 마지막으로 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-182">Let’s find hello last time that a sensor sent data and then did not send events for hello next minute.</span></span> <span data-ttu-id="116eb-183">hello 쿼리 hello AbsenseOfEvent.txt 파일에는입니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-183">hello query is in hello AbsenseOfEvent.txt file.</span></span>

![이벤트의 부재 감지](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-11.png)

<span data-ttu-id="116eb-185">사용 하 여 여기는 **LEFT OUTER** toohello 조인 동일한 데이터 스트림 (자체 조인).</span><span class="sxs-lookup"><span data-stu-id="116eb-185">Here we use a **LEFT OUTER** join toohello same data stream (self-join).</span></span> <span data-ttu-id="116eb-186">**내부** 조인의 경우 결과는 일치 항목이 있는 경우에만 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-186">For an **INNER** join, a result is returned only when a match is found.</span></span>  <span data-ttu-id="116eb-187">에 대 한는 **LEFT OUTER** 조인을 경우 hello hello 조인의 왼쪽의 이벤트를 일치 하지 않으면 모든 hello hello 오른쪽의 열에 대 한 NULL이 있는 행 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-187">For a **LEFT OUTER** join, if an event from hello left side of hello join is unmatched, a row that has NULL for all hello columns of hello right side is returned.</span></span> <span data-ttu-id="116eb-188">이 방법은 매우 유용한 toofind 이벤트의 부재입니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-188">This technique is very useful toofind an absence of events.</span></span> <span data-ttu-id="116eb-189">[조인](https://msdn.microsoft.com/library/azure/dn835026.aspx)에 대한 자세한 내용은 MSDN 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="116eb-189">See our MSDN documentation for more information about [JOIN](https://msdn.microsoft.com/library/azure/dn835026.aspx).</span></span>

## <a name="conclusion"></a><span data-ttu-id="116eb-190">결론</span><span class="sxs-lookup"><span data-stu-id="116eb-190">Conclusion</span></span>
<span data-ttu-id="116eb-191">hello이이 자습서의 목적은 toodemonstrate toowrite 다른 스트림 분석 쿼리 언어 쿼리 및 참조 hello 브라우저에서 발생 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-191">hello purpose of this tutorial is toodemonstrate how toowrite different Stream Analytics Query Language queries and see results in hello browser.</span></span> <span data-ttu-id="116eb-192">그러나 이 과정은 시작일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-192">However, this is just getting started.</span></span> <span data-ttu-id="116eb-193">Stream Analytics으로 많은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-193">You can do so much more with Stream Analytics.</span></span> <span data-ttu-id="116eb-194">스트림 분석은 다양 한 입력 및 출력을 지원 및 수에 사용 하 여 함수가 Azure 기계 학습 toomake 것 데이터 스트림 분석 하기 위한 강력한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-194">Stream Analytics supports a variety of inputs and outputs and can even use functions in Azure Machine Learning toomake it a robust tool for analyzing data streams.</span></span> <span data-ttu-id="116eb-195">사용 하 여 스트림 분석에 대 한 자세한 tooexplore를 시작할 수 있습니다이 [학습 맵](https://azure.microsoft.com/documentation/learning-paths/stream-analytics/)합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-195">You can start tooexplore more about Stream Analytics by using our [learning map](https://azure.microsoft.com/documentation/learning-paths/stream-analytics/).</span></span> <span data-ttu-id="116eb-196">방법에 대 한 자세한 내용은 대 한 hello 문서를 참조 하는 쿼리를 toowrite [일반 쿼리 패턴](stream-analytics-stream-analytics-query-patterns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="116eb-196">For more information about how toowrite queries, read hello article about [common query patterns](stream-analytics-stream-analytics-query-patterns.md).</span></span>

