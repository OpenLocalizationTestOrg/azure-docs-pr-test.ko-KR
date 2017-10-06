---
title: "OMS에서 서비스 관리 커넥터 aaaIT | Microsoft Docs"
description: "Hello IT 서비스 관리 커넥터 toocentrally 모니터를 사용 하 여 OMS에서는 hello ITSM 작업 항목을 관리 하며 모든 문제를 신속 하 게 해결 합니다."
services: log-analytics
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 0b1414d9-b0a7-4e4e-a652-d3a6ff1118c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: v-jysur
ms.openlocfilehash: 33ed5d432591b836eb41ba982c66c96f22879444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a><span data-ttu-id="444f2-103">IT Service Management Connector(미리 보기)를 사용하여 ITSM 작업 항목을 중앙에서 관리</span><span class="sxs-lookup"><span data-stu-id="444f2-103">Centrally manage ITSM work items using IT Service Management Connector (Preview)</span></span>

![IT Service Management Connector 기호](./media/log-analytics-itsmc/itsmc-symbol.png)

<span data-ttu-id="444f2-105">OMS 로그 분석 toocentrally 모니터에 hello IT 서비스 관리 (ITSMC) 커넥터를 사용 하 고 ITSM 제품/서비스 간에 작업 항목을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-105">You can use hello IT Service Management Connector (ITSMC) in OMS Log Analytics toocentrally monitor and manage work items across your ITSM products/services.</span></span>

<span data-ttu-id="444f2-106">hello IT 서비스 관리 커넥터 OMS 로그 분석 기존 IT 서비스 관리 (ITSM) 제품 및 서비스를 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-106">hello IT Service Management Connector integrates your existing IT Service Management (ITSM) products and services with OMS Log Analytics.</span></span>  <span data-ttu-id="444f2-107">hello 솔루션 ITSM 제품/서비스와의 양방향 통합, OMS 사용자 옵션 toocreate 인시던트, 경고 또는 이벤트 ITSM 솔루션에서 제공 하는 경우 hello 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-107">hello solution has bidirectional integration with ITSM products/services, where it provides hello OMS users an option toocreate incidents, alerts, or events in ITSM solution.</span></span> <span data-ttu-id="444f2-108">인시던트, 등의 데이터 가져오기도 수행 하는 hello 커넥터 및 OMS 로그 분석에 ITSM 솔루션에서 변경 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-108">hello connector also  imports data such as incidents, and change requests from ITSM solution into OMS Log Analytics.</span></span>

<span data-ttu-id="444f2-109">IT Service Management Connector를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-109">With IT Service Management Connector, you can:</span></span>

  - <span data-ttu-id="444f2-110">조직에서 사용되는 ITSM 제품/서비스에 대한 작업 항목을 중앙에서 모니터링 및 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-110">Centrally monitor and manage work items for ITSM products/services used across your organization.</span></span>
  - <span data-ttu-id="444f2-111">OMS 경고 및 로그 검색을 통해 ITSM에서 ITSM 작업 항목(예: 경고, 이벤트, 인시던트)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-111">Create ITSM work items (like alert, event, incident) in ITSM from OMS alerts and through log search.</span></span>
  - <span data-ttu-id="444f2-112">ITSM 솔루션에서 인시던트 및 변경 요청을 읽고, Log Analytics 작업 영역에서 관련 로그 데이터와의 상관 관계를 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-112">Read incidents and change requests from your ITSM solution and correlate with relevant log data in Log Analytics workspace.</span></span>
  - <span data-ttu-id="444f2-113">예기치 않은 및 비정상적인 이벤트를 찾아 hello 최종 사용자가 호출 하 고 toohello 기술 지원팀 보고 하기 전에 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-113">Find any unexpected and unusual events and resolve them, even before hello end users call and report them toohello helpdesk.</span></span>
  - <span data-ttu-id="444f2-114">작업 항목 데이터를 Log Analytics로 가져오고 KPI(핵심 성과 지표) 보고서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-114">Import work items data into Log Analytics and create key performance indicator (KPI) reports.</span></span>  <span data-ttu-id="444f2-115">이러한 보고서를 사용하여 중요한 일부 항목을 식별하고 평가한 후 맬웨어 평가와 같은 조치를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-115">Using these reports, you can identify, assess and act on several important items such as malware assessment.</span></span>
  - <span data-ttu-id="444f2-116">엄선된 대시보드를 통해 인시던트, 변경 요청 및 영향 받은 시스템에 대한 심층 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-116">View curated dashboards for deeper insights on incidents, change requests and impacted systems.</span></span>
  - <span data-ttu-id="444f2-117">Hello 로그 분석 작업 영역에서 다른 관리 솔루션으로 상호 연관 시켜 더 빠르게 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-117">Troubleshoot faster by correlating with other management solutions in hello Log Analytics workspace.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="444f2-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="444f2-118">Prerequisites</span></span>

<span data-ttu-id="444f2-119">tooimport hello ITSM 작업 항목 OMS 로그 분석에 hello 솔루션 hello 작업 항목을 가져올 있는 hello OMS의에서 IT 서비스 관리 커넥터 hello 및 hello IT SM 제품/서비스 간의 연결이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-119">tooimport hello ITSM work items into OMS Log Analytics, hello solution requires a connection between hello IT Service Management Connector in hello OMS and hello IT SM product/service from which you import hello work items.</span></span>


## <a name="configuration"></a><span data-ttu-id="444f2-120">구성</span><span class="sxs-lookup"><span data-stu-id="444f2-120">Configuration</span></span>

