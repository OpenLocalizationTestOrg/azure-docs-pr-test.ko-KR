---
title: "Log Analytics에 Operations Manager 연결 | Microsoft Docs"
description: "System Center Operations Manager의 기존 투자를 유지 관리하고 Log Analytics로 확장된 기능을 사용하려면 OMS 작업 영역으로 Operations Manager를 통합할 수 있습니다."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 245ef71e-15a2-4be8-81a1-60101ee2f6e6
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: magoedte
ms.openlocfilehash: bcfffe05dbce2824ea4933997865e8c7e86610b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-operations-manager-to-log-analytics"></a><span data-ttu-id="9974c-103">Log Analytics에 Operations Manager 연결</span><span class="sxs-lookup"><span data-stu-id="9974c-103">Connect Operations Manager to Log Analytics</span></span>
<span data-ttu-id="9974c-104">System Center Operations Manager의 기존 투자를 유지 관리하고 Log Analytics로 확장된 기능을 사용하려면 OMS 작업 영역으로 Operations Manager를 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-104">To maintain your existing investment in System Center Operations Manager and use extended capabilities with Log Analytics, you can integrate Operations Manager with your OMS workspace.</span></span>  <span data-ttu-id="9974c-105">이렇게 하면 Operations Manager를 계속해서 사용하는 동안 OMS의 기회를 활용하여 다음 작업을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-105">This allows you leverage the opportunities of OMS while continuing to use Operations Manager to:</span></span>

* <span data-ttu-id="9974c-106">Operations Manager를 사용하여 IT 서비스의 상태 모니터링 계속</span><span class="sxs-lookup"><span data-stu-id="9974c-106">Continue monitoring the health of your IT services with Operations Manager</span></span>
* <span data-ttu-id="9974c-107">인시던트 및 문제 관리를 지원하는 ITSM 솔루션과 통합 유지 관리</span><span class="sxs-lookup"><span data-stu-id="9974c-107">Maintain integration with your ITSM solutions supporting incident and problem management</span></span>
* <span data-ttu-id="9974c-108">온-프레미스 및 Operations Manager로 모니터링하는 공용 클라우드 IaaS 가상 컴퓨터에 배포된 에이전트의 수명 주기 관리</span><span class="sxs-lookup"><span data-stu-id="9974c-108">Manage the lifecycle of agents deployed to on-premises and public cloud IaaS virtual machines that you monitor with Operations Manager</span></span>

<span data-ttu-id="9974c-109">System Center Operations Manager와 통합하면 Operations Manager에서 데이터 수집, 저장 및 분석에 OMS의 속도 및 효율성을 사용하여 서비스 작업 전략에 값이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-109">Integrating with System Center Operations Manager adds value to your service operations strategy by using the speed and efficiency of OMS in collecting, storing, and analyzing data from Operations Manager.</span></span>  <span data-ttu-id="9974c-110">OMS를 통해 기존 문제 관리 프로세스를 지원하기 위해 오류 문제를 식별하고 재발을 표시하도록 상호 연결하고 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-110">OMS helps correlate and work towards identifying the faults of problems and surfacing recurrences in support of your existing problem management process.</span></span>   <span data-ttu-id="9974c-111">의미 있는 방식으로 이 데이터를 노출하는 다양한 대시보드 및 보고 기능으로 성능, 이벤트 및 경고 데이터를 검사하는 검색 엔진의 유연성은 Operations Manager를 제공하는 OMS의 강점을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-111">The flexibility of the search engine to examine performance, event and alert data, with rich dashboards and reporting capabilities to expose this data in meaningful ways, demonstrates the strength OMS brings in complimenting Operations Manager.</span></span>

<span data-ttu-id="9974c-112">Operations Manager 관리 그룹에 대한 에이전트 보고는 Log Analytics 데이터 원본 및 OMS 구독에서 활성화한 솔루션에 기반한 서버에서 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-112">The agents reporting to the Operations Manager management group collect data from your servers based on the Log Analytics data sources and solutions you have enabled in your OMS subscription.</span></span>  <span data-ttu-id="9974c-113">활성화한 솔루션에 따라 이러한 솔루션의 데이터는 Operations Manager 관리 서버에서 OMS 웹 서비스로 직접 전송되거나 에이전트 관리 시스템에서 수집된 데이터의 양으로 인해 에이전트에서 OMS 웹 서비스로 직접 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-113">Depending on the solution you have enabled, data from these solutions are either sent directly from an Operations Manager management server to the OMS web service, or because of the volume of data collected on the agent-managed system, are sent directly from the agent to OMS web service.</span></span> <span data-ttu-id="9974c-114">관리 서버는 OMS 데이터를 OMS 웹 서비스에 직접 전달하며 OperationsManager 또는 OperationsManagerDW 데이터베이스에 작성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-114">The management server forwards the OMS data directly to the OMS web service; it is never written to the OperationsManager or OperationsManagerDW database.</span></span>  <span data-ttu-id="9974c-115">관리 서버는 OMS 웹 서비스와의 연결이 끊어지더라도 통신이 OMS와 다시 설정될 때까지 데이터를 로컬로 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-115">When a management server loses connectivity with the OMS web service, it caches the data locally until communication is re-established with OMS.</span></span>  <span data-ttu-id="9974c-116">관리 서버가 계획된 유지 관리 또는 계획되지 않은 중단으로 인해 오프라인 상태인 경우 관리 그룹의 다른 관리 서버에서 OMS와의 연결을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-116">If the management server is offline due to planned maintenance or unplanned outage, another management server in the management group resumes connectivity with OMS.</span></span>  

<span data-ttu-id="9974c-117">다음 다이어그램은 방향, 포트를 포함하여 System Center Operations Manager 관리 그룹과 OMS에서 관리 서버와 에이전트 간 연결을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-117">The following diagram depicts the connection between the management servers and agents in a System Center Operations Manager management group and OMS, including the direction and ports.</span></span>   

![oms-operations-manager-integration-diagram](./media/log-analytics-om-agents/oms-operations-manager-connection.png)

