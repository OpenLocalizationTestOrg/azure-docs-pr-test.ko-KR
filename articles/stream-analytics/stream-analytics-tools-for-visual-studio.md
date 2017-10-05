---
title: "Visual Studio용 Azure Stream Analytics 도구 사용 | Microsoft Docs"
description: "Visual Studio용 Azure Stream Analytics 도구 시작 자습서"
keywords: Visual Studio
documentationcenter: 
services: stream-analytics
author: 
manager: 
editor: 
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 
ms.author: 
ms.openlocfilehash: 618c1055795a75e0ed71dacddba3e076f81f4946
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a><span data-ttu-id="dd28d-104">Azure Stream Analytics Tools for Visual Studio 사용</span><span class="sxs-lookup"><span data-stu-id="dd28d-104">Use Azure Stream Analytics Tools for Visual Studio</span></span>
## <a name="introduction"></a><span data-ttu-id="dd28d-105">소개</span><span class="sxs-lookup"><span data-stu-id="dd28d-105">Introduction</span></span>
<span data-ttu-id="dd28d-106">이 자습서에서는 Azure Stream Analytics Tools for Visual Studio를 사용하여 Azure Stream Analytics 작업을 만들고 작성하며 로컬에서 테스트하고 관리 및 디버깅하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-106">In this tutorial, you learn how to use Azure Stream Analytics Tools for Visual Studio to create, author, test locally, manage, and debug your Stream Analytics jobs.</span></span> 

