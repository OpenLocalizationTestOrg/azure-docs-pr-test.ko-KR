---
title: "aaaLog 분석 FAQ | Microsoft Docs"
description: "Hello Azure 로그 분석 서비스에 대 한 질문과 대답 toofrequently 합니다."
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
ms.openlocfilehash: 25931f521cbb6ec840184221c6c1a5794b3445f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-faq"></a><span data-ttu-id="81c00-103">Log Analytics FAQ</span><span class="sxs-lookup"><span data-stu-id="81c00-103">Log Analytics FAQ</span></span>
<span data-ttu-id="81c00-104">Microsoft FAQ는 Microsoft Operations Management Suite(OMS)의 Log Analytics에 대해 자주 묻는 질문의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-104">This Microsoft FAQ is a list of commonly asked questions about Log Analytics in Microsoft Operations Management Suite (OMS).</span></span> <span data-ttu-id="81c00-105">로그 분석에 대 한 추가 질문이 있으면 이동 toohello [토론 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) 여 질문을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-105">If you have any additional questions about Log Analytics, go toohello [discussion forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) and post your questions.</span></span> <span data-ttu-id="81c00-106">자주 묻는 질문 하는 경우 추가 것 toothis 문서 빠르고 쉽게 찾을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-106">When a question is frequently asked, we add it toothis article so that it can be found quickly and easily.</span></span>

## <a name="general"></a><span data-ttu-id="81c00-107">일반</span><span class="sxs-lookup"><span data-stu-id="81c00-107">General</span></span>

### <a name="q-does-log-analytics-use-hello-same-agent-as-azure-security-center"></a><span data-ttu-id="81c00-108">Q.</span><span class="sxs-lookup"><span data-stu-id="81c00-108">Q.</span></span> <span data-ttu-id="81c00-109">로그 분석 hello 사용할 Azure 보안 센터와 동일한 에이전트?</span><span class="sxs-lookup"><span data-stu-id="81c00-109">Does Log Analytics use hello same agent as Azure Security Center?</span></span>

<span data-ttu-id="81c00-110">A.</span><span class="sxs-lookup"><span data-stu-id="81c00-110">A.</span></span> <span data-ttu-id="81c00-111">초기 6 월 2017 Azure 보안 센터 hello Microsoft Monitoring Agent toocollect 및 저장소 데이터를 사용 하 여 시작 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-111">In early June 2017, Azure Security Center began using hello Microsoft Monitoring Agent toocollect and store data.</span></span> <span data-ttu-id="81c00-112">toolearn 더 참조 [Azure 보안 센터 플랫폼 마이그레이션 FAQ](../security-center/security-center-platform-migration-faq.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-112">toolearn more, see [Azure Security Center Platform Migration FAQ](../security-center/security-center-platform-migration-faq.md).</span></span>

### <a name="q-what-checks-are-performed-by-hello-ad-and-sql-assessment-solutions"></a><span data-ttu-id="81c00-113">Q.</span><span class="sxs-lookup"><span data-stu-id="81c00-113">Q.</span></span> <span data-ttu-id="81c00-114">어떤 검사를 수행 하 여 hello AD 및 SQL 평가 솔루션으로?</span><span class="sxs-lookup"><span data-stu-id="81c00-114">What checks are performed by hello AD and SQL Assessment solutions?</span></span>

<span data-ttu-id="81c00-115">A.</span><span class="sxs-lookup"><span data-stu-id="81c00-115">A.</span></span> <span data-ttu-id="81c00-116">hello 다음 쿼리는 현재 수행 하는 모든 검사에 대 한 설명을</span><span class="sxs-lookup"><span data-stu-id="81c00-116">hello following query shows a description of all checks currently performed:</span></span>

```
(Type=SQLAssessmentRecommendation OR Type=ADAssessmentRecommendation) | dedup RecommendationId | select FocusArea, ActionArea, Recommendation, Description | sort Type, FocusArea,ActionArea, Recommendation
```

<span data-ttu-id="81c00-117">hello 결과 수 추가 검토를 위해 내보낸된 tooExcel 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-117">hello results can then be exported tooExcel for further review.</span></span>

### <a name="q-why-do-i-see-something-different-than-oms-in-system-center-operations-manager-console"></a><span data-ttu-id="81c00-118">Q: System Center Operations Manager 콘솔에서 *OMS*와 다르게 표시되는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="81c00-118">Q: Why do I see something different than *OMS* in System Center Operations Manager console?</span></span>