<span data-ttu-id="9974c-119">IT 보안 정책이 네트워크의 컴퓨터가 인터넷에 연결하도록 허용하지 않을 경우 OMS 게이트웨이에 연결하여 구성 정보를 받고 사용하도록 설정한 솔루션에 따라 수집된 데이터를 보내도록 관리 서버를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-119">If your IT security policies do not allow computers on your network to connect to the Internet, management servers can be configured to connect to the OMS Gateway to receive configuration information and send collected data depending on the solution you have enabled.</span></span>  <span data-ttu-id="9974c-120">Operations Manager 관리 그룹이 OMS 게이트웨이를 통해 OMS 서비스와 통신할 수 있도록 구성하는 방법에 대한 자세한 정보 및 단계에 대해서는 [OMS 게이트웨이 사용하여 OMS에 컴퓨터 연결](log-analytics-oms-gateway.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9974c-120">For more information and steps on how to configure your Operations Manager management group to communicate through an OMS Gateway to the OMS service, see [Connect computers to OMS using the OMS Gateway](log-analytics-oms-gateway.md).</span></span>  

## <a name="system-requirements"></a><span data-ttu-id="9974c-121">시스템 요구 사항</span><span class="sxs-lookup"><span data-stu-id="9974c-121">System requirements</span></span>
<span data-ttu-id="9974c-122">시작하기 전에 다음 세부 정보를 검토하여 필수 구성 요소를 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-122">Before starting, review the following details to verify you meet prerequisites.</span></span>

* <span data-ttu-id="9974c-123">OMS는 Operations Manager 2016, Operations Manager 2012 SP1 UR6 이상 및 Operations Manager 2012 R2 UR2 이상만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-123">OMS only supports Operations Manager 2016, Operations Manager 2012 SP1 UR6 and greater, and Operations Manager 2012 R2 UR2 and greater.</span></span>  <span data-ttu-id="9974c-124">프록시 지원은 Operations Manager 2012 SP1 UR7 및 Operations Manager 2012 R2 UR3에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-124">Proxy support was added in Operations Manager 2012 SP1 UR7 and Operations Manager 2012 R2 UR3.</span></span>
* <span data-ttu-id="9974c-125">모든 Operations Manager 에이전트는 최소 지원 요구 사항을 만족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-125">All Operations Manager agents must meet minimum support requirements.</span></span> <span data-ttu-id="9974c-126">에이전트가 최소 업데이트를 따르고 있는지 확인하고, 그렇지 않은 경우 Windows 에이전트 트래픽이 실패하고 많은 오류가 Operations Manager 이벤트 로그를 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-126">Ensure that agents are at the minimum update, otherwise Windows agent traffic may fail and many errors might fill the Operations Manager event log.</span></span>
* <span data-ttu-id="9974c-127">OMS 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-127">An OMS subscription.</span></span>  <span data-ttu-id="9974c-128">자세한 내용은 [Log Analytics 시작](log-analytics-get-started.md)을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-128">For further information, review [Get started with Log Analytics](log-analytics-get-started.md).</span></span>

### <a name="network"></a><span data-ttu-id="9974c-129">네트워크</span><span class="sxs-lookup"><span data-stu-id="9974c-129">Network</span></span>
<span data-ttu-id="9974c-130">아래 정보는 Operations Manager 에이전트, 관리 서버 및 운영 콘솔이 OMS와 통신하는 데 필요한 프록시 및 방화벽 구성 정보를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-130">The information below list the proxy and firewall configuration information required for the Operations Manager agent, management servers, and Operations console to communicate with OMS.</span></span>  <span data-ttu-id="9974c-131">각 구성 요소의 트래픽은 네트워크에서 OMS 서비스로 아웃바운드됩니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-131">Traffic from each component is outbound from your network to the OMS service.</span></span>     

|<span data-ttu-id="9974c-132">리소스</span><span class="sxs-lookup"><span data-stu-id="9974c-132">Resource</span></span> | <span data-ttu-id="9974c-133">포트 번호</span><span class="sxs-lookup"><span data-stu-id="9974c-133">Port number</span></span>| <span data-ttu-id="9974c-134">HTTP 검사 무시</span><span class="sxs-lookup"><span data-stu-id="9974c-134">Bypass HTTP Inspection</span></span>|  
|---------|------|-----------------------|  
|<span data-ttu-id="9974c-135">**에이전트**</span><span class="sxs-lookup"><span data-stu-id="9974c-135">**Agent**</span></span>|||  
|<span data-ttu-id="9974c-136">\*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="9974c-136">\*.ods.opinsights.azure.com</span></span>| <span data-ttu-id="9974c-137">443</span><span class="sxs-lookup"><span data-stu-id="9974c-137">443</span></span> |<span data-ttu-id="9974c-138">예</span><span class="sxs-lookup"><span data-stu-id="9974c-138">Yes</span></span>|  
|<span data-ttu-id="9974c-139">\*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="9974c-139">\*.oms.opinsights.azure.com</span></span>| <span data-ttu-id="9974c-140">443</span><span class="sxs-lookup"><span data-stu-id="9974c-140">443</span></span>|<span data-ttu-id="9974c-141">예</span><span class="sxs-lookup"><span data-stu-id="9974c-141">Yes</span></span>|  
|<span data-ttu-id="9974c-142">\*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="9974c-142">\*.blob.core.windows.net</span></span>| <span data-ttu-id="9974c-143">443</span><span class="sxs-lookup"><span data-stu-id="9974c-143">443</span></span>|<span data-ttu-id="9974c-144">예</span><span class="sxs-lookup"><span data-stu-id="9974c-144">Yes</span></span>|  
|<span data-ttu-id="9974c-145">\*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="9974c-145">\*.azure-automation.net</span></span>| <span data-ttu-id="9974c-146">443</span><span class="sxs-lookup"><span data-stu-id="9974c-146">443</span></span>|<span data-ttu-id="9974c-147">예</span><span class="sxs-lookup"><span data-stu-id="9974c-147">Yes</span></span>|  
|<span data-ttu-id="9974c-148">**관리 서버**</span><span class="sxs-lookup"><span data-stu-id="9974c-148">**Management server**</span></span>|||  
|<span data-ttu-id="9974c-149">\*.service.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="9974c-149">\*.service.opinsights.azure.com</span></span>| <span data-ttu-id="9974c-150">443</span><span class="sxs-lookup"><span data-stu-id="9974c-150">443</span></span>||  
|<span data-ttu-id="9974c-151">\*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="9974c-151">\*.blob.core.windows.net</span></span>| <span data-ttu-id="9974c-152">443</span><span class="sxs-lookup"><span data-stu-id="9974c-152">443</span></span>| <span data-ttu-id="9974c-153">예</span><span class="sxs-lookup"><span data-stu-id="9974c-153">Yes</span></span>|  
|<span data-ttu-id="9974c-154">\*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="9974c-154">\*.ods.opinsights.azure.com</span></span>| <span data-ttu-id="9974c-155">443</span><span class="sxs-lookup"><span data-stu-id="9974c-155">443</span></span>| <span data-ttu-id="9974c-156">예</span><span class="sxs-lookup"><span data-stu-id="9974c-156">Yes</span></span>|  
|<span data-ttu-id="9974c-157">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="9974c-157">*.azure-automation.net</span></span> | <span data-ttu-id="9974c-158">443</span><span class="sxs-lookup"><span data-stu-id="9974c-158">443</span></span>| <span data-ttu-id="9974c-159">예</span><span class="sxs-lookup"><span data-stu-id="9974c-159">Yes</span></span>|  
|<span data-ttu-id="9974c-160">**OMS에 대한 Operations Manager 콘솔**</span><span class="sxs-lookup"><span data-stu-id="9974c-160">**Operations Manager console to OMS**</span></span>|||  
|<span data-ttu-id="9974c-161">service.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="9974c-161">service.systemcenteradvisor.com</span></span>| <span data-ttu-id="9974c-162">443</span><span class="sxs-lookup"><span data-stu-id="9974c-162">443</span></span>||  
|<span data-ttu-id="9974c-163">\*.service.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="9974c-163">\*.service.opinsights.azure.com</span></span>| <span data-ttu-id="9974c-164">443</span><span class="sxs-lookup"><span data-stu-id="9974c-164">443</span></span>||  
|<span data-ttu-id="9974c-165">\*.live.com</span><span class="sxs-lookup"><span data-stu-id="9974c-165">\*.live.com</span></span>| <span data-ttu-id="9974c-166">80 및 443</span><span class="sxs-lookup"><span data-stu-id="9974c-166">80 and 443</span></span>||  
|<span data-ttu-id="9974c-167">\*.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="9974c-167">\*.microsoft.com</span></span>| <span data-ttu-id="9974c-168">80 및 443</span><span class="sxs-lookup"><span data-stu-id="9974c-168">80 and 443</span></span>||  
|<span data-ttu-id="9974c-169">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="9974c-169">\*.microsoftonline.com</span></span>| <span data-ttu-id="9974c-170">80 및 443</span><span class="sxs-lookup"><span data-stu-id="9974c-170">80 and 443</span></span>||  
|<span data-ttu-id="9974c-171">\*.mms.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="9974c-171">\*.mms.microsoft.com</span></span>| <span data-ttu-id="9974c-172">80 및 443</span><span class="sxs-lookup"><span data-stu-id="9974c-172">80 and 443</span></span>||  
|<span data-ttu-id="9974c-173">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="9974c-173">login.windows.net</span></span>| <span data-ttu-id="9974c-174">80 및 443</span><span class="sxs-lookup"><span data-stu-id="9974c-174">80 and 443</span></span>||  


