---
title: "Operations Management Suite-Azure 논리 앱의에서 aaaTrack B2B 메시지 | Microsoft Docs"
description: "Azure Log Analytics를 사용하여 OMS(Operations Management Suite)에서 통합 계정 및 논리 앱에 대한 B2B 통신 추적"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: f385a72008b19408bb45d61c440df0505b688175
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="track-b2b-communication-in-hello-microsoft-operations-management-suite-oms"></a><span data-ttu-id="c0b89-103">Microsoft Operations Management Suite (OMS) hello의 B2B 통신을 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-103">Track B2B communication in hello Microsoft Operations Management Suite (OMS)</span></span>

<span data-ttu-id="c0b89-104">통합 계정을 통해 실행 중인 두 비즈니스 프로세스 또는 응용 프로그램 간의 B2B 통신을 설정한 후 해당 엔터티는 서로 메시지를 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-104">After you set up B2B communication between two running business processes or applications through your integration account, those entities can exchange messages with each other.</span></span> <span data-ttu-id="c0b89-105">toocheck 여부 이러한 메시지가 제대로 처리, AS2, X12, 추적할 수 있습니다 및 사용 하 여 EDIFACT 메시지 [Azure 로그 분석](../log-analytics/log-analytics-overview.md) hello에 [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-105">toocheck whether these messages are processed correctly, you can track AS2, X12, and EDIFACT messages with [Azure Log Analytics](../log-analytics/log-analytics-overview.md) in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="c0b89-106">예를 들어 메시지 추적에 대해 이러한 웹 기반 추적 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-106">For example, you can use these web-based tracking capabilities for tracking messages:</span></span>

* <span data-ttu-id="c0b89-107">메시지 수 및 상태</span><span class="sxs-lookup"><span data-stu-id="c0b89-107">Message count and status</span></span>
* <span data-ttu-id="c0b89-108">승인 상태</span><span class="sxs-lookup"><span data-stu-id="c0b89-108">Acknowledgments status</span></span>
* <span data-ttu-id="c0b89-109">승인된 메시지 상호 연결</span><span class="sxs-lookup"><span data-stu-id="c0b89-109">Correlate messages with acknowledgments</span></span>
* <span data-ttu-id="c0b89-110">실패에 대한 자세한 오류 설명</span><span class="sxs-lookup"><span data-stu-id="c0b89-110">Detailed error descriptions for failures</span></span>
* <span data-ttu-id="c0b89-111">검색 기능</span><span class="sxs-lookup"><span data-stu-id="c0b89-111">Search capabilities</span></span>

## <a name="requirements"></a><span data-ttu-id="c0b89-112">요구 사항</span><span class="sxs-lookup"><span data-stu-id="c0b89-112">Requirements</span></span>

