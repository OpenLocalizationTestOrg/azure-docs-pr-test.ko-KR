---
title: "Azure 스트림 분석에서 aaaPower BI 대시보드 | Microsoft Docs"
description: "실시간 스트리밍 Power BI 대시보드 toogather 비즈니스 인텔리전스를 사용 하 고 스트림 분석 작업에서 대용량 데이터를 분석 합니다."
keywords: "분석 대시보드, 실시간 대시보드"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: fe8db732-4397-4e58-9313-fec9537aa2ad
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: jeffstok
ms.openlocfilehash: cb9127576230e9d327b437b674f31cc23869bfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a><span data-ttu-id="337e5-104">Stream Analytics 및 Power BI: 스트리밍 데이터에 대한 실시간 분석 대시보드</span><span class="sxs-lookup"><span data-stu-id="337e5-104">Stream Analytics and Power BI: A real-time analytics dashboard for streaming data</span></span>
<span data-ttu-id="337e5-105">Azure 스트림 분석 하면 비즈니스 인텔리전스 도구를 선행 hello 중 하나의 tootake 이점은 [Microsoft Power BI](https://powerbi.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-105">Azure Stream Analytics enables you tootake advantage of one of hello leading business intelligence tools, [Microsoft Power BI](https://powerbi.com/).</span></span> <span data-ttu-id="337e5-106">이 문서에서는 Azure Stream Analytics 작업에 대한 출력으로 Power BI를 사용하여 비즈니스 인텔리전스 도구를 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-106">In this article, you learn how create business intelligence tools by using Power BI as an output for your Azure Stream Analytics jobs.</span></span> <span data-ttu-id="337e5-107">또한 학습 방법을 toocreate 실시간 대시보드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-107">You also learn how toocreate and use a real-time dashboard.</span></span>

<span data-ttu-id="337e5-108">이 문서는 hello 스트림 분석에서에서 계속 [실시간 사기 감지](stream-analytics-real-time-fraud-detection.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-108">This article continues from hello Stream Analytics [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="337e5-109">해당 자습서에서 만든 hello 워크플로 작성 하 고 출력 스트리밍 분석 작업에서 검색 되는 사기성 전화 통화를 시각화할 수 있도록 Power BI에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-109">It builds on hello workflow created in that tutorial and adds a Power BI output so that you can visualize fraudulent phone calls that are detected by a Streaming Analytics job.</span></span> 

<span data-ttu-id="337e5-110">이 시나리오를 보여주는 [비디오](https://www.youtube.com/watch?v=SGUpT-a99MA)를 시청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-110">You can watch [a video](https://www.youtube.com/watch?v=SGUpT-a99MA)  that illustrates this scenario.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="337e5-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="337e5-111">Prerequisites</span></span>

<span data-ttu-id="337e5-112">시작 하기 전에 hello 다음 항목이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-112">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="337e5-113">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="337e5-113">An Azure account.</span></span>
* <span data-ttu-id="337e5-114">Power BI에 대한 계정.</span><span class="sxs-lookup"><span data-stu-id="337e5-114">An account for Power BI.</span></span> <span data-ttu-id="337e5-115">회사 계정 또는 학교 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-115">You can use a work account or a school account.</span></span>
* <span data-ttu-id="337e5-116">완성 된 버전의 hello [실시간 사기 감지](stream-analytics-real-time-fraud-detection.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-116">A completed version of hello [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="337e5-117">hello 자습서는 가상의 전화 통화 메타 데이터를 생성 하는 응용 프로그램을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-117">hello tutorial includes an app that generates fictitious telephone-call metadata.</span></span> <span data-ttu-id="337e5-118">Hello 자습서에서는 이벤트 허브는 만들고 hello 전화 통화 데이터 toohello 이벤트 허브를 스트리밍 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-118">In hello tutorial, you create an event hub and send hello streaming phone call data toohello event hub.</span></span> <span data-ttu-id="337e5-119">사기성 호출 (호출 hello hello에 같은 수의 시간이 서로 다른 위치에)를 검색 하는 쿼리를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-119">You write a query that detects fraudulent calls (calls from hello same number at hello same time in different locations).</span></span> 


## <a name="add-power-bi-output"></a><span data-ttu-id="337e5-120">Power BI 출력 추가</span><span class="sxs-lookup"><span data-stu-id="337e5-120">Add Power BI output</span></span>
<span data-ttu-id="337e5-121">Hello 실시간 사기 감지 자습서 hello 출력 tooAzure Blob 저장소를 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-121">In hello real-time fraud detection tutorial, hello output is sent tooAzure Blob storage.</span></span> <span data-ttu-id="337e5-122">이 섹션의 정보 tooPower BI 전송 하는 출력을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-122">In this section, you add an output that sends information tooPower BI.</span></span>

1. <span data-ttu-id="337e5-123">Hello Azure 포털에서에서 앞에서 만든 hello 스트리밍 분석 작업을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-123">In hello Azure portal, open hello Streaming Analytics job that you created earlier.</span></span> <span data-ttu-id="337e5-124">Hello 작업의 이름은 hello 제안 된 이름을 사용 하는 경우 `sa_frauddetection_job_demo`합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-124">If you used hello suggested name, hello job is named `sa_frauddetection_job_demo`.</span></span>

2. <span data-ttu-id="337e5-125">선택 hello **출력** 상자 hello 작업 대시보드의 hello 중간에 선택한 후 **+ 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-125">Select hello **Outputs** box in hello middle of hello job dashboard and then select **+ Add**.</span></span>

3. <span data-ttu-id="337e5-126">**출력 별칭**에 `CallStream-PowerBI`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-126">For **Output Alias**, enter `CallStream-PowerBI`.</span></span> <span data-ttu-id="337e5-127">다른 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-127">You can use a different name.</span></span> <span data-ttu-id="337e5-128">이렇게 하면 hello 이름을 나중에 필요 하기 때문에, 메모를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-128">If you do, make a note of it, because you need hello name later.</span></span> 

4. <span data-ttu-id="337e5-129">**싱크** 아래에서 **Power BI**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-129">Under **Sink**, select **Power BI**.</span></span>

   ![Power BI에 대한 출력 만들기](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. <span data-ttu-id="337e5-131">**권한 부여**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-131">Click **Authorize**.</span></span>

    <span data-ttu-id="337e5-132">회사 또는 학교 계정에 대한 Azure 자격 증명을 제공할 수 있는 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-132">A window opens where you can provide your Azure credentials for a work or school account.</span></span> 

    ![액세스 tooPower BI에 대 한 자격 증명을 입력 합니다.](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. <span data-ttu-id="337e5-134">자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-134">Enter your credentials.</span></span> <span data-ttu-id="337e5-135">업그레이드할 경우 자격 증명을 입력 하면 하는 또한 부여 권한을 toohello 스트리밍 분석 작업 tooaccess 사용자 Power BI의 지역 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-135">Be aware then when you enter your credentials, you're also giving permission toohello Streaming Analytics job tooaccess your Power BI area.</span></span>

7. <span data-ttu-id="337e5-136">Toohello을 반환 하는 때 **새 출력** 블레이드에서 hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-136">When you're returned toohello **New output** blade, enter hello following information:</span></span>

    * <span data-ttu-id="337e5-137">**그룹 작업 영역**: toocreate hello 데이터 집합을 원하는 Power BI 테 넌 트의 작업 영역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-137">**Group Workspace**: Select a workspace in your Power BI tenant where you want toocreate hello dataset.</span></span>
    * <span data-ttu-id="337e5-138">**데이터 집합 이름**: `sa-dataset`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-138">**Dataset Name**:  Enter `sa-dataset`.</span></span> <span data-ttu-id="337e5-139">다른 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-139">You can use a different name.</span></span> <span data-ttu-id="337e5-140">이 경우 나중을 위해 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-140">If you do, make a note of it for later.</span></span>
    * <span data-ttu-id="337e5-141">**테이블 이름**: `fraudulent-calls`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-141">**Table Name**: Enter `fraudulent-calls`.</span></span> <span data-ttu-id="337e5-142">현재, Stream Analytics 작업의 Power BI 출력에는 하나의 데이터 집합에 하나의 테이블만 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-142">Currently, Power BI output from Stream Analytics jobs can have only one table in a dataset.</span></span>

    ![PBI 작업 영역](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > <span data-ttu-id="337e5-144">Power BI 데이터 집합에 없는 테이블 hello hello와 이름이 같은 hello Stream Analytics 작업에서 지정 하는 경우는 스토리를 기존 hello가 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-144">If Power BI has a dataset and table that have hello same names as hello ones that you specify in hello Stream Analytics job, hello existing ones are overwritten.</span></span>
    > <span data-ttu-id="337e5-145">이 데이터 집합 및 테이블을 Power BI 계정에 명시적으로 만들지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-145">We recommend that you do not explicitly create this dataset and table in your Power BI account.</span></span> <span data-ttu-id="337e5-146">스트림 분석 작업 시작 hello 작업 Power BI에 대리 펌핑 출력을 시작 하는 경우 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-146">They are automatically created when you start your Stream Analytics job and hello job starts pumping output into Power BI.</span></span> <span data-ttu-id="337e5-147">작업 쿼리 어떤 결과도 반환 하지 않는 경우 hello 데이터 집합 및 테이블 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-147">If your job query doesn't return any results, hello dataset and table are not  created.</span></span>
    >

8. <span data-ttu-id="337e5-148">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-148">Click **Create**.</span></span>

<span data-ttu-id="337e5-149">hello dataset hello 다음 설정으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-149">hello dataset is created with hello following settings:</span></span>

* <span data-ttu-id="337e5-150">**defaultRetentionPolicy: BasicFIFO**:데이터는 FIFO이고, 최대 200,000개의 행이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-150">**defaultRetentionPolicy: BasicFIFO**: Data is FIFO, with a maximum of 200,000 rows.</span></span>
* <span data-ttu-id="337e5-151">**defaultMode: pushStreaming**: hello dataset 스트리밍 타일 및 기존 보고서를 기반으로 시각적 개체를 모두 지원 (규칙 하위</span><span class="sxs-lookup"><span data-stu-id="337e5-151">**defaultMode: pushStreaming**: hello dataset supports both streaming tiles and traditional report-based visuals (a.k.a.</span></span> <span data-ttu-id="337e5-152">푸시)를 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-152">push).</span></span>

<span data-ttu-id="337e5-153">지금은 다른 플래그로 데이터 집합을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-153">Currently, you can't create datasets with other flags.</span></span>

<span data-ttu-id="337e5-154">Power BI 데이터 집합에 대 한 자세한 내용은 참조 hello [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-154">For more information about Power BI datasets, see hello [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) reference.</span></span>


## <a name="write-hello-query"></a><span data-ttu-id="337e5-155">Hello 쿼리 작성</span><span class="sxs-lookup"><span data-stu-id="337e5-155">Write hello query</span></span>

1. <span data-ttu-id="337e5-156">닫기 hello **출력** 블레이드에 대 한 반환 toohello 작업 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-156">Close hello **Outputs** blade and return toohello job blade.</span></span>

2. <span data-ttu-id="337e5-157">Hello 클릭 **쿼리** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-157">Click hello **Query** box.</span></span> 

3. <span data-ttu-id="337e5-158">다음 쿼리에서 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-158">Enter hello following query.</span></span> <span data-ttu-id="337e5-159">이 쿼리는 비슷한 toohello 자체 조인 쿼리 hello 사기 감지 자습서에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-159">This query is similar toohello self-join query you created in hello fraud-detection tutorial.</span></span> <span data-ttu-id="337e5-160">hello 차이점은이 쿼리 보내는 사용자가 만든 새 결과 toohello 출력 (`CallStream-PowerBI`).</span><span class="sxs-lookup"><span data-stu-id="337e5-160">hello difference is that this query sends results toohello new output you created (`CallStream-PowerBI`).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="337e5-161">Hello 입력 이름을 하지 않은 경우 `CallStream` hello 사기 감지 자습서에서에 대 한 이름을 대체 `CallStream` hello에 **FROM** 및 **조인** hello 쿼리에서 절.</span><span class="sxs-lookup"><span data-stu-id="337e5-161">If you did not name hello input `CallStream` in hello fraud-detection tutorial, substitute your name for `CallStream` in hello **FROM** and **JOIN** clauses in hello query.</span></span>

        /* Our criteria for fraud:
        Calls made from hello same caller tootwo phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where hello caller is hello same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where hello switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. <span data-ttu-id="337e5-162">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-162">Click **Save**.</span></span>


## <a name="test-hello-query"></a><span data-ttu-id="337e5-163">Hello 쿼리 테스트</span><span class="sxs-lookup"><span data-stu-id="337e5-163">Test hello query</span></span>
<span data-ttu-id="337e5-164">이 섹션은 선택 사항이지만 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-164">This section is optional, but recommended.</span></span> 

1. <span data-ttu-id="337e5-165">Hello TelcoStreaming 앱 현재 실행 되지 않는 경우 다음이 단계를 수행 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-165">If hello TelcoStreaming app is not currently running, start it by following these steps:</span></span>

    * <span data-ttu-id="337e5-166">명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-166">Open a command window.</span></span>
    * <span data-ttu-id="337e5-167">Hello telcogenerator.exe와 수정 된 telcodatagen.exe.config 파일이 있는 toohello 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-167">Go toohello folder where hello telcogenerator.exe and modified telcodatagen.exe.config files are.</span></span>
    * <span data-ttu-id="337e5-168">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-168">Run hello following command:</span></span>

            telcodatagen.exe 1000 .2 2

2. <span data-ttu-id="337e5-169">Hello에 **쿼리** 블레이드에서 hello 점 다음 toohello 클릭 `CallStream` 입력 한 다음 선택 **데이터 입력에서 샘플**합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-169">In hello **Query** blade, click hello dots next toohello `CallStream` input and then select **Sample data from input**.</span></span>

3. <span data-ttu-id="337e5-170">3분 분량의 데이터를 원하는 것으로 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-170">Specify that you want three minutes' worth of data and click **OK**.</span></span> <span data-ttu-id="337e5-171">Hello 데이터는 샘플링 된 알림을 받으면 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-171">Wait until you're notified that hello data has been sampled.</span></span>

4. <span data-ttu-id="337e5-172">**테스트**를 클릭하고 결과를 가져오는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-172">Click **Test** and make sure you're getting results.</span></span>


## <a name="run-hello-job"></a><span data-ttu-id="337e5-173">Hello 작업 실행</span><span class="sxs-lookup"><span data-stu-id="337e5-173">Run hello job</span></span>

1. <span data-ttu-id="337e5-174">Hello TelcoStreaming 앱 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-174">Make sure that hello TelcoStreaming app is running.</span></span>

2. <span data-ttu-id="337e5-175">닫기 hello **쿼리** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-175">Close hello **Query** blade.</span></span>

3. <span data-ttu-id="337e5-176">Hello 작업 블레이드에서 클릭 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-176">In hello job blade, click **Start**.</span></span>

    ![Hello 스트림 분석 작업 시작](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

<span data-ttu-id="337e5-178">스트리밍 분석 작업 hello 들어오는 스트림에 사기성 호출에 대 한 검색 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-178">Your Streaming Analytics job starts looking for fraudulent calls in hello incoming stream.</span></span> <span data-ttu-id="337e5-179">hello 작업 hello 데이터 집합 및 테이블 Power BI에서 만들어지고 사기성 호출 toothem hello에 대 한 데이터를 보내기 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-179">hello job also creates hello dataset and table in Power BI and starts sending data about hello fraudulent calls toothem.</span></span>


## <a name="create-hello-dashboard-in-power-bi"></a><span data-ttu-id="337e5-180">Power BI에서 hello 대시보드 만들기</span><span class="sxs-lookup"><span data-stu-id="337e5-180">Create hello dashboard in Power BI</span></span>

1. <span data-ttu-id="337e5-181">너무 이동[Powerbi.com](https://powerbi.com) 회사 또는 학교 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-181">Go too[Powerbi.com](https://powerbi.com) and sign in with your work or school account.</span></span> <span data-ttu-id="337e5-182">Hello 스트림 분석 작업 쿼리 결과 출력 하는 경우 데이터 집합은 이미 생성 되어 있음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-182">If hello Stream Analytics job query outputs results, you see that your dataset is already created:</span></span>

    ![Power BI에서 스트리밍 데이터 집합](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. <span data-ttu-id="337e5-184">작업 영역에서 **+&nbsp;만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-184">In your workspace, click **+&nbsp;Create**.</span></span>

    ![Power BI 작업 영역에서 hello 만들기 단추](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. <span data-ttu-id="337e5-186">새 대시보드를 만들고 이름을 `Fraudulent Calls`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-186">Create a new dashboard and name it `Fraudulent Calls`.</span></span>

    ![대시보드를 만들고 Power BI 작업 영역에서 이름 지정](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. <span data-ttu-id="337e5-188">Hello 창의 hello 위쪽을 클릭 **타일 추가**선택, **스트리밍 데이터 사용자 지정**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-188">At hello top of hello window, click **Add tile**, select **CUSTOM STREAMING DATA**, and then click **Next**.</span></span>

    ![사용자 지정 스트리밍 데이터 집합](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. <span data-ttu-id="337e5-190">**데이터 집합** 아래에서 데이터 집합을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-190">Under **YOUR DATSETS**, select your dataset and then click **Next**.</span></span>

    ![스트리밍 데이터 집합](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. <span data-ttu-id="337e5-192">**시각화 유형을**선택, **카드**, 한 다음 hello **필드** 목록에서 **fraudulentcalls**합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-192">Under **Visualization Type**, select **Card**, and then in hello **Fields** list, select **fraudulentcalls**.</span></span>

    ![새 타일에 대한 시각화 세부 정보](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. <span data-ttu-id="337e5-194">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-194">Click **Next**.</span></span>

8. <span data-ttu-id="337e5-195">제목 및 부제목 같은 타일 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-195">Fill in tile details like a title and subtitle.</span></span>

    ![새 타일에 대한 제목 및 부제목](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. <span data-ttu-id="337e5-197">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-197">Click **Apply**.</span></span>

    <span data-ttu-id="337e5-198">이제 사기 카운터가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-198">Now you have a fraud counter!</span></span>

    ![사기 카운터](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. <span data-ttu-id="337e5-200">다음 hello 단계를 다시 tooadd 타일 (4 단계부터 시작)입니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-200">Follow hello steps again tooadd a tile (starting with step 4).</span></span> <span data-ttu-id="337e5-201">이 이번에는 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-201">This time, do hello following:</span></span>

    * <span data-ttu-id="337e5-202">받을 경우에 너무**시각화 유형을**선택, **꺾은선형 차트**합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-202">When you get too**Visualization Type**, select **Line chart**.</span></span> 
    * <span data-ttu-id="337e5-203">축을 추가하고 **windowend**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-203">Add an axis and select **windowend**.</span></span> 
    * <span data-ttu-id="337e5-204">값을 추가하고 **fraudulentcalls**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-204">Add a value and select **fraudulentcalls**.</span></span>
    * <span data-ttu-id="337e5-205">에 대 한 **시간 창 toodisplay**선택, hello 지난 10 분입니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-205">For **Time window toodisplay**, select hello last 10 minutes.</span></span>

    ![꺾은선형 차트에 대한 타일 만들기](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. <span data-ttu-id="337e5-207">**다음**을 클릭하고 제목 및 부제목을 추가하고 **적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-207">Click **Next**, add a title and subtitle, and click **Apply**.</span></span>

    <span data-ttu-id="337e5-208">Power BI 대시보드 hello 이제 제공 사기성 호출에 대 한 두 개의 데이터 보기 hello 스트리밍 데이터에서에서 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-208">hello Power BI dashboard now gives you two views of data about fraudulent calls as detected in hello streaming data.</span></span>

    ![사기성 호출에 대한 두 가지 타일을 보여 주는 완료된 Power BI 대시보드](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a><span data-ttu-id="337e5-210">Power BI에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="337e5-210">Learn more about Power BI</span></span>

<span data-ttu-id="337e5-211">이 자습서에서는 설명 방법을 toocreate 몇 가지 유형의 데이터 집합에 대 한 시각화입니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-211">This tutorial demonstrates how toocreate only a few kinds of visualizations for a dataset.</span></span> <span data-ttu-id="337e5-212">Power BI는 조직에 대한 다른 고객 비즈니스 인텔리전스 도구를 만드는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-212">Power BI can help you create other customer business intelligence tools for your organization.</span></span> <span data-ttu-id="337e5-213">자세한 내용은 다음 리소스는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="337e5-213">For more ideas, see hello following resources:</span></span>

* <span data-ttu-id="337e5-214">Power BI 대시보드의 또 다른 예로, 감시 hello [Power BI 시작 하기](https://youtu.be/L-Z_6P56aas?t=1m58s) 비디오.</span><span class="sxs-lookup"><span data-stu-id="337e5-214">For another example of a Power BI dashboard, watch hello [Getting Started with Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) video.</span></span>
* <span data-ttu-id="337e5-215">스트리밍 분석을 구성 하는 방법에 대 한 자세한 내용은 작업 출력 tooPower BI 및 hello 검토 Power BI 그룹을 사용 하 여 [Power BI](stream-analytics-define-outputs.md#power-bi) hello 섹션 [스트림 분석 출력](stream-analytics-define-outputs.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="337e5-215">For more information about configuring Streaming Analytics job output tooPower BI and using Power BI groups, review hello [Power BI](stream-analytics-define-outputs.md#power-bi) section of hello [Stream Analytics outputs](stream-analytics-define-outputs.md) article.</span></span> 
* <span data-ttu-id="337e5-216">일반적으로 Power BI를 사용 하는 방법은 [Power BI의 대시보드](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="337e5-216">For information about using Power BI generally, see [Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span></span>


## <a name="learn-about-limitations-and-best-practices"></a><span data-ttu-id="337e5-217">제한 사항 및 모범 사례에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="337e5-217">Learn about limitations and best practices</span></span>
<span data-ttu-id="337e5-218">현재는 대략 1초당 한 번 Power BI를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-218">Currently, Power BI can be called roughly once per second.</span></span> <span data-ttu-id="337e5-219">스트리밍 시각적 개체는 15KB의 패킷을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-219">Streaming visuals support packets of 15 KB.</span></span> <span data-ttu-id="337e5-220">이 외 스트리밍 시각적 개체가 실패 (하지만 푸시 계속 toowork) 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-220">Beyond that, streaming visuals fail (but push continues toowork).</span></span> <span data-ttu-id="337e5-221">이러한 제한 때문에 Power BI는 경우가 많으므로 가장 자연스럽 게 toocases Azure 스트림 분석에서 중요 한 데이터 로드를 줄이기 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-221">Because of these limitations, Power BI lends itself most naturally toocases where Azure Stream Analytics does a significant data load reduction.</span></span> <span data-ttu-id="337e5-222">연속 창 또는 도약 창 tooensure 데이터 푸시 최대 초 당 하나의 푸시 있으며 하는지 hello 처리량 요구 사항 내에서 처음 삽입 쿼리를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-222">We recommend using a Tumbling window or Hopping window tooensure that data push is at most one push per second, and that your query lands within hello throughput requirements.</span></span>

<span data-ttu-id="337e5-223">다음 수식은 toocompute hello 값 toogive hello 창 (초)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-223">You can use hello following equation toocompute hello value toogive your window in seconds:</span></span>

![수식 1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

<span data-ttu-id="337e5-225">예:</span><span class="sxs-lookup"><span data-stu-id="337e5-225">For example:</span></span>

* <span data-ttu-id="337e5-226">1,000대의 장치가 1초 간격으로 데이터를 보내고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-226">You have 1,000 devices sending data at one-second intervals.</span></span>
* <span data-ttu-id="337e5-227">Power BI Pro SKU에 시간당 1000000 행 지원 hello를 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-227">You are using hello Power BI Pro SKU that supports 1,000,000 rows per hour.</span></span>
* <span data-ttu-id="337e5-228">장치 tooPower BI 당 평균 데이터의 toopublish hello 양을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-228">You want toopublish hello amount of average data per device tooPower BI.</span></span>

<span data-ttu-id="337e5-229">결과적으로, hello 수식을 다음과 같이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-229">As a result, hello equation becomes:</span></span>

![수식 2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

<span data-ttu-id="337e5-231">구성이 이와 hello 원래 쿼리 toohello 다음을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-231">Given this configuration, you can change hello original query toohello following:</span></span>

    SELECT
        MAX(hmdt) AS hmdt,
        MAX(temp) AS temp,
        System.TimeStamp AS time,
        dspl
    INTO "CallStream-PowerBI"
    FROM
        Input TIMESTAMP BY time
    GROUP BY
        TUMBLINGWINDOW(ss,4),
        dspl


### <a name="renew-authorization"></a><span data-ttu-id="337e5-232">권한 부여 갱신</span><span class="sxs-lookup"><span data-stu-id="337e5-232">Renew authorization</span></span>
<span data-ttu-id="337e5-233">Hello 암호 작업을 만들거나 마지막으로 인증 된 이후 변경 된 경우 Power BI 계정이 tooreauthenticate 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-233">If hello password has changed since your job was created or last authenticated, you need tooreauthenticate your Power BI account.</span></span> <span data-ttu-id="337e5-234">Azure Multi-factor Authentication은 Azure Active Directory (Azure AD) 테 넌 트에 구성 된 경우에 toorenew Power BI 권한 부여 2 주마다 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-234">If Azure Multi-Factor Authentication is configured on your Azure Active Directory (Azure AD) tenant, you also need toorenew Power BI authorization every two weeks.</span></span> <span data-ttu-id="337e5-235">갱신 하지 않는 경우 작업 출력의 부족과 같이 증상을 볼 수 있습니다 또는 `Authenticate user error` hello 작업 로그에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-235">If you don't renew, you could see symptoms such as a lack of job output or an `Authenticate user error` in hello operation logs.</span></span>

<span data-ttu-id="337e5-236">마찬가지로, 작업에는 hello 토큰이 만료 된 후 시작 되 면 오류가 발생 하 고 hello 작업이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-236">Similarly, if a job starts after hello token has expired, an error occurs and hello job fails.</span></span> <span data-ttu-id="337e5-237">tooresolve이이 문제를 hello 실행 중인 작업을 중지 하 고 Power BI 출력 tooyour 이동.</span><span class="sxs-lookup"><span data-stu-id="337e5-237">tooresolve this issue, stop hello job that's running and go tooyour Power BI output.</span></span> <span data-ttu-id="337e5-238">tooavoid 데이터 손실, 선택 hello **권한 부여를 갱신** 링크를 선택한 다음 hello에서 작업을 다시 시작 **마지막으로 중지 된 시간**합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-238">tooavoid data loss, select hello **Renew authorization** link, and then restart your job from hello **Last Stopped Time**.</span></span>

<span data-ttu-id="337e5-239">Power BI와 hello 권한 부여가 새로 고쳐지지, 녹색 경고에에서 표시 hello 권한 부여 영역 tooreflect hello 문제가 해결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-239">After hello authorization has been refreshed with Power BI, a green alert appears in hello authorization area tooreflect that hello issue has been resolved.</span></span>

## <a name="get-help"></a><span data-ttu-id="337e5-240">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="337e5-240">Get help</span></span>
<span data-ttu-id="337e5-241">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="337e5-241">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="337e5-242">다음 단계</span><span class="sxs-lookup"><span data-stu-id="337e5-242">Next steps</span></span>
* [<span data-ttu-id="337e5-243">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="337e5-243">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="337e5-244">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="337e5-244">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="337e5-245">Azure 스트림 분석 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="337e5-245">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="337e5-246">Azure Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="337e5-246">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="337e5-247">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="337e5-247">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