<span data-ttu-id="81c00-119">A: 사용 중인 Operations Manager의 업데이트 롤업에 따라 *System Center Advisor*, *Operational Insights* 또는 *Log Analytics*에 대한 노드가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-119">A: Depending on what Update Rollup of Operations Manager you are on, you may see a node for *System Center Advisor*, *Operational Insights*, or *Log Analytics*.</span></span>

<span data-ttu-id="81c00-120">텍스트 문자열 업데이트가 너무 hello*OMS* 수동으로 가져올 toobe는 관리 팩에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-120">hello text string update too*OMS* is included in a management pack, which needs toobe imported manually.</span></span> <span data-ttu-id="81c00-121">toosee hello 현재 텍스트와 기능을 hello 최신 System Center Operations Manager 업데이트 롤업 기술 자료 문서 및 새로 고침 hello 콘솔에 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-121">toosee hello current text and functionality, follow hello instructions on hello latest System Center Operations Manager Update Rollup KB article and refresh hello console.</span></span>

### <a name="q-is-there-an-on-premises-version-of-log-analytics"></a><span data-ttu-id="81c00-122">Q: Log Analytics의 *온-프레미스* 버전이 있나요?</span><span class="sxs-lookup"><span data-stu-id="81c00-122">Q: Is there an *on-premises* version of Log Analytics?</span></span>

<span data-ttu-id="81c00-123">A: 아니요.</span><span class="sxs-lookup"><span data-stu-id="81c00-123">A: No.</span></span> <span data-ttu-id="81c00-124">Log Analytics에서 대량의 데이터를 처리하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-124">Log Analytics processes and stores large amounts of data.</span></span> <span data-ttu-id="81c00-125">클라우드 서비스로 로그 분석 수 tooscale 접속 필요한 경우 이며 모든 성능 영향 tooyour 환경 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-125">As a cloud service, Log Analytics is able tooscale-up if necessary and avoid any performance impact tooyour environment.</span></span>

<span data-ttu-id="81c00-126">추가 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-126">Additional benefits include:</span></span>
- <span data-ttu-id="81c00-127">Microsoft은 hello 로그 분석 인프라 비용을 절감 실행</span><span class="sxs-lookup"><span data-stu-id="81c00-127">Microsoft runs hello Log Analytics infrastructure, saving you costs</span></span>
- <span data-ttu-id="81c00-128">정규 기능 배포는 업데이트되고 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-128">Regular deployment of feature updates and fixes.</span></span>

### <a name="q-how-do-i-troubleshoot-that-log-analytics-is-no-longer-collecting-data"></a><span data-ttu-id="81c00-129">Q.</span><span class="sxs-lookup"><span data-stu-id="81c00-129">Q.</span></span> <span data-ttu-id="81c00-130">Log Analytics에서 더 이상 데이터를 수집하지 않는 문제를 어떻게 해결하나요?</span><span class="sxs-lookup"><span data-stu-id="81c00-130">How do I troubleshoot that Log Analytics is no longer collecting data?</span></span>

<span data-ttu-id="81c00-131">A: 경우 hello 무료 가격 책정 계층에 하 고 하루에서 이상 500MB의 데이터를 보낸 hello 일의 hello 나머지 부분에 대 한 데이터 수집 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-131">A: If you are on hello free pricing tier and have sent more than 500 MB of data in a day, data collection stops for hello rest of hello day.</span></span> <span data-ttu-id="81c00-132">표시할 toobe 데이터 또는 hello 일일 제한에 도달 함 로그 분석 데이터 수집을 중지 하는 일반적인 이유는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-132">Reaching hello daily limit is a common reason that Log Analytics stops collecting data, or data appears toobe missing.</span></span>

<span data-ttu-id="81c00-133">Log Analytics는 데이터 수집을 시작하고 중지할 때 *Operation* 형식의 이벤트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-133">Log Analytics creates an event of type *Operation* when data collection starts and stops.</span></span> 

<span data-ttu-id="81c00-134">Hello hello 일일 한도 도달 하 고 누락 된 데이터는 경우에 다음 검색 toocheck에서 쿼리를 실행 합니다.`Type=Operation OperationCategory="Data Collection Status"`</span><span class="sxs-lookup"><span data-stu-id="81c00-134">Run hello following query in search toocheck if you are reaching hello daily limit and missing data: `Type=Operation OperationCategory="Data Collection Status"`</span></span>

<span data-ttu-id="81c00-135">데이터 수집을 중지할 시기를 hello *OperationStatus* 은 **경고**합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-135">When data collection stops, hello *OperationStatus* is **Warning**.</span></span> <span data-ttu-id="81c00-136">데이터 수집 시작 되 면 hello *OperationStatus* 은 **Succeeded**합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-136">When data collection starts, hello *OperationStatus* is **Succeeded**.</span></span> 