<span data-ttu-id="dd28d-107">이 자습서를 완료하고 나면 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-107">After completing this tutorial, you will be able to:</span></span>
* <span data-ttu-id="dd28d-108">Stream Analytics Tools for Visual Studio를 익숙하게 사용 가능</span><span class="sxs-lookup"><span data-stu-id="dd28d-108">Familiarize yourself with Stream Analytics Tools for Visual Studio.</span></span>
* <span data-ttu-id="dd28d-109">Stream Analytics 작업 구성 및 배포</span><span class="sxs-lookup"><span data-stu-id="dd28d-109">Configure and deploy a Stream Analytics job.</span></span>
* <span data-ttu-id="dd28d-110">로컬 샘플 데이터로 로컬에서 작업 테스트</span><span class="sxs-lookup"><span data-stu-id="dd28d-110">Test your job locally with local sample data.</span></span>
* <span data-ttu-id="dd28d-111">모니터링을 사용하여 문제 해결</span><span class="sxs-lookup"><span data-stu-id="dd28d-111">Use monitoring to troubleshoot issues.</span></span>
* <span data-ttu-id="dd28d-112">기존 작업을 프로젝트로 내보내기</span><span class="sxs-lookup"><span data-stu-id="dd28d-112">Export existing jobs to projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd28d-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="dd28d-113">Prerequisites</span></span>
<span data-ttu-id="dd28d-114">이 자습서를 완료하려면 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-114">To complete this tutorial, you need the following prerequisites:</span></span>
* <span data-ttu-id="dd28d-115">[Stream Analytics 자습서를 사용하여 IoT 솔루션 빌드](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics)에서 “Stream Analytics 작업 만들기” 이전의 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-115">Finish the steps that precede "Create a Stream Analytics job" in the [Build an IoT solution by using Stream Analytics tutorial](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span></span> 
* <span data-ttu-id="dd28d-116">Visual Studio 2015, Visual Studio 2013 업데이트 4 또는 Visual Studio 2012를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-116">Use Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012.</span></span> <span data-ttu-id="dd28d-117">Enterprise(Ultimate/Premium), Professional 및 Community Edition이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-117">Enterprise (Ultimate/Premium), Professional, and Community editions are supported.</span></span> <span data-ttu-id="dd28d-118">Express Edition은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-118">Express edition is not supported.</span></span> <span data-ttu-id="dd28d-119">Visual Studio 2017은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-119">Visual Studio 2017 is not supported.</span></span> 
* <span data-ttu-id="dd28d-120">.NET용 Azure SDK 버전 2.7.1 이상을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-120">Use the Azure SDK for .NET version 2.7.1 or later.</span></span> <span data-ttu-id="dd28d-121">[웹 플랫폼 설치 관리자](http://www.microsoft.com/web/downloads/platform.aspx)를 사용하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-121">Install it by using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="dd28d-122">[Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-122">Install the [Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).</span></span>

## <a name="create-a-stream-analytics-project"></a><span data-ttu-id="dd28d-123">Stream Analytics 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="dd28d-123">Create a Stream Analytics project</span></span>
1. <span data-ttu-id="dd28d-124">Visual Studio에서 **파일** 메뉴를 클릭하고 **새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-124">In Visual Studio, click the **File** menu and select **New Project**.</span></span> 

2. <span data-ttu-id="dd28d-125">왼쪽의 템플릿 목록에서 **Stream Analytics**를 선택한 후 **Azure Stream Analytics 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-125">In the templates list on the left, select **Stream Analytics** and then click **Azure Stream Analytics Application**.</span></span>

3. <span data-ttu-id="dd28d-126">다른 프로젝트와 마찬가지로 프로젝트 **이름**, **위치** 및 **솔루션 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-126">Enter the project **Name**, **Location**, and **Solution name** as you do for other projects.</span></span>

    ![새 프로젝트 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    <span data-ttu-id="dd28d-128">**솔루션 탐색기**에 **Toll** 프로젝트가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-128">A **Toll** project is generated in **Solution Explorer**.</span></span>

    ![솔루션 탐색기에 생성된 Toll 프로젝트](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-the-correct-subscription"></a><span data-ttu-id="dd28d-130">올바른 구독 선택</span><span class="sxs-lookup"><span data-stu-id="dd28d-130">Choose the correct subscription</span></span>
1. <span data-ttu-id="dd28d-131">Visual Studio에서 **보기** 메뉴를 클릭하고 **서버 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-131">In Visual Studio, click the **View** menu and open **Server Explorer**.</span></span>

2. <span data-ttu-id="dd28d-132">Azure 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-132">Sign in with your Azure Account.</span></span> 

## <a name="define-the-input-sources"></a><span data-ttu-id="dd28d-133">입력 원본 정의</span><span class="sxs-lookup"><span data-stu-id="dd28d-133">Define the input sources</span></span>
1.  <span data-ttu-id="dd28d-134">**솔루션 탐색기**에서 **입력** 노드를 확장하고 이름을 **Input.json**에서 **EntryStream.json**으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-134">In **Solution Explorer**, expand the **Inputs** node and rename **Input.json** to **EntryStream.json**.</span></span> <span data-ttu-id="dd28d-135">**EntryStream.json**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-135">Double-click **EntryStream.json**.</span></span>
2.  <span data-ttu-id="dd28d-136">이제 **입력 별칭**은 **EntryStream**입니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-136">The **Input Alias** is now **EntryStream**.</span></span> <span data-ttu-id="dd28d-137">입력 별칭이 쿼리 스크립트에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-137">The input alias is used in the query script.</span></span> 
3.  <span data-ttu-id="dd28d-138">**원본 형식**으로 **데이터 스트림**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-138">In **Source Type**, select **Data Stream**.</span></span>
4.  <span data-ttu-id="dd28d-139">**원본**에서 **이벤트 허브**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-139">In **Source**, select **Event Hub**.</span></span>
5.  <span data-ttu-id="dd28d-140">**서비스 버스 네임스페이스**에서 **TollData** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-140">In **Service Bus Namespace**, select the **TollData** option.</span></span>
6.  <span data-ttu-id="dd28d-141">**이벤트 허브 이름**에서 **entry**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-141">In **Event Hub Name**, select **entry**.</span></span>
7.  <span data-ttu-id="dd28d-142">**이벤트 허브 정책 이름**에서 **RootManageSharedAccessKey**(기본값)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-142">In **Event Hub Policy Name**, select **RootManageSharedAccessKey** (the default value).</span></span>
8.  <span data-ttu-id="dd28d-143">**이벤트 직렬화 형식**으로 **Json**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-143">In **Event Serialization Format**, select **Json**.</span></span> 
9.  <span data-ttu-id="dd28d-144">**인코딩**으로 **UTF8**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-144">In **Encoding**, select **UTF8**.</span></span> <span data-ttu-id="dd28d-145">설정은 다음 스크린샷과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-145">Your settings should look like the following screenshot:</span></span>

    ![입력 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. <span data-ttu-id="dd28d-147">마법사를 마치려면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-147">To finish the wizard, click **Save**.</span></span> <span data-ttu-id="dd28d-148">이제 다른 입력 원본을 추가하여 진출 스트림을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-148">Now you can add another input source to create the exit stream.</span></span> <span data-ttu-id="dd28d-149">**입력** 노드를 마우스 오른쪽 단추로 클릭하고 **새 항목**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-149">Right-click the **Inputs** node, and select **New Item**.</span></span>

    ![새 항목](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. <span data-ttu-id="dd28d-151">창에서 **Azure Stream Analytics 입력**을 선택하고 **이름**을 **ExitStream.json**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-151">In the window, select **Azure Stream Analytics Input**, and change the **Name** to **ExitStream.json**.</span></span> <span data-ttu-id="dd28d-152">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-152">Click **Add**.</span></span>

    ![새 항목 추가 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. <span data-ttu-id="dd28d-154">프로젝트에서 **ExitStream.json**을 두 번 클릭하고 진입 스트림과 같은 단계를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-154">Double-click **ExitStream.json** in the project, and follow the same steps as you did for the entry stream.</span></span> <span data-ttu-id="dd28d-155">다음 스크린샷과 같이 **이벤트 허브 이름**에 대해 **exit**을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-155">Be sure to enter **exit** for the **Event Hub Name** as shown in the following screenshot:</span></span>

    ![ExitStream 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    <span data-ttu-id="dd28d-157">이제 두 입력 스트림을 정의했습니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-157">Now you have defined two input streams:</span></span>

    ![진입 및 종료 입력 스트림](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    <span data-ttu-id="dd28d-159">다음으로, 차량 등록 데이터가 있는 Blob 파일에 대해 참조 데이터 입력을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-159">Next, add reference data input for the blob file that contains car registration data.</span></span>

13. <span data-ttu-id="dd28d-160">프로젝트에서 **입력** 노드를 마우스 오른쪽 단추로 클릭한 후 스트림 입력에 대해 수행한 것과 동일한 단계를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-160">Right-click the **Inputs** node in the project, and then follow the same steps as you did for the stream inputs.</span></span> <span data-ttu-id="dd28d-161">**입력 별칭**에 **Registration**을 입력하고 **원본 형식**에서 **참조 데이터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-161">In **Input Alias**, enter **Registration**, and in **Source Type**, select **Reference data**.</span></span>

    ![등록 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. <span data-ttu-id="dd28d-163">**저장소 계정**에서 **tolldata** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-163">In **Storage Account**, select the **tolldata** option.</span></span> <span data-ttu-id="dd28d-164">**컨테이너**에서 **tolldata**를 선택하고 **경로 패턴**에 **registration.json**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-164">In **Container**, select **tolldata**, and in **Path Pattern**, enter **registration.json**.</span></span> <span data-ttu-id="dd28d-165">이 파일 이름은 대/소문자를 구분하므로 소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-165">This file name is case sensitive and should be lowercase.</span></span>
15. <span data-ttu-id="dd28d-166">마법사를 마치려면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-166">To finish the wizard, click **Save**.</span></span>

<span data-ttu-id="dd28d-167">이제 모든 입력이 정의되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-167">Now all the inputs are defined.</span></span>

## <a name="define-the-output"></a><span data-ttu-id="dd28d-168">출력 정의</span><span class="sxs-lookup"><span data-stu-id="dd28d-168">Define the output</span></span>
1.  <span data-ttu-id="dd28d-169">**솔루션 탐색기**에서 **입력** 노드를 확장하고 **Output.json**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-169">In **Solution Explorer**, expand the **Inputs** node and double-click **Output.json**.</span></span>

2.  <span data-ttu-id="dd28d-170">**출력 별칭**에 **output**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-170">In **Output Alias**, enter **output**.</span></span> 
3.  <span data-ttu-id="dd28d-171">**싱크**에서 **SQL Database**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-171">In **Sink**, select **SQL Database**.</span></span>
4.  <span data-ttu-id="dd28d-172">**데이터베이스**에서 **TollDataDB**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-172">In **Database**, select **TollDataDB**.</span></span>
5.  <span data-ttu-id="dd28d-173">**사용자 이름**에 **tolladmin**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-173">In **User Name**, enter **tolladmin**.</span></span> 
6.  <span data-ttu-id="dd28d-174">**암호**에 **123toll!**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-174">In **Password**, enter **123toll!**.</span></span>
7.  <span data-ttu-id="dd28d-175">**테이블**에 **TollDataRefJoin**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-175">In **Table**, enter **TollDataRefJoin**.</span></span>
8.  <span data-ttu-id="dd28d-176">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-176">Click **Save**.</span></span>

    ![출력 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a><span data-ttu-id="dd28d-178">Stream Analytics 쿼리 만들기</span><span class="sxs-lookup"><span data-stu-id="dd28d-178">Create a Stream Analytics query</span></span>
<span data-ttu-id="dd28d-179">이 자습서에서는 요금 데이터와 관련된 여러 가지 비즈니스 질문에 답변합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-179">This tutorial attempts to answer several business questions that are related to toll data.</span></span> <span data-ttu-id="dd28d-180">관련 답변을 제공하기 위해 Stream Analytics에서 사용할 수 있는 Stream Analytics 쿼리도 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-180">It also constructs Stream Analytics queries that can be used in Stream Analytics to provide relevant answers.</span></span>
<span data-ttu-id="dd28d-181">첫 번째 Stream Analytics 작업을 시작하기 전에 간단한 시나리오 및 쿼리 구문을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-181">Before you start your first Stream Analytics job, let’s explore a simple scenario and the query syntax.</span></span>

### <a name="introduction-to-the-stream-analytics-query-language"></a><span data-ttu-id="dd28d-182">Stream Analytics 쿼리 언어 소개</span><span class="sxs-lookup"><span data-stu-id="dd28d-182">Introduction to the Stream Analytics query language</span></span>
<span data-ttu-id="dd28d-183">요금 창구에 들어가는 차량 수를 계산해야 한다고 가정해봅시다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-183">Let’s say that you need to count the number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="dd28d-184">이 예제는 연속 이벤트 스트림이므로 기간을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-184">Because this example is a continuous stream of events, you have to define a period of time.</span></span> <span data-ttu-id="dd28d-185">이 질문을 “3분 간격으로 요금 창구에 진입하는 차량은 몇 대입니까?”로 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-185">Modify the question to be “How many vehicles enter a toll booth every three minutes?”</span></span> <span data-ttu-id="dd28d-186">데이터 수를 세는 이 방법을 일반적으로 연속 개수(Tumbling Count)라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-186">This way to count data is commonly referred to as the tumbling count.</span></span>

<span data-ttu-id="dd28d-187">이 질문에 대답하는 Stream Analytics 쿼리를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-187">Look at the Stream Analytics query that answers this question:</span></span>

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

<span data-ttu-id="dd28d-188">Azure Stream Analytics는 SQL과 유사한 쿼리를 사용하고 몇 가지 확장을 추가하여 쿼리의 시간 관련 측면을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-188">Stream Analytics uses a query language that's like SQL and adds a few extensions to specify time-related aspects of the query.</span></span>

<span data-ttu-id="dd28d-189">자세한 내용을 보려면 MSDN의 쿼리에 사용된 [시간 관리](https://msdn.microsoft.com/library/azure/mt582045.aspx) 및 [창 작업](https://msdn.microsoft.com/library/azure/dn835019.aspx) 구문을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd28d-189">For more information, see [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in the query from MSDN.</span></span>

<span data-ttu-id="dd28d-190">이제 첫 번째 Stream Analytics 쿼리를 작성했고 테스트할 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-190">Now that you have written your first Stream Analytics query, it's time to test it.</span></span> <span data-ttu-id="dd28d-191">다음 경로의 TollApp 폴더에 있는 샘플 데이터 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-191">Use the sample data files located in your TollApp folder in the following path:</span></span>

<span data-ttu-id="dd28d-192">..\TollApp\TollApp\Data</span><span class="sxs-lookup"><span data-stu-id="dd28d-192">..\TollApp\TollApp\Data</span></span>

<span data-ttu-id="dd28d-193">이 폴더에는 다음 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-193">This folder contains the following files:</span></span>
*   <span data-ttu-id="dd28d-194">Entry.json</span><span class="sxs-lookup"><span data-stu-id="dd28d-194">Entry.json</span></span>
*   <span data-ttu-id="dd28d-195">Exit.json</span><span class="sxs-lookup"><span data-stu-id="dd28d-195">Exit.json</span></span>
*   <span data-ttu-id="dd28d-196">registration.json</span><span class="sxs-lookup"><span data-stu-id="dd28d-196">Registration.json</span></span>

## <a name="count-the-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="dd28d-197">요금 창구에 들어가는 차량 수 세기</span><span class="sxs-lookup"><span data-stu-id="dd28d-197">Count the number of vehicles entering a toll booth</span></span>
<span data-ttu-id="dd28d-198">프로젝트에서 **Script.asaql**을 두 번 클릭하여 **쿼리 편집기**에서 스크립트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-198">In the project, double-click **Script.asaql** to open the script in the **Query Editor**.</span></span> <span data-ttu-id="dd28d-199">이전 섹션의 스크립트를 편집기에 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-199">Copy and paste the script in the previous section into the editor.</span></span> <span data-ttu-id="dd28d-200">쿼리 편집기에서는 IntelliSense, 구문 색 지정 및 오류 마커를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-200">The Query Editor supports IntelliSense, syntax coloring, and the error marker.</span></span>

![쿼리 편집기](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a><span data-ttu-id="dd28d-202">로컬에서 Stream Analytics 쿼리 테스트</span><span class="sxs-lookup"><span data-stu-id="dd28d-202">Test Stream Analytics queries locally</span></span>

1. <span data-ttu-id="dd28d-203">구문 오류가 있는지 확인하도록 쿼리를 컴파일하려면 프로젝트를 마우스 오른쪽 단추로 클릭하고 **빌드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-203">To compile the query to see if there is a syntax error, right-click the project and select **Build**.</span></span> 

2. <span data-ttu-id="dd28d-204">샘플 데이터에 대해 이 쿼리의 유효성을 검사하려면 로컬 샘플 데이터를 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-204">To validate this query against sample data, you can use local sample data.</span></span> <span data-ttu-id="dd28d-205">입력을 마우스 오른쪽 단추로 클릭하고 **로컬 입력 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-205">Right-click the input, and select **Add local input**.</span></span>

    ![로컬 입력 추가](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. <span data-ttu-id="dd28d-207">팝업 창에서 로컬 경로의 샘플 데이터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-207">In the pop-up window, select the sample data from your local path.</span></span> <span data-ttu-id="dd28d-208">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-208">Click **Save**.</span></span>

    ![로컬 입력 추가 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    <span data-ttu-id="dd28d-210">**local_EntryStream.json** 파일이 입력 폴더에 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-210">A file named **local_EntryStream.json** is automatically added to your inputs folder.</span></span>

    ![입력 폴더에 추가된 파일](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. <span data-ttu-id="dd28d-212">**쿼리 편집기**에서 **로컬로 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-212">In the **Query Editor**, click **Run Locally**.</span></span> <span data-ttu-id="dd28d-213">또는 F5 키를 눌러도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-213">Or you can press the F5 key.</span></span>

    ![로컬로 실행](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![로컬 실행 출력](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    <span data-ttu-id="dd28d-216">아무 키나 누르면 Visual Studio의 **ASA 로컬 실행 결과** 창에서 출력을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-216">Press any key to view the output in the **ASA Local Run Result** window in Visual Studio.</span></span> 

    ![ASA 로컬 실행 결과 창](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. <span data-ttu-id="dd28d-218">**결과 폴더 열기**를 클릭하여 출력 파일을 CSV 및 JSON 형식 모두로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-218">Click **Open Result Folder** to check the output files both in CSV and JSON format.</span></span>

    ![결과 폴더 열기 출력](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-the-input-data"></a><span data-ttu-id="dd28d-220">입력 데이터 샘플링</span><span class="sxs-lookup"><span data-stu-id="dd28d-220">Sample the input data</span></span>
<span data-ttu-id="dd28d-221">입력 원본에서 로컬 파일로 입력 데이터를 샘플링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-221">You can also sample input data from input sources to a local file.</span></span> 
1. <span data-ttu-id="dd28d-222">입력 구성 파일을 마우스 오른쪽 단추로 클릭하고 **샘플 데이터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-222">Right-click the input config file, and select **Sample Data**.</span></span> 

   ![샘플 데이터](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    <span data-ttu-id="dd28d-224">지금은 이벤트 허브 또는 IoT Hub를 샘플링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-224">You can sample only event hub or IoT hub for now.</span></span> <span data-ttu-id="dd28d-225">다른 입력 원본은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-225">Other input sources are not supported.</span></span>

2. <span data-ttu-id="dd28d-226">팝업 창에서 샘플 데이터를 저장하는 데 사용된 로컬 경로를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-226">In the pop-up window, enter the local path used to save the sample data.</span></span> <span data-ttu-id="dd28d-227">**샘플링**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-227">Click **Sample**.</span></span>

    ![샘플 데이터 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    <span data-ttu-id="dd28d-229">**출력** 창에서 진행률을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-229">You can see the progress in the **Output** window.</span></span> 

    ![출력 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-to-azure"></a><span data-ttu-id="dd28d-231">Stream Analytics 쿼리를 Azure에 제출</span><span class="sxs-lookup"><span data-stu-id="dd28d-231">Submit a Stream Analytics query to Azure</span></span>
1. <span data-ttu-id="dd28d-232">**쿼리 편집기**의 스크립트 편집기에서 **Azure에 제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-232">In the **Query Editor**, click **Submit To Azure** in the script editor.</span></span>

    ![Azure에 제출](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. <span data-ttu-id="dd28d-234">**새 Azure Stream Analytics 작업 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-234">Select **Create a New Azure Stream Analytics Job**.</span></span> <span data-ttu-id="dd28d-235">**작업 이름**을 입력하고 올바른 **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-235">Enter the **Job Name**, and select the correct **Subscription**.</span></span> <span data-ttu-id="dd28d-236">**Submit**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-236">Click **Submit**.</span></span>

    ![작업 전송 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a><span data-ttu-id="dd28d-238">작업 시작</span><span class="sxs-lookup"><span data-stu-id="dd28d-238">Start a job</span></span>
<span data-ttu-id="dd28d-239">이제 작업이 생성되었고 작업 보기가 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-239">Now that your job is created, the job view is automatically opened.</span></span> 
1. <span data-ttu-id="dd28d-240">작업을 시작하려면 **녹색** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-240">To start the job, click the **green arrow** button.</span></span>

    ![작업 시작](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. <span data-ttu-id="dd28d-242">기본 설정을 선택하고 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-242">Select the default setting, and click **Start**.</span></span>
 
    ![작업 시작 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    <span data-ttu-id="dd28d-244">작업 **상태**가 **실행 중**으로 변경되고 **입력 이벤트** 및 **출력 이벤트**가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-244">The job **Status** changes to **Running**, and **Input Events** and **Output Events** appear.</span></span>

    ![작업 요약에서 실행 중 상태](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-the-results-in-visual-studio"></a><span data-ttu-id="dd28d-246">Visual Studio에서 결과 확인</span><span class="sxs-lookup"><span data-stu-id="dd28d-246">Check the results in Visual Studio</span></span>
1. <span data-ttu-id="dd28d-247">Visual Studio에서 **서버 탐색기**를 열고 **TollDataRefJoin** 테이블을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-247">In Visual Studio, open **Server Explorer** and right-click the **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="dd28d-248">**테이블 데이터 표시**를 선택하면 작업의 출력을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-248">Select **Show Table Data** to see the output of your job.</span></span>
   
    ![서버 탐색기의 테이블 데이터 표시 선택 영역](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-the-job-metrics"></a><span data-ttu-id="dd28d-250">작업 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="dd28d-250">View the job metrics</span></span>
<span data-ttu-id="dd28d-251">몇 가지 기본 작업 통계는 **Job Metrics(작업 메트릭)**에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-251">Some basic job statistics can be found in **Job Metrics**.</span></span> 

![작업 메트릭 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-the-job-in-server-explorer"></a><span data-ttu-id="dd28d-253">서버 탐색기에 작업 나열</span><span class="sxs-lookup"><span data-stu-id="dd28d-253">List the job in Server Explorer</span></span>
<span data-ttu-id="dd28d-254">**서버 탐색기**에서 **Stream Analytics 작업**을 클릭하고 **새로 고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-254">In **Server Explorer**, click **Stream Analytics Jobs** and then click **Refresh**.</span></span> <span data-ttu-id="dd28d-255">작업이 **Stream Analytics 작업** 아래 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-255">The job appears under **Stream Analytics jobs**.</span></span>

![서버 탐색기에 나열된 Stream Analytics 작업](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-the-job-view"></a><span data-ttu-id="dd28d-257">작업 보기 열기</span><span class="sxs-lookup"><span data-stu-id="dd28d-257">Open the job view</span></span>
<span data-ttu-id="dd28d-258">작업 보기를 열려면 작업 노드를 확장하고 **작업 보기** 노드를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-258">To open the job view, expand your job node and double-click the **Job View** node.</span></span>

![작업 보기 노드](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-to-a-project"></a><span data-ttu-id="dd28d-260">기존 작업을 프로젝트로 내보내기</span><span class="sxs-lookup"><span data-stu-id="dd28d-260">Export an existing job to a project</span></span>
<span data-ttu-id="dd28d-261">두 가지 방법으로 기존 작업을 프로젝트로 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-261">There are two ways you can export an existing job to a project.</span></span>

<span data-ttu-id="dd28d-262">**서버 탐색기**에서 **Stream Analytics 작업** 노드의 작업 노드를 마우스 오른쪽 단추로 클릭하고 **새 Stream Analytics 프로젝트로 내보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-262">In **Server Explorer**, right-click the job node in the **Stream Analytics Jobs** node and select **Export to New Stream Analytics Project**.</span></span>

![새 Stream Analytics 프로젝트로 내보내기](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

<span data-ttu-id="dd28d-264">**솔루션 탐색기**에 프로젝트가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-264">The project is generated in **Solution Explorer**.</span></span>

![솔루션 탐색기에 생성된 프로젝트](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
<span data-ttu-id="dd28d-266">작업 보기를 사용하고 **프로젝트 생성**을 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-266">You also can use the job view, and click **Generate Project**.</span></span>

![프로젝트 생성](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a><span data-ttu-id="dd28d-268">알려진 문제 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="dd28d-268">Known issues and limitations</span></span>
 
- <span data-ttu-id="dd28d-269">Power BI 출력 및 Azure Date Lake Store 출력에 대한 지원은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-269">There is no support for Power BI output and Azure Date Lake Store output.</span></span>
- <span data-ttu-id="dd28d-270">JavaScript 사용자 정의 함수를 추가 또는 변경하기 위한 편집기 지원은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dd28d-270">There is no editor support for adding or changing JavaScript user-defined functions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd28d-271">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dd28d-271">Next steps</span></span>
* [<span data-ttu-id="dd28d-272">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="dd28d-272">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="dd28d-273">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="dd28d-273">Get started by using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="dd28d-274">Azure 스트림 분석 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="dd28d-274">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="dd28d-275">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="dd28d-275">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="dd28d-276">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="dd28d-276">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
