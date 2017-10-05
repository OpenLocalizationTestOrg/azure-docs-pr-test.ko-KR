---
title: Log Analytics FAQ | Microsoft Docs
description: "Azure Log Analytics 서비스에 대해 자주 묻는 질문에 대한 답변입니다."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: ad536ff7-2c60-4850-a46d-230bc9e1ab45
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 8ddea06b1a90e9b1599466ad4d1c3af7a6dc8ba9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="log-analytics-faq"></a><span data-ttu-id="86bb9-103">Log Analytics FAQ</span><span class="sxs-lookup"><span data-stu-id="86bb9-103">Log Analytics FAQ</span></span>
<span data-ttu-id="86bb9-104">Microsoft FAQ는 Microsoft Operations Management Suite(OMS)의 Log Analytics에 대해 자주 묻는 질문의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-104">This Microsoft FAQ is a list of commonly asked questions about Log Analytics in Microsoft Operations Management Suite (OMS).</span></span> <span data-ttu-id="86bb9-105">Log Analytics에 대한 추가 질문이 있으면 [토론 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights)으로 이동하여 질문을 게시하세요.</span><span class="sxs-lookup"><span data-stu-id="86bb9-105">If you have any additional questions about Log Analytics, go to the [discussion forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) and post your questions.</span></span> <span data-ttu-id="86bb9-106">자주 묻는 질문일 경우 빠르고 쉽게 찾을 수 있도록 이 문서에 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-106">When a question is frequently asked, we add it to this article so that it can be found quickly and easily.</span></span>

## <a name="general"></a><span data-ttu-id="86bb9-107">일반</span><span class="sxs-lookup"><span data-stu-id="86bb9-107">General</span></span>

### <a name="q-does-log-analytics-use-the-same-agent-as-azure-security-center"></a><span data-ttu-id="86bb9-108">Q.</span><span class="sxs-lookup"><span data-stu-id="86bb9-108">Q.</span></span> <span data-ttu-id="86bb9-109">Log Analytics는 Azure Security Center와 같은 에이전트를 사용합니까?</span><span class="sxs-lookup"><span data-stu-id="86bb9-109">Does Log Analytics use the same agent as Azure Security Center?</span></span>

<span data-ttu-id="86bb9-110">A.</span><span class="sxs-lookup"><span data-stu-id="86bb9-110">A.</span></span> <span data-ttu-id="86bb9-111">2017년 6월 초에 Azure Security Center는 Microsoft Monitoring Agent를 사용하여 데이터를 수집하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-111">In early June 2017, Azure Security Center began using the Microsoft Monitoring Agent to collect and store data.</span></span> <span data-ttu-id="86bb9-112">자세한 내용은 [Azure Security Center 플랫폼 마이그레이션 FAQ](../security-center/security-center-platform-migration-faq.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86bb9-112">To learn more, see [Azure Security Center Platform Migration FAQ](../security-center/security-center-platform-migration-faq.md).</span></span>

### <a name="q-what-checks-are-performed-by-the-ad-and-sql-assessment-solutions"></a><span data-ttu-id="86bb9-113">Q.</span><span class="sxs-lookup"><span data-stu-id="86bb9-113">Q.</span></span> <span data-ttu-id="86bb9-114">AD 및 SQL 평가 솔루션에서 수행하는 검사는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="86bb9-114">What checks are performed by the AD and SQL Assessment solutions?</span></span>

<span data-ttu-id="86bb9-115">A.</span><span class="sxs-lookup"><span data-stu-id="86bb9-115">A.</span></span> <span data-ttu-id="86bb9-116">다음 쿼리는 현재 수행하는 모든 검사에 대한 설명을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-116">The following query shows a description of all checks currently performed:</span></span>

```
(Type=SQLAssessmentRecommendation OR Type=ADAssessmentRecommendation) | dedup RecommendationId | select FocusArea, ActionArea, Recommendation, Description | sort Type, FocusArea,ActionArea, Recommendation
```

<span data-ttu-id="86bb9-117">추가 검토를 위해 결과를 Excel로 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-117">The results can then be exported to Excel for further review.</span></span>

### <a name="q-why-do-i-see-something-different-than-oms-in-system-center-operations-manager-console"></a><span data-ttu-id="86bb9-118">Q: System Center Operations Manager 콘솔에서 *OMS*와 다르게 표시되는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="86bb9-118">Q: Why do I see something different than *OMS* in System Center Operations Manager console?</span></span>

