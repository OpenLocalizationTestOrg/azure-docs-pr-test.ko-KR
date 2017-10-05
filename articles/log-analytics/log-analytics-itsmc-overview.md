---
title: "OMS의 IT Service Management Connector | Microsoft Docs"
description: "IT Service Management Connector를 사용하여 중앙에서 OMS의 ITSM 작업 항목을 모니터링 및 관리하고 문제를 빠르게 해결합니다."
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
ms.openlocfilehash: 54974ef06efdae69ddbfa12b1ba9278b48b113d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a><span data-ttu-id="1a935-103">IT Service Management Connector(미리 보기)를 사용하여 ITSM 작업 항목을 중앙에서 관리</span><span class="sxs-lookup"><span data-stu-id="1a935-103">Centrally manage ITSM work items using IT Service Management Connector (Preview)</span></span>

![IT Service Management Connector 기호](./media/log-analytics-itsmc/itsmc-symbol.png)

<span data-ttu-id="1a935-105">OMS Log Analytics에서 IT Service Management Connector를 사용하여 ITSM 제품/서비스에서 작업 항목을 중앙에서 모니터링하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-105">You can use the IT Service Management Connector (ITSMC) in OMS Log Analytics to centrally monitor and manage work items across your ITSM products/services.</span></span>

<span data-ttu-id="1a935-106">IT Service Management Connector는 기존 ITSM(IT Service Management) 제품 및 서비스를 OMS Log Analytics에 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-106">The IT Service Management Connector integrates your existing IT Service Management (ITSM) products and services with OMS Log Analytics.</span></span>  <span data-ttu-id="1a935-107">이 솔루션은 ITSM 제품/서비스와 양방향으로 통합되어 OMS 사용자가 ITSM 솔루션에서 인시던트, 경고 또는 이벤트를 만드는 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-107">The solution has bidirectional integration with ITSM products/services, where it provides the OMS users an option to create incidents, alerts, or events in ITSM solution.</span></span> <span data-ttu-id="1a935-108">또한 이 커넥터는 ITSM 솔루션의 인시던트 및 변경 요청과 같은 데이터를 OMS Log Analytics로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-108">The connector also  imports data such as incidents, and change requests from ITSM solution into OMS Log Analytics.</span></span>

<span data-ttu-id="1a935-109">IT Service Management Connector를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-109">With IT Service Management Connector, you can:</span></span>

  - <span data-ttu-id="1a935-110">조직에서 사용되는 ITSM 제품/서비스에 대한 작업 항목을 중앙에서 모니터링 및 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-110">Centrally monitor and manage work items for ITSM products/services used across your organization.</span></span>
  - <span data-ttu-id="1a935-111">OMS 경고 및 로그 검색을 통해 ITSM에서 ITSM 작업 항목(예: 경고, 이벤트, 인시던트)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-111">Create ITSM work items (like alert, event, incident) in ITSM from OMS alerts and through log search.</span></span>
  - <span data-ttu-id="1a935-112">ITSM 솔루션에서 인시던트 및 변경 요청을 읽고, Log Analytics 작업 영역에서 관련 로그 데이터와의 상관 관계를 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-112">Read incidents and change requests from your ITSM solution and correlate with relevant log data in Log Analytics workspace.</span></span>
  - <span data-ttu-id="1a935-113">최종 사용자가 지원 부서에 전화를 해서 보고하기 전에 예기치 않은 비정상적인 이벤트를 찾아 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-113">Find any unexpected and unusual events and resolve them, even before the end users call and report them to the helpdesk.</span></span>
  - <span data-ttu-id="1a935-114">작업 항목 데이터를 Log Analytics로 가져오고 KPI(핵심 성과 지표) 보고서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-114">Import work items data into Log Analytics and create key performance indicator (KPI) reports.</span></span>  <span data-ttu-id="1a935-115">이러한 보고서를 사용하여 중요한 일부 항목을 식별하고 평가한 후 맬웨어 평가와 같은 조치를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-115">Using these reports, you can identify, assess and act on several important items such as malware assessment.</span></span>
  - <span data-ttu-id="1a935-116">엄선된 대시보드를 통해 인시던트, 변경 요청 및 영향 받은 시스템에 대한 심층 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-116">View curated dashboards for deeper insights on incidents, change requests and impacted systems.</span></span>
  - <span data-ttu-id="1a935-117">Log Analytics 작업 영역에서 다른 관리 솔루션과 상호 연결하여 더 빠르게 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-117">Troubleshoot faster by correlating with other management solutions in the Log Analytics workspace.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="1a935-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1a935-118">Prerequisites</span></span>

<span data-ttu-id="1a935-119">ITSM 작업 항목을 OMS Log Analytics로 가져오기 위해 솔루션에서 OMS의 IT Service Management Connector와 작업 항목을 가져오는 ITSM 제품/서비스가 서로 연결되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-119">To import the ITSM work items into OMS Log Analytics, the solution requires a connection between the IT Service Management Connector in the OMS and the IT SM product/service from which you import the work items.</span></span>


## <a name="configuration"></a><span data-ttu-id="1a935-120">구성</span><span class="sxs-lookup"><span data-stu-id="1a935-120">Configuration</span></span>

<span data-ttu-id="1a935-121">[솔루션 갤러리에서 Log Analytics 솔루션 추가](log-analytics-add-solutions.md)에 설명된 프로세스를 사용하여 OMS 작업 영역에 IT Service Management Connector 솔루션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-121">Add the IT Service Management Connector solution to your OMS work space, using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