<span data-ttu-id="444f2-121">에 설명 된 hello 프로세스를 사용 하 여 IT 서비스 관리 커넥터 솔루션 tooyour OMS 작업 공간에 추가 hello [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-121">Add hello IT Service Management Connector solution tooyour OMS work space, using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

<span data-ttu-id="444f2-122">IT 서비스 관리 커넥터 hello 솔루션 갤러리에 나와 있는 것 처럼 타일:</span><span class="sxs-lookup"><span data-stu-id="444f2-122">IT Service Management Connector tile as you see in hello Solutions gallery:</span></span>

![커넥터 타일](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

<span data-ttu-id="444f2-124">성공적으로 추가 후 나타납니다에서 IT 서비스 관리 커넥터 hello **OMS** > **설정** > **연결 된 원본입니다.**</span><span class="sxs-lookup"><span data-stu-id="444f2-124">After successful addition, you will see hello IT Service Management Connector under **OMS** > **Settings** > **Connected Sources.**</span></span>

![ITSMC가 연결되어 있습니다.](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> <span data-ttu-id="444f2-126">Hello IT 서비스 관리 커넥터 기본적으로 24 시간 마다 한 번에 hello 연결의 데이터를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-126">By default, hello IT Service Management Connector refreshes hello connection's data once in every 24 hours.</span></span> <span data-ttu-id="444f2-127">toorefresh 편집 또는 템플릿에 대 한 즉시 연결의 데이터 업데이트, 변경한 hello 새로 고침 단추 표시 다음 tooyour 연결을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-127">toorefresh your connection's data instantly for any edits or template updates that you make, click hello refresh button displayed next tooyour connection.</span></span>

 ![ITSMC 새로 고침](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a><span data-ttu-id="444f2-129">관리 팩</span><span class="sxs-lookup"><span data-stu-id="444f2-129">Management packs</span></span>
<span data-ttu-id="444f2-130">이 솔루션에는 관리 팩이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-130">This solution does not require any management packs.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="444f2-131">연결된 소스</span><span class="sxs-lookup"><span data-stu-id="444f2-131">Connected sources</span></span>

<span data-ttu-id="444f2-132">hello 다음 ITSM 제품/서비스에서 지 원하는 IT 서비스 관리 커넥터 hello:</span><span class="sxs-lookup"><span data-stu-id="444f2-132">hello following ITSM products/services are supported by hello IT Service Management Connector:</span></span>

- [<span data-ttu-id="444f2-133">SCSM(System Center Service Manager)</span><span class="sxs-lookup"><span data-stu-id="444f2-133">System Center Service Manager (SCSM)</span></span>](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="444f2-134">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="444f2-134">ServiceNow</span></span>](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="444f2-135">Provance</span><span class="sxs-lookup"><span data-stu-id="444f2-135">Provance</span></span>](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [<span data-ttu-id="444f2-136">Cherwell</span><span class="sxs-lookup"><span data-stu-id="444f2-136">Cherwell</span></span>](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-hello-solution"></a><span data-ttu-id="444f2-137">Hello 솔루션을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="444f2-137">Using hello solution</span></span>

<span data-ttu-id="444f2-138">Hello OMS IT 서비스 관리 커넥터를 ITSM 서비스에 연결 하면 hello 로그 분석 서비스에서 연결 하는 hello ITSM 제품/서비스 hello 데이터 수집을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-138">Once you connect hello OMS IT Service Management Connector with your ITSM service, hello Log Analytics services starts gathering hello data from hello connected ITSM products/service.</span></span>

> [!NOTE]
> - <span data-ttu-id="444f2-139">IT Service Management Connector 솔루션에서 가져온 데이터는 **ServiceDesk_CL**이라는 이벤트로 Log Analytics에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-139">Data imported by IT Service Management Connector solution appears in Log Analytics as events named **ServiceDesk_CL**.</span></span>
- <span data-ttu-id="444f2-140">이벤트에는 **ServiceDeskWorkItemType_s**라는 필드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-140">Event contains a field named **ServiceDeskWorkItemType_s**.</span></span> <span data-ttu-id="444f2-141">으로 인시던트를 해당 값을 사용할 수 있습니다 또는 변경 요청, hello에 따라 작업 항목 hello에 포함 된 데이터는 **ServiceDesk_CL** 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-141">which can take its value as incident, or change request, depending on hello work item data contained in hello **ServiceDesk_CL** event.</span></span>

## <a name="input-data"></a><span data-ttu-id="444f2-142">데이터 입력</span><span class="sxs-lookup"><span data-stu-id="444f2-142">Input data</span></span>
<span data-ttu-id="444f2-143">작업 hello ITSM 제품/서비스에서 가져온 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-143">Work items imported from hello ITSM products/services.</span></span>

<span data-ttu-id="444f2-144">hello 다음 정보를 보여 줍니다 hello IT 서비스 관리 커넥터에 의해 수집 된 데이터의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-144">hello following information shows examples of data gathered by hello IT Service Management connector:</span></span>

> [!NOTE]
> <span data-ttu-id="444f2-145">Hello에 따라 작업 항목 형식으로 로그 분석 가져올 **ServiceDesk_CL** hello 다음 필드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-145">Depending on hello work item type imported into Log Analytics, **ServiceDesk_CL** contains hello following fields:</span></span>

<span data-ttu-id="444f2-146">**작업 항목:** **인시던트**</span><span class="sxs-lookup"><span data-stu-id="444f2-146">**Work item:** **Incidents**</span></span>  
<span data-ttu-id="444f2-147">ServiceDeskWorkItemType_s="Incident"</span><span class="sxs-lookup"><span data-stu-id="444f2-147">ServiceDeskWorkItemType_s="Incident"</span></span>

<span data-ttu-id="444f2-148">**필드**</span><span class="sxs-lookup"><span data-stu-id="444f2-148">**Fields**</span></span>

- <span data-ttu-id="444f2-149">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="444f2-149">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="444f2-150">서비스 데스크 ID</span><span class="sxs-lookup"><span data-stu-id="444f2-150">Service Desk ID</span></span>
- <span data-ttu-id="444f2-151">시스템 상태</span><span class="sxs-lookup"><span data-stu-id="444f2-151">State</span></span>
- <span data-ttu-id="444f2-152">긴급도</span><span class="sxs-lookup"><span data-stu-id="444f2-152">Urgency</span></span>
- <span data-ttu-id="444f2-153">영향</span><span class="sxs-lookup"><span data-stu-id="444f2-153">Impact</span></span>
- <span data-ttu-id="444f2-154">우선 순위</span><span class="sxs-lookup"><span data-stu-id="444f2-154">Priority</span></span>
- <span data-ttu-id="444f2-155">에스컬레이션</span><span class="sxs-lookup"><span data-stu-id="444f2-155">Escalation</span></span>
- <span data-ttu-id="444f2-156">만든 사람</span><span class="sxs-lookup"><span data-stu-id="444f2-156">Created By</span></span>
- <span data-ttu-id="444f2-157">해결한 사람</span><span class="sxs-lookup"><span data-stu-id="444f2-157">Resolved By</span></span>
- <span data-ttu-id="444f2-158">종결한 사람</span><span class="sxs-lookup"><span data-stu-id="444f2-158">Closed By</span></span>
- <span data-ttu-id="444f2-159">원본</span><span class="sxs-lookup"><span data-stu-id="444f2-159">Source</span></span>
- <span data-ttu-id="444f2-160">할당 대상</span><span class="sxs-lookup"><span data-stu-id="444f2-160">Assigned To</span></span>
- <span data-ttu-id="444f2-161">Category</span><span class="sxs-lookup"><span data-stu-id="444f2-161">Category</span></span>
- <span data-ttu-id="444f2-162">제목</span><span class="sxs-lookup"><span data-stu-id="444f2-162">Title</span></span>
- <span data-ttu-id="444f2-163">설명</span><span class="sxs-lookup"><span data-stu-id="444f2-163">Description</span></span>
- <span data-ttu-id="444f2-164">만든 날짜</span><span class="sxs-lookup"><span data-stu-id="444f2-164">Created Date</span></span>
- <span data-ttu-id="444f2-165">종결한 날짜</span><span class="sxs-lookup"><span data-stu-id="444f2-165">Closed Date</span></span>
- <span data-ttu-id="444f2-166">해결한 날짜</span><span class="sxs-lookup"><span data-stu-id="444f2-166">Resolved Date</span></span>
- <span data-ttu-id="444f2-167">마지막으로 수정한 날짜</span><span class="sxs-lookup"><span data-stu-id="444f2-167">Last Modified Date</span></span>
- <span data-ttu-id="444f2-168">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="444f2-168">Computer</span></span>


<span data-ttu-id="444f2-169">**작업 항목:** **변경 요청**</span><span class="sxs-lookup"><span data-stu-id="444f2-169">**Work item:** **Change Requests**</span></span>

<span data-ttu-id="444f2-170">ServiceDeskWorkItemType_s="ChangeRequest"</span><span class="sxs-lookup"><span data-stu-id="444f2-170">ServiceDeskWorkItemType_s="ChangeRequest"</span></span>

<span data-ttu-id="444f2-171">**필드**</span><span class="sxs-lookup"><span data-stu-id="444f2-171">**Fields**</span></span>
- <span data-ttu-id="444f2-172">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="444f2-172">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="444f2-173">서비스 데스크 ID</span><span class="sxs-lookup"><span data-stu-id="444f2-173">Service Desk ID</span></span>
- <span data-ttu-id="444f2-174">만든 사람</span><span class="sxs-lookup"><span data-stu-id="444f2-174">Created By</span></span>
- <span data-ttu-id="444f2-175">종결한 사람</span><span class="sxs-lookup"><span data-stu-id="444f2-175">Closed By</span></span>
- <span data-ttu-id="444f2-176">원본</span><span class="sxs-lookup"><span data-stu-id="444f2-176">Source</span></span>
- <span data-ttu-id="444f2-177">할당 대상</span><span class="sxs-lookup"><span data-stu-id="444f2-177">Assigned To</span></span>
- <span data-ttu-id="444f2-178">제목</span><span class="sxs-lookup"><span data-stu-id="444f2-178">Title</span></span>
- <span data-ttu-id="444f2-179">형식</span><span class="sxs-lookup"><span data-stu-id="444f2-179">Type</span></span>
- <span data-ttu-id="444f2-180">Category</span><span class="sxs-lookup"><span data-stu-id="444f2-180">Category</span></span>
- <span data-ttu-id="444f2-181">시스템 상태</span><span class="sxs-lookup"><span data-stu-id="444f2-181">State</span></span>
- <span data-ttu-id="444f2-182">에스컬레이션</span><span class="sxs-lookup"><span data-stu-id="444f2-182">Escalation</span></span>
- <span data-ttu-id="444f2-183">충돌 상태</span><span class="sxs-lookup"><span data-stu-id="444f2-183">Conflict Status</span></span>
- <span data-ttu-id="444f2-184">긴급도</span><span class="sxs-lookup"><span data-stu-id="444f2-184">Urgency</span></span>
- <span data-ttu-id="444f2-185">우선 순위</span><span class="sxs-lookup"><span data-stu-id="444f2-185">Priority</span></span>
- <span data-ttu-id="444f2-186">위험</span><span class="sxs-lookup"><span data-stu-id="444f2-186">Risk</span></span>
- <span data-ttu-id="444f2-187">영향</span><span class="sxs-lookup"><span data-stu-id="444f2-187">Impact</span></span>
- <span data-ttu-id="444f2-188">할당 대상</span><span class="sxs-lookup"><span data-stu-id="444f2-188">Assigned To</span></span>
- <span data-ttu-id="444f2-189">만든 날짜</span><span class="sxs-lookup"><span data-stu-id="444f2-189">Created Date</span></span>
- <span data-ttu-id="444f2-190">종결한 날짜</span><span class="sxs-lookup"><span data-stu-id="444f2-190">Closed Date</span></span>
- <span data-ttu-id="444f2-191">마지막으로 수정한 날짜</span><span class="sxs-lookup"><span data-stu-id="444f2-191">Last Modified Date</span></span>
- <span data-ttu-id="444f2-192">요청한 날짜</span><span class="sxs-lookup"><span data-stu-id="444f2-192">Requested Date</span></span>
- <span data-ttu-id="444f2-193">예상된 시작 날짜</span><span class="sxs-lookup"><span data-stu-id="444f2-193">Planned Start Date</span></span>
- <span data-ttu-id="444f2-194">예상된 종료 날짜</span><span class="sxs-lookup"><span data-stu-id="444f2-194">Planned End Date</span></span>
- <span data-ttu-id="444f2-195">작업 시작 날짜</span><span class="sxs-lookup"><span data-stu-id="444f2-195">Work Start Date</span></span>
- <span data-ttu-id="444f2-196">작업 종료 날짜</span><span class="sxs-lookup"><span data-stu-id="444f2-196">Work End Date</span></span>
- <span data-ttu-id="444f2-197">설명</span><span class="sxs-lookup"><span data-stu-id="444f2-197">Description</span></span>
- <span data-ttu-id="444f2-198">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="444f2-198">Computer</span></span>

## <a name="output-data-for-a-servicenow-incident"></a><span data-ttu-id="444f2-199">ServiceNow 인시던트에 대한 출력 데이터</span><span class="sxs-lookup"><span data-stu-id="444f2-199">Output data for a ServiceNow incident</span></span>

| <span data-ttu-id="444f2-200">OMS 필드</span><span class="sxs-lookup"><span data-stu-id="444f2-200">OMS field</span></span> | <span data-ttu-id="444f2-201">ITSM 필드</span><span class="sxs-lookup"><span data-stu-id="444f2-201">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="444f2-202">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="444f2-202">ServiceDeskId_s</span></span>| <span data-ttu-id="444f2-203">Number</span><span class="sxs-lookup"><span data-stu-id="444f2-203">Number</span></span> |
| <span data-ttu-id="444f2-204">IncidentState_s</span><span class="sxs-lookup"><span data-stu-id="444f2-204">IncidentState_s</span></span> | <span data-ttu-id="444f2-205">시스템 상태</span><span class="sxs-lookup"><span data-stu-id="444f2-205">State</span></span> |
| <span data-ttu-id="444f2-206">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="444f2-206">Urgency_s</span></span> |<span data-ttu-id="444f2-207">긴급도</span><span class="sxs-lookup"><span data-stu-id="444f2-207">Urgency</span></span> |
| <span data-ttu-id="444f2-208">Impact_s</span><span class="sxs-lookup"><span data-stu-id="444f2-208">Impact_s</span></span> |<span data-ttu-id="444f2-209">영향</span><span class="sxs-lookup"><span data-stu-id="444f2-209">Impact</span></span>|
| <span data-ttu-id="444f2-210">Priority_s</span><span class="sxs-lookup"><span data-stu-id="444f2-210">Priority_s</span></span> | <span data-ttu-id="444f2-211">우선 순위</span><span class="sxs-lookup"><span data-stu-id="444f2-211">Priority</span></span> |
| <span data-ttu-id="444f2-212">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="444f2-212">CreatedBy_s</span></span> | <span data-ttu-id="444f2-213">보고자</span><span class="sxs-lookup"><span data-stu-id="444f2-213">Opened by</span></span> |
| <span data-ttu-id="444f2-214">ResolvedBy_s</span><span class="sxs-lookup"><span data-stu-id="444f2-214">ResolvedBy_s</span></span> | <span data-ttu-id="444f2-215">해결한 사람</span><span class="sxs-lookup"><span data-stu-id="444f2-215">Resolved by</span></span>|
| <span data-ttu-id="444f2-216">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="444f2-216">ClosedBy_s</span></span>  | <span data-ttu-id="444f2-217">종결한 사람</span><span class="sxs-lookup"><span data-stu-id="444f2-217">Closed by</span></span> |
| <span data-ttu-id="444f2-218">Source_s</span><span class="sxs-lookup"><span data-stu-id="444f2-218">Source_s</span></span>| <span data-ttu-id="444f2-219">연락처 유형</span><span class="sxs-lookup"><span data-stu-id="444f2-219">Contact type</span></span> |
| <span data-ttu-id="444f2-220">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="444f2-220">AssignedTo_s</span></span> | <span data-ttu-id="444f2-221">너무 할당</span><span class="sxs-lookup"><span data-stu-id="444f2-221">Assigned too</span></span> |
| <span data-ttu-id="444f2-222">Category_s</span><span class="sxs-lookup"><span data-stu-id="444f2-222">Category_s</span></span> | <span data-ttu-id="444f2-223">Category</span><span class="sxs-lookup"><span data-stu-id="444f2-223">Category</span></span> |
| <span data-ttu-id="444f2-224">Title_s</span><span class="sxs-lookup"><span data-stu-id="444f2-224">Title_s</span></span>|  <span data-ttu-id="444f2-225">간단한 설명</span><span class="sxs-lookup"><span data-stu-id="444f2-225">Short description</span></span> |
| <span data-ttu-id="444f2-226">Description_s</span><span class="sxs-lookup"><span data-stu-id="444f2-226">Description_s</span></span>|  <span data-ttu-id="444f2-227">참고 사항</span><span class="sxs-lookup"><span data-stu-id="444f2-227">Notes</span></span> |
| <span data-ttu-id="444f2-228">CreatedDate_t</span><span class="sxs-lookup"><span data-stu-id="444f2-228">CreatedDate_t</span></span>|  <span data-ttu-id="444f2-229">열림</span><span class="sxs-lookup"><span data-stu-id="444f2-229">Opened</span></span> |
| <span data-ttu-id="444f2-230">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="444f2-230">ClosedDate_t</span></span>| <span data-ttu-id="444f2-231">closed</span><span class="sxs-lookup"><span data-stu-id="444f2-231">closed</span></span>|
| <span data-ttu-id="444f2-232">ResolvedDate_t</span><span class="sxs-lookup"><span data-stu-id="444f2-232">ResolvedDate_t</span></span>|<span data-ttu-id="444f2-233">해결됨</span><span class="sxs-lookup"><span data-stu-id="444f2-233">Resolved</span></span>|
| <span data-ttu-id="444f2-234">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="444f2-234">Computer</span></span>  | <span data-ttu-id="444f2-235">구성 항목</span><span class="sxs-lookup"><span data-stu-id="444f2-235">Configuration item</span></span> |

## <a name="output-data-for-a-servicenow-change-request"></a><span data-ttu-id="444f2-236">ServiceNow 변경 요청에 대한 출력 데이터</span><span class="sxs-lookup"><span data-stu-id="444f2-236">Output data for a ServiceNow change request</span></span>

| <span data-ttu-id="444f2-237">OMS 필드</span><span class="sxs-lookup"><span data-stu-id="444f2-237">OMS field</span></span> | <span data-ttu-id="444f2-238">ITSM 필드</span><span class="sxs-lookup"><span data-stu-id="444f2-238">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="444f2-239">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="444f2-239">ServiceDeskId_s</span></span>| <span data-ttu-id="444f2-240">Number</span><span class="sxs-lookup"><span data-stu-id="444f2-240">Number</span></span> |
| <span data-ttu-id="444f2-241">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="444f2-241">CreatedBy_s</span></span> | <span data-ttu-id="444f2-242">요청자</span><span class="sxs-lookup"><span data-stu-id="444f2-242">Requested by</span></span> |
| <span data-ttu-id="444f2-243">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="444f2-243">ClosedBy_s</span></span> | <span data-ttu-id="444f2-244">종결한 사람</span><span class="sxs-lookup"><span data-stu-id="444f2-244">Closed by</span></span> |
| <span data-ttu-id="444f2-245">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="444f2-245">AssignedTo_s</span></span> | <span data-ttu-id="444f2-246">너무 할당</span><span class="sxs-lookup"><span data-stu-id="444f2-246">Assigned too</span></span> |
| <span data-ttu-id="444f2-247">Title_s</span><span class="sxs-lookup"><span data-stu-id="444f2-247">Title_s</span></span>|  <span data-ttu-id="444f2-248">간단한 설명</span><span class="sxs-lookup"><span data-stu-id="444f2-248">Short description</span></span> |
| <span data-ttu-id="444f2-249">Type_s</span><span class="sxs-lookup"><span data-stu-id="444f2-249">Type_s</span></span>|  <span data-ttu-id="444f2-250">형식</span><span class="sxs-lookup"><span data-stu-id="444f2-250">Type</span></span> |
| <span data-ttu-id="444f2-251">Category_s</span><span class="sxs-lookup"><span data-stu-id="444f2-251">Category_s</span></span>|  <span data-ttu-id="444f2-252">범주</span><span class="sxs-lookup"><span data-stu-id="444f2-252">Catgory</span></span> |
| <span data-ttu-id="444f2-253">CRState_s</span><span class="sxs-lookup"><span data-stu-id="444f2-253">CRState_s</span></span>|  <span data-ttu-id="444f2-254">시스템 상태</span><span class="sxs-lookup"><span data-stu-id="444f2-254">State</span></span>|
| <span data-ttu-id="444f2-255">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="444f2-255">Urgency_s</span></span>|  <span data-ttu-id="444f2-256">긴급도</span><span class="sxs-lookup"><span data-stu-id="444f2-256">Urgency</span></span> |
| <span data-ttu-id="444f2-257">Priority_s</span><span class="sxs-lookup"><span data-stu-id="444f2-257">Priority_s</span></span>| <span data-ttu-id="444f2-258">우선 순위</span><span class="sxs-lookup"><span data-stu-id="444f2-258">Priority</span></span>|
| <span data-ttu-id="444f2-259">Risk_s</span><span class="sxs-lookup"><span data-stu-id="444f2-259">Risk_s</span></span>| <span data-ttu-id="444f2-260">위험</span><span class="sxs-lookup"><span data-stu-id="444f2-260">Risk</span></span>|
| <span data-ttu-id="444f2-261">Impact_s</span><span class="sxs-lookup"><span data-stu-id="444f2-261">Impact_s</span></span>| <span data-ttu-id="444f2-262">영향</span><span class="sxs-lookup"><span data-stu-id="444f2-262">Impact</span></span>|
| <span data-ttu-id="444f2-263">RequestedDate_t</span><span class="sxs-lookup"><span data-stu-id="444f2-263">RequestedDate_t</span></span>  | <span data-ttu-id="444f2-264">요청한 날짜</span><span class="sxs-lookup"><span data-stu-id="444f2-264">Requested by date</span></span> |
| <span data-ttu-id="444f2-265">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="444f2-265">ClosedDate_t</span></span> | <span data-ttu-id="444f2-266">종결한 날짜</span><span class="sxs-lookup"><span data-stu-id="444f2-266">Closed date</span></span> |
| <span data-ttu-id="444f2-267">PlannedStartDate_t</span><span class="sxs-lookup"><span data-stu-id="444f2-267">PlannedStartDate_t</span></span>  |     <span data-ttu-id="444f2-268">예상된 시작 날짜</span><span class="sxs-lookup"><span data-stu-id="444f2-268">Planned start date</span></span> |
| <span data-ttu-id="444f2-269">PlannedEndDate_t</span><span class="sxs-lookup"><span data-stu-id="444f2-269">PlannedEndDate_t</span></span>  |   <span data-ttu-id="444f2-270">예상된 종료 날짜</span><span class="sxs-lookup"><span data-stu-id="444f2-270">Planned end date</span></span> |
| <span data-ttu-id="444f2-271">WorkStartDate_t</span><span class="sxs-lookup"><span data-stu-id="444f2-271">WorkStartDate_t</span></span>  | <span data-ttu-id="444f2-272">실제 시작 날짜</span><span class="sxs-lookup"><span data-stu-id="444f2-272">Actual start date</span></span> |
| <span data-ttu-id="444f2-273">WorkEndDate_t</span><span class="sxs-lookup"><span data-stu-id="444f2-273">WorkEndDate_t</span></span> | <span data-ttu-id="444f2-274">실제 종료 날짜</span><span class="sxs-lookup"><span data-stu-id="444f2-274">Actual end date</span></span>|
| <span data-ttu-id="444f2-275">Description_s</span><span class="sxs-lookup"><span data-stu-id="444f2-275">Description_s</span></span> | <span data-ttu-id="444f2-276">설명</span><span class="sxs-lookup"><span data-stu-id="444f2-276">Description</span></span> |
| <span data-ttu-id="444f2-277">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="444f2-277">Computer</span></span>  | <span data-ttu-id="444f2-278">구성 항목</span><span class="sxs-lookup"><span data-stu-id="444f2-278">Configuration Item</span></span> |

<span data-ttu-id="444f2-279">**ITSM 데이터에 대한 샘플 Log Analytics 화면:**</span><span class="sxs-lookup"><span data-stu-id="444f2-279">**Sample Log Analytics screen for ITSM data:**</span></span>

![Log Analytics 화면](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a><span data-ttu-id="444f2-281">IT Service Management Connector - 다른 OMS 솔루션과의 통합</span><span class="sxs-lookup"><span data-stu-id="444f2-281">IT Service Management connector – integration with other OMS solutions</span></span>

<span data-ttu-id="444f2-282">현재 IT 서비스를 관리 하는 커넥터 서비스 맵 솔루션 hello와의 통합을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-282">IT Service Management Connector, currently supports integration with hello Service Map solution.</span></span>

<span data-ttu-id="444f2-283">서비스 맵 Windows에서 응용 프로그램 구성 요소를 hello 및 Linux 시스템 및 지도 hello 서비스 간의 통신에 자동으로 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-283">Service Map automatically discovers hello application components on Windows and Linux systems and maps hello communication between services.</span></span> <span data-ttu-id="444f2-284">Tooview를 때 서버 –으로 볼 중요 한 서비스를 제공 하는 상호 연결 된 시스템 있습니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-284">It allows you tooview your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="444f2-285">서비스 맵은 서버, 프로세스 및 에이전트 설치 이외에 구성이 필요 없는 TCP 연결 아키텍처의 포트 간 연결을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-285">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span> <span data-ttu-id="444f2-286">추가 정보: [서비스 맵](../operations-management-suite/operations-management-suite-service-map.md)</span><span class="sxs-lookup"><span data-stu-id="444f2-286">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="444f2-287">이 통합을 hello 다음 예제와 같이 hello ITSM 솔루션에서 만든 hello 서비스 지원 센터 항목을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-287">With this integration, you can view hello service desk items created in hello ITSM solutions as shown in hello following example:</span></span>

![<span data-ttu-id="444f2-288">통합된 솔루션</span><span class="sxs-lookup"><span data-stu-id="444f2-288">Integrated solution</span></span> ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a><span data-ttu-id="444f2-289">OMS 경고에 대한 ITSM 작업 항목 만들기</span><span class="sxs-lookup"><span data-stu-id="444f2-289">Create ITSM work items for OMS alerts</span></span>

<span data-ttu-id="444f2-290">Hello OMS 경고에 대 한 연결 hello ITSM 소스에 연결 된 작업 항목을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-290">For hello OMS alerts, you can create associated work items in hello connected ITSM sources.</span></span>  <span data-ttu-id="444f2-291">toodo 절차를 수행 하는이 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="444f2-291">toodo this, use hello following procedure:</span></span>

1. <span data-ttu-id="444f2-292">**로그 검색** 창 tooview 데이터를 로그 검색 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-292">From **Log Search** window, run a log search query tooview data.</span></span> <span data-ttu-id="444f2-293">쿼리 결과 작업 항목에 대 한 hello 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-293">Query results are hello source for work items.</span></span>
2. <span data-ttu-id="444f2-294">**로그 검색**, 클릭 **경고** tooopen hello **경고 규칙 추가** 페이지.</span><span class="sxs-lookup"><span data-stu-id="444f2-294">In **Log Search**, click **Alert** tooopen hello **Add Alert Rule** page.</span></span>

    ![Log Analytics 화면](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. <span data-ttu-id="444f2-296">Hello에 **경고 규칙 추가** 창의 hello 필요한 세부 정보를 제공할 **이름**, **심각도**, **검색 쿼리**, 및  **경고 조건** (시간 창/메트릭 측정).</span><span class="sxs-lookup"><span data-stu-id="444f2-296">On hello **Add Alert Rule** window, provide hello required details for **Name**, **Severity**,  **Search query**, and **Alert criteria** (Time Window/Metric measurement).</span></span>
4. <span data-ttu-id="444f2-297">**ITSM 작업**에 대해 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-297">Select **Yes** for **ITSM Actions**.</span></span>
5. <span data-ttu-id="444f2-298">Hello에서 ITSM 연결을 선택 **연결 선택** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-298">Select your ITSM connection from hello **Select Connection** list.</span></span>
6. <span data-ttu-id="444f2-299">필요에 따라 hello 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-299">Provide hello details as required.</span></span>
7. <span data-ttu-id="444f2-300">이 경고를 선택 하는 hello의 각 로그 항목에 대 한 별도 작업 항목 toocreate **각 로그 항목에 대 한 개별 작업 항목을 만들** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-300">toocreate a separate work item for each log entry of this alert, select hello **Create individual work items for each log entry** checkbox.</span></span>

    <span data-ttu-id="444f2-301">또는</span><span class="sxs-lookup"><span data-stu-id="444f2-301">Or</span></span>

    <span data-ttu-id="444f2-302">이 확인란을 선택 하지 않은 toocreate 하나의 작업 항목을 개수에 관계 없이 로그 항목에서이 경고에 대 한 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-302">leave this checkbox unselected toocreate only one work item for any number of log entries under this alert.</span></span>

7. <span data-ttu-id="444f2-303">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-303">Click **Save**.</span></span>

<span data-ttu-id="444f2-304">hello OMS 경고는 만들어집니다 **경고**합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-304">hello OMS alert will be created under **Alerts**.</span></span> <span data-ttu-id="444f2-305">안녕 해당 ITSM 연결의 작업 항목이 hello 지정한 경고 조건이 충족 되 면 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-305">hello corresponding ITSM connection's work items are created when hello specified alert's condition is met.</span></span>

## <a name="create-itsm-work-items-from-oms-logs"></a><span data-ttu-id="444f2-306">OMS 로그에서 ITSM 작업 항목 만들기</span><span class="sxs-lookup"><span data-stu-id="444f2-306">Create ITSM work items from OMS logs</span></span>

<span data-ttu-id="444f2-307">OMS 로그 검색을 사용 하 여 연결 하는 hello ITSM 소스에서 작업 항목을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-307">You can create work items in hello connected ITSM sources by using OMS Log Search.</span></span> <span data-ttu-id="444f2-308">toodo 절차를 수행 하는이 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="444f2-308">toodo this, use hello following procedure:</span></span>

1. <span data-ttu-id="444f2-309">**로그 검색**, hello 필요한 데이터를 검색, hello 세부 정보를 선택 하 고 클릭 **작업 항목 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-309">From **Log Search**,  search hello required data, select hello detail, and click **Create work item**.</span></span>

    <span data-ttu-id="444f2-310">hello **ITSM 작업 만들기 항목** 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-310">hello **Create ITSM Work item** window appears:</span></span>

    ![Log Analytics 화면](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   <span data-ttu-id="444f2-312">Hello 다음 세부 정보를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-312">Add hello following details:</span></span>

  - <span data-ttu-id="444f2-313">**작업 항목 제목**: hello 작업 항목에 대 한 Title 합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-313">**Work item Title**: Title for hello work item.</span></span>
  - <span data-ttu-id="444f2-314">**작업 항목 설명**: hello 새 작업 항목에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-314">**Work item Description**: Description for hello new work item.</span></span>
  - <span data-ttu-id="444f2-315">**컴퓨터에 영향을 받는**:이 로그 데이터를 찾을 수 hello 컴퓨터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-315">**Affected Computer**: Name of hello computer where this log data was found.</span></span>
  - <span data-ttu-id="444f2-316">**연결을 선택**: ITSM 연결 하려는 toocreate이 작업 항목.</span><span class="sxs-lookup"><span data-stu-id="444f2-316">**Select Connection**:  ITSM connection in which you want toocreate this work item.</span></span>
  - <span data-ttu-id="444f2-317">**작업 항목**: 작업 항목의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-317">**Work item**:  Type of work item.</span></span>

3. <span data-ttu-id="444f2-318">toouse 인시던트의 기존 작업 항목 템플릿을 클릭 **예** 아래 **생성 작업 항목 템플릿을 기반으로 hello** 옵션 선택한 다음 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-318">toouse an existing work item template for an incident, click **Yes** under **Generate work item based on hello template** option and then click **Create**.</span></span>

    <span data-ttu-id="444f2-319">또는</span><span class="sxs-lookup"><span data-stu-id="444f2-319">Or,</span></span>

    <span data-ttu-id="444f2-320">클릭 **아니요** tooprovide 사용자 사용자 지정 된 값을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-320">Click **No** if you want tooprovide your customized values.</span></span>

4. <span data-ttu-id="444f2-321">Hello hello에 적절 한 값을 제공 **연락처 유형**, **영향**, **긴급도**, **범주**, 및 **하위 범주**  텍스트 상자 및 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-321">Provide hello appropriate values in hello **Contact Type**, **Impact**, **Urgency**, **Category**, and **Sub Category** text boxes, and then click **Create**.</span></span>

<span data-ttu-id="444f2-322">OMS에서 볼 수 있습니다 ITSM hello에 hello 작업 항목이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-322">hello work item will be created in hello ITSM, which you can also view in OMS.</span></span>

## <a name="troubleshoot-itsm-connections-in-oms"></a><span data-ttu-id="444f2-323">OMS에서 ITSM 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="444f2-323">Troubleshoot ITSM connections in OMS</span></span>
1.  <span data-ttu-id="444f2-324">연결 된 소스 UI에서 연결이 실패 하 고 hello 얻게 **연결을 저장 하는 동안 오류가 발생 했습니다.** 메시지에서 다음 hello지 않습니다:</span><span class="sxs-lookup"><span data-stu-id="444f2-324">If connection fails from connected source's UI and you get hello **Error in saving connection** message, do hello following:</span></span>
 - <span data-ttu-id="444f2-325">ServiceNow, Cherwell 및 Provance 연결의 경우 확인 하면 hello를 올바르게 입력 한 사용자 이름/암호 및 클라이언트 ID/클라이언트 암호 각 hello 연결에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-325">In case of ServiceNow, Cherwell and Provance connections, ensure you correctly entered  hello username/password and  client ID/client secret  for each of hello connections.</span></span> <span data-ttu-id="444f2-326">Hello 오류가 계속 되 면 hello 해당 ITSM 제품 toomake hello 연결에서 충분 한 권한이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-326">If hello error persists, check if you have sufficient privileges  in hello corresponding ITSM product toomake hello connection.</span></span>
 - <span data-ttu-id="444f2-327">서비스 관리자의 경우 확인 hello 웹 앱을 배포 했습니다. 하이브리드 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-327">In case of Service Manager, ensure that hello Web app is successfully deployed and hybrid connection is created.</span></span> <span data-ttu-id="444f2-328">tooverify hello 성공적으로 연결 hello 온-프레미스 서비스 관리자 컴퓨터와, hello를 만들기 위한 hello 설명서에 설명 된 대로 hello 웹 앱 URL을 방문 [하이브리드 연결](log-analytics-itsmc-connections.md#configure-the-hybrid-connection)합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-328">tooverify hello connection is successfully established with hello on-prem Service Manager machine, visit hello  Web app URL as detailed in hello documentation for making hello [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>

2.  <span data-ttu-id="444f2-329">OMS에서 ServiceNow에서 데이터 동기화 시작 되지 않은, 해당 hello ServiceNow 인스턴스 중지 중이 아님를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-329">If data from ServiceNow is not getting synced in OMS, ensure that hello ServiceNow instance is not sleeping.</span></span> <span data-ttu-id="444f2-330">이 발생할 수 있습니다 잠시 hello에 유휴 상태일 때 ServiceNow Dev 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="444f2-330">This might sometime happen in hello ServiceNow Dev instances, when idle.</span></span> <span data-ttu-id="444f2-331">다른 보고서 hello 문제가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-331">Else, report hello issue.</span></span>
3.  <span data-ttu-id="444f2-332">OMS에서 경고를 가져오는 발생 하지만 작업 항목을 가져오는에서 ITSM 제품 또는 구성 항목 toowork 만든/연결 된 항목을 가져오지 않습니다. 만들거나 다음 hello 않는 일반 정보를:</span><span class="sxs-lookup"><span data-stu-id="444f2-332">If Alerts are getting fired from OMS but work items are not getting created in ITSM product or configuration items are not getting created/linked toowork items or for any generic information, do hello following:</span></span>
 -  <span data-ttu-id="444f2-333">OMS 포털의 IT 서비스 관리 커넥터 솔루션에 사용 되는 tooget 연결/작업 항목/컴퓨터 등의 요약 될 수 있습니다. Hello 상태 블레이드에서 hello 오류 메시지, 너무 탐색**로그 검색** hello 오류 메시지에 hello 세부 정보를 사용 하 여 hello 오류가 있는 hello 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-333">IT Service Management Connector solution in OMS portal could be used tooget a summary of connections/work items/computers etc. Click hello error message in hello status blade, navigate too**Log Search** and view hello connection that has hello error by using hello details in hello error message.</span></span>
 - <span data-ttu-id="444f2-334">hello에 hello 오류/관련 정보를 직접 볼 수 **로그 검색** 페이지를 사용 하 여 *유형 = ServiceDeskLog_CL*합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-334">you can directly view hello errors/related information in hello **Log Search** page using *Type=ServiceDeskLog_CL*.</span></span>

## <a name="troubleshoot-service-manager-web-app-deployment"></a><span data-ttu-id="444f2-335">Service Manager 웹앱 배포 문제 해결</span><span class="sxs-lookup"><span data-stu-id="444f2-335">Troubleshoot Service Manager Web App deployment</span></span>
1.  <span data-ttu-id="444f2-336">웹 앱 배포 문제를 발생 시 hello 구독에 대 한 충분 한 권한이 있는지 확인 toocreate/배포 하는 리소스를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-336">In case of any trouble with web app deployment, ensure you have sufficient permissions in hello subscription mentioned toocreate/deploy resources.</span></span>
2.  <span data-ttu-id="444f2-337">경우 **개체 참조가 개체의 tooinstance 설정 되지** hello를 실행 하는 동안 오류 메시지가 표시 됩니다. [스크립트](log-analytics-itsmc-service-manager-script.md) 에서 유효한 값을 입력 했는지 확인 **사용자 구성**섹션.</span><span class="sxs-lookup"><span data-stu-id="444f2-337">If **Object reference not set tooinstance of an object** error message appears while running hello [script](log-analytics-itsmc-service-manager-script.md) ensure that you entered valid values  under **User Configuration** section.</span></span>
3.  <span data-ttu-id="444f2-338">Toocreate 서비스 버스 릴레이 네임 스페이스를 실패 한 경우 해당 hello 필요한 hello 구독에 리소스 공급자가 등록을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-338">If you fail toocreate service bus relay namespace, ensure that hello required resource provider is registered in hello subscription.</span></span> <span data-ttu-id="444f2-339">등록 되지 않은 경우 hello Azure 포털에서에서 만들 수동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-339">If not registered, manually create it from hello Azure portal.</span></span> <span data-ttu-id="444f2-340">하지만 만들 수도 있습니다 [hello 하이브리드 연결을 만드는](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) hello Azure 포털에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-340">You can also create it while [creating hello hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from hello Azure portal.</span></span>


## <a name="contact-us"></a><span data-ttu-id="444f2-341">문의처</span><span class="sxs-lookup"><span data-stu-id="444f2-341">Contact us</span></span>

<span data-ttu-id="444f2-342">모든 쿼리 또는 hello IT 서비스 관리 커넥터에 대 한 피드백에 게 문의 하세요. [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-342">For any queries or feedback on hello IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="444f2-343">다음 단계</span><span class="sxs-lookup"><span data-stu-id="444f2-343">Next steps</span></span>
<span data-ttu-id="444f2-344">[서비스 관리 커넥터 ITSM 제품/서비스 tooIT 추가](log-analytics-itsmc-connections.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="444f2-344">[Add ITSM products/services tooIT Service Management Connector](log-analytics-itsmc-connections.md).</span></span>