## <a name="connecting-operations-manager-to-oms"></a><span data-ttu-id="9974c-175">OMS에 Operations Manager 연결</span><span class="sxs-lookup"><span data-stu-id="9974c-175">Connecting Operations Manager to OMS</span></span>
<span data-ttu-id="9974c-176">Operations Manager 관리 그룹을 구성하도록 다음과 같은 일련의 단계를 수행하여 OMS 작업 영역 중 하나에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-176">Perform the following series of steps to configure your Operations Manager management group to connect to one of your OMS workspaces.</span></span>

1. <span data-ttu-id="9974c-177">Operations Manager 콘솔에서 **관리** 작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-177">In the Operations Manager console, select the **Administration** workspace.</span></span>
2. <span data-ttu-id="9974c-178">Operations Management Suite 노드를 확장하고 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-178">Expand the Operations Management Suite node and click **Connection**.</span></span>
3. <span data-ttu-id="9974c-179">**Operations Management Suite에 등록** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-179">Click the **Register to Operations Management Suite** link.</span></span>
4. <span data-ttu-id="9974c-180">**Operations Management Suite 등록 마법사: 인증** 페이지에서 OMS 구독과 연결된 관리자 계정의 전자 메일 주소 또는 전화 번호와 암호를 입력하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-180">On the **Operations Management Suite Onboarding Wizard: Authentication** page, enter the email address or phone number and password of the administrator account that is associated with your OMS subscription, and click **Sign in**.</span></span>
5. <span data-ttu-id="9974c-181">성공적으로 인증된 후에 **Operations Management Suite 등록 마법사: 작업 영역 선택** 페이지에 OMS 작업 영역을 선택하라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-181">After you are successfully authenticated, on the **Operations Management Suite Onboarding Wizard: Select Workspace** page, you are prompted to select your OMS workspace.</span></span>  <span data-ttu-id="9974c-182">둘 이상의 작업 영역이 있는 경우 드롭다운 목록에서 Operations Manager 관리 그룹으로 등록하려는 작업 영역을 선택한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-182">If you have more than one workspace, select the workspace you want to register with the Operations Manager management group from the drop-down list, and then click **Next**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9974c-183">Operations Manager는 한 번에 하나의 OMS 작업 영역을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-183">Operations Manager only supports one OMS workspace at a time.</span></span> <span data-ttu-id="9974c-184">이전 작업 영역으로 OMS에 등록된 연결 및 컴퓨터는 OMS에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-184">The connection and the computers that were registered to OMS with the previous workspace are removed from OMS.</span></span>
   > 
   > 
6. <span data-ttu-id="9974c-185">**Operations Management Suite 등록 마법사: 요약** 페이지에서 설정을 확인하고 올바른 경우 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-185">On the **Operations Management Suite Onboarding Wizard: Summary** page, confirm your settings and if they are correct, click **Create**.</span></span>
7. <span data-ttu-id="9974c-186">**Operations Management Suite 등록 마법사: 마침** 페이지에서 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-186">On the **Operations Management Suite Onboarding Wizard: Finish** page, click **Close**.</span></span>

