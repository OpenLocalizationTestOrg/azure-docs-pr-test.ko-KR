---
title: "Azure Stream Analytics의 Power BI 대시보드 | Microsoft Docs"
description: "실시간 스트리밍 Power BI 대시보드를 사용하여 비즈니스 인텔리전스를 수집하고 Stream Analytics 작업에서 대량의 데이터를 분석합니다."
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
ms.openlocfilehash: 874d9b8701a24deb3cc21aa74cb51870155c7c9c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a><span data-ttu-id="8252f-104">Stream Analytics 및 Power BI: 스트리밍 데이터에 대한 실시간 분석 대시보드</span><span class="sxs-lookup"><span data-stu-id="8252f-104">Stream Analytics and Power BI: A real-time analytics dashboard for streaming data</span></span>
<span data-ttu-id="8252f-105">Azure Stream Analytics를 사용하면 최고의 비즈니스 인텔리전스 도구 중 하나인 [Microsoft Power BI](https://powerbi.com/)를 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-105">Azure Stream Analytics enables you to take advantage of one of the leading business intelligence tools, [Microsoft Power BI](https://powerbi.com/).</span></span> <span data-ttu-id="8252f-106">이 문서에서는 Azure Stream Analytics 작업에 대한 출력으로 Power BI를 사용하여 비즈니스 인텔리전스 도구를 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-106">In this article, you learn how create business intelligence tools by using Power BI as an output for your Azure Stream Analytics jobs.</span></span> <span data-ttu-id="8252f-107">실시간 대시보드를 만들고 사용하는 방법도 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-107">You also learn how to create and use a real-time dashboard.</span></span>

<span data-ttu-id="8252f-108">이 문서는 Stream Analytics [실시간 사기 감지](stream-analytics-real-time-fraud-detection.md) 자습서로부터 내용이 이어집니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-108">This article continues from the Stream Analytics [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="8252f-109">해당 자습서에서 만든 워크플로를 기반으로 하고 Power BI 출력을 추가하여 Streaming Analytics 작업에서 감지한 사기성 전화를 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-109">It builds on the workflow created in that tutorial and adds a Power BI output so that you can visualize fraudulent phone calls that are detected by a Streaming Analytics job.</span></span> 

<span data-ttu-id="8252f-110">이 시나리오를 보여주는 [비디오](https://www.youtube.com/watch?v=SGUpT-a99MA)를 시청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-110">You can watch [a video](https://www.youtube.com/watch?v=SGUpT-a99MA)  that illustrates this scenario.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="8252f-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8252f-111">Prerequisites</span></span>

<span data-ttu-id="8252f-112">시작하기 전에 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-112">Before you start, make sure you have the following:</span></span>

* <span data-ttu-id="8252f-113">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="8252f-113">An Azure account.</span></span>
* <span data-ttu-id="8252f-114">Power BI에 대한 계정.</span><span class="sxs-lookup"><span data-stu-id="8252f-114">An account for Power BI.</span></span> <span data-ttu-id="8252f-115">회사 계정 또는 학교 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-115">You can use a work account or a school account.</span></span>
* <span data-ttu-id="8252f-116">[실시간 사기 감지](stream-analytics-real-time-fraud-detection.md) 자습서의 완료된 버전.</span><span class="sxs-lookup"><span data-stu-id="8252f-116">A completed version of the [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="8252f-117">자습서에는 가상의 전화 통화 메타데이터를 생성하는 앱이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-117">The tutorial includes an app that generates fictitious telephone-call metadata.</span></span> <span data-ttu-id="8252f-118">자습서에서 이벤트 허브를 만들고 스트리밍 전화 통화 데이터를 이벤트 허브로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-118">In the tutorial, you create an event hub and send the streaming phone call data to the event hub.</span></span> <span data-ttu-id="8252f-119">사기성 호출(서로 다른 위치에서 동시에 같은 번호에서 발신되는 전화)을 감지하는 쿼리를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-119">You write a query that detects fraudulent calls (calls from the same number at the same time in different locations).</span></span> 


## <a name="add-power-bi-output"></a><span data-ttu-id="8252f-120">Power BI 출력 추가</span><span class="sxs-lookup"><span data-stu-id="8252f-120">Add Power BI output</span></span>
<span data-ttu-id="8252f-121">실시간 사기 감지 자습서에서 출력은 Azure Blob Storage로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-121">In the real-time fraud detection tutorial, the output is sent to Azure Blob storage.</span></span> <span data-ttu-id="8252f-122">이 섹션에서는 Power BI로 정보를 보내는 출력을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-122">In this section, you add an output that sends information to Power BI.</span></span>

1. <span data-ttu-id="8252f-123">Azure Portal에서 이전에 만든 Streaming Analytics 작업을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-123">In the Azure portal, open the Streaming Analytics job that you created earlier.</span></span> <span data-ttu-id="8252f-124">제안된 이름을 사용한 경우 작업 이름은 `sa_frauddetection_job_demo`입니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-124">If you used the suggested name, the job is named `sa_frauddetection_job_demo`.</span></span>

2. <span data-ttu-id="8252f-125">작업 대시보드 중간에 있는 **출력** 상자를 선택한 후 **+ 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-125">Select the **Outputs** box in the middle of the job dashboard and then select **+ Add**.</span></span>

3. <span data-ttu-id="8252f-126">**출력 별칭**에 `CallStream-PowerBI`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-126">For **Output Alias**, enter `CallStream-PowerBI`.</span></span> <span data-ttu-id="8252f-127">다른 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-127">You can use a different name.</span></span> <span data-ttu-id="8252f-128">이 경우 나중에 이름이 필요하기 때문에 메모해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-128">If you do, make a note of it, because you need the name later.</span></span> 

4. <span data-ttu-id="8252f-129">**싱크** 아래에서 **Power BI**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-129">Under **Sink**, select **Power BI**.</span></span>

   ![Power BI에 대한 출력 만들기](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. <span data-ttu-id="8252f-131">**권한 부여**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-131">Click **Authorize**.</span></span>

    <span data-ttu-id="8252f-132">회사 또는 학교 계정에 대한 Azure 자격 증명을 제공할 수 있는 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-132">A window opens where you can provide your Azure credentials for a work or school account.</span></span> 

    ![Power BI에 액세스하기 위한 자격 증명 입력](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. <span data-ttu-id="8252f-134">자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-134">Enter your credentials.</span></span> <span data-ttu-id="8252f-135">자격 증명을 입력하면 Streaming Analytic 작업에 권한을 부여하여 Power BI 영역에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-135">Be aware then when you enter your credentials, you're also giving permission to the Streaming Analytics job to access your Power BI area.</span></span>

7. <span data-ttu-id="8252f-136">**새 출력** 블레이드로 돌아가면 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-136">When you're returned to the **New output** blade, enter the following information:</span></span>

    * <span data-ttu-id="8252f-137">**그룹 작업 영역**: 데이터 집합을 만들려는 Power BI 테넌트에서 작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-137">**Group Workspace**: Select a workspace in your Power BI tenant where you want to create the dataset.</span></span>
    * <span data-ttu-id="8252f-138">**데이터 집합 이름**: `sa-dataset`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-138">**Dataset Name**:  Enter `sa-dataset`.</span></span> <span data-ttu-id="8252f-139">다른 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-139">You can use a different name.</span></span> <span data-ttu-id="8252f-140">이 경우 나중을 위해 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-140">If you do, make a note of it for later.</span></span>
    * <span data-ttu-id="8252f-141">**테이블 이름**: `fraudulent-calls`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-141">**Table Name**: Enter `fraudulent-calls`.</span></span> <span data-ttu-id="8252f-142">현재, Stream Analytics 작업의 Power BI 출력에는 하나의 데이터 집합에 하나의 테이블만 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-142">Currently, Power BI output from Stream Analytics jobs can have only one table in a dataset.</span></span>

    ![PBI 작업 영역](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > <span data-ttu-id="8252f-144">이 Stream Analytics 작업에서 지정한 것과 동일한 이름의 데이터 집합과 테이블이 Power BI에 있는 경우에는 기존 항목을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-144">If Power BI has a dataset and table that have the same names as the ones that you specify in the Stream Analytics job, the existing ones are overwritten.</span></span>
    > <span data-ttu-id="8252f-145">이 데이터 집합 및 테이블을 Power BI 계정에 명시적으로 만들지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-145">We recommend that you do not explicitly create this dataset and table in your Power BI account.</span></span> <span data-ttu-id="8252f-146">이들은 Stream Analytics 작업을 시작하고 작업이 Power BI로 출력을 시작할 때 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-146">They are automatically created when you start your Stream Analytics job and the job starts pumping output into Power BI.</span></span> <span data-ttu-id="8252f-147">작업 쿼리가 어떤 결과도 반환하지 않으면 데이터 집합 및 테이블은 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-147">If your job query doesn't return any results, the dataset and table are not  created.</span></span>
    >

8. <span data-ttu-id="8252f-148">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-148">Click **Create**.</span></span>

<span data-ttu-id="8252f-149">데이터 집합은 다음과 같은 설정으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-149">The dataset is created with the following settings:</span></span>

* <span data-ttu-id="8252f-150">**defaultRetentionPolicy: BasicFIFO**:데이터는 FIFO이고, 최대 200,000개의 행이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-150">**defaultRetentionPolicy: BasicFIFO**: Data is FIFO, with a maximum of 200,000 rows.</span></span>
* <span data-ttu-id="8252f-151">**defaultMode: pushStreaming**: 데이터 집합이 스트리밍 타일 및 기존의 보고서 기반 시각적 개체(즉, </span><span class="sxs-lookup"><span data-stu-id="8252f-151">**defaultMode: pushStreaming**: The dataset supports both streaming tiles and traditional report-based visuals (a.k.a.</span></span> <span data-ttu-id="8252f-152">푸시)를 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-152">push).</span></span>

<span data-ttu-id="8252f-153">지금은 다른 플래그로 데이터 집합을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-153">Currently, you can't create datasets with other flags.</span></span>

<span data-ttu-id="8252f-154">Power BI 데이터 집합에 대한 자세한 내용은 [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8252f-154">For more information about Power BI datasets, see the [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) reference.</span></span>


## <a name="write-the-query"></a><span data-ttu-id="8252f-155">쿼리 작성</span><span class="sxs-lookup"><span data-stu-id="8252f-155">Write the query</span></span>

1. <span data-ttu-id="8252f-156">**출력** 블레이드를 닫고 작업 블레이드로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-156">Close the **Outputs** blade and return to the job blade.</span></span>

2. <span data-ttu-id="8252f-157">**쿼리** 상자를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-157">Click the **Query** box.</span></span> 

3. <span data-ttu-id="8252f-158">다음 쿼리를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-158">Enter the following query.</span></span> <span data-ttu-id="8252f-159">이 쿼리는 사기 감지 자습서에서 만든 셀프 조인 쿼리와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-159">This query is similar to the self-join query you created in the fraud-detection tutorial.</span></span> <span data-ttu-id="8252f-160">차이점은 이 쿼리에서 사용자가 만든 새 출력으로 결과는 보낸다는 점입니다(`CallStream-PowerBI`).</span><span class="sxs-lookup"><span data-stu-id="8252f-160">The difference is that this query sends results to the new output you created (`CallStream-PowerBI`).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="8252f-161">사기 감지 자습서에서 입력 `CallStream`에 이름을 지정하지 않으면 쿼리에서 **FROM** 및 **JOIN** 절의 `CallStream` 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-161">If you did not name the input `CallStream` in the fraud-detection tutorial, substitute your name for `CallStream` in the **FROM** and **JOIN** clauses in the query.</span></span>

        /* Our criteria for fraud:
        Calls made from the same caller to two phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where the caller is the same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where the switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. <span data-ttu-id="8252f-162">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-162">Click **Save**.</span></span>


## <a name="test-the-query"></a><span data-ttu-id="8252f-163">쿼리 테스트</span><span class="sxs-lookup"><span data-stu-id="8252f-163">Test the query</span></span>
<span data-ttu-id="8252f-164">이 섹션은 선택 사항이지만 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-164">This section is optional, but recommended.</span></span> 

1. <span data-ttu-id="8252f-165">TelcoStreaming 앱은 현재 실행 중이 아니며 다음 단계에 따라 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-165">If the TelcoStreaming app is not currently running, start it by following these steps:</span></span>

    * <span data-ttu-id="8252f-166">명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-166">Open a command window.</span></span>
    * <span data-ttu-id="8252f-167">telcogenerator.exe 및 수정된 telcodatagen.exe.config 파일이 있는 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-167">Go to the folder where the telcogenerator.exe and modified telcodatagen.exe.config files are.</span></span>
    * <span data-ttu-id="8252f-168">다음 명령 실행:</span><span class="sxs-lookup"><span data-stu-id="8252f-168">Run the following command:</span></span>

            telcodatagen.exe 1000 .2 2

2. <span data-ttu-id="8252f-169">**쿼리** 블레이드에서 `CallStream` 입력 옆에 있는 점을 클릭한 후 **입력의 샘플 데이터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-169">In the **Query** blade, click the dots next to the `CallStream` input and then select **Sample data from input**.</span></span>

3. <span data-ttu-id="8252f-170">3분 분량의 데이터를 원하는 것으로 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-170">Specify that you want three minutes' worth of data and click **OK**.</span></span> <span data-ttu-id="8252f-171">데이터가 샘플링되었다는 알림을 받을 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-171">Wait until you're notified that the data has been sampled.</span></span>

4. <span data-ttu-id="8252f-172">**테스트**를 클릭하고 결과를 가져오는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-172">Click **Test** and make sure you're getting results.</span></span>


## <a name="run-the-job"></a><span data-ttu-id="8252f-173">작업 실행</span><span class="sxs-lookup"><span data-stu-id="8252f-173">Run the job</span></span>

1. <span data-ttu-id="8252f-174">TelcoStreaming 앱 실행되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-174">Make sure that the TelcoStreaming app is running.</span></span>

2. <span data-ttu-id="8252f-175">**쿼리** 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-175">Close the **Query** blade.</span></span>

3. <span data-ttu-id="8252f-176">작업 블레이드에서 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-176">In the job blade, click **Start**.</span></span>

    ![Stream Analytic 작업 시작](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

<span data-ttu-id="8252f-178">Streaming Analytics 작업이 들어오는 스트림에서 사기성 호출을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-178">Your Streaming Analytics job starts looking for fraudulent calls in the incoming stream.</span></span> <span data-ttu-id="8252f-179">작업은 Power BI에서 데이터 집합 및 테이블을 만들고 사기성 호출에 대한 데이터 보내기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-179">The job also creates the dataset and table in Power BI and starts sending data about the fraudulent calls to them.</span></span>


## <a name="create-the-dashboard-in-power-bi"></a><span data-ttu-id="8252f-180">Power BI에서 대시보드 만들기</span><span class="sxs-lookup"><span data-stu-id="8252f-180">Create the dashboard in Power BI</span></span>

1. <span data-ttu-id="8252f-181">[Powerbi.com](https://powerbi.com)으로 이동한 다음 회사 또는 학교 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-181">Go to [Powerbi.com](https://powerbi.com) and sign in with your work or school account.</span></span> <span data-ttu-id="8252f-182">Stream Analytics 작업 쿼리가 결과를 출력하면, 사용자 데이터 집합이 이미 생성되어 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-182">If the Stream Analytics job query outputs results, you see that your dataset is already created:</span></span>

    ![Power BI에서 스트리밍 데이터 집합](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. <span data-ttu-id="8252f-184">작업 영역에서 **+&nbsp;만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-184">In your workspace, click **+&nbsp;Create**.</span></span>

    ![Power BI 작업 영역에서 만들기 단추](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. <span data-ttu-id="8252f-186">새 대시보드를 만들고 이름을 `Fraudulent Calls`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-186">Create a new dashboard and name it `Fraudulent Calls`.</span></span>

    ![대시보드를 만들고 Power BI 작업 영역에서 이름 지정](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. <span data-ttu-id="8252f-188">창의 맨 위에서 **타일 추가**를 클릭하고 **사용자 지정 스트리밍 데이터**를 선택한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-188">At the top of the window, click **Add tile**, select **CUSTOM STREAMING DATA**, and then click **Next**.</span></span>

    ![사용자 지정 스트리밍 데이터 집합](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. <span data-ttu-id="8252f-190">**데이터 집합** 아래에서 데이터 집합을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-190">Under **YOUR DATSETS**, select your dataset and then click **Next**.</span></span>

    ![스트리밍 데이터 집합](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. <span data-ttu-id="8252f-192">**시각화 유형** 아래에서 **카드**를 선택한 다음 **필드** 목록에서 **fraudulentcalls**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-192">Under **Visualization Type**, select **Card**, and then in the **Fields** list, select **fraudulentcalls**.</span></span>

    ![새 타일에 대한 시각화 세부 정보](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. <span data-ttu-id="8252f-194">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-194">Click **Next**.</span></span>

8. <span data-ttu-id="8252f-195">제목 및 부제목 같은 타일 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-195">Fill in tile details like a title and subtitle.</span></span>

    ![새 타일에 대한 제목 및 부제목](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. <span data-ttu-id="8252f-197">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-197">Click **Apply**.</span></span>

    <span data-ttu-id="8252f-198">이제 사기 카운터가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-198">Now you have a fraud counter!</span></span>

    ![사기 카운터](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. <span data-ttu-id="8252f-200">타일을 추가하는 단계를 다시 진행합니다(4단계부터 시작).</span><span class="sxs-lookup"><span data-stu-id="8252f-200">Follow the steps again to add a tile (starting with step 4).</span></span> <span data-ttu-id="8252f-201">이때 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-201">This time, do the following:</span></span>

    * <span data-ttu-id="8252f-202">**시각화 유형**으로 이동하여 **꺾은선형 차트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-202">When you get to **Visualization Type**, select **Line chart**.</span></span> 
    * <span data-ttu-id="8252f-203">축을 추가하고 **windowend**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-203">Add an axis and select **windowend**.</span></span> 
    * <span data-ttu-id="8252f-204">값을 추가하고 **fraudulentcalls**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-204">Add a value and select **fraudulentcalls**.</span></span>
    * <span data-ttu-id="8252f-205">**표시할 시간 창**에 지난 10분을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-205">For **Time window to display**, select the last 10 minutes.</span></span>

    ![꺾은선형 차트에 대한 타일 만들기](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. <span data-ttu-id="8252f-207">**다음**을 클릭하고 제목 및 부제목을 추가하고 **적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-207">Click **Next**, add a title and subtitle, and click **Apply**.</span></span>

    <span data-ttu-id="8252f-208">이제 Power BI 대시보드에 스트리밍 데이터에서 감지된 대로 사기성 호출에 대한 두 가지 데이터 보기가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-208">The Power BI dashboard now gives you two views of data about fraudulent calls as detected in the streaming data.</span></span>

    ![사기성 호출에 대한 두 가지 타일을 보여 주는 완료된 Power BI 대시보드](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a><span data-ttu-id="8252f-210">Power BI에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="8252f-210">Learn more about Power BI</span></span>

<span data-ttu-id="8252f-211">이 자습서에서는 데이터 집합에 대해 몇 가지 종류의 차트를 만드는 방법만 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-211">This tutorial demonstrates how to create only a few kinds of visualizations for a dataset.</span></span> <span data-ttu-id="8252f-212">Power BI는 조직에 대한 다른 고객 비즈니스 인텔리전스 도구를 만드는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-212">Power BI can help you create other customer business intelligence tools for your organization.</span></span> <span data-ttu-id="8252f-213">자세한 개념은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8252f-213">For more ideas, see the following resources:</span></span>

* <span data-ttu-id="8252f-214">Power BI 대시보드의 다른 예제는 [Power BI 시작](https://youtu.be/L-Z_6P56aas?t=1m58s) 비디오를 보세요.</span><span class="sxs-lookup"><span data-stu-id="8252f-214">For another example of a Power BI dashboard, watch the [Getting Started with Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) video.</span></span>
* <span data-ttu-id="8252f-215">Power BI에 Streaming Analytics 작업 출력 구성 및 Power BI 그룹 사용에 대한 자세한 내용은 [Stream Analytics 출력](stream-analytics-define-outputs.md) 문서의 [Power BI](stream-analytics-define-outputs.md#power-bi) 섹션을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="8252f-215">For more information about configuring Streaming Analytics job output to Power BI and using Power BI groups, review the [Power BI](stream-analytics-define-outputs.md#power-bi) section of the [Stream Analytics outputs](stream-analytics-define-outputs.md) article.</span></span> 
* <span data-ttu-id="8252f-216">일반적으로 Power BI를 사용 하는 방법은 [Power BI의 대시보드](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8252f-216">For information about using Power BI generally, see [Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span></span>


## <a name="learn-about-limitations-and-best-practices"></a><span data-ttu-id="8252f-217">제한 사항 및 모범 사례에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="8252f-217">Learn about limitations and best practices</span></span>
<span data-ttu-id="8252f-218">현재는 대략 1초당 한 번 Power BI를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-218">Currently, Power BI can be called roughly once per second.</span></span> <span data-ttu-id="8252f-219">스트리밍 시각적 개체는 15KB의 패킷을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-219">Streaming visuals support packets of 15 KB.</span></span> <span data-ttu-id="8252f-220">이보다 크면 스트리밍 시각적 개체가 실패합니다(푸시는 계속 작동).</span><span class="sxs-lookup"><span data-stu-id="8252f-220">Beyond that, streaming visuals fail (but push continues to work).</span></span> <span data-ttu-id="8252f-221">이러한 제한 사항 때문에 Power BI는 Azure Stream Analytics가 데이터 부하를 상당히 줄이는 경우에 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-221">Because of these limitations, Power BI lends itself most naturally to cases where Azure Stream Analytics does a significant data load reduction.</span></span> <span data-ttu-id="8252f-222">연속 창 또는 도약 창을 사용하여 데이터 푸시가 최대 초당 한번의 푸시를 수행하고 쿼리가 처리량 요구 사항 범위 내에 있도록 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-222">We recommend using a Tumbling window or Hopping window to ensure that data push is at most one push per second, and that your query lands within the throughput requirements.</span></span>

<span data-ttu-id="8252f-223">다음 수식을 사용하여 값을 초 단위로 계산하여 창에 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-223">You can use the following equation to compute the value to give your window in seconds:</span></span>

![수식 1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

<span data-ttu-id="8252f-225">예:</span><span class="sxs-lookup"><span data-stu-id="8252f-225">For example:</span></span>

* <span data-ttu-id="8252f-226">1,000대의 장치가 1초 간격으로 데이터를 보내고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-226">You have 1,000 devices sending data at one-second intervals.</span></span>
* <span data-ttu-id="8252f-227">시간당 1,000,000개의 행을 지원하는 Power BI Pro SKU를 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-227">You are using the Power BI Pro SKU that supports 1,000,000 rows per hour.</span></span>
* <span data-ttu-id="8252f-228">장치당 평균 데이터 양을 Power BI에 게시하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-228">You want to publish the amount of average data per device to Power BI.</span></span>

<span data-ttu-id="8252f-229">그 결과, 수식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-229">As a result, the equation becomes:</span></span>

![수식 2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

<span data-ttu-id="8252f-231">이 구성이 지정되면 원래 쿼리를 다음과 같이 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-231">Given this configuration, you can change the original query to the following:</span></span>

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


### <a name="renew-authorization"></a><span data-ttu-id="8252f-232">권한 부여 갱신</span><span class="sxs-lookup"><span data-stu-id="8252f-232">Renew authorization</span></span>
<span data-ttu-id="8252f-233">작업을 만들거나 마지막으로 인증한 후에 암호가 변경된 경우 Power BI 계정을 다시 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-233">If the password has changed since your job was created or last authenticated, you need to reauthenticate your Power BI account.</span></span> <span data-ttu-id="8252f-234">Azure Multi-Factor Authentication가 Azure Active Directory(Azure AD) 테넌트에서 구성된 경우 2주마다 Power BI 권한 부여도 갱신해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-234">If Azure Multi-Factor Authentication is configured on your Azure Active Directory (Azure AD) tenant, you also need to renew Power BI authorization every two weeks.</span></span> <span data-ttu-id="8252f-235">갱신하지 않으면 작업 출력 부족 또는 작업 로그에 `Authenticate user error`와 같은 증상을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-235">If you don't renew, you could see symptoms such as a lack of job output or an `Authenticate user error` in the operation logs.</span></span>

<span data-ttu-id="8252f-236">마찬가지로 토큰이 만료된 후 작업이 시작되면 오류가 발생하고 작업이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-236">Similarly, if a job starts after the token has expired, an error occurs and the job fails.</span></span> <span data-ttu-id="8252f-237">이 문제를 해결하려면 실행 중인 작업을 중지하고 Power BI 출력으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-237">To resolve this issue, stop the job that's running and go to your Power BI output.</span></span> <span data-ttu-id="8252f-238">데이터 손실을 방지하기 위해 **권한 부여 갱신** 링크를 클릭한 다음 **마지막 중지 시간**부터 작업을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-238">To avoid data loss, select the **Renew authorization** link, and then restart your job from the **Last Stopped Time**.</span></span>

<span data-ttu-id="8252f-239">Power BI를 사용하여 권한 부여가 새로 고쳐지면 권한 부여 영역에 문제가 해결되었음을 나타내는 녹색 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8252f-239">After the authorization has been refreshed with Power BI, a green alert appears in the authorization area to reflect that the issue has been resolved.</span></span>

## <a name="get-help"></a><span data-ttu-id="8252f-240">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="8252f-240">Get help</span></span>
<span data-ttu-id="8252f-241">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8252f-241">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8252f-242">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8252f-242">Next steps</span></span>
* [<span data-ttu-id="8252f-243">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="8252f-243">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="8252f-244">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="8252f-244">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="8252f-245">Azure 스트림 분석 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="8252f-245">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="8252f-246">Azure Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="8252f-246">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="8252f-247">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="8252f-247">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