<span data-ttu-id="86bb9-119">A: 사용 중인 Operations Manager의 업데이트 롤업에 따라 *System Center Advisor*, *Operational Insights* 또는 *Log Analytics*에 대한 노드가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-119">A: Depending on what Update Rollup of Operations Manager you are on, you may see a node for *System Center Advisor*, *Operational Insights*, or *Log Analytics*.</span></span>

<span data-ttu-id="86bb9-120">*OMS* 에 대한 텍스트 문자열 업데이트가 수동으로 가져와야 하는 관리 팩에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-120">The text string update to *OMS* is included in a management pack, which needs to be imported manually.</span></span> <span data-ttu-id="86bb9-121">현재 텍스트 및 기능을 보려면 최신 System Center Operations Manager 업데이트 롤업 기술 자료 문서의 지침을 따르고 콘솔을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-121">To see the current text and functionality, follow the instructions on the latest System Center Operations Manager Update Rollup KB article and refresh the console.</span></span>

### <a name="q-is-there-an-on-premises-version-of-log-analytics"></a><span data-ttu-id="86bb9-122">Q: Log Analytics의 *온-프레미스* 버전이 있나요?</span><span class="sxs-lookup"><span data-stu-id="86bb9-122">Q: Is there an *on-premises* version of Log Analytics?</span></span>

<span data-ttu-id="86bb9-123">A: 아니요.</span><span class="sxs-lookup"><span data-stu-id="86bb9-123">A: No.</span></span> <span data-ttu-id="86bb9-124">Log Analytics에서 대량의 데이터를 처리하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-124">Log Analytics processes and stores large amounts of data.</span></span> <span data-ttu-id="86bb9-125">클라우드 서비스로 Log Analytics는 필요한 경우 강화하여 환경에 대한 성능 영향을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-125">As a cloud service, Log Analytics is able to scale-up if necessary and avoid any performance impact to your environment.</span></span>

<span data-ttu-id="86bb9-126">추가 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-126">Additional benefits include:</span></span>
- <span data-ttu-id="86bb9-127">Microsoft는 Log Analytics 인프라를 실행하여 비용을 절감합니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-127">Microsoft runs the Log Analytics infrastructure, saving you costs</span></span>
- <span data-ttu-id="86bb9-128">정규 기능 배포는 업데이트되고 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-128">Regular deployment of feature updates and fixes.</span></span>

### <a name="q-how-do-i-troubleshoot-that-log-analytics-is-no-longer-collecting-data"></a><span data-ttu-id="86bb9-129">Q.</span><span class="sxs-lookup"><span data-stu-id="86bb9-129">Q.</span></span> <span data-ttu-id="86bb9-130">Log Analytics에서 더 이상 데이터를 수집하지 않는 문제를 어떻게 해결하나요?</span><span class="sxs-lookup"><span data-stu-id="86bb9-130">How do I troubleshoot that Log Analytics is no longer collecting data?</span></span>

<span data-ttu-id="86bb9-131">A: 무료 가격 책정 계층에 있고 하루에 500MB 이상의 데이터를 보낸 경우 남은 날 동안 데이터 수집이 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-131">A: If you are on the free pricing tier and have sent more than 500 MB of data in a day, data collection stops for the rest of the day.</span></span> <span data-ttu-id="86bb9-132">일일 한도에 도달하는 것은 Log Analytics가 데이터 수집을 중지하고 데이터가 사라진 것처럼 표시되는 일반적인 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-132">Reaching the daily limit is a common reason that Log Analytics stops collecting data, or data appears to be missing.</span></span>

<span data-ttu-id="86bb9-133">Log Analytics는 데이터 수집을 시작하고 중지할 때 *Operation* 형식의 이벤트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-133">Log Analytics creates an event of type *Operation* when data collection starts and stops.</span></span> 

<span data-ttu-id="86bb9-134">일일 한도에 도달하고 데이터 누락이 있는지 확인하려면 검색에서 다음 쿼리를 실행합니다. `Type=Operation OperationCategory="Data Collection Status"`</span><span class="sxs-lookup"><span data-stu-id="86bb9-134">Run the following query in search to check if you are reaching the daily limit and missing data: `Type=Operation OperationCategory="Data Collection Status"`</span></span>