### <a name="add-agent-managed-computers"></a><span data-ttu-id="9974c-187">에이전트 관리 컴퓨터 추가</span><span class="sxs-lookup"><span data-stu-id="9974c-187">Add agent-managed computers</span></span>
<span data-ttu-id="9974c-188">OMS 작업 영역과 통합을 구성한 후 OMS와의 연결을 설정하고 에이전트 보고에서 관리 그룹으로 데이터가 수집되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-188">After configuring integration with your OMS workspace, this only establishes a connection with OMS, no data is collected from the agents reporting to your management group.</span></span> <span data-ttu-id="9974c-189">이는 Log Analytics에 대한 데이터를 수집할 특정 에이전트 관리 컴퓨터를 구성할 때까지 일어나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-189">This won’t happen until after you configure which specific agent-managed computers collects data for Log Analytics.</span></span> <span data-ttu-id="9974c-190">컴퓨터 개체를 개별적으로 선택하거나 Windows 컴퓨터 개체를 포함하는 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-190">You can either select the computer objects individually or you can select a group that contains Windows computer objects.</span></span> <span data-ttu-id="9974c-191">논리 디스크 또는 SQL 데이터베이스와 같은 다른 클래스의 인스턴스를 포함하는 그룹을 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-191">You cannot select a group that  contains instances of another class, such as logical disks or SQL databases.</span></span>

1. <span data-ttu-id="9974c-192">Operations Manager 콘솔을 열고 **관리** 작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-192">Open the Operations Manager console and select the **Administration** workspace.</span></span>
2. <span data-ttu-id="9974c-193">Operations Management Suite 노드를 확장하고 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-193">Expand the Operations Management Suite node and click **Connection**.</span></span>
3. <span data-ttu-id="9974c-194">창 오른쪽 작업 제목 아래의 **컴퓨터/그룹 추가** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-194">Click the **Add a Computer/Group** link under the Actions heading on the right-side of the pane.</span></span>
4. <span data-ttu-id="9974c-195">**컴퓨터 검색** 대화 상자에서, Operations Manager에서 모니터링하는 컴퓨터 또는 그룹을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-195">In the **Computer Search** dialog box, you can search for computers or groups monitored by Operations Manager.</span></span> <span data-ttu-id="9974c-196">OMS에 등록할 컴퓨터 또는 그룹을 선택하고 **추가**를 클릭한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-196">Select computers or groups to onboard to OMS, click **Add**, and then click **OK**.</span></span>

<span data-ttu-id="9974c-197">운영 콘솔의 **관리** 작업 영역에서 Operations Management Suite 아래의 관리되는 컴퓨터 노드에서 데이터를 수집하도록 구성된 컴퓨터 및 그룹을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-197">You can view computers and groups configured to collect data from the Managed Computers node under Operations Management Suite in the **Administration** workspace of the Operations console.</span></span>  <span data-ttu-id="9974c-198">여기에서 필요에 따라 컴퓨터 및 그룹을 추가하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-198">From here, you can add or remove computers and groups as necessary.</span></span>

### <a name="configure-oms-proxy-settings-in-the-operations-console"></a><span data-ttu-id="9974c-199">운영 콘솔에서 OMS 프록시 설정 구성</span><span class="sxs-lookup"><span data-stu-id="9974c-199">Configure OMS proxy settings in the Operations console</span></span>
<span data-ttu-id="9974c-200">내부 프록시 서버가 관리 그룹 및 OMS 웹 서비스 사이에 있는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-200">Perform the following steps if an internal proxy server is between the management group and OMS web service.</span></span>  <span data-ttu-id="9974c-201">이러한 설정은 관리 그룹에서 중앙 집중식으로 관리되며 OMS에 대한 데이터를 수집하는 범위에 포함된 에이전트 관리 시스템에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-201">These settings are centrally managed from the management group and distributed to agent-managed systems that are included in the scope to collect data for OMS.</span></span>  <span data-ttu-id="9974c-202">이는 특정 솔루션이 관리 서버를 우회하고 데이터를 OMS 웹 서비스에 직접 보낼 때 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-202">This is beneficial for when certain solutions bypass the management server and send data directly to OMS web service.</span></span>