* <span data-ttu-id="c0b89-113">진단 로깅과 함께 설정된 논리 앱.</span><span class="sxs-lookup"><span data-stu-id="c0b89-113">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="c0b89-114">자세한 내용은 [어떻게 toocreate 논리 앱](logic-apps-create-a-logic-app.md) 및 [어떻게 tooset 해당 논리 앱에 대 한 로깅을](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-114">Learn [how toocreate a logic app](logic-apps-create-a-logic-app.md) and [how tooset up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

* <span data-ttu-id="c0b89-115">모니터링 및 로깅을 사용하여 설정된 통합 계정.</span><span class="sxs-lookup"><span data-stu-id="c0b89-115">An integration account that's set up with monitoring and logging.</span></span> <span data-ttu-id="c0b89-116">자세한 [어떻게 toocreate 통합 계정](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) 및 [방법을 모니터링 해당 계정에 대 한 로깅을 켜고 tooset](../logic-apps/logic-apps-monitor-b2b-message.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-116">Learn [how toocreate an integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) and [how tooset up monitoring and logging for that account](../logic-apps/logic-apps-monitor-b2b-message.md).</span></span>

* <span data-ttu-id="c0b89-117">아직 없는 경우, [진단 데이터 tooLog 분석 게시](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) OMS에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-117">If you haven't already, [publish diagnostic data tooLog Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) in OMS.</span></span>

> [!NOTE]
> <span data-ttu-id="c0b89-118">Hello에 대 한 작업 영역 있어야 hello 이전 요구 사항을 충족 한 [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-118">After you've met hello previous requirements, you should have a workspace in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="c0b89-119">사용 해야 hello OMS에서이 프로그램 B2B 통신을 추적 하기 위한 동일한 OMS 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-119">You should use hello same OMS workspace for tracking your B2B communication in OMS.</span></span> 
>  
> <span data-ttu-id="c0b89-120">OMS 작업 영역에 없을 경우에 대해 배울 [어떻게 toocreate OMS 작업 영역](../log-analytics/log-analytics-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-120">If you don't have an OMS workspace, learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

## <a name="add-hello-logic-apps-b2b-solution-toohello-operations-management-suite-oms"></a><span data-ttu-id="c0b89-121">Hello 논리 앱 B2B 솔루션 toohello Operations Management Suite (OMS)를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-121">Add hello Logic Apps B2B solution toohello Operations Management Suite (OMS)</span></span>

<span data-ttu-id="c0b89-122">논리 앱에 대 한 B2B 메시지를 추적 하는 OMS toohave, hello를 추가 해야 **논리 앱 B2B** 솔루션 toohello OMS 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-122">toohave OMS track B2B messages for your logic app, you must add hello **Logic Apps B2B** solution toohello OMS portal.</span></span> <span data-ttu-id="c0b89-123">에 대 한 자세한 내용은 [솔루션 tooOMS 추가](../log-analytics/log-analytics-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-123">Learn more about [adding solutions tooOMS](../log-analytics/log-analytics-get-started.md).</span></span>

1. <span data-ttu-id="c0b89-124">Hello에 [Azure 포털](https://portal.azure.com), 선택 **더 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-124">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="c0b89-125">"로그 분석"에 대해 검색한 후 다음과 같이 **Log Analytics**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-125">Search for "log analytics", and then choose **Log Analytics** as shown here:</span></span>

   ![Log Analytics 찾기](media/logic-apps-track-b2b-messages-omsportal/browseloganalytics.png)

2. <span data-ttu-id="c0b89-127">**Log Analytics** 아래에서 OMS 작업 영역을 찾고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-127">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![OMS 작업 영역 선택](media/logic-apps-track-b2b-messages-omsportal/selectla.png)

3. <span data-ttu-id="c0b89-129">**관리** 아래에서 **OMS 포털**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-129">Under **Management**, choose **OMS Portal**.</span></span>

   ![OMS 포털 선택](media/logic-apps-track-b2b-messages-omsportal/omsportalpage.png)

4. <span data-ttu-id="c0b89-131">Hello OMS 홈 페이지를 연 후 선택 **솔루션 갤러리**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-131">After hello OMS home page opens, choose **Solutions Gallery**.</span></span>    

   ![솔루션 갤러리 선택](media/logic-apps-track-b2b-messages-omsportal/omshomepage1.png)

5. <span data-ttu-id="c0b89-133">**모든 솔루션** 아래에서 **Logic Apps B2B**를 찾고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-133">Under **All solutions**, find and choose **Logic Apps B2B**.</span></span>     

   ![Logic Apps B2B 선택](media/logic-apps-track-b2b-messages-omsportal/omshomepage2.png)

6. <span data-ttu-id="c0b89-135">**Logic Apps B2B** 아래에서 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-135">Under **Logic Apps B2B**, choose **Add**.</span></span>

   ![[추가] 선택](media/logic-apps-track-b2b-messages-omsportal/omshomepage3.png)

   <span data-ttu-id="c0b89-137">Hello OMS 홈 페이지에서 타일에 대 한 hello **논리 앱 B2B 메시지** 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-137">On hello OMS home page, hello tile for **Logic Apps B2B Messages** now appears.</span></span> 
   <span data-ttu-id="c0b89-138">이 타일 B2B 메시지를 처리할 경우 hello 메시지 수를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-138">This tile updates hello message count when your B2B messages are processed.</span></span>

   ![OMS 홈페이지, Logic Apps B2B 메시지 타일](media/logic-apps-track-b2b-messages-omsportal/omshomepage4.png)

<a name="message-status-details"></a>

## <a name="track-message-status-and-details-in-hello-operations-management-suite"></a><span data-ttu-id="c0b89-140">메시지 상태 및 hello Operations Management Suite에에서 대 한 세부 정보를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-140">Track message status and details in hello Operations Management Suite</span></span>

1. <span data-ttu-id="c0b89-141">B2B 메시지를 처리 한 후에 hello 상태 및 해당 메시지에 대 한 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-141">After your B2B messages are processed, you can view hello status and details for those messages.</span></span> <span data-ttu-id="c0b89-142">Hello OMS 홈 페이지에서 선택 hello **논리 앱 B2B 메시지** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-142">On hello OMS home page, choose hello **Logic Apps B2B Messages** tile.</span></span>

   ![업데이트된 메시지 수](media/logic-apps-track-b2b-messages-omsportal/omshomepage6.png)

   > [!NOTE]
   > <span data-ttu-id="c0b89-144">기본적으로 hello **논리 앱 B2B 메시지** 타일 하루에 따라 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-144">By default, hello **Logic Apps B2B Messages** tile shows data based on a single day.</span></span> <span data-ttu-id="c0b89-145">toochange hello 데이터 범위 tooa 다른 간격 hello hello OMS 페이지 위쪽에 hello 범위 컨트롤을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-145">toochange hello data scope tooa different interval, choose hello scope control at hello top of hello OMS page:</span></span>
   > 
   > ![데이터 범위 변경](media/logic-apps-track-b2b-messages-omsportal/change-interval.png)
   >

2. <span data-ttu-id="c0b89-147">Hello 메시지 상태 후 대시보드가 나타납니다 하루에 따라 데이터를 표시 하는 특정 메시지 유형에 대 한 자세한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-147">After hello message status dashboard appears, you can view more details for a specific message type, which shows data based on a single day.</span></span> <span data-ttu-id="c0b89-148">Hello 타일을 **AS2**, **X12**, 또는 **EDIFACT**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-148">Choose hello tile for **AS2**, **X12**, or **EDIFACT**.</span></span>

   ![메시지 상태 보기](media/logic-apps-track-b2b-messages-omsportal/omshomepage5.png)

   <span data-ttu-id="c0b89-150">선택한 타일에 대한 메시지 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-150">A list of messages appears for your chosen tile.</span></span> 
   <span data-ttu-id="c0b89-151">이러한 메시지 속성 설명을 볼 수 toolearn hello 속성 각 메시지 유형에 대 한 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="c0b89-151">toolearn more about hello properties for each message type, see these message property descriptions:</span></span>

   * [<span data-ttu-id="c0b89-152">AS2 메시지 속성</span><span class="sxs-lookup"><span data-stu-id="c0b89-152">AS2 message properties</span></span>](#as2-message-properties)
   * [<span data-ttu-id="c0b89-153">X12 메시지 속성</span><span class="sxs-lookup"><span data-stu-id="c0b89-153">X12 message properties</span></span>](#x12-message-properties)
   * [<span data-ttu-id="c0b89-154">EDIFACT 메시지 속성</span><span class="sxs-lookup"><span data-stu-id="c0b89-154">EDIFACT message properties</span></span>](#EDIFACT-message-properties)

   <span data-ttu-id="c0b89-155">예를 들어 AS2 메시지 목록은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-155">For example, here's what an AS2 message list might look like:</span></span>

   ![AS2 메시지 보기](media/logic-apps-track-b2b-messages-omsportal/as2messagelist.png)

3. <span data-ttu-id="c0b89-157">특정 메시지의 tooview 또는 내보내기 hello 입력 및 출력, 해당 메시지를 선택 하 고 선택 **다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-157">tooview or export hello inputs and outputs for specific messages, select those messages, and choose **Download**.</span></span> <span data-ttu-id="c0b89-158">메시지가 나타나면 hello.zip 파일 tooyour 로컬 컴퓨터를 저장 하 고 해당 파일을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-158">When you're prompted, save hello .zip file tooyour local computer, and then extract that file.</span></span> 

   <span data-ttu-id="c0b89-159">선택 된 각 메시지에 대 한 폴더를 포함 하는 hello 압축 푼된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-159">hello extracted folder includes a folder for each selected message.</span></span> 
   <span data-ttu-id="c0b89-160">승인 설정한 경우 hello 메시지 폴더는 또한 승인 세부 정보로 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-160">If you set up acknowledgements, hello message folder also includes files with acknowledgement details.</span></span> 
   <span data-ttu-id="c0b89-161">각 메시지 폴더에는 적어도 다음 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-161">Each message folder has at least these files:</span></span> 
   
   * <span data-ttu-id="c0b89-162">페이로드 및 출력 페이로드의 세부 정보를 입력 하는 hello로 읽을 파일</span><span class="sxs-lookup"><span data-stu-id="c0b89-162">Human-readable files with hello input payload and output payload details</span></span>
   * <span data-ttu-id="c0b89-163">Hello 입 / 출력을 사용 하 여 인코딩된 파일</span><span class="sxs-lookup"><span data-stu-id="c0b89-163">Encoded files with hello inputs and outputs</span></span>

   <span data-ttu-id="c0b89-164">각 메시지 유형에 대해 hello 폴더와 여기에 파일 이름 형식을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-164">For each message type, you can find hello folder and file name formats here:</span></span>

   * [<span data-ttu-id="c0b89-165">AS2 폴더 및 파일 이름 형식</span><span class="sxs-lookup"><span data-stu-id="c0b89-165">AS2 folder and file name formats</span></span>](#as2-folder-file-names)
   * [<span data-ttu-id="c0b89-166">X12 폴더 및 파일 이름 형식</span><span class="sxs-lookup"><span data-stu-id="c0b89-166">X12 folder and file name formats</span></span>](#x12-folder-file-names)
   * [<span data-ttu-id="c0b89-167">EDIFACT 폴더 및 파일 이름 형식</span><span class="sxs-lookup"><span data-stu-id="c0b89-167">EDIFACT folder and file name formats</span></span>](#edifact-folder-file-names)

   ![메시지 파일 다운로드](media/logic-apps-track-b2b-messages-omsportal/download-messages.png)

4. <span data-ttu-id="c0b89-169">tooview 동일 hello가 있는 모든 동작 ID를 hello에서 실행 **로그 검색** 페이지 hello 메시지 목록에서 메시지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-169">tooview all actions that have hello same run ID, on hello **Log Search** page, choose a message from hello message list.</span></span>

   <span data-ttu-id="c0b89-170">특정 결과에 대해 열 또는 검색별로 이러한 작업을 정렬할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-170">You can sort these actions by column, or search for specific results.</span></span>

   ![Hello 사용 하 여 작업 같은 실행 ID](media/logic-apps-track-b2b-messages-omsportal/logsearch.png)

   * <span data-ttu-id="c0b89-172">미리 작성 된 쿼리를 사용 하 여 toosearch 결과 선택 **즐겨찾기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-172">toosearch results with prebuilt queries, choose **Favorites**.</span></span>

   * <span data-ttu-id="c0b89-173">자세한 내용은 [toobuild 필터를 추가 하 여 쿼리 하는 방법을](logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-173">Learn [how toobuild queries by adding filters](logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md).</span></span> 
   <span data-ttu-id="c0b89-174">에 대 한 자세한 정보 또는 [로그 분석에서 toofind 데이터 로그를 검색 하는 방법](../log-analytics/log-analytics-log-searches.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-174">Or learn more about [how toofind data with log searches in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

   * <span data-ttu-id="c0b89-175">hello 열 및 값과 함께 업데이트 hello 쿼리 필터로 toouse 되도록 hello 검색 상자에 toochange 쿼리.</span><span class="sxs-lookup"><span data-stu-id="c0b89-175">toochange query in hello search box, update hello query with hello columns and values that you want toouse as filters.</span></span>

<a name="message-list-property-descriptions"></a>

## <a name="property-descriptions-and-name-formats-for-as2-x12-and-edifact-messages"></a><span data-ttu-id="c0b89-176">AS2, X12 및 EDIFACT 메시지에 대한 속성 설명 및 이름 형식</span><span class="sxs-lookup"><span data-stu-id="c0b89-176">Property descriptions and name formats for AS2, X12, and EDIFACT messages</span></span>

<span data-ttu-id="c0b89-177">각 메시지 유형에 대해 hello 속성 설명 및 다운로드 한 메시지 파일에 대 한 이름 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-177">For each message type, here are hello property descriptions and name formats for downloaded message files.</span></span>

<a name="as2-message-properties"></a>

### <a name="as2-message-property-descriptions"></a><span data-ttu-id="c0b89-178">AS2 메시지 속성 설명</span><span class="sxs-lookup"><span data-stu-id="c0b89-178">AS2 message property descriptions</span></span>

<span data-ttu-id="c0b89-179">다음은 각 AS2 메시지에 대 한 hello 속성 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-179">Here are hello property descriptions for each AS2 message.</span></span>

| <span data-ttu-id="c0b89-180">속성</span><span class="sxs-lookup"><span data-stu-id="c0b89-180">Property</span></span> | <span data-ttu-id="c0b89-181">설명</span><span class="sxs-lookup"><span data-stu-id="c0b89-181">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c0b89-182">보낸 사람</span><span class="sxs-lookup"><span data-stu-id="c0b89-182">Sender</span></span> | <span data-ttu-id="c0b89-183">지정 된 hello 게스트 파트너 **수신 설정**에 지정 된 hello 호스트 파트너 또는 **송신 설정** AS2 규약에 대 한</span><span class="sxs-lookup"><span data-stu-id="c0b89-183">hello guest partner specified in **Receive Settings**, or hello host partner specified in **Send Settings** for an AS2 agreement</span></span> |
| <span data-ttu-id="c0b89-184">받는 사람</span><span class="sxs-lookup"><span data-stu-id="c0b89-184">Receiver</span></span> | <span data-ttu-id="c0b89-185">지정 된 hello 호스트 파트너 **수신 설정**에 지정 된 hello 게스트 파트너 또는 **송신 설정** AS2 규약에 대 한</span><span class="sxs-lookup"><span data-stu-id="c0b89-185">hello host partner specified in **Receive Settings**, or hello guest partner specified in **Send Settings** for an AS2 agreement</span></span> |
| <span data-ttu-id="c0b89-186">논리 앱</span><span class="sxs-lookup"><span data-stu-id="c0b89-186">Logic App</span></span> | <span data-ttu-id="c0b89-187">hello AS2 작업을 설정 하는 hello 논리 앱</span><span class="sxs-lookup"><span data-stu-id="c0b89-187">hello logic app where hello AS2 actions are set up</span></span> |
| <span data-ttu-id="c0b89-188">가동 상태</span><span class="sxs-lookup"><span data-stu-id="c0b89-188">Status</span></span> | <span data-ttu-id="c0b89-189">hello AS2 메시지 상태</span><span class="sxs-lookup"><span data-stu-id="c0b89-189">hello AS2 message status</span></span> <br><span data-ttu-id="c0b89-190">성공 = 유효한 AS2 메시지를 받거나 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-190">Success = Received or sent a valid AS2 message.</span></span> <span data-ttu-id="c0b89-191">MDN이 설정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-191">No MDN is set up.</span></span> <br><span data-ttu-id="c0b89-192">성공 = 유효한 AS2 메시지를 받거나 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-192">Success = Received or sent a valid AS2 message.</span></span> <span data-ttu-id="c0b89-193">MDN이 설정 및 수신됩니다. 또는 MDN이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-193">MDN is set up and received, or MDN is sent.</span></span> <br><span data-ttu-id="c0b89-194">실패 = 유효하지 않은 AS2 메시지를 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-194">Failed = Received an invalid AS2 message.</span></span> <span data-ttu-id="c0b89-195">MDN이 설정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-195">No MDN is set up.</span></span> <br><span data-ttu-id="c0b89-196">보류 중 = 유효한 AS2 메시지를 받거나 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-196">Pending = Received or sent a valid AS2 message.</span></span> <span data-ttu-id="c0b89-197">MDN이 설정되었고 MDN을 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-197">MDN is set up, and MDN is expected.</span></span> |
| <span data-ttu-id="c0b89-198">Ack</span><span class="sxs-lookup"><span data-stu-id="c0b89-198">Ack</span></span> | <span data-ttu-id="c0b89-199">hello MDN 메시지 상태</span><span class="sxs-lookup"><span data-stu-id="c0b89-199">hello MDN message status</span></span> <br><span data-ttu-id="c0b89-200">수락됨 = 양의 MDN을 받거나 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-200">Accepted = Received or sent a positive MDN.</span></span> <br><span data-ttu-id="c0b89-201">보류 중인 = MDN을 보내거나 tooreceive 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-201">Pending = Waiting tooreceive or send an MDN.</span></span> <br><span data-ttu-id="c0b89-202">거부됨 = 음의 MDN을 받거나 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-202">Rejected = Received or sent a negative MDN.</span></span> <br><span data-ttu-id="c0b89-203">않아도 = MDN hello 계약에 설정 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-203">Not Required = MDN is not set up in hello agreement.</span></span> |
| <span data-ttu-id="c0b89-204">방향</span><span class="sxs-lookup"><span data-stu-id="c0b89-204">Direction</span></span> | <span data-ttu-id="c0b89-205">hello AS2 메시지 방향</span><span class="sxs-lookup"><span data-stu-id="c0b89-205">hello AS2 message direction</span></span> |
| <span data-ttu-id="c0b89-206">상관관계 ID</span><span class="sxs-lookup"><span data-stu-id="c0b89-206">Correlation ID</span></span> | <span data-ttu-id="c0b89-207">모든 hello 트리거 및 논리 앱의 동작을 상호 연결 하는 hello ID</span><span class="sxs-lookup"><span data-stu-id="c0b89-207">hello ID that correlates all hello triggers and actions in a logic app</span></span> |
| <span data-ttu-id="c0b89-208">메시지 ID</span><span class="sxs-lookup"><span data-stu-id="c0b89-208">Message ID</span></span> | <span data-ttu-id="c0b89-209">hello AS2 메시지 헤더에서 hello AS2 메시지 ID</span><span class="sxs-lookup"><span data-stu-id="c0b89-209">hello AS2 message ID from hello AS2 message headers</span></span> |
| <span data-ttu-id="c0b89-210">Timestamp</span><span class="sxs-lookup"><span data-stu-id="c0b89-210">Timestamp</span></span> | <span data-ttu-id="c0b89-211">hello 시간 hello AS2 동작 hello 메시지를 처리 하는 시기</span><span class="sxs-lookup"><span data-stu-id="c0b89-211">hello time when hello AS2 action processed hello message</span></span> |
|          |             |

<a name="as2-folder-file-names"></a>

### <a name="as2-name-formats-for-downloaded-message-files"></a><span data-ttu-id="c0b89-212">다운로드한 메시지 파일에 대한 AS2 이름 형식</span><span class="sxs-lookup"><span data-stu-id="c0b89-212">AS2 name formats for downloaded message files</span></span>

<span data-ttu-id="c0b89-213">다음은 각 다운로드 된 AS2 메시지 폴더 및 파일에 대 한 hello 이름 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-213">Here are hello name formats for each downloaded AS2 message folder and files.</span></span>

| <span data-ttu-id="c0b89-214">폴더 또는 파일</span><span class="sxs-lookup"><span data-stu-id="c0b89-214">Folder or file</span></span> | <span data-ttu-id="c0b89-215">이름 형식</span><span class="sxs-lookup"><span data-stu-id="c0b89-215">Name format</span></span> |
| :------------- | :---------- |
| <span data-ttu-id="c0b89-216">메시지 폴더</span><span class="sxs-lookup"><span data-stu-id="c0b89-216">Message folder</span></span> | <span data-ttu-id="c0b89-217">[보낸 사람]\_[받는 사람]\_AS2\_[상관 관계-ID]\_[메시지-ID]\_[타임스탬프]</span><span class="sxs-lookup"><span data-stu-id="c0b89-217">[sender]\_[receiver]\_AS2\_[correlation-ID]\_[message-ID]\_[timestamp]</span></span> |
| <span data-ttu-id="c0b89-218">입력, 출력 및 설정한 경우 승인 파일</span><span class="sxs-lookup"><span data-stu-id="c0b89-218">Input, output, and if set up, acknowledgement files</span></span> | <span data-ttu-id="c0b89-219">**입력 페이로드**: [보낸 사람]\_[받는 사람]\_AS2\_[상관 관계-ID]\_입력_페이로드.txt</span><span class="sxs-lookup"><span data-stu-id="c0b89-219">**Input payload**: [sender]\_[receiver]\_AS2\_[correlation-ID]\_input_payload.txt</span></span> </p><span data-ttu-id="c0b89-220">**출력 페이로드**: [보낸 사람]\_[받는 사람]\_AS2\_[상관 관계-ID]\_출력\_페이로드.txt</span><span class="sxs-lookup"><span data-stu-id="c0b89-220">**Output payload**: [sender]\_[receiver]\_AS2\_[correlation-ID]\_output\_payload.txt</span></span> </p></p><span data-ttu-id="c0b89-221">**입력**: [보낸 사람]\_[받는 사람]\_AS2\_[상관 관계-ID]\_입력.txt</span><span class="sxs-lookup"><span data-stu-id="c0b89-221">**Inputs**: [sender]\_[receiver]\_AS2\_[correlation-ID]\_inputs.txt</span></span> </p></p><span data-ttu-id="c0b89-222">**출력**: [보낸 사람]\_[받는 사람]\_AS2\_[상관 관계-ID]\_출력.txt</span><span class="sxs-lookup"><span data-stu-id="c0b89-222">**Outputs**: [sender]\_[receiver]\_AS2\_[correlation-ID]\_outputs.txt</span></span> |
|          |             |

<a name="x12-message-properties"></a>

### <a name="x12-message-property-descriptions"></a><span data-ttu-id="c0b89-223">X12 메시지 속성 설명</span><span class="sxs-lookup"><span data-stu-id="c0b89-223">X12 message property descriptions</span></span>

<span data-ttu-id="c0b89-224">다음은 hello 속성에 대 한 각 X12 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-224">Here are hello property descriptions for each X12 message.</span></span>

| <span data-ttu-id="c0b89-225">속성</span><span class="sxs-lookup"><span data-stu-id="c0b89-225">Property</span></span> | <span data-ttu-id="c0b89-226">설명</span><span class="sxs-lookup"><span data-stu-id="c0b89-226">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c0b89-227">보낸 사람</span><span class="sxs-lookup"><span data-stu-id="c0b89-227">Sender</span></span> | <span data-ttu-id="c0b89-228">지정 된 hello 게스트 파트너 **수신 설정**에 지정 된 hello 호스트 파트너 또는 **송신 설정** x12 계약</span><span class="sxs-lookup"><span data-stu-id="c0b89-228">hello guest partner specified in **Receive Settings**, or hello host partner specified in **Send Settings** for an X12 agreement</span></span> |
| <span data-ttu-id="c0b89-229">받는 사람</span><span class="sxs-lookup"><span data-stu-id="c0b89-229">Receiver</span></span> | <span data-ttu-id="c0b89-230">지정 된 hello 호스트 파트너 **수신 설정**, 또는 hello 게스트 파트너에 지정 된 **송신 설정** x12 계약</span><span class="sxs-lookup"><span data-stu-id="c0b89-230">hello host partner specified in **Receive Settings**, or hello guest partner specified in **Send Settings** for an X12 agreement</span></span> |
| <span data-ttu-id="c0b89-231">논리 앱</span><span class="sxs-lookup"><span data-stu-id="c0b89-231">Logic App</span></span> | <span data-ttu-id="c0b89-232">hello X12 작업을 설정 하는 hello 논리 앱</span><span class="sxs-lookup"><span data-stu-id="c0b89-232">hello logic app where hello X12 actions are set up</span></span> |
| <span data-ttu-id="c0b89-233">가동 상태</span><span class="sxs-lookup"><span data-stu-id="c0b89-233">Status</span></span> | <span data-ttu-id="c0b89-234">hello X12 메시지 상태</span><span class="sxs-lookup"><span data-stu-id="c0b89-234">hello X12 message status</span></span> <br><span data-ttu-id="c0b89-235">성공 = 유효한 X12 메시지를 받거나 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-235">Success = Received or sent a valid X12 message.</span></span> <span data-ttu-id="c0b89-236">기능 Ack가 설정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-236">No functional ack is set up.</span></span> <br><span data-ttu-id="c0b89-237">성공 = 유효한 X12 메시지를 받거나 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-237">Success = Received or sent a valid X12 message.</span></span> <span data-ttu-id="c0b89-238">기능 Ack가 설정되고 수신되었거나 기능 Ack가 전송되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-238">Functional ack is set up and received, or a functional ack is sent.</span></span> <br><span data-ttu-id="c0b89-239">실패 = 유효하지 않은 X12 메시지를 받거나 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-239">Failed = Received or sent an invalid X12 message.</span></span> <br><span data-ttu-id="c0b89-240">보류 중 = 유효한 X12 메시지를 받거나 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-240">Pending = Received or sent a valid X12 message.</span></span> <span data-ttu-id="c0b89-241">기능 Ack가 설정되었고 기능 Ack를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-241">Functional ack is set up, and a functional ack is expected.</span></span> |
| <span data-ttu-id="c0b89-242">Ack</span><span class="sxs-lookup"><span data-stu-id="c0b89-242">Ack</span></span> | <span data-ttu-id="c0b89-243">기능 Ack(997) 상태</span><span class="sxs-lookup"><span data-stu-id="c0b89-243">Functional Ack (997) status</span></span> <br><span data-ttu-id="c0b89-244">수락됨 = 양의 기능 Ack를 받거나 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-244">Accepted = Received or sent a positive functional ack.</span></span> <br><span data-ttu-id="c0b89-245">거부됨 = 음의 기능 Ack를 받거나 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-245">Rejected = Received or sent a negative functional ack.</span></span> <br><span data-ttu-id="c0b89-246">보류 중 = 기능 Ack를 기다렸지만 받지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-246">Pending = Expecting a functional ack but not received.</span></span> <br><span data-ttu-id="c0b89-247">보류 = 기능 ack 생성 되지만 toopartner를 보낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-247">Pending = Generated a functional ack but can't send toopartner.</span></span> <br><span data-ttu-id="c0b89-248">필요하지 않음 = 기능 Ack가 설정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-248">Not Required = Functional ack is not set up.</span></span> |
| <span data-ttu-id="c0b89-249">방향</span><span class="sxs-lookup"><span data-stu-id="c0b89-249">Direction</span></span> | <span data-ttu-id="c0b89-250">hello X12 메시지 방향</span><span class="sxs-lookup"><span data-stu-id="c0b89-250">hello X12 message direction</span></span> |
| <span data-ttu-id="c0b89-251">상관관계 ID</span><span class="sxs-lookup"><span data-stu-id="c0b89-251">Correlation ID</span></span> | <span data-ttu-id="c0b89-252">모든 hello 트리거 및 논리 앱의 동작을 상호 연결 하는 hello ID</span><span class="sxs-lookup"><span data-stu-id="c0b89-252">hello ID that correlates all hello triggers and actions in a logic app</span></span> |
| <span data-ttu-id="c0b89-253">메시지 유형</span><span class="sxs-lookup"><span data-stu-id="c0b89-253">Msg type</span></span> | <span data-ttu-id="c0b89-254">hello EDI X 12 메시지 유형</span><span class="sxs-lookup"><span data-stu-id="c0b89-254">hello EDI X12 message type</span></span> |
| <span data-ttu-id="c0b89-255">ICN</span><span class="sxs-lookup"><span data-stu-id="c0b89-255">ICN</span></span> | <span data-ttu-id="c0b89-256">hello X12 메시지에 대 한 hello 교환 컨트롤 번호</span><span class="sxs-lookup"><span data-stu-id="c0b89-256">hello Interchange Control Number for hello X12 message</span></span> |
| <span data-ttu-id="c0b89-257">TSCN</span><span class="sxs-lookup"><span data-stu-id="c0b89-257">TSCN</span></span> | <span data-ttu-id="c0b89-258">hello X12 메시지에 대 한 hello 트랜잭션 집합 컨트롤 번호</span><span class="sxs-lookup"><span data-stu-id="c0b89-258">hello Transaction Set Control Number for hello X12 message</span></span> |
| <span data-ttu-id="c0b89-259">Timestamp</span><span class="sxs-lookup"><span data-stu-id="c0b89-259">Timestamp</span></span> | <span data-ttu-id="c0b89-260">hello 시간 hello X12 동작 hello 메시지를 처리 하는 시간</span><span class="sxs-lookup"><span data-stu-id="c0b89-260">hello time when hello X12 action processed hello message</span></span> |
|          |             |

<a name="x12-folder-file-names"></a>

### <a name="x12-name-formats-for-downloaded-message-files"></a><span data-ttu-id="c0b89-261">다운로드한 메시지 파일에 대한 X12 이름 형식</span><span class="sxs-lookup"><span data-stu-id="c0b89-261">X12 name formats for downloaded message files</span></span>

<span data-ttu-id="c0b89-262">X12 각 다운로드에 대 한 hello 이름 형식을 다음은 메시지 폴더 및 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-262">Here are hello name formats for each downloaded X12 message folder and files.</span></span>

| <span data-ttu-id="c0b89-263">폴더 또는 파일</span><span class="sxs-lookup"><span data-stu-id="c0b89-263">Folder or file</span></span> | <span data-ttu-id="c0b89-264">이름 형식</span><span class="sxs-lookup"><span data-stu-id="c0b89-264">Name format</span></span> |
| :------------- | :---------- |
| <span data-ttu-id="c0b89-265">메시지 폴더</span><span class="sxs-lookup"><span data-stu-id="c0b89-265">Message folder</span></span> | <span data-ttu-id="c0b89-266">[보낸 사람]\_[받는 사람]\_X12\_[교환-컨트롤-번호]\_[글로벌-컨트롤-번호]\_[트랜잭션-집합-컨트롤-번호]\_[타임스탬프]</span><span class="sxs-lookup"><span data-stu-id="c0b89-266">[sender]\_[receiver]\_X12\_[interchange-control-number]\_[global-control-number]\_[transaction-set-control-number]\_[timestamp]</span></span> |
| <span data-ttu-id="c0b89-267">입력, 출력 및 설정한 경우 승인 파일</span><span class="sxs-lookup"><span data-stu-id="c0b89-267">Input, output, and if set up, acknowledgement files</span></span> | <span data-ttu-id="c0b89-268">**입력 페이로드**: [보낸 사람]\_[받는 사람]\_X12\_[교환-컨트롤-번호]\_입력_페이로드.txt</span><span class="sxs-lookup"><span data-stu-id="c0b89-268">**Input payload**: [sender]\_[receiver]\_X12\_[interchange-control-number]\_input_payload.txt</span></span> </p><span data-ttu-id="c0b89-269">**출력 페이로드**: [보낸 사람]\_[받는 사람]\_X12\_[교환-컨트롤-번호]\_출력\_페이로드.txt</span><span class="sxs-lookup"><span data-stu-id="c0b89-269">**Output payload**: [sender]\_[receiver]\_X12\_[interchange-control-number]\_output\_payload.txt</span></span> </p></p><span data-ttu-id="c0b89-270">**입력**: [보낸 사람]\_[받는 사람]\_X12\_[교환-컨트롤-번호]\_입력.txt</span><span class="sxs-lookup"><span data-stu-id="c0b89-270">**Inputs**: [sender]\_[receiver]\_X12\_[interchange-control-number]\_inputs.txt</span></span> </p></p><span data-ttu-id="c0b89-271">**출력**: [보낸 사람]\_[받는 사람]\_X12\_[교환-컨트롤-번호]\_출력.txt</span><span class="sxs-lookup"><span data-stu-id="c0b89-271">**Outputs**: [sender]\_[receiver]\_X12\_[interchange-control-number]\_outputs.txt</span></span> |
|          |             |

<a name="EDIFACT-message-properties"></a>

### <a name="edifact-message-property-descriptions"></a><span data-ttu-id="c0b89-272">EDIFACT 메시지 속성 설명</span><span class="sxs-lookup"><span data-stu-id="c0b89-272">EDIFACT message property descriptions</span></span>

<span data-ttu-id="c0b89-273">다음은 각 EDIFACT 메시지에 대 한 hello 속성 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-273">Here are hello property descriptions for each EDIFACT message.</span></span>

| <span data-ttu-id="c0b89-274">속성</span><span class="sxs-lookup"><span data-stu-id="c0b89-274">Property</span></span> | <span data-ttu-id="c0b89-275">설명</span><span class="sxs-lookup"><span data-stu-id="c0b89-275">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c0b89-276">보낸 사람</span><span class="sxs-lookup"><span data-stu-id="c0b89-276">Sender</span></span> | <span data-ttu-id="c0b89-277">지정 된 hello 게스트 파트너 **수신 설정**에 지정 된 hello 호스트 파트너 또는 **송신 설정** EDIFACT 규약에 대 한</span><span class="sxs-lookup"><span data-stu-id="c0b89-277">hello guest partner specified in **Receive Settings**, or hello host partner specified in **Send Settings** for an EDIFACT agreement</span></span> |
| <span data-ttu-id="c0b89-278">받는 사람</span><span class="sxs-lookup"><span data-stu-id="c0b89-278">Receiver</span></span> | <span data-ttu-id="c0b89-279">지정 된 hello 호스트 파트너 **수신 설정**에 지정 된 hello 게스트 파트너 또는 **송신 설정** EDIFACT 규약에 대 한</span><span class="sxs-lookup"><span data-stu-id="c0b89-279">hello host partner specified in **Receive Settings**, or hello guest partner specified in **Send Settings** for an EDIFACT agreement</span></span> |
| <span data-ttu-id="c0b89-280">논리 앱</span><span class="sxs-lookup"><span data-stu-id="c0b89-280">Logic App</span></span> | <span data-ttu-id="c0b89-281">hello EDIFACT 작업을 설정 하는 hello 논리 앱</span><span class="sxs-lookup"><span data-stu-id="c0b89-281">hello logic app where hello EDIFACT actions are set up</span></span> |
| <span data-ttu-id="c0b89-282">가동 상태</span><span class="sxs-lookup"><span data-stu-id="c0b89-282">Status</span></span> | <span data-ttu-id="c0b89-283">hello EDIFACT 메시지 상태</span><span class="sxs-lookup"><span data-stu-id="c0b89-283">hello EDIFACT message status</span></span> <br><span data-ttu-id="c0b89-284">성공 = 유효한 EDIFACT 메시지를 받거나 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-284">Success = Received or sent a valid EDIFACT message.</span></span> <span data-ttu-id="c0b89-285">기능 Ack가 설정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-285">No functional ack is set up.</span></span> <br><span data-ttu-id="c0b89-286">성공 = 유효한 EDIFACT 메시지를 받거나 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-286">Success = Received or sent a valid EDIFACT message.</span></span> <span data-ttu-id="c0b89-287">기능 Ack가 설정되고 수신되었거나 기능 Ack가 전송되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-287">Functional ack is set up and received, or a functional ack is sent.</span></span> <br><span data-ttu-id="c0b89-288">실패 = 유효하지 않은 EDIFACT 메시지를 받거나 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-288">Failed = Received or sent an invalid EDIFACT message</span></span> <br><span data-ttu-id="c0b89-289">보류 중 = 유효한 EDIFACT 메시지를 받거나 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-289">Pending = Received or sent a valid EDIFACT message.</span></span> <span data-ttu-id="c0b89-290">기능 Ack가 설정되었고 기능 Ack를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-290">Functional ack is set up, and a functional ack is expected.</span></span> |
| <span data-ttu-id="c0b89-291">Ack</span><span class="sxs-lookup"><span data-stu-id="c0b89-291">Ack</span></span> | <span data-ttu-id="c0b89-292">기능 Ack(997) 상태</span><span class="sxs-lookup"><span data-stu-id="c0b89-292">Functional Ack (997) status</span></span> <br><span data-ttu-id="c0b89-293">수락됨 = 양의 기능 Ack를 받거나 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-293">Accepted = Received or sent a positive functional ack.</span></span> <br><span data-ttu-id="c0b89-294">거부됨 = 음의 기능 Ack를 받거나 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-294">Rejected = Received or sent a negative functional ack.</span></span> <br><span data-ttu-id="c0b89-295">보류 중 = 기능 Ack를 기다렸지만 받지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-295">Pending = Expecting a functional ack but not received.</span></span> <br><span data-ttu-id="c0b89-296">보류 = 기능 ack 생성 되지만 toopartner를 보낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-296">Pending = Generated a functional ack but can't send toopartner.</span></span> <br><span data-ttu-id="c0b89-297">필요하지 않음 = 기능 Ack가 설정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-297">Not Required = Functional Ack is not set up.</span></span> |
| <span data-ttu-id="c0b89-298">방향</span><span class="sxs-lookup"><span data-stu-id="c0b89-298">Direction</span></span> | <span data-ttu-id="c0b89-299">hello EDIFACT 메시지 방향</span><span class="sxs-lookup"><span data-stu-id="c0b89-299">hello EDIFACT message direction</span></span> |
| <span data-ttu-id="c0b89-300">상관관계 ID</span><span class="sxs-lookup"><span data-stu-id="c0b89-300">Correlation ID</span></span> | <span data-ttu-id="c0b89-301">모든 hello 트리거 및 논리 앱의 동작을 상호 연결 하는 hello ID</span><span class="sxs-lookup"><span data-stu-id="c0b89-301">hello ID that correlates all hello triggers and actions in a logic app</span></span> |
| <span data-ttu-id="c0b89-302">메시지 유형</span><span class="sxs-lookup"><span data-stu-id="c0b89-302">Msg type</span></span> | <span data-ttu-id="c0b89-303">hello EDIFACT 메시지 유형</span><span class="sxs-lookup"><span data-stu-id="c0b89-303">hello EDIFACT message type</span></span> |
| <span data-ttu-id="c0b89-304">ICN</span><span class="sxs-lookup"><span data-stu-id="c0b89-304">ICN</span></span> | <span data-ttu-id="c0b89-305">hello EDIFACT 메시지에 대 한 hello 교환 컨트롤 번호</span><span class="sxs-lookup"><span data-stu-id="c0b89-305">hello Interchange Control Number for hello EDIFACT message</span></span> |
| <span data-ttu-id="c0b89-306">TSCN</span><span class="sxs-lookup"><span data-stu-id="c0b89-306">TSCN</span></span> | <span data-ttu-id="c0b89-307">hello EDIFACT 메시지에 대 한 hello 트랜잭션 집합 컨트롤 번호</span><span class="sxs-lookup"><span data-stu-id="c0b89-307">hello Transaction Set Control Number for hello EDIFACT message</span></span> |
| <span data-ttu-id="c0b89-308">Timestamp</span><span class="sxs-lookup"><span data-stu-id="c0b89-308">Timestamp</span></span> | <span data-ttu-id="c0b89-309">hello 시간 hello EDIFACT 동작 hello 메시지를 처리 하는 시기</span><span class="sxs-lookup"><span data-stu-id="c0b89-309">hello time when hello EDIFACT action processed hello message</span></span> |
|          |               |

<a name="edifact-folder-file-names"></a>

### <a name="edifact-name-formats-for-downloaded-message-files"></a><span data-ttu-id="c0b89-310">다운로드한 메시지 파일에 대한 EDIFACT 이름 형식</span><span class="sxs-lookup"><span data-stu-id="c0b89-310">EDIFACT name formats for downloaded message files</span></span>

<span data-ttu-id="c0b89-311">다음은 각 다운로드 한 EDIFACT 메시지 폴더 및 파일에 대 한 hello 이름 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c0b89-311">Here are hello name formats for each downloaded EDIFACT message folder and files.</span></span>

| <span data-ttu-id="c0b89-312">폴더 또는 파일</span><span class="sxs-lookup"><span data-stu-id="c0b89-312">Folder or file</span></span> | <span data-ttu-id="c0b89-313">이름 형식</span><span class="sxs-lookup"><span data-stu-id="c0b89-313">Name format</span></span> |
| :------------- | :---------- |
| <span data-ttu-id="c0b89-314">메시지 폴더</span><span class="sxs-lookup"><span data-stu-id="c0b89-314">Message folder</span></span> | <span data-ttu-id="c0b89-315">[보낸 사람]\_[받는 사람]\_EDIFACT\_[교환-컨트롤-번호]\_[글로벌-컨트롤-번호]\_[트랜잭션-집합-컨트롤-번호]\_[타임스탬프]</span><span class="sxs-lookup"><span data-stu-id="c0b89-315">[sender]\_[receiver]\_EDIFACT\_[interchange-control-number]\_[global-control-number]\_[transaction-set-control-number]\_[timestamp]</span></span> |
| <span data-ttu-id="c0b89-316">입력, 출력 및 설정한 경우 승인 파일</span><span class="sxs-lookup"><span data-stu-id="c0b89-316">Input, output, and if set up, acknowledgement files</span></span> | <span data-ttu-id="c0b89-317">**입력 페이로드**: [보낸 사람]\_[받는 사람]\_EDIFACT\_[교환-컨트롤-번호]\_입력_페이로드.txt</span><span class="sxs-lookup"><span data-stu-id="c0b89-317">**Input payload**: [sender]\_[receiver]\_EDIFACT\_[interchange-control-number]\_input_payload.txt</span></span> </p><span data-ttu-id="c0b89-318">**출력 페이로드**: [보낸 사람]\_[받는 사람]\_EDIFACT\_[교환-컨트롤-번호]\_출력\_페이로드.txt</span><span class="sxs-lookup"><span data-stu-id="c0b89-318">**Output payload**: [sender]\_[receiver]\_EDIFACT\_[interchange-control-number]\_output\_payload.txt</span></span> </p></p><span data-ttu-id="c0b89-319">**입력**: [보낸 사람]\_[받는 사람]\_EDIFACT\_[교환-컨트롤-번호]\_입력.txt</span><span class="sxs-lookup"><span data-stu-id="c0b89-319">**Inputs**: [sender]\_[receiver]\_EDIFACT\_[interchange-control-number]\_inputs.txt</span></span> </p></p><span data-ttu-id="c0b89-320">**출력**: [보낸 사람]\_[받는 사람]\_EDIFACT\_[교환-컨트롤-번호]\_출력.txt</span><span class="sxs-lookup"><span data-stu-id="c0b89-320">**Outputs**: [sender]\_[receiver]\_EDIFACT\_[interchange-control-number]\_outputs.txt</span></span> |
|          |             |

## <a name="next-steps"></a><span data-ttu-id="c0b89-321">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c0b89-321">Next steps</span></span>

* [<span data-ttu-id="c0b89-322">Operations Management Suite에서 B2B 메시지에 대한 쿼리</span><span class="sxs-lookup"><span data-stu-id="c0b89-322">Query for B2B messages in Operations Management Suite</span></span>](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md)
* [<span data-ttu-id="c0b89-323">AS2 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="c0b89-323">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="c0b89-324">X12 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="c0b89-324">X12 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="c0b89-325">사용자 지정 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="c0b89-325">Custom tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)