<span data-ttu-id="1a935-122">솔루션 갤러리에 표시되는 IT Service Management Connector 타일:</span><span class="sxs-lookup"><span data-stu-id="1a935-122">IT Service Management Connector tile as you see in the Solutions gallery:</span></span>

![커넥터 타일](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

<span data-ttu-id="1a935-124">성공적으로 추가한 후 **OMS** > **설정** > **연결된 원본** 아래에 IT Service Management Connector가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-124">After successful addition, you will see the IT Service Management Connector under **OMS** > **Settings** > **Connected Sources.**</span></span>

![ITSMC가 연결되어 있습니다.](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> <span data-ttu-id="1a935-126">기본적으로 IT Service Management Connector는 24시간마다 한 번씩 연결 데이터를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-126">By default, the IT Service Management Connector refreshes the connection's data once in every 24 hours.</span></span> <span data-ttu-id="1a935-127">적용한 편집 내용 또는 템플릿 업데이트에 대해 연결 데이터를 즉시 새로 고치려면 연결 옆에 표시된 새로 고침 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-127">To refresh your connection's data instantly for any edits or template updates that you make, click the refresh button displayed next to your connection.</span></span>

 ![ITSMC 새로 고침](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a><span data-ttu-id="1a935-129">관리 팩</span><span class="sxs-lookup"><span data-stu-id="1a935-129">Management packs</span></span>
<span data-ttu-id="1a935-130">이 솔루션에는 관리 팩이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-130">This solution does not require any management packs.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="1a935-131">연결된 소스</span><span class="sxs-lookup"><span data-stu-id="1a935-131">Connected sources</span></span>

<span data-ttu-id="1a935-132">다음 ITSM 제품/서비스는 IT Service Management Connector를 통해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-132">The following ITSM products/services are supported by the IT Service Management Connector:</span></span>

- [<span data-ttu-id="1a935-133">SCSM(System Center Service Manager)</span><span class="sxs-lookup"><span data-stu-id="1a935-133">System Center Service Manager (SCSM)</span></span>](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="1a935-134">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="1a935-134">ServiceNow</span></span>](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="1a935-135">Provance</span><span class="sxs-lookup"><span data-stu-id="1a935-135">Provance</span></span>](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [<span data-ttu-id="1a935-136">Cherwell</span><span class="sxs-lookup"><span data-stu-id="1a935-136">Cherwell</span></span>](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-the-solution"></a><span data-ttu-id="1a935-137">솔루션 사용</span><span class="sxs-lookup"><span data-stu-id="1a935-137">Using the solution</span></span>

<span data-ttu-id="1a935-138">OMS IT Service Management Connector를 ITSM 서비스에 연결하면 Log Analytics 서비스가 연결된 ITSM 제품/서비스로부터 데이터를 수집하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-138">Once you connect the OMS IT Service Management Connector with your ITSM service, the Log Analytics services starts gathering the data from the connected ITSM products/service.</span></span>

> [!NOTE]
> - <span data-ttu-id="1a935-139">IT Service Management Connector 솔루션에서 가져온 데이터는 **ServiceDesk_CL**이라는 이벤트로 Log Analytics에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-139">Data imported by IT Service Management Connector solution appears in Log Analytics as events named **ServiceDesk_CL**.</span></span>
- <span data-ttu-id="1a935-140">이벤트에는 **ServiceDeskWorkItemType_s**라는 필드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-140">Event contains a field named **ServiceDeskWorkItemType_s**.</span></span> <span data-ttu-id="1a935-141">이 필드는 **ServiceDesk_CL** 이벤트에 포함된 작업 항목 데이터에 따라 인시던트 또는 변경 요청으로 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-141">which can take its value as incident, or change request, depending on the work item data contained in the **ServiceDesk_CL** event.</span></span>

## <a name="input-data"></a><span data-ttu-id="1a935-142">데이터 입력</span><span class="sxs-lookup"><span data-stu-id="1a935-142">Input data</span></span>
<span data-ttu-id="1a935-143">ITSM 제품/서비스에서 가져온 작업 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-143">Work items imported from the ITSM products/services.</span></span>

<span data-ttu-id="1a935-144">다음 정보는 IT Service Management Connector에서 수집된 데이터 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-144">The following information shows examples of data gathered by the IT Service Management connector:</span></span>

> [!NOTE]
> <span data-ttu-id="1a935-145">Log Analytics로 가져온 작업 항목 형식에 따라 **ServiceDesk_CL**에는 다음 필드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-145">Depending on the work item type imported into Log Analytics, **ServiceDesk_CL** contains the following fields:</span></span>

<span data-ttu-id="1a935-146">**작업 항목:** **인시던트**</span><span class="sxs-lookup"><span data-stu-id="1a935-146">**Work item:** **Incidents**</span></span>  
<span data-ttu-id="1a935-147">ServiceDeskWorkItemType_s="Incident"</span><span class="sxs-lookup"><span data-stu-id="1a935-147">ServiceDeskWorkItemType_s="Incident"</span></span>

<span data-ttu-id="1a935-148">**필드**</span><span class="sxs-lookup"><span data-stu-id="1a935-148">**Fields**</span></span>

- <span data-ttu-id="1a935-149">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="1a935-149">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="1a935-150">서비스 데스크 ID</span><span class="sxs-lookup"><span data-stu-id="1a935-150">Service Desk ID</span></span>
- <span data-ttu-id="1a935-151">시스템 상태</span><span class="sxs-lookup"><span data-stu-id="1a935-151">State</span></span>
- <span data-ttu-id="1a935-152">긴급도</span><span class="sxs-lookup"><span data-stu-id="1a935-152">Urgency</span></span>
- <span data-ttu-id="1a935-153">영향</span><span class="sxs-lookup"><span data-stu-id="1a935-153">Impact</span></span>
- <span data-ttu-id="1a935-154">우선 순위</span><span class="sxs-lookup"><span data-stu-id="1a935-154">Priority</span></span>
- <span data-ttu-id="1a935-155">에스컬레이션</span><span class="sxs-lookup"><span data-stu-id="1a935-155">Escalation</span></span>
- <span data-ttu-id="1a935-156">만든 사람</span><span class="sxs-lookup"><span data-stu-id="1a935-156">Created By</span></span>
- <span data-ttu-id="1a935-157">해결한 사람</span><span class="sxs-lookup"><span data-stu-id="1a935-157">Resolved By</span></span>
- <span data-ttu-id="1a935-158">종결한 사람</span><span class="sxs-lookup"><span data-stu-id="1a935-158">Closed By</span></span>
- <span data-ttu-id="1a935-159">원본</span><span class="sxs-lookup"><span data-stu-id="1a935-159">Source</span></span>
- <span data-ttu-id="1a935-160">할당 대상</span><span class="sxs-lookup"><span data-stu-id="1a935-160">Assigned To</span></span>
- <span data-ttu-id="1a935-161">Category</span><span class="sxs-lookup"><span data-stu-id="1a935-161">Category</span></span>
- <span data-ttu-id="1a935-162">제목</span><span class="sxs-lookup"><span data-stu-id="1a935-162">Title</span></span>
- <span data-ttu-id="1a935-163">설명</span><span class="sxs-lookup"><span data-stu-id="1a935-163">Description</span></span>
- <span data-ttu-id="1a935-164">만든 날짜</span><span class="sxs-lookup"><span data-stu-id="1a935-164">Created Date</span></span>
- <span data-ttu-id="1a935-165">종결한 날짜</span><span class="sxs-lookup"><span data-stu-id="1a935-165">Closed Date</span></span>
- <span data-ttu-id="1a935-166">해결한 날짜</span><span class="sxs-lookup"><span data-stu-id="1a935-166">Resolved Date</span></span>
- <span data-ttu-id="1a935-167">마지막으로 수정한 날짜</span><span class="sxs-lookup"><span data-stu-id="1a935-167">Last Modified Date</span></span>
- <span data-ttu-id="1a935-168">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="1a935-168">Computer</span></span>


<span data-ttu-id="1a935-169">**작업 항목:** **변경 요청**</span><span class="sxs-lookup"><span data-stu-id="1a935-169">**Work item:** **Change Requests**</span></span>

<span data-ttu-id="1a935-170">ServiceDeskWorkItemType_s="ChangeRequest"</span><span class="sxs-lookup"><span data-stu-id="1a935-170">ServiceDeskWorkItemType_s="ChangeRequest"</span></span>

<span data-ttu-id="1a935-171">**필드**</span><span class="sxs-lookup"><span data-stu-id="1a935-171">**Fields**</span></span>
- <span data-ttu-id="1a935-172">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="1a935-172">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="1a935-173">서비스 데스크 ID</span><span class="sxs-lookup"><span data-stu-id="1a935-173">Service Desk ID</span></span>
- <span data-ttu-id="1a935-174">만든 사람</span><span class="sxs-lookup"><span data-stu-id="1a935-174">Created By</span></span>
- <span data-ttu-id="1a935-175">종결한 사람</span><span class="sxs-lookup"><span data-stu-id="1a935-175">Closed By</span></span>
- <span data-ttu-id="1a935-176">원본</span><span class="sxs-lookup"><span data-stu-id="1a935-176">Source</span></span>
- <span data-ttu-id="1a935-177">할당 대상</span><span class="sxs-lookup"><span data-stu-id="1a935-177">Assigned To</span></span>
- <span data-ttu-id="1a935-178">제목</span><span class="sxs-lookup"><span data-stu-id="1a935-178">Title</span></span>
- <span data-ttu-id="1a935-179">형식</span><span class="sxs-lookup"><span data-stu-id="1a935-179">Type</span></span>
- <span data-ttu-id="1a935-180">Category</span><span class="sxs-lookup"><span data-stu-id="1a935-180">Category</span></span>
- <span data-ttu-id="1a935-181">시스템 상태</span><span class="sxs-lookup"><span data-stu-id="1a935-181">State</span></span>
- <span data-ttu-id="1a935-182">에스컬레이션</span><span class="sxs-lookup"><span data-stu-id="1a935-182">Escalation</span></span>
- <span data-ttu-id="1a935-183">충돌 상태</span><span class="sxs-lookup"><span data-stu-id="1a935-183">Conflict Status</span></span>
- <span data-ttu-id="1a935-184">긴급도</span><span class="sxs-lookup"><span data-stu-id="1a935-184">Urgency</span></span>
- <span data-ttu-id="1a935-185">우선 순위</span><span class="sxs-lookup"><span data-stu-id="1a935-185">Priority</span></span>
- <span data-ttu-id="1a935-186">위험</span><span class="sxs-lookup"><span data-stu-id="1a935-186">Risk</span></span>
- <span data-ttu-id="1a935-187">영향</span><span class="sxs-lookup"><span data-stu-id="1a935-187">Impact</span></span>
- <span data-ttu-id="1a935-188">할당 대상</span><span class="sxs-lookup"><span data-stu-id="1a935-188">Assigned To</span></span>
- <span data-ttu-id="1a935-189">만든 날짜</span><span class="sxs-lookup"><span data-stu-id="1a935-189">Created Date</span></span>
- <span data-ttu-id="1a935-190">종결한 날짜</span><span class="sxs-lookup"><span data-stu-id="1a935-190">Closed Date</span></span>
- <span data-ttu-id="1a935-191">마지막으로 수정한 날짜</span><span class="sxs-lookup"><span data-stu-id="1a935-191">Last Modified Date</span></span>
- <span data-ttu-id="1a935-192">요청한 날짜</span><span class="sxs-lookup"><span data-stu-id="1a935-192">Requested Date</span></span>
- <span data-ttu-id="1a935-193">예상된 시작 날짜</span><span class="sxs-lookup"><span data-stu-id="1a935-193">Planned Start Date</span></span>
- <span data-ttu-id="1a935-194">예상된 종료 날짜</span><span class="sxs-lookup"><span data-stu-id="1a935-194">Planned End Date</span></span>
- <span data-ttu-id="1a935-195">작업 시작 날짜</span><span class="sxs-lookup"><span data-stu-id="1a935-195">Work Start Date</span></span>
- <span data-ttu-id="1a935-196">작업 종료 날짜</span><span class="sxs-lookup"><span data-stu-id="1a935-196">Work End Date</span></span>
- <span data-ttu-id="1a935-197">설명</span><span class="sxs-lookup"><span data-stu-id="1a935-197">Description</span></span>
- <span data-ttu-id="1a935-198">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="1a935-198">Computer</span></span>

## <a name="output-data-for-a-servicenow-incident"></a><span data-ttu-id="1a935-199">ServiceNow 인시던트에 대한 출력 데이터</span><span class="sxs-lookup"><span data-stu-id="1a935-199">Output data for a ServiceNow incident</span></span>

| <span data-ttu-id="1a935-200">OMS 필드</span><span class="sxs-lookup"><span data-stu-id="1a935-200">OMS field</span></span> | <span data-ttu-id="1a935-201">ITSM 필드</span><span class="sxs-lookup"><span data-stu-id="1a935-201">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="1a935-202">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="1a935-202">ServiceDeskId_s</span></span>| <span data-ttu-id="1a935-203">Number</span><span class="sxs-lookup"><span data-stu-id="1a935-203">Number</span></span> |
| <span data-ttu-id="1a935-204">IncidentState_s</span><span class="sxs-lookup"><span data-stu-id="1a935-204">IncidentState_s</span></span> | <span data-ttu-id="1a935-205">시스템 상태</span><span class="sxs-lookup"><span data-stu-id="1a935-205">State</span></span> |
| <span data-ttu-id="1a935-206">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="1a935-206">Urgency_s</span></span> |<span data-ttu-id="1a935-207">긴급도</span><span class="sxs-lookup"><span data-stu-id="1a935-207">Urgency</span></span> |
| <span data-ttu-id="1a935-208">Impact_s</span><span class="sxs-lookup"><span data-stu-id="1a935-208">Impact_s</span></span> |<span data-ttu-id="1a935-209">영향</span><span class="sxs-lookup"><span data-stu-id="1a935-209">Impact</span></span>|
| <span data-ttu-id="1a935-210">Priority_s</span><span class="sxs-lookup"><span data-stu-id="1a935-210">Priority_s</span></span> | <span data-ttu-id="1a935-211">우선 순위</span><span class="sxs-lookup"><span data-stu-id="1a935-211">Priority</span></span> |
| <span data-ttu-id="1a935-212">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="1a935-212">CreatedBy_s</span></span> | <span data-ttu-id="1a935-213">보고자</span><span class="sxs-lookup"><span data-stu-id="1a935-213">Opened by</span></span> |
| <span data-ttu-id="1a935-214">ResolvedBy_s</span><span class="sxs-lookup"><span data-stu-id="1a935-214">ResolvedBy_s</span></span> | <span data-ttu-id="1a935-215">해결한 사람</span><span class="sxs-lookup"><span data-stu-id="1a935-215">Resolved by</span></span>|
| <span data-ttu-id="1a935-216">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="1a935-216">ClosedBy_s</span></span>  | <span data-ttu-id="1a935-217">종결한 사람</span><span class="sxs-lookup"><span data-stu-id="1a935-217">Closed by</span></span> |
| <span data-ttu-id="1a935-218">Source_s</span><span class="sxs-lookup"><span data-stu-id="1a935-218">Source_s</span></span>| <span data-ttu-id="1a935-219">연락처 유형</span><span class="sxs-lookup"><span data-stu-id="1a935-219">Contact type</span></span> |
| <span data-ttu-id="1a935-220">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="1a935-220">AssignedTo_s</span></span> | <span data-ttu-id="1a935-221">할당 대상</span><span class="sxs-lookup"><span data-stu-id="1a935-221">Assigned to</span></span>  |
| <span data-ttu-id="1a935-222">Category_s</span><span class="sxs-lookup"><span data-stu-id="1a935-222">Category_s</span></span> | <span data-ttu-id="1a935-223">Category</span><span class="sxs-lookup"><span data-stu-id="1a935-223">Category</span></span> |
| <span data-ttu-id="1a935-224">Title_s</span><span class="sxs-lookup"><span data-stu-id="1a935-224">Title_s</span></span>|  <span data-ttu-id="1a935-225">간단한 설명</span><span class="sxs-lookup"><span data-stu-id="1a935-225">Short description</span></span> |
| <span data-ttu-id="1a935-226">Description_s</span><span class="sxs-lookup"><span data-stu-id="1a935-226">Description_s</span></span>|  <span data-ttu-id="1a935-227">참고 사항</span><span class="sxs-lookup"><span data-stu-id="1a935-227">Notes</span></span> |
| <span data-ttu-id="1a935-228">CreatedDate_t</span><span class="sxs-lookup"><span data-stu-id="1a935-228">CreatedDate_t</span></span>|  <span data-ttu-id="1a935-229">열림</span><span class="sxs-lookup"><span data-stu-id="1a935-229">Opened</span></span> |
| <span data-ttu-id="1a935-230">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="1a935-230">ClosedDate_t</span></span>| <span data-ttu-id="1a935-231">closed</span><span class="sxs-lookup"><span data-stu-id="1a935-231">closed</span></span>|
| <span data-ttu-id="1a935-232">ResolvedDate_t</span><span class="sxs-lookup"><span data-stu-id="1a935-232">ResolvedDate_t</span></span>|<span data-ttu-id="1a935-233">해결됨</span><span class="sxs-lookup"><span data-stu-id="1a935-233">Resolved</span></span>|
| <span data-ttu-id="1a935-234">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="1a935-234">Computer</span></span>  | <span data-ttu-id="1a935-235">구성 항목</span><span class="sxs-lookup"><span data-stu-id="1a935-235">Configuration item</span></span> |

## <a name="output-data-for-a-servicenow-change-request"></a><span data-ttu-id="1a935-236">ServiceNow 변경 요청에 대한 출력 데이터</span><span class="sxs-lookup"><span data-stu-id="1a935-236">Output data for a ServiceNow change request</span></span>

| <span data-ttu-id="1a935-237">OMS 필드</span><span class="sxs-lookup"><span data-stu-id="1a935-237">OMS field</span></span> | <span data-ttu-id="1a935-238">ITSM 필드</span><span class="sxs-lookup"><span data-stu-id="1a935-238">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="1a935-239">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="1a935-239">ServiceDeskId_s</span></span>| <span data-ttu-id="1a935-240">Number</span><span class="sxs-lookup"><span data-stu-id="1a935-240">Number</span></span> |
| <span data-ttu-id="1a935-241">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="1a935-241">CreatedBy_s</span></span> | <span data-ttu-id="1a935-242">요청자</span><span class="sxs-lookup"><span data-stu-id="1a935-242">Requested by</span></span> |
| <span data-ttu-id="1a935-243">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="1a935-243">ClosedBy_s</span></span> | <span data-ttu-id="1a935-244">종결한 사람</span><span class="sxs-lookup"><span data-stu-id="1a935-244">Closed by</span></span> |
| <span data-ttu-id="1a935-245">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="1a935-245">AssignedTo_s</span></span> | <span data-ttu-id="1a935-246">할당 대상</span><span class="sxs-lookup"><span data-stu-id="1a935-246">Assigned to</span></span>  |
| <span data-ttu-id="1a935-247">Title_s</span><span class="sxs-lookup"><span data-stu-id="1a935-247">Title_s</span></span>|  <span data-ttu-id="1a935-248">간단한 설명</span><span class="sxs-lookup"><span data-stu-id="1a935-248">Short description</span></span> |
| <span data-ttu-id="1a935-249">Type_s</span><span class="sxs-lookup"><span data-stu-id="1a935-249">Type_s</span></span>|  <span data-ttu-id="1a935-250">형식</span><span class="sxs-lookup"><span data-stu-id="1a935-250">Type</span></span> |
| <span data-ttu-id="1a935-251">Category_s</span><span class="sxs-lookup"><span data-stu-id="1a935-251">Category_s</span></span>|  <span data-ttu-id="1a935-252">범주</span><span class="sxs-lookup"><span data-stu-id="1a935-252">Catgory</span></span> |
| <span data-ttu-id="1a935-253">CRState_s</span><span class="sxs-lookup"><span data-stu-id="1a935-253">CRState_s</span></span>|  <span data-ttu-id="1a935-254">시스템 상태</span><span class="sxs-lookup"><span data-stu-id="1a935-254">State</span></span>|
| <span data-ttu-id="1a935-255">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="1a935-255">Urgency_s</span></span>|  <span data-ttu-id="1a935-256">긴급도</span><span class="sxs-lookup"><span data-stu-id="1a935-256">Urgency</span></span> |
| <span data-ttu-id="1a935-257">Priority_s</span><span class="sxs-lookup"><span data-stu-id="1a935-257">Priority_s</span></span>| <span data-ttu-id="1a935-258">우선 순위</span><span class="sxs-lookup"><span data-stu-id="1a935-258">Priority</span></span>|
| <span data-ttu-id="1a935-259">Risk_s</span><span class="sxs-lookup"><span data-stu-id="1a935-259">Risk_s</span></span>| <span data-ttu-id="1a935-260">위험</span><span class="sxs-lookup"><span data-stu-id="1a935-260">Risk</span></span>|
| <span data-ttu-id="1a935-261">Impact_s</span><span class="sxs-lookup"><span data-stu-id="1a935-261">Impact_s</span></span>| <span data-ttu-id="1a935-262">영향</span><span class="sxs-lookup"><span data-stu-id="1a935-262">Impact</span></span>|
| <span data-ttu-id="1a935-263">RequestedDate_t</span><span class="sxs-lookup"><span data-stu-id="1a935-263">RequestedDate_t</span></span>  | <span data-ttu-id="1a935-264">요청한 날짜</span><span class="sxs-lookup"><span data-stu-id="1a935-264">Requested by date</span></span> |
| <span data-ttu-id="1a935-265">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="1a935-265">ClosedDate_t</span></span> | <span data-ttu-id="1a935-266">종결한 날짜</span><span class="sxs-lookup"><span data-stu-id="1a935-266">Closed date</span></span> |
| <span data-ttu-id="1a935-267">PlannedStartDate_t</span><span class="sxs-lookup"><span data-stu-id="1a935-267">PlannedStartDate_t</span></span>  |     <span data-ttu-id="1a935-268">예상된 시작 날짜</span><span class="sxs-lookup"><span data-stu-id="1a935-268">Planned start date</span></span> |
| <span data-ttu-id="1a935-269">PlannedEndDate_t</span><span class="sxs-lookup"><span data-stu-id="1a935-269">PlannedEndDate_t</span></span>  |   <span data-ttu-id="1a935-270">예상된 종료 날짜</span><span class="sxs-lookup"><span data-stu-id="1a935-270">Planned end date</span></span> |
| <span data-ttu-id="1a935-271">WorkStartDate_t</span><span class="sxs-lookup"><span data-stu-id="1a935-271">WorkStartDate_t</span></span>  | <span data-ttu-id="1a935-272">실제 시작 날짜</span><span class="sxs-lookup"><span data-stu-id="1a935-272">Actual start date</span></span> |
| <span data-ttu-id="1a935-273">WorkEndDate_t</span><span class="sxs-lookup"><span data-stu-id="1a935-273">WorkEndDate_t</span></span> | <span data-ttu-id="1a935-274">실제 종료 날짜</span><span class="sxs-lookup"><span data-stu-id="1a935-274">Actual end date</span></span>|
| <span data-ttu-id="1a935-275">Description_s</span><span class="sxs-lookup"><span data-stu-id="1a935-275">Description_s</span></span> | <span data-ttu-id="1a935-276">설명</span><span class="sxs-lookup"><span data-stu-id="1a935-276">Description</span></span> |
| <span data-ttu-id="1a935-277">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="1a935-277">Computer</span></span>  | <span data-ttu-id="1a935-278">구성 항목</span><span class="sxs-lookup"><span data-stu-id="1a935-278">Configuration Item</span></span> |

<span data-ttu-id="1a935-279">**ITSM 데이터에 대한 샘플 Log Analytics 화면:**</span><span class="sxs-lookup"><span data-stu-id="1a935-279">**Sample Log Analytics screen for ITSM data:**</span></span>

![Log Analytics 화면](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a><span data-ttu-id="1a935-281">IT Service Management Connector - 다른 OMS 솔루션과의 통합</span><span class="sxs-lookup"><span data-stu-id="1a935-281">IT Service Management connector – integration with other OMS solutions</span></span>

<span data-ttu-id="1a935-282">현재 IT Service Management Connector는 서비스 맵 솔루션과의 통합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-282">IT Service Management Connector, currently supports integration with the Service Map solution.</span></span>

<span data-ttu-id="1a935-283">서비스 맵은 Windows 및 Linux 시스템에서 응용 프로그램 구성 요소를 자동으로 검색하고 서비스 간 통신을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-283">Service Map automatically discovers the application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="1a935-284">따라서 생각처럼 중요한 서비스를 제공하는 상호 연결된 시스템으로 서버를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-284">It allows you to view your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="1a935-285">서비스 맵은 서버, 프로세스 및 에이전트 설치 이외에 구성이 필요 없는 TCP 연결 아키텍처의 포트 간 연결을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-285">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span> <span data-ttu-id="1a935-286">추가 정보: [서비스 맵](../operations-management-suite/operations-management-suite-service-map.md)</span><span class="sxs-lookup"><span data-stu-id="1a935-286">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="1a935-287">이 통합을 사용하면 다음 예제와 같이 ITSM 솔루션에서 만든 서비스 데스크 항목을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-287">With this integration, you can view the service desk items created in the ITSM solutions as shown in the following example:</span></span>

![<span data-ttu-id="1a935-288">통합된 솔루션</span><span class="sxs-lookup"><span data-stu-id="1a935-288">Integrated solution</span></span> ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a><span data-ttu-id="1a935-289">OMS 경고에 대한 ITSM 작업 항목 만들기</span><span class="sxs-lookup"><span data-stu-id="1a935-289">Create ITSM work items for OMS alerts</span></span>

<span data-ttu-id="1a935-290">OMS 경고의 경우 연결된 ITSM 원본에서 연결된 작업 항목을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-290">For the OMS alerts, you can create associated work items in the connected ITSM sources.</span></span>  <span data-ttu-id="1a935-291">이렇게 하려면 다음 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-291">To do this, use the following procedure:</span></span>

1. <span data-ttu-id="1a935-292">**로그 검색** 창에서 로그 검색 쿼리를 실행하여 데이터를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-292">From **Log Search** window, run a log search query to view data.</span></span> <span data-ttu-id="1a935-293">쿼리 결과는 작업 항목의 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-293">Query results are the source for work items.</span></span>
2. <span data-ttu-id="1a935-294">**로그 검색**에서 **경고**를 클릭하여 **경고 규칙 추가** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-294">In **Log Search**, click **Alert** to open the **Add Alert Rule** page.</span></span>

    ![Log Analytics 화면](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. <span data-ttu-id="1a935-296">**경고 규칙 추가** 창에서 **이름**, **심각도**, **검색 쿼리** 및 **경고 조건**(기간/메트릭 측정)에 대한 필수 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-296">On the **Add Alert Rule** window, provide the required details for **Name**, **Severity**,  **Search query**, and **Alert criteria** (Time Window/Metric measurement).</span></span>
4. <span data-ttu-id="1a935-297">**ITSM 작업**에 대해 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-297">Select **Yes** for **ITSM Actions**.</span></span>
5. <span data-ttu-id="1a935-298">**연결 선택** 목록에서 ITSM 연결을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-298">Select your ITSM connection from the **Select Connection** list.</span></span>
6. <span data-ttu-id="1a935-299">필요에 따라 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-299">Provide the details as required.</span></span>
7. <span data-ttu-id="1a935-300">이 경고의 각 로그 항목에 대해 별도 작업 항목을 만들려면 **각 로그 항목에 대해 개별 작업 항목 만들기** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-300">To create a separate work item for each log entry of this alert, select the **Create individual work items for each log entry** checkbox.</span></span>

    <span data-ttu-id="1a935-301">또는</span><span class="sxs-lookup"><span data-stu-id="1a935-301">Or</span></span>

    <span data-ttu-id="1a935-302">이 경고에서 제한없는 수의 로그 항목에 대해 하나의 작업 항목만 만들려면 이 확인란을 선택 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-302">leave this checkbox unselected to create only one work item for any number of log entries under this alert.</span></span>

7. <span data-ttu-id="1a935-303">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-303">Click **Save**.</span></span>

<span data-ttu-id="1a935-304">**경고** 아래에 OMS 경고가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-304">The OMS alert will be created under **Alerts**.</span></span> <span data-ttu-id="1a935-305">지정된 경고 조건이 충족되면 해당 ITSM 연결의 작업 항목이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-305">The corresponding ITSM connection's work items are created when the specified alert's condition is met.</span></span>

## <a name="create-itsm-work-items-from-oms-logs"></a><span data-ttu-id="1a935-306">OMS 로그에서 ITSM 작업 항목 만들기</span><span class="sxs-lookup"><span data-stu-id="1a935-306">Create ITSM work items from OMS logs</span></span>

<span data-ttu-id="1a935-307">OMS 로그 검색을 사용하여 연결된 ITSM 원본에서 작업 항목을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-307">You can create work items in the connected ITSM sources by using OMS Log Search.</span></span> <span data-ttu-id="1a935-308">이렇게 하려면 다음 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-308">To do this, use the following procedure:</span></span>

1. <span data-ttu-id="1a935-309">**로그 검색**에서 필요한 데이터를 검색하고 세부 정보를 선택한 후 **작업 항목 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-309">From **Log Search**,  search the required data, select the detail, and click **Create work item**.</span></span>

    <span data-ttu-id="1a935-310">**ITSM 작업 항목 만들기** 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-310">The **Create ITSM Work item** window appears:</span></span>

    ![Log Analytics 화면](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   <span data-ttu-id="1a935-312">다음 세부 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-312">Add the following details:</span></span>

  - <span data-ttu-id="1a935-313">**작업 항목 제목**: 작업 항목의 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-313">**Work item Title**: Title for the work item.</span></span>
  - <span data-ttu-id="1a935-314">**작업 항목 설명**: 새 작업 항목에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-314">**Work item Description**: Description for the new work item.</span></span>
  - <span data-ttu-id="1a935-315">**영향을 받는 컴퓨터**: 이 로그 데이터가 있는 컴퓨터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-315">**Affected Computer**: Name of the computer where this log data was found.</span></span>
  - <span data-ttu-id="1a935-316">**연결 선택**: 이 작업 항목을 만들려는 ITSM 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-316">**Select Connection**:  ITSM connection in which you want to create this work item.</span></span>
  - <span data-ttu-id="1a935-317">**작업 항목**: 작업 항목의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-317">**Work item**:  Type of work item.</span></span>

3. <span data-ttu-id="1a935-318">인시던트에 대한 기존 작업 항목 템플릿을 사용하려면 **템플릿을 기준으로 작업 항목 생성** 옵션에서 **예**를 클릭한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-318">To use an existing work item template for an incident, click **Yes** under **Generate work item based on the template** option and then click **Create**.</span></span>

    <span data-ttu-id="1a935-319">또는</span><span class="sxs-lookup"><span data-stu-id="1a935-319">Or,</span></span>

    <span data-ttu-id="1a935-320">사용자 지정한 값을 제공하려는 경우 **아니요**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-320">Click **No** if you want to provide your customized values.</span></span>

4. <span data-ttu-id="1a935-321">**연락처 유형**, **영향**, **긴급도**, **범주** 및 **하위 범주** 텍스트 상자에 적절한 값을 입력하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-321">Provide the appropriate values in the **Contact Type**, **Impact**, **Urgency**, **Category**, and **Sub Category** text boxes, and then click **Create**.</span></span>

<span data-ttu-id="1a935-322">ITSM에 작업 항목이 생성됩니다. 이 항목은 OMS에서도 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-322">The work item will be created in the ITSM, which you can also view in OMS.</span></span>

## <a name="troubleshoot-itsm-connections-in-oms"></a><span data-ttu-id="1a935-323">OMS에서 ITSM 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="1a935-323">Troubleshoot ITSM connections in OMS</span></span>
1.  <span data-ttu-id="1a935-324">연결된 원본의 UI에서 연결에 실패하고 **연결을 저장하는 동안 오류 발생** 메시지가 나타나는 경우 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-324">If connection fails from connected source's UI and you get the **Error in saving connection** message, do the following:</span></span>
 - <span data-ttu-id="1a935-325">ServiceNow, Cherwell 및 Provance 연결의 경우 각 연결에 대한 사용자 이름/암호 및 클라이언트 ID/클라이언트 암호를 올바르게 입력했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-325">In case of ServiceNow, Cherwell and Provance connections, ensure you correctly entered  the username/password and  client ID/client secret  for each of the connections.</span></span> <span data-ttu-id="1a935-326">오류가 계속되면 해당 ITSM 제품에서 연결을 설정할 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-326">If the error persists, check if you have sufficient privileges  in the corresponding ITSM product to make the connection.</span></span>
 - <span data-ttu-id="1a935-327">Service Manager의 웹앱이 배포되고 하이브리드 연결이 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-327">In case of Service Manager, ensure that the Web app is successfully deployed and hybrid connection is created.</span></span> <span data-ttu-id="1a935-328">온-프레미스 Service Manager 컴퓨터와의 연결이 성공적으로 설정되었는지 확인하려면 [하이브리드 연결](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) 설정 설명서에 따라 웹앱 URL을 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-328">To verify the connection is successfully established with the on-prem Service Manager machine, visit the  Web app URL as detailed in the documentation for making the [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>

2.  <span data-ttu-id="1a935-329">OMS에서 ServiceNow의 데이터가 동기화되지 않는 경우 ServiceNow 인스턴스가 중지 중이지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-329">If data from ServiceNow is not getting synced in OMS, ensure that the ServiceNow instance is not sleeping.</span></span> <span data-ttu-id="1a935-330">이는 유휴 상태일 때 ServiceNow Dev 인스턴스에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-330">This might sometime happen in the ServiceNow Dev instances, when idle.</span></span> <span data-ttu-id="1a935-331">다른 문제를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-331">Else, report the issue.</span></span>
3.  <span data-ttu-id="1a935-332">OMS에서 경고를 실행되지만 ITSM에서 작업 항목이 생성되지 않거나 구성 항목이 생성/작업 항목에 연결되지 않는 경우 또는 일반적인 정보가 필요한 경우 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-332">If Alerts are getting fired from OMS but work items are not getting created in ITSM product or configuration items are not getting created/linked to work items or for any generic information, do the following:</span></span>
 -  <span data-ttu-id="1a935-333">OMS 포털의 IT Service Management Connector 솔루션을 사용하여 연결/작업 항목/컴퓨터 등에 대한 요약을 가져올 수 있습니다. 상태 블레이드에서 오류 메시지를 클릭하고 **로그 검색**으로 이동한 후 오류 메시지의 세부 정보를 사용하여 오류가 있는 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-333">IT Service Management Connector solution in OMS portal could be used to get a summary of connections/work items/computers etc. Click the error message in the status blade, navigate to **Log Search** and view the connection that has the error by using the details in the error message.</span></span>
 - <span data-ttu-id="1a935-334">*Type=ServiceDeskLog_CL*을 사용하여 **로그 검색** 페이지에서 오류/관련 정보를 직접 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-334">you can directly view the errors/related information in the **Log Search** page using *Type=ServiceDeskLog_CL*.</span></span>

## <a name="troubleshoot-service-manager-web-app-deployment"></a><span data-ttu-id="1a935-335">Service Manager 웹앱 배포 문제 해결</span><span class="sxs-lookup"><span data-stu-id="1a935-335">Troubleshoot Service Manager Web App deployment</span></span>
1.  <span data-ttu-id="1a935-336">웹앱 배포 문제가 발생한 경우 구독에 리소스 생성/배포 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-336">In case of any trouble with web app deployment, ensure you have sufficient permissions in the subscription mentioned to create/deploy resources.</span></span>
2.  <span data-ttu-id="1a935-337">[스크립트](log-analytics-itsmc-service-manager-script.md)를 실행하는 동안 **개체 참조가 개체의 인스턴스로 설정되지 않음** 오류 메시지가 나타나는 경우 **사용자 구성** 섹션에서 올바른 값을 입력했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-337">If **Object reference not set to instance of an object** error message appears while running the [script](log-analytics-itsmc-service-manager-script.md) ensure that you entered valid values  under **User Configuration** section.</span></span>
3.  <span data-ttu-id="1a935-338">Service Bus Relay 네임스페이스 만들기에 실패한 경우 구독에 필요한 리소스 공급자가 등록되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-338">If you fail to create service bus relay namespace, ensure that the required resource provider is registered in the subscription.</span></span> <span data-ttu-id="1a935-339">등록되지 않은 경우 Azure Portal에서 수동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-339">If not registered, manually create it from the Azure portal.</span></span> <span data-ttu-id="1a935-340">Azure Portal에서 [하이브리드 연결을 만드는](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) 동안 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a935-340">You can also create it while [creating the hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from the Azure portal.</span></span>


## <a name="contact-us"></a><span data-ttu-id="1a935-341">문의처</span><span class="sxs-lookup"><span data-stu-id="1a935-341">Contact us</span></span>

<span data-ttu-id="1a935-342">IT Service Management Connector에 대해 질문이나 의견이 있는 경우 [omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com)으로 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="1a935-342">For any queries or feedback on the IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a935-343">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1a935-343">Next steps</span></span>
<span data-ttu-id="1a935-344">[ITSM 제품/서비스를 IT Service Management Connector에 추가](log-analytics-itsmc-connections.md).</span><span class="sxs-lookup"><span data-stu-id="1a935-344">[Add ITSM products/services to IT Service Management Connector](log-analytics-itsmc-connections.md).</span></span>