<span data-ttu-id="86bb9-135">데이터 수집이 중지되는 경우 *OperationStatus*가 **Warning**입니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-135">When data collection stops, the *OperationStatus* is **Warning**.</span></span> <span data-ttu-id="86bb9-136">데이터 수집이 시작되는 경우 *OperationStatus*가 **Succeeded**입니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-136">When data collection starts, the *OperationStatus* is **Succeeded**.</span></span> 

<span data-ttu-id="86bb9-137">다음 표에서 데이터 수집을 중지하는 이유 및 데이터 수집을 다시 시작하는 권장되는 작업을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-137">The following table describes reasons that data collection stops and a suggested action to resume data collection:</span></span>

| <span data-ttu-id="86bb9-138">데이터 수집 중지 이유</span><span class="sxs-lookup"><span data-stu-id="86bb9-138">Reason data collection stops</span></span>                       | <span data-ttu-id="86bb9-139">데이터 수집을 다시 시작하려면</span><span class="sxs-lookup"><span data-stu-id="86bb9-139">To resume data collection</span></span> |
| -------------------------------------------------- | ----------------  |
| <span data-ttu-id="86bb9-140">무료 데이터의 일일 한도 도달<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="86bb9-140">Daily limit of free data reached<sup>1</sup></span></span>       | <span data-ttu-id="86bb9-141">수집이 다음 날에 자동으로 다시 시작될 때까지 대기 또는</span><span class="sxs-lookup"><span data-stu-id="86bb9-141">Wait until the following day for collection to automatically restart, or</span></span><br> <span data-ttu-id="86bb9-142">유료 가격 책정 계층으로 변경</span><span class="sxs-lookup"><span data-stu-id="86bb9-142">Change to a paid pricing tier</span></span> |
| <span data-ttu-id="86bb9-143">Azure 구독이 다음으로 인해 일시 중단된 상태:</span><span class="sxs-lookup"><span data-stu-id="86bb9-143">Azure subscription is in a suspended state due to:</span></span> <br> <span data-ttu-id="86bb9-144">평가판 종료</span><span class="sxs-lookup"><span data-stu-id="86bb9-144">Free trial ended</span></span> <br> <span data-ttu-id="86bb9-145">Azure 암호 만료</span><span class="sxs-lookup"><span data-stu-id="86bb9-145">Azure pass expired</span></span> <br> <span data-ttu-id="86bb9-146">월별 지출 한도 도달(예: MSDN 또는 Visual Studio 구독에서)</span><span class="sxs-lookup"><span data-stu-id="86bb9-146">Monthly spending limit reached (for example on an MSDN or Visual Studio subscription)</span></span>                          | <span data-ttu-id="86bb9-147">유료 구독으로 전환</span><span class="sxs-lookup"><span data-stu-id="86bb9-147">Convert to a paid subscription</span></span> <br> <span data-ttu-id="86bb9-148">유료 구독으로 전환</span><span class="sxs-lookup"><span data-stu-id="86bb9-148">Convert to a paid subscription</span></span> <br> <span data-ttu-id="86bb9-149">한도 제거 또는 한도가 재설정될 때까지 대기</span><span class="sxs-lookup"><span data-stu-id="86bb9-149">Remove limit, or wait until limit resets</span></span> |

<span data-ttu-id="86bb9-150"><sup>1</sup> 작업 영역이 무료 가격 책정 계층에 있는 경우 일당 500MB의 데이터를 서비스에 전송하도록 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-150"><sup>1</sup> If your workspace is on the free pricing tier, you're limited to sending 500 MB of data per day to the service.</span></span> <span data-ttu-id="86bb9-151">일일 한도에 도달하면 데이터 수집이 다음 날까지 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-151">When you reach the daily limit, data collection stops until the next day.</span></span> <span data-ttu-id="86bb9-152">데이터 수집이 중지되는 동안 전송된 데이터가 인덱싱되지 않으며 검색에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-152">Data sent while data collection is stopped is not indexed and is not available for searching.</span></span> <span data-ttu-id="86bb9-153">데이터 수집이 다시 시작되면 전송된 새 데이터에 대해서만 프로세스가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-153">When data collection resumes, processing occurs only for new data sent.</span></span> 

<span data-ttu-id="86bb9-154">Log Analytics는 UTC 시간을 사용하고 매일 UTC 자정에 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-154">Log Analytics uses UTC time and each day starts at midnight UTC.</span></span> <span data-ttu-id="86bb9-155">작업 영역이 일일 한도에 도달하면 다음 UTC 날의 처음 한 시간 동안 프로세스가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-155">If the workspace reaches the daily limit, processing resumes during the first hour of the next UTC day.</span></span>