<span data-ttu-id="81c00-137">hello 다음 표에서 데이터 수집을 중지 하는 이유 및 제안된 하는 조치 tooresume 데이터 수집:</span><span class="sxs-lookup"><span data-stu-id="81c00-137">hello following table describes reasons that data collection stops and a suggested action tooresume data collection:</span></span>

| <span data-ttu-id="81c00-138">데이터 수집 중지 이유</span><span class="sxs-lookup"><span data-stu-id="81c00-138">Reason data collection stops</span></span>                       | <span data-ttu-id="81c00-139">tooresume 데이터 수집</span><span class="sxs-lookup"><span data-stu-id="81c00-139">tooresume data collection</span></span> |
| -------------------------------------------------- | ----------------  |
| <span data-ttu-id="81c00-140">무료 데이터의 일일 한도 도달<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="81c00-140">Daily limit of free data reached<sup>1</sup></span></span>       | <span data-ttu-id="81c00-141">Hello 다음 날에 게 컬렉션 tooautomatically 다시 시작 될 때까지 대기 또는</span><span class="sxs-lookup"><span data-stu-id="81c00-141">Wait until hello following day for collection tooautomatically restart, or</span></span><br> <span data-ttu-id="81c00-142">변경 tooa 유료 가격 책정 계층</span><span class="sxs-lookup"><span data-stu-id="81c00-142">Change tooa paid pricing tier</span></span> |
| <span data-ttu-id="81c00-143">Azure 구독이 다음으로 인해 일시 중단된 상태:</span><span class="sxs-lookup"><span data-stu-id="81c00-143">Azure subscription is in a suspended state due to:</span></span> <br> <span data-ttu-id="81c00-144">평가판 종료</span><span class="sxs-lookup"><span data-stu-id="81c00-144">Free trial ended</span></span> <br> <span data-ttu-id="81c00-145">Azure 암호 만료</span><span class="sxs-lookup"><span data-stu-id="81c00-145">Azure pass expired</span></span> <br> <span data-ttu-id="81c00-146">월별 지출 한도 도달(예: MSDN 또는 Visual Studio 구독에서)</span><span class="sxs-lookup"><span data-stu-id="81c00-146">Monthly spending limit reached (for example on an MSDN or Visual Studio subscription)</span></span>                          | <span data-ttu-id="81c00-147">Tooa 유료 구독으로 변환</span><span class="sxs-lookup"><span data-stu-id="81c00-147">Convert tooa paid subscription</span></span> <br> <span data-ttu-id="81c00-148">Tooa 유료 구독으로 변환</span><span class="sxs-lookup"><span data-stu-id="81c00-148">Convert tooa paid subscription</span></span> <br> <span data-ttu-id="81c00-149">한도 제거 또는 한도가 재설정될 때까지 대기</span><span class="sxs-lookup"><span data-stu-id="81c00-149">Remove limit, or wait until limit resets</span></span> |

<span data-ttu-id="81c00-150"><sup>1</sup> 을 hello 무료 가격 책정 계층에서 작업 영역을 하는 경우 제한 된 toosending 500MB의 데이터 일 toohello 서비스 당 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-150"><sup>1</sup> If your workspace is on hello free pricing tier, you're limited toosending 500 MB of data per day toohello service.</span></span> <span data-ttu-id="81c00-151">Hello 일일 한도 도달 하면 hello 다음 날까지 데이터 수집을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-151">When you reach hello daily limit, data collection stops until hello next day.</span></span> <span data-ttu-id="81c00-152">데이터 수집이 중지되는 동안 전송된 데이터가 인덱싱되지 않으며 검색에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-152">Data sent while data collection is stopped is not indexed and is not available for searching.</span></span> <span data-ttu-id="81c00-153">데이터 수집이 다시 시작되면 전송된 새 데이터에 대해서만 프로세스가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-153">When data collection resumes, processing occurs only for new data sent.</span></span> 

<span data-ttu-id="81c00-154">Log Analytics는 UTC 시간을 사용하고 매일 UTC 자정에 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-154">Log Analytics uses UTC time and each day starts at midnight UTC.</span></span> <span data-ttu-id="81c00-155">Hello 작업 영역 hello 일일 한도 도달 하면 처리가 hello UTC 다음날 hello의 첫 번째 시간 동안 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-155">If hello workspace reaches hello daily limit, processing resumes during hello first hour of hello next UTC day.</span></span>

