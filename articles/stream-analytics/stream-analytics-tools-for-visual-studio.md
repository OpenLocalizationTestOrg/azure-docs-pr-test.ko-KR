---
title: "Azure 스트림 분석 Tools for Visual Studio aaaUse | Microsoft Docs"
description: "Azure 스트림 분석 Tools for Visual Studio hello에 대 한 자습서 시작"
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
ms.openlocfilehash: bda8e548040509a6f29f1b713268bc38f73228fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a><span data-ttu-id="59214-104">Azure Stream Analytics Tools for Visual Studio 사용</span><span class="sxs-lookup"><span data-stu-id="59214-104">Use Azure Stream Analytics Tools for Visual Studio</span></span>
## <a name="introduction"></a><span data-ttu-id="59214-105">소개</span><span class="sxs-lookup"><span data-stu-id="59214-105">Introduction</span></span>
<span data-ttu-id="59214-106">이 자습서에서는 방법 Visual Studio toocreate toouse Azure 스트림 분석 도구를 작성, 로컬로 테스트, 관리 및 스트림 분석 작업을 디버그 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="59214-106">In this tutorial, you learn how toouse Azure Stream Analytics Tools for Visual Studio toocreate, author, test locally, manage, and debug your Stream Analytics jobs.</span></span> 