### <a name="q-how-can-i-be-notified-when-data-collection-stops"></a><span data-ttu-id="86bb9-156">Q.</span><span class="sxs-lookup"><span data-stu-id="86bb9-156">Q.</span></span> <span data-ttu-id="86bb9-157">데이터 수집이 중지될 때 알림을 받을 수 있는 방법은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="86bb9-157">How can I be notified when data collection stops?</span></span>

<span data-ttu-id="86bb9-158">A: [경고 규칙 만들기](log-analytics-alerts-creating.md#create-an-alert-rule)에 설명한 단계를 사용하여 데이터 수집이 중단되는 경우 알림을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-158">A: Use the steps described in [create an alert rule](log-analytics-alerts-creating.md#create-an-alert-rule) to be notified when data collection stops.</span></span>

<span data-ttu-id="86bb9-159">데이터 수집이 중단되는 경우에 대한 경고를 만드는 시기는 다음을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-159">When creating the alert for when data collection stops, set the:</span></span>
- <span data-ttu-id="86bb9-160">**이름**을 *데이터 수집 중지됨*으로</span><span class="sxs-lookup"><span data-stu-id="86bb9-160">**Name** to *Data collection stopped*</span></span>
- <span data-ttu-id="86bb9-161">**심각도**를 *경고*로</span><span class="sxs-lookup"><span data-stu-id="86bb9-161">**Severity** to *Warning*</span></span>
- <span data-ttu-id="86bb9-162">**쿼리 검색**을 `Type=Operation OperationCategory="Data Collection Status" OperationStatus=Warning`으로</span><span class="sxs-lookup"><span data-stu-id="86bb9-162">**Search query** to `Type=Operation OperationCategory="Data Collection Status" OperationStatus=Warning`</span></span>
- <span data-ttu-id="86bb9-163">**시간 창**을 *2시간*으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-163">**Time window** to *2 Hours*.</span></span>
- <span data-ttu-id="86bb9-164">사용량 데이터가 시간당 한 번만 업데이트되므로 **경고 빈도**를 1시간으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-164">**Alert frequency** to be one hour since the usage data only updates once per hour.</span></span>
- <span data-ttu-id="86bb9-165">**경고 생성 기준**을 *결과의 수*로</span><span class="sxs-lookup"><span data-stu-id="86bb9-165">**Generate alert based on** to be *number of results*</span></span>
- <span data-ttu-id="86bb9-166">**결과 수**를 *0보다 큼*으로</span><span class="sxs-lookup"><span data-stu-id="86bb9-166">**Number of results** to be *Greater than 0*</span></span>

<span data-ttu-id="86bb9-167">[경고 규칙에 작업 추가](log-analytics-alerts-actions.md)에 설명한 단계를 사용하여 경고 규칙에 전자 메일, 웹후크 또는 Runbook 작업을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-167">Use the steps described in [add actions to alert rules](log-analytics-alerts-actions.md) configure an e-mail, webhook, or runbook action for the alert rule.</span></span>


## <a name="configuration"></a><span data-ttu-id="86bb9-168">구성</span><span class="sxs-lookup"><span data-stu-id="86bb9-168">Configuration</span></span>
### <a name="q-can-i-change-the-name-of-the-tableblob-container-used-to-read-from-azure-diagnostics-wad"></a><span data-ttu-id="86bb9-169">Q.</span><span class="sxs-lookup"><span data-stu-id="86bb9-169">Q.</span></span> <span data-ttu-id="86bb9-170">WAD(Azure 진단)에서 읽어오는 데 사용되는 테이블/Blob 컨테이너의 이름을 변경할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="86bb9-170">Can I change the name of the table/blob container used to read from Azure Diagnostics (WAD)?</span></span>

<span data-ttu-id="86bb9-171">A.</span><span class="sxs-lookup"><span data-stu-id="86bb9-171">A.</span></span> <span data-ttu-id="86bb9-172">아니요, 현재 Azure 저장소의 임의 테이블 또는 컨테이너에서 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-172">No, it is not currently possible to read from arbitrary tables or containers in Azure storage.</span></span>

### <a name="q-what-ip-addresses-does-the-log-analytics-service-use-how-do-i-ensure-that-my-firewall-only-allows-traffic-to-the-log-analytics-service"></a><span data-ttu-id="86bb9-173">Q.</span><span class="sxs-lookup"><span data-stu-id="86bb9-173">Q.</span></span> <span data-ttu-id="86bb9-174">Log Analytics 서비스에서 사용하는 IP 주소는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="86bb9-174">What IP addresses does the Log Analytics service use?</span></span> <span data-ttu-id="86bb9-175">내 방화벽에서 Log Analytics 서비스에 대한 트래픽만 허용하도록 하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="86bb9-175">How do I ensure that my firewall only allows traffic to the Log Analytics service?</span></span>

<span data-ttu-id="86bb9-176">A.</span><span class="sxs-lookup"><span data-stu-id="86bb9-176">A.</span></span> <span data-ttu-id="86bb9-177">Log Analytics 서비스는 Azure를 기반으로 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-177">The Log Analytics service is built on top of Azure.</span></span> <span data-ttu-id="86bb9-178">Log Analytics IP 주소는 [Microsoft Azure 데이터 센터 IP 범위](http://www.microsoft.com/download/details.aspx?id=41653)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-178">Log Analytics IP addresses are in the [Microsoft Azure Datacenter IP Ranges](http://www.microsoft.com/download/details.aspx?id=41653).</span></span>

<span data-ttu-id="86bb9-179">서비스 배포가 수행되면서 Log Analytics 서비스의 실제 IP 주소가 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-179">As service deployments are made, the actual IP addresses of the Log Analytics service change.</span></span> <span data-ttu-id="86bb9-180">방화벽을 통과하도록 허용할 DNS 이름이 [Log Analytics에서 프록시 및 방화벽 설정 구성](log-analytics-proxy-firewall.md)에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-180">The DNS names to allow through your firewall are documented at [Configure proxy and firewall settings in Log Analytics](log-analytics-proxy-firewall.md).</span></span>

### <a name="q-i-use-expressroute-for-connecting-to-azure-does-my-log-analytics-traffic-use-my-expressroute-connection"></a><span data-ttu-id="86bb9-181">Q.</span><span class="sxs-lookup"><span data-stu-id="86bb9-181">Q.</span></span> <span data-ttu-id="86bb9-182">Express 경로를 사용하여 Azure에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-182">I use ExpressRoute for connecting to Azure.</span></span> <span data-ttu-id="86bb9-183">Log Analytics 트래픽이 내 ExpressRoute 연결을 사용하나요?</span><span class="sxs-lookup"><span data-stu-id="86bb9-183">Does my Log Analytics traffic use my ExpressRoute connection?</span></span>

<span data-ttu-id="86bb9-184">A.</span><span class="sxs-lookup"><span data-stu-id="86bb9-184">A.</span></span> <span data-ttu-id="86bb9-185">여러 유형의 Express 경로 트래픽이 [Express 경로 설명서](../expressroute/expressroute-faqs.md#supported-services)에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-185">The different types of ExpressRoute traffic are described in the [ExpressRoute documentation](../expressroute/expressroute-faqs.md#supported-services).</span></span>

<span data-ttu-id="86bb9-186">Log Analytics에 대한 트래픽은 공용 피어링 Express 경로 회로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-186">Traffic to Log Analytics uses the public-peering ExpressRoute circuit.</span></span>

### <a name="q-is-there-a-simple-and-easy-way-to-move-an-existing-log-analytics-workspace-to-another-log-analytics-workspaceazure-subscription"></a><span data-ttu-id="86bb9-187">Q.</span><span class="sxs-lookup"><span data-stu-id="86bb9-187">Q.</span></span> <span data-ttu-id="86bb9-188">기존 Log Analytics 작업 영역을 다른 Log Analytics 작업 영역/Azure 구독으로 이동할 간단하고 쉬운 방법이 있나요?</span><span class="sxs-lookup"><span data-stu-id="86bb9-188">Is there a simple and easy way to move an existing Log Analytics workspace to another Log Analytics workspace/Azure subscription?</span></span>

<span data-ttu-id="86bb9-189">A.</span><span class="sxs-lookup"><span data-stu-id="86bb9-189">A.</span></span> <span data-ttu-id="86bb9-190">`Move-AzureRmResource` cmdlet을 사용하면 Log Analytics 작업 영역을 이동할 수 있으며 한 Azure 구독에서 다른 구독으로 자동화 계정도 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-190">The `Move-AzureRmResource` cmdlet lets you move a Log Analytics workspace, and also an Automation account from one Azure subscription to another.</span></span> <span data-ttu-id="86bb9-191">자세한 내용은 [Move-AzureRmResource](http://msdn.microsoft.com/library/mt652516.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86bb9-191">For more information, see [Move-AzureRmResource](http://msdn.microsoft.com/library/mt652516.aspx).</span></span>

<span data-ttu-id="86bb9-192">이러한 변경은 Azure 포털에서 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-192">This change can also be made in the Azure portal.</span></span>

<span data-ttu-id="86bb9-193">데이터를 한 Log Analytics 작업 영역에서 다른 작업 영역으로 이동하거나 Log Analytics 데이터가 저장된 지역을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-193">You can’t move data from one Log Analytics workspace to another, or change the region that Log Analytics data is stored in.</span></span>

### <a name="q-how-do-i-add-log-analytics-to-system-center-operations-manager"></a><span data-ttu-id="86bb9-194">Q: Log Analytics를 System Center Operations Manager에 추가하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="86bb9-194">Q: How do I add Log Analytics to System Center Operations Manager?</span></span>

<span data-ttu-id="86bb9-195">A: 최신 업데이트 롤업으로 업데이트 및 관리 팩 가져오기를 통해 Operations Manager를 Log Analytics에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-195">A:  Updating to the latest update rollup and importing management packs enables you to connect Operations Manager to Log Analytics.</span></span>

>[!NOTE]
><span data-ttu-id="86bb9-196">Log Analytics에 Operations Manager 연결은 System Center Operations Manager 2012 SP1 이상에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-196">The Operations Manager connection to Log Analytics is only available for System Center Operations Manager 2012 SP1 and later.</span></span>

### <a name="q-how-can-i-confirm-that-an-agent-is-able-to-communicate-with-log-analytics"></a><span data-ttu-id="86bb9-197">Q: 에이전트가 Log Analytics와 통신할 수 있는지 어떻게 확인하나요?</span><span class="sxs-lookup"><span data-stu-id="86bb9-197">Q: How can I confirm that an agent is able to communicate with Log Analytics?</span></span>

<span data-ttu-id="86bb9-198">A: 에이전트가 OMS와 통신할 수 있는지 확인하려면 제어판, 보안 및 설정, **Microsoft Monitoring Agent**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-198">A: To ensure that the agent can communicate with OMS, go to: Control Panel, Security & Settings, **Microsoft Monitoring Agent**.</span></span>

<span data-ttu-id="86bb9-199">**Azure Log Analytics(OMS)** 탭 아래에서 녹색 확인 표시를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-199">Under the **Azure Log Analytics (OMS)** tab, look for a green check mark.</span></span> <span data-ttu-id="86bb9-200">녹색 확인 표시 아이콘은 에이전트가 OMS 서비스와 통신할 수 있음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-200">A green check mark icon confirms that the agent is able to communicate with the OMS service.</span></span>

<span data-ttu-id="86bb9-201">노란색 경고 아이콘은 에이전트가 OMS와 통신하는 데 문제가 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-201">A yellow warning icon means the agent is having issues communication with OMS.</span></span> <span data-ttu-id="86bb9-202">한 가지 일반적인 이유는 Microsoft Monitoring Agent 서비스가 중지되었기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-202">One common reason is the Microsoft Monitoring Agent service has stopped.</span></span> <span data-ttu-id="86bb9-203">서비스 제어 관리자를 사용하여 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-203">Use service control manager to restart the service.</span></span>

### <a name="q-how-do-i-stop-an-agent-from-communicating-with-log-analytics"></a><span data-ttu-id="86bb9-204">Q: 에이전트가 Log Analytics와의 통신을 중지하도록 하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="86bb9-204">Q: How do I stop an agent from communicating with Log Analytics?</span></span>

<span data-ttu-id="86bb9-205">A: System Center Operations Manager의 Advisor 관리 컴퓨터 목록에서 컴퓨터를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-205">A: In System Center Operations Manager, remove the computer from the Advisor managed computer list.</span></span> <span data-ttu-id="86bb9-206">Operations Manager는 Log Analytics에 더 이상 보고하지 않도록 에이전트의 구성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-206">Operations Manager updates the configuration of the agent to no longer report to Log Analytics.</span></span> <span data-ttu-id="86bb9-207">Log Analytics에 직접 연결된 에이전트인 경우 제어판, 보안 및 설정, **Microsoft Monitoring Agent**를 통해 통신을 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-207">For agents connected to Log Analytics directly, you can stop them from communicating through: Control Panel, Security & Settings, **Microsoft Monitoring Agent**.</span></span>
<span data-ttu-id="86bb9-208">**Azure Log Analytics(OMS)**아래에서 나열된 모든 작업 영역을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-208">Under **Azure Log Analytics (OMS)**, remove all workspaces listed.</span></span>

### <a name="q-why-am-i-getting-an-error-when-i-try-to-move-my-workspace-from-one-azure-subscription-to-another"></a><span data-ttu-id="86bb9-209">Q: 내 작업 영역을 특정 Azure 구독에서 다른 구독으로 이동하려고 하는 경우 오류가 발생하는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="86bb9-209">Q: Why am I getting an error when I try to move my workspace from one Azure subscription to another?</span></span>

<span data-ttu-id="86bb9-210">A: Azure Portal을 사용하는 경우 이동에 대해 작업 영역만 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-210">A: If you are using the Azure portal, ensure only the workspace is selected for the move.</span></span> <span data-ttu-id="86bb9-211">솔루션을 선택하지 마십시오. 작업 영역이 이동한 후 자동으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-211">Do not select the solutions -- they will automatically move after the workspace moves.</span></span> 

<span data-ttu-id="86bb9-212">두 Azure 구독에서 권한을 갖는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-212">Ensure you have permission in both Azure subscriptions.</span></span>

## <a name="agent-data"></a><span data-ttu-id="86bb9-213">에이전트 데이터</span><span class="sxs-lookup"><span data-stu-id="86bb9-213">Agent data</span></span>
### <a name="q-how-much-data-can-i-send-through-the-agent-to-log-analytics-is-there-a-maximum-amount-of-data-per-customer"></a><span data-ttu-id="86bb9-214">Q.</span><span class="sxs-lookup"><span data-stu-id="86bb9-214">Q.</span></span> <span data-ttu-id="86bb9-215">에이전트를 통해 Log Analytics로 얼마나 많은 데이터를 보낼 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="86bb9-215">How much data can I send through the agent to Log Analytics?</span></span> <span data-ttu-id="86bb9-216">고객 한 명당 최대 데이터 용량이 있나요?</span><span class="sxs-lookup"><span data-stu-id="86bb9-216">Is there a maximum amount of data per customer?</span></span>
<span data-ttu-id="86bb9-217">A.</span><span class="sxs-lookup"><span data-stu-id="86bb9-217">A.</span></span> <span data-ttu-id="86bb9-218">무료 요금제에서는 작업 영역당 일일 용량을 500MB로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-218">The free plan sets a daily cap of 500 MB per workspace.</span></span> <span data-ttu-id="86bb9-219">표준 및 프리미엄 요금제에는 업로드되는 데이터 양에 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-219">The standard and premium plans have no limit on the amount of data that is uploaded.</span></span> <span data-ttu-id="86bb9-220">클라우드 서비스로 Log Analytics는 고객의 데이터 볼륨(일일 테라바이트 단위까지)을 처리하도록 자동 강화되도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-220">As a cloud service, Log Analytics is designed to automatically scale up to handle the volume coming from a customer – even if it is terabytes per day.</span></span>

<span data-ttu-id="86bb9-221">Log Analytics 에이전트는 작은 공간을 갖도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-221">The Log Analytics agent was designed to ensure it has a small footprint.</span></span> <span data-ttu-id="86bb9-222">고객 중 한 명이 에이전트에 대해 수행한 테스트와 그에 대한 의견을 다룬 블로그를 작성했습니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-222">One of our customers wrote a blog about the tests they performed against our agent and how impressed they were.</span></span> <span data-ttu-id="86bb9-223">데이터 볼륨은 사용하도록 설정한 솔루션에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-223">The data volume varies based on the solutions you enable.</span></span> <span data-ttu-id="86bb9-224">[사용량](log-analytics-usage.md) 페이지에서 데이터 볼륨에 대한 자세한 정보를 확인하고 솔루션별로 정리된 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-224">You can find detailed information on the data volume and see the breakup by solution in the [Usage](log-analytics-usage.md) page.</span></span>

<span data-ttu-id="86bb9-225">자세한 내용은 OMS 에이전트의 적은 사용 공간에 대한 [고객 블로그](http://thoughtsonopsmgr.blogspot.com/2015/09/one-small-footprint-for-server-one.html) 를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-225">For more information, you can read a [customer blog](http://thoughtsonopsmgr.blogspot.com/2015/09/one-small-footprint-for-server-one.html) about the low footprint of the OMS agent.</span></span>

### <a name="q-how-much-network-bandwidth-is-used-by-the-microsoft-management-agent-mma-when-sending-data-to-log-analytics"></a><span data-ttu-id="86bb9-226">Q.</span><span class="sxs-lookup"><span data-stu-id="86bb9-226">Q.</span></span> <span data-ttu-id="86bb9-227">데이터를 Log Analytics로 전송할 때 Microsoft Management Agent(MMA)에 사용된 네트워크 대역폭은 얼마나 되나요?</span><span class="sxs-lookup"><span data-stu-id="86bb9-227">How much network bandwidth is used by the Microsoft Management Agent (MMA) when sending data to Log Analytics?</span></span>

<span data-ttu-id="86bb9-228">A.</span><span class="sxs-lookup"><span data-stu-id="86bb9-228">A.</span></span> <span data-ttu-id="86bb9-229">대역폭은 전송된 데이터 양에 대한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-229">Bandwidth is a function on the amount of data sent.</span></span> <span data-ttu-id="86bb9-230">네트워크를 통해 데이터가 전송되는 동안 데이터가 압축됩니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-230">Data is compressed as it is sent over the network.</span></span>

### <a name="q-how-much-data-is-sent-per-agent"></a><span data-ttu-id="86bb9-231">Q.</span><span class="sxs-lookup"><span data-stu-id="86bb9-231">Q.</span></span> <span data-ttu-id="86bb9-232">에이전트당 얼마나 많은 데이터가 전송되나요?</span><span class="sxs-lookup"><span data-stu-id="86bb9-232">How much data is sent per agent?</span></span>

<span data-ttu-id="86bb9-233">A.</span><span class="sxs-lookup"><span data-stu-id="86bb9-233">A.</span></span> <span data-ttu-id="86bb9-234">에이전트당 전송되는 데이터의 양에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-234">The amount of data sent per agent depends on:</span></span>

* <span data-ttu-id="86bb9-235">사용하도록 설정한 솔루션</span><span class="sxs-lookup"><span data-stu-id="86bb9-235">The solutions you have enabled</span></span>
* <span data-ttu-id="86bb9-236">수집되는 로그 및 성능 카운터 수</span><span class="sxs-lookup"><span data-stu-id="86bb9-236">The number of logs and performance counters being collected</span></span>
* <span data-ttu-id="86bb9-237">로그에 있는 데이터 볼륨</span><span class="sxs-lookup"><span data-stu-id="86bb9-237">The volume of data in the logs</span></span>

<span data-ttu-id="86bb9-238">무료 가격 책정 계층은 여러 서버에 등록하고 일반적인 데이터 볼륨을 측정하는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-238">The free pricing tier is a good way to onboard several servers and gauge the typical data volume.</span></span> <span data-ttu-id="86bb9-239">전체 사용 현황은 [사용량](log-analytics-usage.md) 페이지에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-239">Overall usage is shown on the [Usage](log-analytics-usage.md) page.</span></span>

<span data-ttu-id="86bb9-240">WireData 에이전트를 실행할 수 있는 컴퓨터의 경우 다음 쿼리를 사용하여 전송 중인 데이터의 양을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="86bb9-240">For computers that are able to run the WireData agent, use the following query to see how much data is being sent:</span></span>

```
Type=WireData (ProcessName="C:\\Program Files\\Microsoft Monitoring Agent\\Agent\\MonitoringHost.exe") (Direction=Outbound) | measure Sum(TotalBytes) by Computer
```



## <a name="next-steps"></a><span data-ttu-id="86bb9-241">다음 단계</span><span class="sxs-lookup"><span data-stu-id="86bb9-241">Next steps</span></span>
* <span data-ttu-id="86bb9-242">[Log Analytics 시작](log-analytics-get-started.md) 에서 Log Analytics에 대한 정보와 Log Analytics를 몇 분 만에 시작 및 실행하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="86bb9-242">[Get started with Log Analytics](log-analytics-get-started.md) to learn more about Log Analytics and get up and running in minutes.</span></span>