### <a name="q-how-can-i-be-notified-when-data-collection-stops"></a><span data-ttu-id="81c00-156">Q.</span><span class="sxs-lookup"><span data-stu-id="81c00-156">Q.</span></span> <span data-ttu-id="81c00-157">데이터 수집이 중지될 때 알림을 받을 수 있는 방법은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="81c00-157">How can I be notified when data collection stops?</span></span>

<span data-ttu-id="81c00-158">A:에서 설명 하는 hello 단계를 사용 하 여 [경고 규칙을 생성할](log-analytics-alerts-creating.md#create-an-alert-rule) toobe 데이터 수집이 중지 될 때 알림을 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-158">A: Use hello steps described in [create an alert rule](log-analytics-alerts-creating.md#create-an-alert-rule) toobe notified when data collection stops.</span></span>

<span data-ttu-id="81c00-159">데이터 수집을 중지 하는 것에 대 한 hello 경고를 만들 때 설정 된:</span><span class="sxs-lookup"><span data-stu-id="81c00-159">When creating hello alert for when data collection stops, set the:</span></span>
- <span data-ttu-id="81c00-160">**이름** 너무*데이터 수집 중지*</span><span class="sxs-lookup"><span data-stu-id="81c00-160">**Name** too*Data collection stopped*</span></span>
- <span data-ttu-id="81c00-161">**심각도** 너무*경고*</span><span class="sxs-lookup"><span data-stu-id="81c00-161">**Severity** too*Warning*</span></span>
- <span data-ttu-id="81c00-162">**검색 쿼리** 너무`Type=Operation OperationCategory="Data Collection Status" OperationStatus=Warning`</span><span class="sxs-lookup"><span data-stu-id="81c00-162">**Search query** too`Type=Operation OperationCategory="Data Collection Status" OperationStatus=Warning`</span></span>
- <span data-ttu-id="81c00-163">**시간 창** 너무*2 시간*합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-163">**Time window** too*2 Hours*.</span></span>
- <span data-ttu-id="81c00-164">**경고 빈도** toobe 1 시간 이후 hello 사용 현황 데이터는 시간당 한 번만 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-164">**Alert frequency** toobe one hour since hello usage data only updates once per hour.</span></span>
- <span data-ttu-id="81c00-165">**경고에 따라 생성** toobe *결과의 수*</span><span class="sxs-lookup"><span data-stu-id="81c00-165">**Generate alert based on** toobe *number of results*</span></span>
- <span data-ttu-id="81c00-166">**결과 수가** toobe *0 보다 큰*</span><span class="sxs-lookup"><span data-stu-id="81c00-166">**Number of results** toobe *Greater than 0*</span></span>

<span data-ttu-id="81c00-167">에 설명 된 hello 단계를 사용 하 여 [동작 tooalert 규칙 추가](log-analytics-alerts-actions.md) hello 경고 규칙에 대 한 전자 메일, webhook, 또는 runbook 작업을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-167">Use hello steps described in [add actions tooalert rules](log-analytics-alerts-actions.md) configure an e-mail, webhook, or runbook action for hello alert rule.</span></span>


## <a name="configuration"></a><span data-ttu-id="81c00-168">구성</span><span class="sxs-lookup"><span data-stu-id="81c00-168">Configuration</span></span>
### <a name="q-can-i-change-hello-name-of-hello-tableblob-container-used-tooread-from-azure-diagnostics-wad"></a><span data-ttu-id="81c00-169">Q.</span><span class="sxs-lookup"><span data-stu-id="81c00-169">Q.</span></span> <span data-ttu-id="81c00-170">변경 테이블/blob 사용 되는 컨테이너 tooread hello의 hello 이름에서 WAD (Azure 진단)?</span><span class="sxs-lookup"><span data-stu-id="81c00-170">Can I change hello name of hello table/blob container used tooread from Azure Diagnostics (WAD)?</span></span>

<span data-ttu-id="81c00-171">A.</span><span class="sxs-lookup"><span data-stu-id="81c00-171">A.</span></span> <span data-ttu-id="81c00-172">아니요, 현재는 가능 tooread 임의의 테이블 또는 컨테이너에에서 없는 Azure 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-172">No, it is not currently possible tooread from arbitrary tables or containers in Azure storage.</span></span>

### <a name="q-what-ip-addresses-does-hello-log-analytics-service-use-how-do-i-ensure-that-my-firewall-only-allows-traffic-toohello-log-analytics-service"></a><span data-ttu-id="81c00-173">Q.</span><span class="sxs-lookup"><span data-stu-id="81c00-173">Q.</span></span> <span data-ttu-id="81c00-174">IP 주소 로그 분석 서비스 사용 하 여 hello가?</span><span class="sxs-lookup"><span data-stu-id="81c00-174">What IP addresses does hello Log Analytics service use?</span></span> <span data-ttu-id="81c00-175">방화벽만 트래픽 toohello 로그 분석 서비스를 허용 하는지 확인?</span><span class="sxs-lookup"><span data-stu-id="81c00-175">How do I ensure that my firewall only allows traffic toohello Log Analytics service?</span></span>

<span data-ttu-id="81c00-176">A.</span><span class="sxs-lookup"><span data-stu-id="81c00-176">A.</span></span> <span data-ttu-id="81c00-177">hello 로그 분석 서비스는 Azure를 기반으로 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-177">hello Log Analytics service is built on top of Azure.</span></span> <span data-ttu-id="81c00-178">로그 분석 IP 주소는 hello [Microsoft Azure 데이터 센터 IP 범위](http://www.microsoft.com/download/details.aspx?id=41653)합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-178">Log Analytics IP addresses are in hello [Microsoft Azure Datacenter IP Ranges](http://www.microsoft.com/download/details.aspx?id=41653).</span></span>

<span data-ttu-id="81c00-179">서비스 배포는 hello hello 로그 분석 서비스의 실제 IP 주소가 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-179">As service deployments are made, hello actual IP addresses of hello Log Analytics service change.</span></span> <span data-ttu-id="81c00-180">방화벽을 통해 DNS 이름을 tooallow hello에 정리 되어 [로그 분석에서 프록시 및 방화벽 설정을 구성할](log-analytics-proxy-firewall.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-180">hello DNS names tooallow through your firewall are documented at [Configure proxy and firewall settings in Log Analytics](log-analytics-proxy-firewall.md).</span></span>

### <a name="q-i-use-expressroute-for-connecting-tooazure-does-my-log-analytics-traffic-use-my-expressroute-connection"></a><span data-ttu-id="81c00-181">Q.</span><span class="sxs-lookup"><span data-stu-id="81c00-181">Q.</span></span> <span data-ttu-id="81c00-182">TooAzure 연결 하기 위한 ExpressRoute 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-182">I use ExpressRoute for connecting tooAzure.</span></span> <span data-ttu-id="81c00-183">Log Analytics 트래픽이 내 ExpressRoute 연결을 사용하나요?</span><span class="sxs-lookup"><span data-stu-id="81c00-183">Does my Log Analytics traffic use my ExpressRoute connection?</span></span>

<span data-ttu-id="81c00-184">A.</span><span class="sxs-lookup"><span data-stu-id="81c00-184">A.</span></span> <span data-ttu-id="81c00-185">hello 다양 한 유형의 express 경로 트래픽이 hello에 설명 되어 [express 경로 설명서](../expressroute/expressroute-faqs.md#supported-services)합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-185">hello different types of ExpressRoute traffic are described in hello [ExpressRoute documentation](../expressroute/expressroute-faqs.md#supported-services).</span></span>

<span data-ttu-id="81c00-186">트래픽 tooLog 분석 hello 공용 피어 링 express 경로 회로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-186">Traffic tooLog Analytics uses hello public-peering ExpressRoute circuit.</span></span>

### <a name="q-is-there-a-simple-and-easy-way-toomove-an-existing-log-analytics-workspace-tooanother-log-analytics-workspaceazure-subscription"></a><span data-ttu-id="81c00-187">Q.</span><span class="sxs-lookup"><span data-stu-id="81c00-187">Q.</span></span> <span data-ttu-id="81c00-188">쉽고 간단한 방법이 toomove 기존 로그 분석 작업 영역 tooanother 로그 분석 작업 영역/Azure 구독 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="81c00-188">Is there a simple and easy way toomove an existing Log Analytics workspace tooanother Log Analytics workspace/Azure subscription?</span></span>

<span data-ttu-id="81c00-189">A.</span><span class="sxs-lookup"><span data-stu-id="81c00-189">A.</span></span> <span data-ttu-id="81c00-190">hello `Move-AzureRmResource` cmdlet을 사용 하면 로그 분석 작업 영역 및 자동화 계정에서 하나의 Azure 구독 tooanother 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-190">hello `Move-AzureRmResource` cmdlet lets you move a Log Analytics workspace, and also an Automation account from one Azure subscription tooanother.</span></span> <span data-ttu-id="81c00-191">자세한 내용은 [Move-AzureRmResource](http://msdn.microsoft.com/library/mt652516.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81c00-191">For more information, see [Move-AzureRmResource](http://msdn.microsoft.com/library/mt652516.aspx).</span></span>

<span data-ttu-id="81c00-192">이 변경 hello Azure 포털에서에서 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-192">This change can also be made in hello Azure portal.</span></span>

<span data-ttu-id="81c00-193">한 로그 분석 작업 영역 tooanother에서 데이터를 이동 하거나 로그 분석 데이터에 저장 되어 있는 hello 지역을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-193">You can’t move data from one Log Analytics workspace tooanother, or change hello region that Log Analytics data is stored in.</span></span>

### <a name="q-how-do-i-add-log-analytics-toosystem-center-operations-manager"></a><span data-ttu-id="81c00-194">Q: 로그 분석 tooSystem Center Operations Manager 추가 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="81c00-194">Q: How do I add Log Analytics tooSystem Center Operations Manager?</span></span>

<span data-ttu-id="81c00-195">A: toohello 최신 업데이트 롤업으로 업데이트 하 고 관리 팩을 가져오는 사용 하면 Operations Manager tooLog tooconnect 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-195">A:  Updating toohello latest update rollup and importing management packs enables you tooconnect Operations Manager tooLog Analytics.</span></span>

>[!NOTE]
><span data-ttu-id="81c00-196">Operations Manager 연결 tooLog hello 분석은 System Center Operations Manager 2012 SP1 이상에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-196">hello Operations Manager connection tooLog Analytics is only available for System Center Operations Manager 2012 SP1 and later.</span></span>

### <a name="q-how-can-i-confirm-that-an-agent-is-able-toocommunicate-with-log-analytics"></a><span data-ttu-id="81c00-197">Q: 에이전트와 로그 분석 수 toocommunicate 인지 확인할 수는 어떻게</span><span class="sxs-lookup"><span data-stu-id="81c00-197">Q: How can I confirm that an agent is able toocommunicate with Log Analytics?</span></span>

<span data-ttu-id="81c00-198">A: tooensure hello 에이전트가 OMS와 통신할 수로 이동: 제어판, 보안 및 설정, **Microsoft Monitoring Agent**합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-198">A: tooensure that hello agent can communicate with OMS, go to: Control Panel, Security & Settings, **Microsoft Monitoring Agent**.</span></span>

<span data-ttu-id="81c00-199">Hello에서 **Azure 로그 분석 (OMS)** 탭에서 녹색 확인 표시를 찾으세요.</span><span class="sxs-lookup"><span data-stu-id="81c00-199">Under hello **Azure Log Analytics (OMS)** tab, look for a green check mark.</span></span> <span data-ttu-id="81c00-200">녹색 확인 표시 아이콘이 hello 에이전트가 OMS 서비스 hello로 수 toocommunicate을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-200">A green check mark icon confirms that hello agent is able toocommunicate with hello OMS service.</span></span>

<span data-ttu-id="81c00-201">노란색 경고 아이콘은 hello 에이전트가 OMS와 통신 문제는 데 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-201">A yellow warning icon means hello agent is having issues communication with OMS.</span></span> <span data-ttu-id="81c00-202">일반적인 이유 중 하나는 hello Microsoft Monitoring Agent 서비스가 중지 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-202">One common reason is hello Microsoft Monitoring Agent service has stopped.</span></span> <span data-ttu-id="81c00-203">서비스 제어 관리자 toorestart hello 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-203">Use service control manager toorestart hello service.</span></span>

### <a name="q-how-do-i-stop-an-agent-from-communicating-with-log-analytics"></a><span data-ttu-id="81c00-204">Q: 에이전트가 Log Analytics와의 통신을 중지하도록 하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="81c00-204">Q: How do I stop an agent from communicating with Log Analytics?</span></span>

<span data-ttu-id="81c00-205">A: System Center Operations Manager에서 hello 관리자 관리 되는 컴퓨터 목록에서 hello 컴퓨터를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-205">A: In System Center Operations Manager, remove hello computer from hello Advisor managed computer list.</span></span> <span data-ttu-id="81c00-206">Operations Manager 업데이트 hello hello 에이전트 toono 긴 보고서 tooLog 분석의 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-206">Operations Manager updates hello configuration of hello agent toono longer report tooLog Analytics.</span></span> <span data-ttu-id="81c00-207">에이전트 tooLog 분석에 직접 연결에 대 한를 통해 통신할 중지할 수 있습니다: 제어판, 보안 및 설정, **Microsoft Monitoring Agent**합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-207">For agents connected tooLog Analytics directly, you can stop them from communicating through: Control Panel, Security & Settings, **Microsoft Monitoring Agent**.</span></span>
<span data-ttu-id="81c00-208">**Azure Log Analytics(OMS)**아래에서 나열된 모든 작업 영역을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-208">Under **Azure Log Analytics (OMS)**, remove all workspaces listed.</span></span>

### <a name="q-why-am-i-getting-an-error-when-i-try-toomove-my-workspace-from-one-azure-subscription-tooanother"></a><span data-ttu-id="81c00-209">Q 하는 동안 오류가 발생 하면 toomove 내 작업 영역에서 Azure 구독 하나 tooanother?</span><span class="sxs-lookup"><span data-stu-id="81c00-209">Q: Why am I getting an error when I try toomove my workspace from one Azure subscription tooanother?</span></span>

<span data-ttu-id="81c00-210">A: hello Azure 포털을 사용 하는 경우 hello 이동에 대 한만 hello 작업 영역을 선택 하는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-210">A: If you are using hello Azure portal, ensure only hello workspace is selected for hello move.</span></span> <span data-ttu-id="81c00-211">Hello 솔루션을 선택 하지 마십시오-hello 작업 영역 이동 되 면 자동으로 이동 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-211">Do not select hello solutions -- they will automatically move after hello workspace moves.</span></span> 

<span data-ttu-id="81c00-212">두 Azure 구독에서 권한을 갖는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-212">Ensure you have permission in both Azure subscriptions.</span></span>

## <a name="agent-data"></a><span data-ttu-id="81c00-213">에이전트 데이터</span><span class="sxs-lookup"><span data-stu-id="81c00-213">Agent data</span></span>
### <a name="q-how-much-data-can-i-send-through-hello-agent-toolog-analytics-is-there-a-maximum-amount-of-data-per-customer"></a><span data-ttu-id="81c00-214">Q.</span><span class="sxs-lookup"><span data-stu-id="81c00-214">Q.</span></span> <span data-ttu-id="81c00-215">Hello 에이전트 tooLog 분석을 통해 보낼 수 있는 데이터의 크기는 있습니까?</span><span class="sxs-lookup"><span data-stu-id="81c00-215">How much data can I send through hello agent tooLog Analytics?</span></span> <span data-ttu-id="81c00-216">고객 한 명당 최대 데이터 용량이 있나요?</span><span class="sxs-lookup"><span data-stu-id="81c00-216">Is there a maximum amount of data per customer?</span></span>
<span data-ttu-id="81c00-217">A.</span><span class="sxs-lookup"><span data-stu-id="81c00-217">A.</span></span> <span data-ttu-id="81c00-218">hello 무료 계획 작업 영역당 500MB의 일일 한도가 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-218">hello free plan sets a daily cap of 500 MB per workspace.</span></span> <span data-ttu-id="81c00-219">hello 표준 및 프리미엄 계획 hello 업로드 된 데이터 크기 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-219">hello standard and premium plans have no limit on hello amount of data that is uploaded.</span></span> <span data-ttu-id="81c00-220">로그 분석은 설계 된 클라우드 서비스로 tooautomatically 수직 확장 toohandle hello 볼륨 1 일당 수 테라바이트가 되더라도 고객 으로부터 제공 될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-220">As a cloud service, Log Analytics is designed tooautomatically scale up toohandle hello volume coming from a customer – even if it is terabytes per day.</span></span>

<span data-ttu-id="81c00-221">hello 로그 분석 에이전트에서이 공간이 작도록 설계 된 tooensure.</span><span class="sxs-lookup"><span data-stu-id="81c00-221">hello Log Analytics agent was designed tooensure it has a small footprint.</span></span> <span data-ttu-id="81c00-222">한 고객 hello에 대해 수행한 테스트 되었으면 그 결과 얼마나 만족 한은 에이전트에 대 한 블로그를 썼습니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-222">One of our customers wrote a blog about hello tests they performed against our agent and how impressed they were.</span></span> <span data-ttu-id="81c00-223">hello 데이터 볼륨을 사용 하도록 설정 하면 hello 솔루션에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-223">hello data volume varies based on hello solutions you enable.</span></span> <span data-ttu-id="81c00-224">Hello 별 hello에 솔루션에 의해 참조와 hello 데이터 볼륨에 대 한 자세한 정보를 찾을 수 [사용](log-analytics-usage.md) 페이지.</span><span class="sxs-lookup"><span data-stu-id="81c00-224">You can find detailed information on hello data volume and see hello breakup by solution in hello [Usage](log-analytics-usage.md) page.</span></span>

<span data-ttu-id="81c00-225">자세한 내용은 참조는 [고객 블로그](http://thoughtsonopsmgr.blogspot.com/2015/09/one-small-footprint-for-server-one.html) hello hello OMS 에이전트의 작은 사용 공간에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-225">For more information, you can read a [customer blog](http://thoughtsonopsmgr.blogspot.com/2015/09/one-small-footprint-for-server-one.html) about hello low footprint of hello OMS agent.</span></span>

### <a name="q-how-much-network-bandwidth-is-used-by-hello-microsoft-management-agent-mma-when-sending-data-toolog-analytics"></a><span data-ttu-id="81c00-226">Q.</span><span class="sxs-lookup"><span data-stu-id="81c00-226">Q.</span></span> <span data-ttu-id="81c00-227">얼마나 많은 네트워크 대역폭 사용 되는 Microsoft Management Agent (MMA) hello 하 여 데이터 tooLog 분석에 보낼 때</span><span class="sxs-lookup"><span data-stu-id="81c00-227">How much network bandwidth is used by hello Microsoft Management Agent (MMA) when sending data tooLog Analytics?</span></span>

<span data-ttu-id="81c00-228">A.</span><span class="sxs-lookup"><span data-stu-id="81c00-228">A.</span></span> <span data-ttu-id="81c00-229">대역폭은 전송 된 데이터의 hello 금액에는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-229">Bandwidth is a function on hello amount of data sent.</span></span> <span data-ttu-id="81c00-230">데이터는 hello 네트워크를 통해 전송 될 때 압축 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-230">Data is compressed as it is sent over hello network.</span></span>

### <a name="q-how-much-data-is-sent-per-agent"></a><span data-ttu-id="81c00-231">Q.</span><span class="sxs-lookup"><span data-stu-id="81c00-231">Q.</span></span> <span data-ttu-id="81c00-232">에이전트당 얼마나 많은 데이터가 전송되나요?</span><span class="sxs-lookup"><span data-stu-id="81c00-232">How much data is sent per agent?</span></span>

<span data-ttu-id="81c00-233">A.</span><span class="sxs-lookup"><span data-stu-id="81c00-233">A.</span></span> <span data-ttu-id="81c00-234">hello 에이전트당 전송 되는 데이터에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-234">hello amount of data sent per agent depends on:</span></span>

* <span data-ttu-id="81c00-235">설정한 hello 솔루션</span><span class="sxs-lookup"><span data-stu-id="81c00-235">hello solutions you have enabled</span></span>
* <span data-ttu-id="81c00-236">로그 및 성능 카운터 수집 되 고 hello 수</span><span class="sxs-lookup"><span data-stu-id="81c00-236">hello number of logs and performance counters being collected</span></span>
* <span data-ttu-id="81c00-237">hello 로그에서 데이터의 hello 볼륨</span><span class="sxs-lookup"><span data-stu-id="81c00-237">hello volume of data in hello logs</span></span>

<span data-ttu-id="81c00-238">hello 무료 가격 책정 계층은 좋은 방법 tooonboard 여러 서버 및 hello 일반적인 데이터 볼륨을 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-238">hello free pricing tier is a good way tooonboard several servers and gauge hello typical data volume.</span></span> <span data-ttu-id="81c00-239">Hello에 사용량이 표시 되는 전반적인 [사용](log-analytics-usage.md) 페이지.</span><span class="sxs-lookup"><span data-stu-id="81c00-239">Overall usage is shown on hello [Usage](log-analytics-usage.md) page.</span></span>

<span data-ttu-id="81c00-240">컴퓨터 수 toorun hello WireData 에이전트에 대해 얼마나 많은 데이터가 전송 되는 쿼리 toosee 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-240">For computers that are able toorun hello WireData agent, use hello following query toosee how much data is being sent:</span></span>

```
Type=WireData (ProcessName="C:\\Program Files\\Microsoft Monitoring Agent\\Agent\\MonitoringHost.exe") (Direction=Outbound) | measure Sum(TotalBytes) by Computer
```



## <a name="next-steps"></a><span data-ttu-id="81c00-241">다음 단계</span><span class="sxs-lookup"><span data-stu-id="81c00-241">Next steps</span></span>
* <span data-ttu-id="81c00-242">[로그 분석 작업 시작](log-analytics-get-started.md) toolearn 로그 분석 및 분 단위로 실행할에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c00-242">[Get started with Log Analytics](log-analytics-get-started.md) toolearn more about Log Analytics and get up and running in minutes.</span></span>