<span data-ttu-id="59214-107">이 자습서를 완료하고 나면 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59214-107">After completing this tutorial, you will be able to:</span></span>
* <span data-ttu-id="59214-108">Stream Analytics Tools for Visual Studio를 익숙하게 사용 가능</span><span class="sxs-lookup"><span data-stu-id="59214-108">Familiarize yourself with Stream Analytics Tools for Visual Studio.</span></span>
* <span data-ttu-id="59214-109">Stream Analytics 작업 구성 및 배포</span><span class="sxs-lookup"><span data-stu-id="59214-109">Configure and deploy a Stream Analytics job.</span></span>
* <span data-ttu-id="59214-110">로컬 샘플 데이터로 로컬에서 작업 테스트</span><span class="sxs-lookup"><span data-stu-id="59214-110">Test your job locally with local sample data.</span></span>
* <span data-ttu-id="59214-111">Tootroubleshoot 문제 모니터링을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-111">Use monitoring tootroubleshoot issues.</span></span>
* <span data-ttu-id="59214-112">기존 작업 tooprojects를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="59214-112">Export existing jobs tooprojects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59214-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="59214-113">Prerequisites</span></span>
<span data-ttu-id="59214-114">toocomplete이이 자습서에서는 다음 필수 구성 요소는 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="59214-114">toocomplete this tutorial, you need hello following prerequisites:</span></span>
* <span data-ttu-id="59214-115">Hello에 "스트림 분석 작업 만들기" 앞에 있는 hello 단계 완료 [스트림 분석 자습서를 사용 하 여 IoT 솔루션 작성](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics)합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-115">Finish hello steps that precede "Create a Stream Analytics job" in hello [Build an IoT solution by using Stream Analytics tutorial](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span></span> 
* <span data-ttu-id="59214-116">Visual Studio 2015, Visual Studio 2013 업데이트 4 또는 Visual Studio 2012를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-116">Use Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012.</span></span> <span data-ttu-id="59214-117">Enterprise(Ultimate/Premium), Professional 및 Community Edition이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="59214-117">Enterprise (Ultimate/Premium), Professional, and Community editions are supported.</span></span> <span data-ttu-id="59214-118">Express Edition은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="59214-118">Express edition is not supported.</span></span> <span data-ttu-id="59214-119">Visual Studio 2017은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="59214-119">Visual Studio 2017 is not supported.</span></span> 
* <span data-ttu-id="59214-120">사용 하 여 hello Azure SDK for.NET 버전 2.7.1 이상.</span><span class="sxs-lookup"><span data-stu-id="59214-120">Use hello Azure SDK for .NET version 2.7.1 or later.</span></span> <span data-ttu-id="59214-121">Hello를 사용 하 여 설치 [웹 플랫폼 설치 관리자](http://www.microsoft.com/web/downloads/platform.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-121">Install it by using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="59214-122">Hello 설치 [스트림 분석 Tools for Visual Studio](http://aka.ms/asatoolsvs)합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-122">Install hello [Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).</span></span>

## <a name="create-a-stream-analytics-project"></a><span data-ttu-id="59214-123">Stream Analytics 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="59214-123">Create a Stream Analytics project</span></span>
1. <span data-ttu-id="59214-124">Visual Studio에서 클릭 hello **파일** 메뉴와 선택 **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-124">In Visual Studio, click hello **File** menu and select **New Project**.</span></span> 

2. <span data-ttu-id="59214-125">Hello hello 왼쪽의 템플릿 목록에서 선택 **스트림 분석** 클릭 하 고 **Azure 스트림 분석 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-125">In hello templates list on hello left, select **Stream Analytics** and then click **Azure Stream Analytics Application**.</span></span>

3. <span data-ttu-id="59214-126">Hello 프로젝트 입력 **이름**, **위치**, 및 **솔루션 이름** 다른 프로젝트의 경우와 마찬가지로 합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-126">Enter hello project **Name**, **Location**, and **Solution name** as you do for other projects.</span></span>

    ![새 프로젝트 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    <span data-ttu-id="59214-128">**솔루션 탐색기**에 **Toll** 프로젝트가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="59214-128">A **Toll** project is generated in **Solution Explorer**.</span></span>

    ![솔루션 탐색기에 생성된 Toll 프로젝트](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-hello-correct-subscription"></a><span data-ttu-id="59214-130">Hello 올바른 구독이 선택</span><span class="sxs-lookup"><span data-stu-id="59214-130">Choose hello correct subscription</span></span>
1. <span data-ttu-id="59214-131">Visual Studio에서 클릭 hello **보기** 메뉴를 열고 다음 **서버 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-131">In Visual Studio, click hello **View** menu and open **Server Explorer**.</span></span>

2. <span data-ttu-id="59214-132">Azure 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-132">Sign in with your Azure Account.</span></span> 

## <a name="define-hello-input-sources"></a><span data-ttu-id="59214-133">Hello 입력된 소스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-133">Define hello input sources</span></span>
1.  <span data-ttu-id="59214-134">**솔루션 탐색기**, hello 확장 **입력** 노드 및 이름 바꾸기 **Input.json** 너무**EntryStream.json**합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-134">In **Solution Explorer**, expand hello **Inputs** node and rename **Input.json** too**EntryStream.json**.</span></span> <span data-ttu-id="59214-135">**EntryStream.json**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-135">Double-click **EntryStream.json**.</span></span>
2.  <span data-ttu-id="59214-136">hello **입력 별칭** 이제 **EntryStream**합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-136">hello **Input Alias** is now **EntryStream**.</span></span> <span data-ttu-id="59214-137">hello 입력 별칭은 hello 쿼리 스크립트에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59214-137">hello input alias is used in hello query script.</span></span> 
3.  <span data-ttu-id="59214-138">**원본 형식**으로 **데이터 스트림**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-138">In **Source Type**, select **Data Stream**.</span></span>
4.  <span data-ttu-id="59214-139">**원본**에서 **이벤트 허브**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-139">In **Source**, select **Event Hub**.</span></span>
5.  <span data-ttu-id="59214-140">**서비스 버스 Namespace**선택, hello **TollData** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="59214-140">In **Service Bus Namespace**, select hello **TollData** option.</span></span>
6.  <span data-ttu-id="59214-141">**이벤트 허브 이름**에서 **entry**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-141">In **Event Hub Name**, select **entry**.</span></span>
7.  <span data-ttu-id="59214-142">**이벤트 허브 정책 이름**선택, **RootManageSharedAccessKey** (기본값 hello).</span><span class="sxs-lookup"><span data-stu-id="59214-142">In **Event Hub Policy Name**, select **RootManageSharedAccessKey** (hello default value).</span></span>
8.  <span data-ttu-id="59214-143">**이벤트 직렬화 형식**으로 **Json**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-143">In **Event Serialization Format**, select **Json**.</span></span> 
9.  <span data-ttu-id="59214-144">**인코딩**으로 **UTF8**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-144">In **Encoding**, select **UTF8**.</span></span> <span data-ttu-id="59214-145">설정에 따라 스크린 샷 hello 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59214-145">Your settings should look like hello following screenshot:</span></span>

    ![입력 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. <span data-ttu-id="59214-147">toofinish hello 마법사 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-147">toofinish hello wizard, click **Save**.</span></span> <span data-ttu-id="59214-148">이제 다른 toocreate hello 종료 스트림 입력된 소스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59214-148">Now you can add another input source toocreate hello exit stream.</span></span> <span data-ttu-id="59214-149">마우스 오른쪽 단추로 클릭 hello **입력** 노드를 선택한 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-149">Right-click hello **Inputs** node, and select **New Item**.</span></span>

    ![새 항목](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. <span data-ttu-id="59214-151">Hello 창에서 선택한 **Azure 스트림 분석 입력**, hello 변경 **이름** 너무**ExitStream.json**합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-151">In hello window, select **Azure Stream Analytics Input**, and change hello **Name** too**ExitStream.json**.</span></span> <span data-ttu-id="59214-152">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-152">Click **Add**.</span></span>

    ![새 항목 추가 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. <span data-ttu-id="59214-154">두 번 클릭 **ExitStream.json** hello 프로젝트 및 hello 입력 스트림에 대해 수행한 것 처럼 동일한 단계에 따라 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59214-154">Double-click **ExitStream.json** in hello project, and follow hello same steps as you did for hello entry stream.</span></span> <span data-ttu-id="59214-155">수 있는지 tooenter **종료** hello에 대 한 **이벤트 허브 이름** hello 스크린 샷 뒤에 표시 된 대로:</span><span class="sxs-lookup"><span data-stu-id="59214-155">Be sure tooenter **exit** for hello **Event Hub Name** as shown in hello following screenshot:</span></span>

    ![ExitStream 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    <span data-ttu-id="59214-157">이제 두 입력 스트림을 정의했습니다.</span><span class="sxs-lookup"><span data-stu-id="59214-157">Now you have defined two input streams:</span></span>

    ![진입 및 종료 입력 스트림](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    <span data-ttu-id="59214-159">다음으로, 자동차 대 한 등록 데이터를 포함 하는 hello blob 파일에 대 한 참조 데이터 입력을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-159">Next, add reference data input for hello blob file that contains car registration data.</span></span>

13. <span data-ttu-id="59214-160">마우스 오른쪽 단추로 클릭 hello **입력** hello 프로젝트 및 hello 스트림 입력에 대해 수행한 것 처럼 동일한 단계에 따라 hello에서 노드.</span><span class="sxs-lookup"><span data-stu-id="59214-160">Right-click hello **Inputs** node in hello project, and then follow hello same steps as you did for hello stream inputs.</span></span> <span data-ttu-id="59214-161">**입력 별칭**에 **Registration**을 입력하고 **원본 형식**에서 **참조 데이터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-161">In **Input Alias**, enter **Registration**, and in **Source Type**, select **Reference data**.</span></span>

    ![등록 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. <span data-ttu-id="59214-163">**저장소 계정**선택, hello **tolldata** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="59214-163">In **Storage Account**, select hello **tolldata** option.</span></span> <span data-ttu-id="59214-164">**컨테이너**에서 **tolldata**를 선택하고 **경로 패턴**에 **registration.json**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-164">In **Container**, select **tolldata**, and in **Path Pattern**, enter **registration.json**.</span></span> <span data-ttu-id="59214-165">이 파일 이름은 대/소문자를 구분하므로 소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-165">This file name is case sensitive and should be lowercase.</span></span>
15. <span data-ttu-id="59214-166">toofinish hello 마법사 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-166">toofinish hello wizard, click **Save**.</span></span>

<span data-ttu-id="59214-167">이제 모든 hello 입력 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59214-167">Now all hello inputs are defined.</span></span>

## <a name="define-hello-output"></a><span data-ttu-id="59214-168">Hello 출력을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-168">Define hello output</span></span>
1.  <span data-ttu-id="59214-169">**솔루션 탐색기**, hello 확장 **입력** 노드와 두 번 클릭 **Output.json**합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-169">In **Solution Explorer**, expand hello **Inputs** node and double-click **Output.json**.</span></span>

2.  <span data-ttu-id="59214-170">**출력 별칭**에 **output**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-170">In **Output Alias**, enter **output**.</span></span> 
3.  <span data-ttu-id="59214-171">**싱크**에서 **SQL Database**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-171">In **Sink**, select **SQL Database**.</span></span>
4.  <span data-ttu-id="59214-172">**데이터베이스**에서 **TollDataDB**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-172">In **Database**, select **TollDataDB**.</span></span>
5.  <span data-ttu-id="59214-173">**사용자 이름**에 **tolladmin**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-173">In **User Name**, enter **tolladmin**.</span></span> 
6.  <span data-ttu-id="59214-174">**암호**에 **123toll!**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-174">In **Password**, enter **123toll!**.</span></span>
7.  <span data-ttu-id="59214-175">**테이블**에 **TollDataRefJoin**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-175">In **Table**, enter **TollDataRefJoin**.</span></span>
8.  <span data-ttu-id="59214-176">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-176">Click **Save**.</span></span>

    ![출력 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a><span data-ttu-id="59214-178">Stream Analytics 쿼리 만들기</span><span class="sxs-lookup"><span data-stu-id="59214-178">Create a Stream Analytics query</span></span>
<span data-ttu-id="59214-179">이 자습서는 여러 가지 비즈니스 질문을 관련된 tootoll 데이터 tooanswer를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-179">This tutorial attempts tooanswer several business questions that are related tootoll data.</span></span> <span data-ttu-id="59214-180">또한 tooprovide 관련 응답 스트림 분석에에서 사용할 수 있는 스트림 분석 쿼리를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-180">It also constructs Stream Analytics queries that can be used in Stream Analytics tooprovide relevant answers.</span></span>
<span data-ttu-id="59214-181">첫 번째 스트림 분석 작업을 시작 하기 전에 간단한 시나리오 및 hello 쿼리 구문을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="59214-181">Before you start your first Stream Analytics job, let’s explore a simple scenario and hello query syntax.</span></span>

### <a name="introduction-toohello-stream-analytics-query-language"></a><span data-ttu-id="59214-182">소개 toohello 스트림 분석 쿼리 언어</span><span class="sxs-lookup"><span data-stu-id="59214-182">Introduction toohello Stream Analytics query language</span></span>
<span data-ttu-id="59214-183">Toocount hello 수가 차량이 요금 소 창구를 입력 해야 하는 경우를 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="59214-183">Let’s say that you need toocount hello number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="59214-184">이 예제에서는 이벤트의 연속 스트림을 이므로의 toodefine를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-184">Because this example is a continuous stream of events, you have toodefine a period of time.</span></span> <span data-ttu-id="59214-185">Hello 질문 toobe "개수 차량 입력 요금 소 창구 3 분 마다?"를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-185">Modify hello question toobe “How many vehicles enter a toll booth every three minutes?”</span></span> <span data-ttu-id="59214-186">데이터는 일반적으로이 방식으로 toocount tooas hello 텀블 링 개수를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-186">This way toocount data is commonly referred tooas hello tumbling count.</span></span>

<span data-ttu-id="59214-187">이 질문에 응답 하는 hello 스트림 분석 쿼리를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-187">Look at hello Stream Analytics query that answers this question:</span></span>

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

<span data-ttu-id="59214-188">스트림 분석 쿼리 언어는 SQL 유사 하며 추가 하는 몇 가지 확장 toospecify 시간 관련 쿼리의 항목이 hello 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-188">Stream Analytics uses a query language that's like SQL and adds a few extensions toospecify time-related aspects of hello query.</span></span>

<span data-ttu-id="59214-189">자세한 내용은 참조 [시간 관리](https://msdn.microsoft.com/library/azure/mt582045.aspx) 및 [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) MSDN에서 hello 쿼리에 사용 되는 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="59214-189">For more information, see [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in hello query from MSDN.</span></span>

<span data-ttu-id="59214-190">이제 첫 번째 스트림 분석 쿼리를 작성 한 인지 시간 tootest 것입니다.</span><span class="sxs-lookup"><span data-stu-id="59214-190">Now that you have written your first Stream Analytics query, it's time tootest it.</span></span> <span data-ttu-id="59214-191">경로 따라 hello에 TollApp 폴더에 있는 hello 샘플 데이터 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-191">Use hello sample data files located in your TollApp folder in hello following path:</span></span>

<span data-ttu-id="59214-192">..\TollApp\TollApp\Data</span><span class="sxs-lookup"><span data-stu-id="59214-192">..\TollApp\TollApp\Data</span></span>

<span data-ttu-id="59214-193">이 폴더는 hello를 다음 파일이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59214-193">This folder contains hello following files:</span></span>
*   <span data-ttu-id="59214-194">Entry.json</span><span class="sxs-lookup"><span data-stu-id="59214-194">Entry.json</span></span>
*   <span data-ttu-id="59214-195">Exit.json</span><span class="sxs-lookup"><span data-stu-id="59214-195">Exit.json</span></span>
*   <span data-ttu-id="59214-196">registration.json</span><span class="sxs-lookup"><span data-stu-id="59214-196">Registration.json</span></span>

## <a name="count-hello-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="59214-197">개수 hello 차량이 요금 소 창구를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-197">Count hello number of vehicles entering a toll booth</span></span>
<span data-ttu-id="59214-198">Hello 프로젝트에서 두 번 클릭 **Script.asaql** hello에서 tooopen hello 스크립트 **쿼리 편집기**합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-198">In hello project, double-click **Script.asaql** tooopen hello script in hello **Query Editor**.</span></span> <span data-ttu-id="59214-199">복사한 hello 이전 단원의 hello 스크립트 hello 편집기에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="59214-199">Copy and paste hello script in hello previous section into hello editor.</span></span> <span data-ttu-id="59214-200">hello 쿼리 편집기는 IntelliSense, 구문 색 지정 및 hello 오류 표식 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-200">hello Query Editor supports IntelliSense, syntax coloring, and hello error marker.</span></span>

![쿼리 편집기](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a><span data-ttu-id="59214-202">로컬에서 Stream Analytics 쿼리 테스트</span><span class="sxs-lookup"><span data-stu-id="59214-202">Test Stream Analytics queries locally</span></span>

1. <span data-ttu-id="59214-203">구문 오류가 있을 경우 toocompile hello 쿼리 toosee hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-203">toocompile hello query toosee if there is a syntax error, right-click hello project and select **Build**.</span></span> 

2. <span data-ttu-id="59214-204">toovalidate이이 쿼리 샘플 데이터에 대해 로컬 샘플 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59214-204">toovalidate this query against sample data, you can use local sample data.</span></span> <span data-ttu-id="59214-205">Hello 입력을 마우스 오른쪽 단추로 클릭 하 고 선택 **로컬 입력 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-205">Right-click hello input, and select **Add local input**.</span></span>

    ![로컬 입력 추가](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. <span data-ttu-id="59214-207">Hello 팝업 창에 사용자의 로컬 경로에서 hello 예제 데이터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-207">In hello pop-up window, select hello sample data from your local path.</span></span> <span data-ttu-id="59214-208">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-208">Click **Save**.</span></span>

    ![로컬 입력 추가 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    <span data-ttu-id="59214-210">라는 파일 **local_EntryStream.json** tooyour 입력 폴더에 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59214-210">A file named **local_EntryStream.json** is automatically added tooyour inputs folder.</span></span>

    ![파일 추가 tooinputs 폴더](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. <span data-ttu-id="59214-212">Hello에 **쿼리 편집기**, 클릭 **로컬로 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-212">In hello **Query Editor**, click **Run Locally**.</span></span> <span data-ttu-id="59214-213">또는 hello F5 키를 눌러 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59214-213">Or you can press hello F5 key.</span></span>

    ![로컬로 실행](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![로컬 실행 출력](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    <span data-ttu-id="59214-216">Hello에서 모든 키 tooview hello 출력을 눌러 **ASA 로컬 실행 결과** Visual Studio의 창.</span><span class="sxs-lookup"><span data-stu-id="59214-216">Press any key tooview hello output in hello **ASA Local Run Result** window in Visual Studio.</span></span> 

    ![ASA 로컬 실행 결과 창](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. <span data-ttu-id="59214-218">클릭 **결과 폴더 열기** toocheck hello 출력 파일을 모두 CSV 및 JSON 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="59214-218">Click **Open Result Folder** toocheck hello output files both in CSV and JSON format.</span></span>

    ![결과 폴더 열기 출력](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-hello-input-data"></a><span data-ttu-id="59214-220">샘플 hello에 대 한 입력된 데이터</span><span class="sxs-lookup"><span data-stu-id="59214-220">Sample hello input data</span></span>
<span data-ttu-id="59214-221">샘플 입력된 데이터 입력된 소스 tooa 로컬 파일에서 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59214-221">You can also sample input data from input sources tooa local file.</span></span> 
1. <span data-ttu-id="59214-222">Hello 입력된 구성 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 **예제 데이터**합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-222">Right-click hello input config file, and select **Sample Data**.</span></span> 

   ![샘플 데이터](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    <span data-ttu-id="59214-224">지금은 이벤트 허브 또는 IoT Hub를 샘플링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59214-224">You can sample only event hub or IoT hub for now.</span></span> <span data-ttu-id="59214-225">다른 입력 원본은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="59214-225">Other input sources are not supported.</span></span>

2. <span data-ttu-id="59214-226">Hello 팝업 창에 hello 사용 되는 로컬 경로 toosave hello 샘플 데이터를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-226">In hello pop-up window, enter hello local path used toosave hello sample data.</span></span> <span data-ttu-id="59214-227">**샘플링**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-227">Click **Sample**.</span></span>

    ![샘플 데이터 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    <span data-ttu-id="59214-229">Hello hello 진행 상황을 볼 수 있습니다 **출력** 창.</span><span class="sxs-lookup"><span data-stu-id="59214-229">You can see hello progress in hello **Output** window.</span></span> 

    ![출력 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-tooazure"></a><span data-ttu-id="59214-231">스트림 분석 쿼리 tooAzure 제출</span><span class="sxs-lookup"><span data-stu-id="59214-231">Submit a Stream Analytics query tooAzure</span></span>
1. <span data-ttu-id="59214-232">Hello에 **쿼리 편집기**, 클릭 **tooAzure 제출** hello 스크립트 편집기에서.</span><span class="sxs-lookup"><span data-stu-id="59214-232">In hello **Query Editor**, click **Submit tooAzure** in hello script editor.</span></span>

    ![TooAzure 제출](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. <span data-ttu-id="59214-234">**새 Azure Stream Analytics 작업 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-234">Select **Create a New Azure Stream Analytics Job**.</span></span> <span data-ttu-id="59214-235">Hello 입력 **작업 이름**, 올바른 선택 hello 및 **구독**합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-235">Enter hello **Job Name**, and select hello correct **Subscription**.</span></span> <span data-ttu-id="59214-236">**제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-236">Click **Submit**.</span></span>

    ![작업 전송 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a><span data-ttu-id="59214-238">작업 시작</span><span class="sxs-lookup"><span data-stu-id="59214-238">Start a job</span></span>
<span data-ttu-id="59214-239">사용자 작업을 만든 했으므로 hello 작업 보기 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="59214-239">Now that your job is created, hello job view is automatically opened.</span></span> 
1. <span data-ttu-id="59214-240">toostart hello 작업을 hello 클릭 **녹색 화살표** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="59214-240">toostart hello job, click hello **green arrow** button.</span></span>

    ![작업 시작](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. <span data-ttu-id="59214-242">Hello 기본 설정을 선택 하 고 클릭 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-242">Select hello default setting, and click **Start**.</span></span>
 
    ![작업 시작 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    <span data-ttu-id="59214-244">hello 작업 **상태** 쪽 변경**실행**, 및 **입력 이벤트** 및 **출력 이벤트** 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="59214-244">hello job **Status** changes too**Running**, and **Input Events** and **Output Events** appear.</span></span>

    ![작업 요약에서 실행 중 상태](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-hello-results-in-visual-studio"></a><span data-ttu-id="59214-246">Visual Studio에서 hello 결과 확인</span><span class="sxs-lookup"><span data-stu-id="59214-246">Check hello results in Visual Studio</span></span>
1. <span data-ttu-id="59214-247">Visual Studio에서 열고 **서버 탐색기** hello 마우스 오른쪽 단추로 클릭 하 고 **TollDataRefJoin** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="59214-247">In Visual Studio, open **Server Explorer** and right-click hello **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="59214-248">선택 **테이블 데이터 표시** 작업의 toosee hello 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-248">Select **Show Table Data** toosee hello output of your job.</span></span>
   
    ![서버 탐색기의 테이블 데이터 표시 선택 영역](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-hello-job-metrics"></a><span data-ttu-id="59214-250">Hello 작업 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="59214-250">View hello job metrics</span></span>
<span data-ttu-id="59214-251">몇 가지 기본 작업 통계는 **Job Metrics(작업 메트릭)**에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59214-251">Some basic job statistics can be found in **Job Metrics**.</span></span> 

![작업 메트릭 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-hello-job-in-server-explorer"></a><span data-ttu-id="59214-253">서버 탐색기에서 목록 hello 작업</span><span class="sxs-lookup"><span data-stu-id="59214-253">List hello job in Server Explorer</span></span>
<span data-ttu-id="59214-254">**서버 탐색기**에서 **Stream Analytics 작업**을 클릭하고 **새로 고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-254">In **Server Explorer**, click **Stream Analytics Jobs** and then click **Refresh**.</span></span> <span data-ttu-id="59214-255">hello 작업 아래에 나타납니다. **스트림 분석 작업이**합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-255">hello job appears under **Stream Analytics jobs**.</span></span>

![서버 탐색기에 나열된 Stream Analytics 작업](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-hello-job-view"></a><span data-ttu-id="59214-257">열기 hello 작업 보기</span><span class="sxs-lookup"><span data-stu-id="59214-257">Open hello job view</span></span>
<span data-ttu-id="59214-258">tooopen hello 작업 보기 작업 노드를 확장 하 고 hello를 두 번 클릭 **작업 보기** 노드.</span><span class="sxs-lookup"><span data-stu-id="59214-258">tooopen hello job view, expand your job node and double-click hello **Job View** node.</span></span>

![작업 보기 노드](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-tooa-project"></a><span data-ttu-id="59214-260">기존 작업 tooa 프로젝트 내보내기</span><span class="sxs-lookup"><span data-stu-id="59214-260">Export an existing job tooa project</span></span>
<span data-ttu-id="59214-261">두 가지 방법으로 기존 작업 tooa 프로젝트를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59214-261">There are two ways you can export an existing job tooa project.</span></span>

<span data-ttu-id="59214-262">**서버 탐색기**, hello에 hello 작업 노드를 마우스 오른쪽 단추로 클릭 **스트림 분석 작업** 노드 선택한 **tooNew 스트림 분석 프로젝트 내보내기**합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-262">In **Server Explorer**, right-click hello job node in hello **Stream Analytics Jobs** node and select **Export tooNew Stream Analytics Project**.</span></span>

![스트림 분석 프로젝트 tooNew 내보내기](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

<span data-ttu-id="59214-264">hello 프로젝트에 생성 됩니다 **솔루션 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-264">hello project is generated in **Solution Explorer**.</span></span>

![솔루션 탐색기에 생성된 프로젝트](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
<span data-ttu-id="59214-266">Hello 작업 보기를 사용 하 고 수도 있습니다 클릭 **프로젝트 생성**합니다.</span><span class="sxs-lookup"><span data-stu-id="59214-266">You also can use hello job view, and click **Generate Project**.</span></span>

![프로젝트 생성](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a><span data-ttu-id="59214-268">알려진 문제 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="59214-268">Known issues and limitations</span></span>
 
- <span data-ttu-id="59214-269">Power BI 출력 및 Azure Date Lake Store 출력에 대한 지원은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59214-269">There is no support for Power BI output and Azure Date Lake Store output.</span></span>
- <span data-ttu-id="59214-270">JavaScript 사용자 정의 함수를 추가 또는 변경하기 위한 편집기 지원은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59214-270">There is no editor support for adding or changing JavaScript user-defined functions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59214-271">다음 단계</span><span class="sxs-lookup"><span data-stu-id="59214-271">Next steps</span></span>
* [<span data-ttu-id="59214-272">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="59214-272">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="59214-273">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="59214-273">Get started by using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="59214-274">Azure 스트림 분석 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="59214-274">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="59214-275">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="59214-275">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="59214-276">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="59214-276">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