1. <span data-ttu-id="9974c-203">Operations Manager 콘솔을 열고 **관리** 작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-203">Open the Operations Manager console and select the **Administration** workspace.</span></span>
2. <span data-ttu-id="9974c-204">Operations Management Suite를 확장한 다음 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-204">Expand Operations Management Suite, and then click **Connections**.</span></span>
3. <span data-ttu-id="9974c-205">OMS 연결 보기에서 **프록시 서버 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-205">In the OMS Connection view, click **Configure Proxy Server**.</span></span>
4. <span data-ttu-id="9974c-206">**Operations Management Suite 마법사: 프록시 서버** 페이지에서 **프록시 서버를 사용하여 Operations Management Suite에 액세스**를 선택하고 포트 번호와 함께 URL을 입력(예: http://corpproxy:80 )한 다음 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-206">On **Operations Management Suite Wizard: Proxy Server** page, select **Use a proxy server to access the Operations Management Suite**, and then type the URL with the port number, for example, http://corpproxy:80 and then click **Finish**.</span></span>

<span data-ttu-id="9974c-207">프록시 서버에 인증이 필요한 경우 다음 단계를 수행하여 관리 그룹에서 OMS에 보고하는 관리되는 컴퓨터에 전파해야 하는 자격 증명 및 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-207">If your proxy server requires authentication, perform the following steps to configure credentials and settings that need to propagate to managed computers that reports to OMS in the management group.</span></span>

1. <span data-ttu-id="9974c-208">Operations Manager 콘솔을 열고 **관리** 작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-208">Open the Operations Manager console and select the **Administration** workspace.</span></span>
2. <span data-ttu-id="9974c-209">**RunAs 구성**에서 **프로필**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-209">Under **RunAs Configuration**, select **Profiles**.</span></span>
3. <span data-ttu-id="9974c-210">**프로필 프록시로 시스템 센터 관리자 실행** 프로필을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-210">Open the **System Center Advisor Run As Profile Proxy** profile.</span></span>
4. <span data-ttu-id="9974c-211">실행 프로필 마법사에서 추가를 클릭하여 실행 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-211">In the Run As Profile Wizard, click Add to use a Run As account.</span></span> <span data-ttu-id="9974c-212">[실행 계정](https://technet.microsoft.com/library/hh321655.aspx)을 만들거나 기존 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-212">You can create a [Run As account](https://technet.microsoft.com/library/hh321655.aspx) or use an existing account.</span></span> <span data-ttu-id="9974c-213">이 계정에는 프록시 서버를 통과할 수 있는 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-213">This account needs to have sufficient permissions to pass through the proxy server.</span></span>
5. <span data-ttu-id="9974c-214">관리할 계정을 설정하려면 **선택된 클래스, 그룹 또는 개체**를 선택하고 **선택...**을 클릭한 다음</span><span class="sxs-lookup"><span data-stu-id="9974c-214">To set the account to manage, choose **A selected class, group, or object**, click **Select…**</span></span> <span data-ttu-id="9974c-215">**그룹...**을 클릭하여</span><span class="sxs-lookup"><span data-stu-id="9974c-215">and then click **Group…**</span></span> <span data-ttu-id="9974c-216">**그룹 검색** 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-216">to open the **Group Search** box.</span></span>
6. <span data-ttu-id="9974c-217">**Microsoft System Center Advisor 모니터링 서버 그룹**을 검색한 다음 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-217">Search for and then select **Microsoft System Center Advisor Monitoring Server Group**.</span></span>  <span data-ttu-id="9974c-218">그룹을 선택한 후 **확인**을 클릭하여 **그룹 검색** 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-218">Click **OK** after selecting the group to close the **Group Search** box.</span></span>
7. <span data-ttu-id="9974c-219">**확인**을 클릭하여 **실행 계정 추가** 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-219">Click **OK** to close the **Add a Run As account** box.</span></span>
8. <span data-ttu-id="9974c-220">**저장** 을 클릭하여 마법사를 완료하고 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-220">Click **Save** to complete the wizard and save your changes.</span></span>

<span data-ttu-id="9974c-221">연결이 만들어지고 OMS에 데이터를 수집 및 보고할 에이전트를 구성한 후 다음 구성이 관리 그룹 순서에 관계 없이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-221">After the connection is created and you configure which agents will collect and report data to OMS, the following configuration is applied in the management group, not necessarily in order:</span></span>

* <span data-ttu-id="9974c-222">실행 계정 **Microsoft.SystemCenter.Advisor.RunAsAccount.Certificate** 가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-222">The Run As Account **Microsoft.SystemCenter.Advisor.RunAsAccount.Certificate** is created.</span></span>  <span data-ttu-id="9974c-223">이 계정은 실행 프로필 **Microsoft System Center Advisor Run As Profile Blob**과 연결되고 두 개의 클래스 **수집 서버** 및 **Operations Manager 관리 그룹**을 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-223">It is associated with the Run As profile **Microsoft System Center Advisor Run As Profile Blob** and is targeting two classes - **Collection Server** and **Operations Manager Management Group**.</span></span>
* <span data-ttu-id="9974c-224">두 개의 커넥터가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-224">Two connectors are created.</span></span>  <span data-ttu-id="9974c-225">첫 번째는 **Microsoft.SystemCenter.Advisor.DataConnector**로 이름이 지정되고 관리 그룹에 있는 모든 클래스의 인스턴스에서 생성된 모든 경고를 OMS Log Analytics로 전달하는 구독으로 자동으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-225">The first is named **Microsoft.SystemCenter.Advisor.DataConnector** and is automatically configured with a subscription that forwards all alerts generated from instances of all classes in the management group to OMS Log Analytics.</span></span> <span data-ttu-id="9974c-226">두 번째 커넥터는 **Advisor Connector**이며 OMS 웹 서비스와 통신하고 데이터를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-226">The second connector is **Advisor Connector**, which is responsible for communicating with OMS web service and sharing data.</span></span>
* <span data-ttu-id="9974c-227">관리 그룹에서 데이터를 수집하도록 선택한 에이전트 및 그룹은 **Microsoft System Center Advisor 모니터링 서버 그룹**에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-227">Agents and groups that you have selected to collect data in the management group is added to the **Microsoft System Center Advisor Monitoring Server Group**.</span></span>

## <a name="management-pack-updates"></a><span data-ttu-id="9974c-228">관리 팩 업데이트</span><span class="sxs-lookup"><span data-stu-id="9974c-228">Management pack updates</span></span>
<span data-ttu-id="9974c-229">구성이 완료되면 Operations Manager 관리 그룹에서 OMS 서비스와의 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-229">After configuration is completed, the Operations Manager management group establishes a connection with the OMS service.</span></span>  <span data-ttu-id="9974c-230">관리 서버는 웹 서비스와 동기화하고 Operations Manager와 통합하도록 활성화한 솔루션에 대한 관리 팩의 형태로 업데이트된 구성 정보를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-230">The management server synchronizes with the web service and receive updated configuration information in the form of management packs for the solutions you have enabled that integrate with Operations Manager.</span></span>   <span data-ttu-id="9974c-231">Operations Manager는 이러한 관리 팩의 업데이트를 확인하고 사용할 수 있을 때 자동으로 다운로드하고 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-231">Operations Manager  checks for updates of these management packs and automatically download and imports them when they’re available.</span></span>  <span data-ttu-id="9974c-232">특히 이 동작을 제어하는 두 개의 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-232">There are two rules in particular which control this behavior:</span></span>

* <span data-ttu-id="9974c-233">**Microsoft.SystemCenter.Advisor.MPUpdate** - 기본 OMS 관리 팩을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-233">**Microsoft.SystemCenter.Advisor.MPUpdate** - Updates the base OMS management packs.</span></span> <span data-ttu-id="9974c-234">기본적으로 12시간마다 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-234">Runs every 12 hours by default.</span></span>
* <span data-ttu-id="9974c-235">**Microsoft.SystemCenter.Advisor.Core.GetIntelligencePacksRule** - 작업 영역에서 활성화된 솔루션 관리 팩을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-235">**Microsoft.SystemCenter.Advisor.Core.GetIntelligencePacksRule** - Updates solution management packs enabled in your workspace.</span></span> <span data-ttu-id="9974c-236">기본적으로 5분마다 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-236">Runs every five (5) minutes by default.</span></span>

<span data-ttu-id="9974c-237">비활성화하여 자동 다운로드를 방지하거나 관리 서버에서 새 관리 팩을 사용할 수 있고 다운로드해야 하는 경우를 결정하도록 OMS와 동기화하는 빈도를 수정하기 위해 이러한 두 규칙을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-237">You can override these two rules to either prevent automatic download by disabling them, or modify the frequency for how often the management server synchronizes with OMS to determine if a new management pack is available and should be downloaded.</span></span>  <span data-ttu-id="9974c-238">[규칙 또는 모니터를 재정의하는 방법](https://technet.microsoft.com/library/hh212869.aspx) 단계를 따라 초 단위 값으로 **Frequency** 매개 변수를 수정하여 동기화 일정을 변경하거나 **Enabled** 매개 변수를 수정하여 규칙을 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-238">Follow the steps [How to Override a Rule or Monitor](https://technet.microsoft.com/library/hh212869.aspx) to modify the **Frequency** parameter with a value in seconds to change the synchronization schedule, or modify the **Enabled** parameter to disable the rules.</span></span>  <span data-ttu-id="9974c-239">Operations Manager 관리 그룹 클래스의 모든 개체에 대한 재정의를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-239">Target the overrides to all objects of class Operations Manager Management Group.</span></span>

<span data-ttu-id="9974c-240">프로덕션 관리 그룹에서 관리 팩 릴리스 제어를 위해 기존 변경 제어 프로세스를 계속 따르려는 경우 규칙을 비활성화하고 업데이트가 허용될 때 특정 시간 동안 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-240">If you want to continue following your existing change control process for controlling management pack releases in your production management group, you can disable the rules and enable them during specific times when updates are allowed.</span></span> <span data-ttu-id="9974c-241">사용자 환경에 개발 또는 QA 관리 그룹이 있고 인터넷에 연결되어 있는 경우 OMS 작업 영역으로 해당 관리 그룹을 구성하여 이 시나리오를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-241">If you have a development or QA management group in your environment and it has connectivity to the Internet, you can configure that management group with an OMS workspace to support this scenario.</span></span>  <span data-ttu-id="9974c-242">이렇게 하면 프로덕션 관리 그룹으로 릴리스하기 전에 OMS 관리 팩의 반복적인 릴리스를 검토 및 평가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-242">This allows you to review and evaluate the iterative releases of the OMS management packs before releasing them into your production management group.</span></span>

## <a name="switch-an-operations-manager-group-to-a-new-oms-workspace"></a><span data-ttu-id="9974c-243">Operations Manager 그룹을 새 OMS 작업 영역으로 전환</span><span class="sxs-lookup"><span data-stu-id="9974c-243">Switch an Operations Manager group to a new OMS Workspace</span></span>
1. <span data-ttu-id="9974c-244">OMS 구독에 로그인하고 [Microsoft Operations Management Suite](http://oms.microsoft.com/)에 작업 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-244">Log in to your OMS subscription and create a workspace in [Microsoft Operations Management Suite](http://oms.microsoft.com/).</span></span>
2. <span data-ttu-id="9974c-245">Operations Manager 관리자 역할의 구성원인 계정을 사용하여 Operations Manager 콘솔을 열고 **관리** 작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-245">Open the Operations Manager console with an account that is a member of the Operations Manager Administrators role and select the **Administration** workspace.</span></span>
3. <span data-ttu-id="9974c-246">Operations Management Suite를 확장하고 **연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-246">Expand Operations Management Suite, and select **Connections**.</span></span>
4. <span data-ttu-id="9974c-247">창 중간의 **Operations Management Suite 다시 구성** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-247">Select the **Re-configure Operation Management Suite** link on the middle-side of the pane.</span></span>
5. <span data-ttu-id="9974c-248">**Operations Management Suite 등록 마법사** 의 지시를 따라 전자 메일 주소 또는 전화 번호 및 새 OMS 구독과 연결된 관리자 계정의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-248">Follow the **Operations Management Suite Onboarding Wizard** and enter the email address or phone number and password of the administrator account that is associated with your new OMS workspace.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9974c-249">**Operations Management Suite 등록 마법사: 작업 영역 선택** 페이지는 사용 중인 기존 작업 영역을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-249">The **Operations Management Suite Onboarding Wizard: Select Workspace** page presents the existing workspace that is in use.</span></span>
   > 
   > 

## <a name="validate-operations-manager-integration-with-oms"></a><span data-ttu-id="9974c-250">OMS와 Operations Manager 통합 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="9974c-250">Validate Operations Manager Integration with OMS</span></span>
<span data-ttu-id="9974c-251">OMS에서 Operations Manager 통합이 성공적인지 확인할 수 있는 몇 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-251">There are a few different ways you can verify that your OMS to Operations Manager integration is successful.</span></span>

### <a name="to-confirm-integration-from-the-oms-portal"></a><span data-ttu-id="9974c-252">OMS 포털에서 통합을 확인하려면</span><span class="sxs-lookup"><span data-stu-id="9974c-252">To confirm integration from the OMS portal</span></span>
1. <span data-ttu-id="9974c-253">OMS 포털에서 **설정** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-253">In the OMS portal, click the **Settings** tile</span></span>
2. <span data-ttu-id="9974c-254">**연결된 원본**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-254">Select  **Connected Sources**.</span></span>
3. <span data-ttu-id="9974c-255">System Center Operations Manager 섹션 아래의 테이블에 데이터를 마지막으로 받았을 때 에이전트 및 상태 수와 함께 나열된 관리 그룹의 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-255">In the table under the System Center Operations Manager section, you should see the name of the management group listed with the number of agents and status when data was last received.</span></span>
   
   ![oms-settings-connectedsources](./media/log-analytics-om-agents/oms-settings-connectedsources.png)
4. <span data-ttu-id="9974c-257">설정 페이지의 왼쪽 아래에 있는 **작업 영역 ID** 의 값에 주목하십시오.</span><span class="sxs-lookup"><span data-stu-id="9974c-257">Note the **Workspace ID** value under the left-side of the Settings page.</span></span>  <span data-ttu-id="9974c-258">아래 Operations Manager 관리 그룹을 기준으로 이 값의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-258">You validate it against your Operations Manager management group below.</span></span>  

### <a name="to-confirm-integration-from-the-operations-console"></a><span data-ttu-id="9974c-259">운영 콘솔에서 통합을 확인하려면</span><span class="sxs-lookup"><span data-stu-id="9974c-259">To confirm integration from the Operations console</span></span>
1. <span data-ttu-id="9974c-260">Operations Manager 콘솔을 열고 **관리** 작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-260">Open the Operations Manager console and select the **Administration** workspace.</span></span>
2. <span data-ttu-id="9974c-261">**관리 팩**을 선택하고 **찾기:** 텍스트 상자에 **관리자** 또는 **인텔리전스**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-261">Select **Management Packs** and in the **Look for:** text box type **Advisor** or **Intelligence**.</span></span>
3. <span data-ttu-id="9974c-262">활성화한 솔루션에 따라 검색 결과에 나열된 해당 관리 팩을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-262">Depending on the solutions you have enabled, you see a corresponding management pack listed in the search results.</span></span>  <span data-ttu-id="9974c-263">예를 들어 경고 관리 솔루션을 활성화한 경우 관리 팩 Microsoft System Center Advisor 경고 관리가 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-263">For example, if you have enabled the Alert Management solution, the management pack Microsoft System Center Advisor Alert Management is in the list.</span></span>
4. <span data-ttu-id="9974c-264">**모니터링** 보기에서 **Operations Management Suite\Health State** 보기로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-264">From the **Monitoring** view, navigate to the **Operations Management Suite\Health State** view.</span></span>  <span data-ttu-id="9974c-265">**관리 서버 상태** 창 아래에서 관리 서버를 선택하고 **상세 보기** 창에서 **인증 서비스 URI** 속성의 값이 OMS 작업 영역 ID와 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-265">Select a Management server under the **Management Server State** pane, and in the **Detail View** pane confirm the value for property **Authentication service URI** matches the OMS Workspace ID.</span></span>
   
   ![oms-opsmgr-mg-authsvcuri-property-ms](./media/log-analytics-om-agents/oms-opsmgr-mg-authsvcuri-property-ms.png)

## <a name="remove-integration-with-oms"></a><span data-ttu-id="9974c-267">OMS와의 통합 제거</span><span class="sxs-lookup"><span data-stu-id="9974c-267">Remove Integration with OMS</span></span>
<span data-ttu-id="9974c-268">Operations Manager 관리 그룹과 OMS 작업 영역 간의 통합이 더 이상 필요하지 않은 경우 관리 그룹에서 연결 및 구성을 올바르게 제거하는 데 필요한 여러 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-268">When you no longer require integration between your Operations Manager management group and OMS workspace, there are several steps required to properly remove the connection and configuration in the management group.</span></span> <span data-ttu-id="9974c-269">다음 절차는 관리 그룹 참조를 삭제하여 OMS 작업 영역을 업데이트하고 OMS 커넥터를 삭제한 다음 OMS를 지원하는 관리 팩을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-269">The following procedure has you update your OMS workspace by deleting the reference of your management group, delete the OMS connectors, and then delete management packs supporting OMS.</span></span>   

<span data-ttu-id="9974c-270">Operations Manager와 통합하도록 활성화한 솔루션용 관리 팩 및 OMS 서비스와의 통합을 지원하는 데 필요한 관리 팩은 관리 그룹에서 쉽게 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-270">Management packs for the solutions you have enabled that integrate with Operations Manager and the management packs required to support integration with the OMS service cannot be easily deleted from the management group.</span></span>  <span data-ttu-id="9974c-271">일부 OMS 관리 팩이 관련된 다른 관리 팩에 대해 종속성을 갖기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-271">This is because some of the OMS management packs have dependencies on other related management packs.</span></span>  <span data-ttu-id="9974c-272">다른 관리 팩에 대해 종속성이 있는 관리 팩을 삭제하려면 TechNet 스크립트 센터에서 [종속성이 있는 관리 팩 제거](https://gallery.technet.microsoft.com/scriptcenter/Script-to-remove-a-84f6873e) 스크립트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-272">To delete management packs having a dependency on other management packs, download the script [remove a management pack with dependencies](https://gallery.technet.microsoft.com/scriptcenter/Script-to-remove-a-84f6873e) from TechNet Script Center.</span></span>  

1. <span data-ttu-id="9974c-273">Operations Manager 관리자 역할의 구성원인 계정을 사용하여 Operations Manager 명령 셸을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-273">Open the Operations Manager Command Shell with an account that is a member of the Operations Manager Administrators role.</span></span>
   
    > [!WARNING]
    > <span data-ttu-id="9974c-274">계속 진행하기 전에 이름에 Advisor 또는 IntelligencePack이 포함된 사용자 지정 관리 팩이 없는지 확인합니다. 그렇지 않으면 다음 단계에 관리 그룹에서 이들을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-274">Verify you do not have any custom management packs with the word Advisor or IntelligencePack in the name before proceeding, otherwise the following steps delete them from the management group.</span></span>
    > 

2. <span data-ttu-id="9974c-275">명령 셸 프롬프트에서 `Get-SCOMManagementPack -name "*Advisor*" | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`</span><span class="sxs-lookup"><span data-stu-id="9974c-275">From the command shell prompt, type `Get-SCOMManagementPack -name "*Advisor*" | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`</span></span>
3. <span data-ttu-id="9974c-276">그런 다음 `Get-SCOMManagementPack -name “*IntelligencePack*” | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`</span><span class="sxs-lookup"><span data-stu-id="9974c-276">Next type, `Get-SCOMManagementPack -name “*IntelligencePack*” | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`</span></span>
4. <span data-ttu-id="9974c-277">다른 System Center Advisor 관리 팩에 대해 종속성이 있는 나머지 모든 관리 팩을 제거하려면 이전에 TechNet 스크립트 센터에서 다운로드한 *RecursiveRemove.ps1*을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-277">To remove any management packs remaining which have a dependency on other System Center Advisor management packs, use the script *RecursiveRemove.ps1* you downloaded from the TechNet Script Center earlier.</span></span>  
 
    > [!NOTE]
    > <span data-ttu-id="9974c-278">Microsoft System Center Advisor 또는 Microsoft System Center Advisor 내부 관리 팩은 삭제하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="9974c-278">Do not delete the Microsoft System Center Advisor or Microsoft System Center Advisor Internal management packs.</span></span>  
    >  

5. <span data-ttu-id="9974c-279">Operations Manager 관리자 역할의 구성원인 계정을 사용하여 Operations Manager 작업 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-279">Open the Operations Manager Operations console with an account that is a member of the Operations Manager Administrators role.</span></span>
6. <span data-ttu-id="9974c-280">**관리** 아래에서 **관리 팩** 노드를 선택하고 **찾기:** 상자에 **관리자**를 입력합니다. 이 경우에도 다음 관리 팩을 관리 그룹으로 가져올 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-280">Under **Administration**, select the **Management Packs** node and in the **Look for:** box, type **Advisor** and verify the following management packs are still imported in your management group:</span></span>
   
   * <span data-ttu-id="9974c-281">Microsoft System Center Advisor</span><span class="sxs-lookup"><span data-stu-id="9974c-281">Microsoft System Center Advisor</span></span>
   * <span data-ttu-id="9974c-282">Microsoft System Center Advisor Internal</span><span class="sxs-lookup"><span data-stu-id="9974c-282">Microsoft System Center Advisor Internal</span></span>
7. <span data-ttu-id="9974c-283">OMS 포털에서 **설정** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-283">In the OMS portal, click the **Settings** tile.</span></span>
8. <span data-ttu-id="9974c-284">**연결된 원본**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-284">Select **Connected Sources**.</span></span>
9. <span data-ttu-id="9974c-285">System Center Operations Manager 섹션 아래의 표에 작업 영역에서 제거하려는 관리 그룹의 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-285">In the table under the System Center Operations Manager section, you should see the name of the management group you want to remove from the workspace.</span></span>  <span data-ttu-id="9974c-286">**마지막 데이터** 열 아래에서 **제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-286">Under the column **Last Data**, click **Remove**.</span></span>  
   
    > [!NOTE]
    > <span data-ttu-id="9974c-287">14일간 연결된 관리 그룹에서 감지된 활동이 없을 경우 그 후에는 **제거** 링크를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-287">The **Remove** link will not be available until after 14 days if there is no activity detected from the connected management group.</span></span>  
    > 

10. <span data-ttu-id="9974c-288">제거를 계속할지 확인하라는 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-288">A window will appear asking you to confirm that you want to proceed with the removal.</span></span>  <span data-ttu-id="9974c-289">**예** 를 클릭하여 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-289">Click **Yes** to proceed.</span></span> 

<span data-ttu-id="9974c-290">두 커넥터(Microsoft.SystemCenter.Advisor.DataConnector 및 Advisor 커넥터)를 삭제하려면 PowerShell 스크립트를 컴퓨터에 저장하고 다음 예제를 사용하여 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-290">To delete the two connectors - Microsoft.SystemCenter.Advisor.DataConnector and Advisor Connector, save the PowerShell script below to your computer and execute using the following examples:</span></span>

```
    .\OM2012_DeleteConnector.ps1 “Advisor Connector” <ManagementServerName>
    .\OM2012_DeleteConnectors.ps1 “Microsoft.SytemCenter.Advisor.DataConnector” <ManagementServerName>
```

> [!NOTE]
> <span data-ttu-id="9974c-291">이 스크립트를 실행하는 컴퓨터(관리 서버가 아니라면)에 관리 그룹의 버전에 따라 Operations Manager 명령 셸을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-291">The computer you run this script from, if not a management server, should have the Operations Manager command shell installed depending on the version of your management group.</span></span>
> 
> 

```
    `param(
    [String] $connectorName,
    [String] $msName="localhost"
    )
    $mg = new-object Microsoft.EnterpriseManagement.ManagementGroup $msName
    $admin = $mg.GetConnectorFrameworkAdministration()
    ##########################################################################################
    # Configures a connector with the specified name.
    ##########################################################################################
    function New-Connector([String] $name)
    {
         $connectorForTest = $null;
         foreach($connector in $admin.GetMonitoringConnectors())
    {
    if($connectorName.Name -eq ${name})
    {
         $connectorForTest = Get-SCOMConnector -id $connector.id
    }
    }
    if ($connectorForTest -eq $null)
    {
         $testConnector = New-Object Microsoft.EnterpriseManagement.ConnectorFramework.ConnectorInfo
         $testConnector.Name = $name
         $testConnector.Description = "${name} Description"
         $testConnector.DiscoveryDataIsManaged = $false
         $connectorForTest = $admin.Setup($testConnector)
         $connectorForTest.Initialize();
    }
    return $connectorForTest
    }
    ##########################################################################################
    # Removes a connector with the specified name.
    ##########################################################################################
    function Remove-Connector([String] $name)
    {
        $testConnector = $null
        foreach($connector in $admin.GetMonitoringConnectors())
       {
        if($connector.Name -eq ${name})
       {
         $testConnector = Get-SCOMConnector -id $connector.id
       }
      }
     if ($testConnector -ne $null)
     {
        if($testConnector.Initialized)
     {
     foreach($alert in $testConnector.GetMonitoringAlerts())
     {
       $alert.ConnectorId = $null;
       $alert.Update("Delete Connector");
     }
     $testConnector.Uninitialize()
     }
     $connectorIdForTest = $admin.Cleanup($testConnector)
     }
    }
    ##########################################################################################
    # Delete a connector's Subscription
    ##########################################################################################
    function Delete-Subscription([String] $name)
    {
      foreach($testconnector in $admin.GetMonitoringConnectors())
      {
      if($testconnector.Name -eq $name)
      {
        $connector = Get-SCOMConnector -id $testconnector.id
      }
    }
    $subs = $admin.GetConnectorSubscriptions()
    foreach($sub in $subs)
    {
      if($sub.MonitoringConnectorId -eq $connector.id)
      {
        $admin.DeleteConnectorSubscription($admin.GetConnectorSubscription($sub.Id))
      }
     }
    }
    #New-Connector $connectorName
    write-host "Delete-Subscription"
    Delete-Subscription $connectorName
    write-host "Remove-Connector"
    Remove-Connector $connectorName
```

<span data-ttu-id="9974c-292">향후 관리 그룹을 OMS 작업 영역에 다시 연결할 계획이 있는 경우 관리 그룹에 적용한 최근 업데이트 롤업에서 `Microsoft.SystemCenter.Advisor.Resources.\<Language>\.mpb` 관리 팩 파일을 다시 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-292">In the future if you plan on reconnecting your management group to an OMS workspace, you  need to re-import the `Microsoft.SystemCenter.Advisor.Resources.\<Language>\.mpb` management pack file from the most recent update rollup applied to your management group.</span></span>  <span data-ttu-id="9974c-293">이 파일은 `%ProgramFiles%\Microsoft System Center 2012` 또는 `System Center 2012 R2\Operations Manager\Server\Management Packs for Update Rollups` 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9974c-293">You can find this file in the `%ProgramFiles%\Microsoft System Center 2012` or the `System Center 2012 R2\Operations Manager\Server\Management Packs for Update Rollups` folder.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9974c-294">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9974c-294">Next steps</span></span>
<span data-ttu-id="9974c-295">기능을 추가하고 데이터를 수집하려면 [솔루션 갤러리에서 Log Analytics 솔루션 추가](log-analytics-add-solutions.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9974c-295">To add functionality and gather data, see [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>


