---
title: "OMS 로그 분석에서 aaaResponses tooalerts | Microsoft Docs"
description: "로그 분석에 OMS 리포지토리에 중요 한 정보를 식별 및 수 사전 문제점을 알려 경고나 작업 tooattempt toocorrect 호출을 합니다.  이 문서에서는 어떻게 toocreate 경고 규칙 및 세부 정보 hello 다양 한 작업 취할 수를 설명 합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d24bb726a96e7143985f111c0599dc4e7898b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-actions-tooalert-rules-in-log-analytics"></a><span data-ttu-id="4bec9-104">로그 분석의 동작 tooalert 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="4bec9-104">Add actions tooalert rules in Log Analytics</span></span>
<span data-ttu-id="4bec9-105">때는 [로그 분석에 경고가 생성 됩니다](log-analytics-alerts.md), hello 옵션이 [구성 hello 경고 규칙](log-analytics-alerts.md) tooperform 하나 이상의 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-105">When an [alert is created in Log Analytics](log-analytics-alerts.md), you have hello option of [configuring hello alert rule](log-analytics-alerts.md) tooperform one or more actions.</span></span>  <span data-ttu-id="4bec9-106">이 문서에서는 각 종류를 구성 하는 방법에 사용할 수 있는 다른 작업 hello 및 세부 정보를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-106">This article describes hello different actions that are available and details on configuring each kind.</span></span>

| <span data-ttu-id="4bec9-107">동작</span><span class="sxs-lookup"><span data-stu-id="4bec9-107">Action</span></span> | <span data-ttu-id="4bec9-108">설명</span><span class="sxs-lookup"><span data-stu-id="4bec9-108">Description</span></span> |
|:--|:--|
| [<span data-ttu-id="4bec9-109">Email</span><span class="sxs-lookup"><span data-stu-id="4bec9-109">Email</span></span>](#email-actions) | <span data-ttu-id="4bec9-110">Hello 경고 tooone 또는 더 많은 수신자 한 hello 세부 정보가 포함 된 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-110">Send an e-mail with hello details of hello alert tooone or more recipients.</span></span> |
| [<span data-ttu-id="4bec9-111">웹후크</span><span class="sxs-lookup"><span data-stu-id="4bec9-111">Webhook</span></span>](#webhook-actions) | <span data-ttu-id="4bec9-112">단일 HTTP POST 요청을 통해 외부 프로세스를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-112">Invoke an external process through a single HTTP POST request.</span></span> |
| [<span data-ttu-id="4bec9-113">Runbook</span><span class="sxs-lookup"><span data-stu-id="4bec9-113">Runbook</span></span>](#runbook-actions) | <span data-ttu-id="4bec9-114">Azure Automation에서 Runbook을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-114">Start a runbook in Azure Automation.</span></span> |


## <a name="email-actions"></a><span data-ttu-id="4bec9-115">전자 메일 작업</span><span class="sxs-lookup"><span data-stu-id="4bec9-115">Email actions</span></span>
<span data-ttu-id="4bec9-116">전자 메일 작업 hello 경고 tooone 또는 더 많은 수신자 한 hello 세부 정보가 포함 된 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-116">Email actions send an e-mail with hello details of hello alert tooone or more recipients.</span></span>  <span data-ttu-id="4bec9-117">Hello 메일의 hello 주체를 지정할 수는 있지만 콘텐츠는 로그 분석에 의해 생성 되는 표준 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-117">You can specify hello subject of hello mail, but it's content is a standard format constructed by Log Analytics.</span></span>  <span data-ttu-id="4bec9-118">Hello 로그 검색에서 반환 된 tooten 레코드를의 추가 toodetails에 hello 경고의 hello 이름과 같은 요약 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-118">It includes summary information such as hello name of hello alert in addition toodetails of up tooten records returned by hello log search.</span></span>  <span data-ttu-id="4bec9-119">또한 해당 쿼리에서 hello 레코드의 전체 집합을 반환 하는 로그 분석에 링크 tooa 로그 검색을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-119">It also includes a link tooa log search in Log Analytics that will return hello entire set of records from that query.</span></span>   <span data-ttu-id="4bec9-120">hello 메일의 보낸 사람이 hello *Microsoft Operations Management Suite 팀 &lt; noreply@oms.microsoft.com &gt;* 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-120">hello sender of hello mail is *Microsoft Operations Management Suite Team &lt;noreply@oms.microsoft.com&gt;*.</span></span> 

<span data-ttu-id="4bec9-121">전자 메일 작업 hello 속성 hello 표 다음에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-121">Email actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="4bec9-122">속성</span><span class="sxs-lookup"><span data-stu-id="4bec9-122">Property</span></span> | <span data-ttu-id="4bec9-123">설명</span><span class="sxs-lookup"><span data-stu-id="4bec9-123">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4bec9-124">제목</span><span class="sxs-lookup"><span data-stu-id="4bec9-124">Subject</span></span> |<span data-ttu-id="4bec9-125">Hello 전자 메일의 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-125">Subject in hello email.</span></span>  <span data-ttu-id="4bec9-126">Hello 메일의 본문 hello를 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-126">You cannot modify hello body of hello mail.</span></span> |
| <span data-ttu-id="4bec9-127">받는 사람</span><span class="sxs-lookup"><span data-stu-id="4bec9-127">Recipients</span></span> |<span data-ttu-id="4bec9-128">모든 전자 메일 받는 사람의 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-128">Addresses of all e-mail recipients.</span></span>  <span data-ttu-id="4bec9-129">세미콜론 (;)를 사용 하 여 여러 개의 주소가 다음 별도 hello 주소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-129">If you specify more than one address, then separate hello addresses with a semicolon (;).</span></span> |


## <a name="webhook-actions"></a><span data-ttu-id="4bec9-130">웹후크 작업</span><span class="sxs-lookup"><span data-stu-id="4bec9-130">Webhook actions</span></span>

<span data-ttu-id="4bec9-131">Webhook 작업 tooinvoke 단일 HTTP POST 요청을 통해 외부 프로세스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-131">Webhook actions allow you tooinvoke an external process through a single HTTP POST request.</span></span>  <span data-ttu-id="4bec9-132">호출 중인 hello 서비스 webhook을 지원 하 고 모든 페이로드 사용 방식 결정 해야 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-132">hello service being called should support webhooks and determine how it will use any payload it receives.</span></span>  <span data-ttu-id="4bec9-133">또한 webhook hello 요청은 형식 API에 대 한 이해는 hello로 특별히 지원 하지 않는 REST API를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-133">You could also call a REST API that doesn't specifically support webhooks as long as hello request is in a format that hello API understands.</span></span>  <span data-ttu-id="4bec9-134">응답 tooan 경고에는 webhook을 사용 하는 예제는 메시지를 보내도록 [Slack](http://slack.com) 에서 인시던트를 만들거나 [PagerDuty](http://pagerduty.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-134">Examples of using a webhook in response tooan alert are sending a message in [Slack](http://slack.com) or creating an incident in [PagerDuty](http://pagerduty.com/).</span></span>  <span data-ttu-id="4bec9-135">제공 되는 전체 연습은 webhook toocall 여유 시간을 사용 하 여 경고 규칙을 만드는 [로그 분석 경고에 대 한 Webhook](log-analytics-alerts-webhooks.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-135">A complete walkthrough of creating an alert rule with a webhook toocall Slack is available at [Webhooks in Log Analytics alerts](log-analytics-alerts-webhooks.md).</span></span>

<span data-ttu-id="4bec9-136">Webhook 작업 hello 속성 hello 표 다음에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-136">Webhook actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="4bec9-137">속성</span><span class="sxs-lookup"><span data-stu-id="4bec9-137">Property</span></span> | <span data-ttu-id="4bec9-138">설명</span><span class="sxs-lookup"><span data-stu-id="4bec9-138">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4bec9-139">Webhook URL</span><span class="sxs-lookup"><span data-stu-id="4bec9-139">Webhook URL</span></span> |<span data-ttu-id="4bec9-140">hello webhook의 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-140">hello URL of hello webhook.</span></span> |
| <span data-ttu-id="4bec9-141">사용자 지정 JSON 페이로드</span><span class="sxs-lookup"><span data-stu-id="4bec9-141">Custom JSON payload</span></span> |<span data-ttu-id="4bec9-142">사용자 지정 페이로드 toosend hello webhook 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-142">Custom payload toosend with hello webhook.</span></span>  <span data-ttu-id="4bec9-143">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4bec9-143">See below for details.</span></span> |


<span data-ttu-id="4bec9-144">Webhook URL을 포함 하 고 hello 데이터가 JSON으로 서식이 지정 된 페이로드 toohello 외부 서비스를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-144">Webhooks include a URL and a payload formatted in JSON that is hello data sent toohello external service.</span></span>  <span data-ttu-id="4bec9-145">기본적으로 hello 페이로드는 다음 표에 hello에 hello 값을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-145">By default, hello payload will include hello values in hello following table.</span></span>  <span data-ttu-id="4bec9-146">사용자 고유의 중 하나를 사용자 지정이 페이로드의 tooreplace를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-146">You can choose tooreplace this payload with a custom one of your own.</span></span>  <span data-ttu-id="4bec9-147">이 경우 사용할 수 있습니다 hello 테이블에 있는 hello 변수에 각 매개 변수 tooinclude hello에 대 한 해당 값에 사용자 지정 페이로드.</span><span class="sxs-lookup"><span data-stu-id="4bec9-147">In that case you can use hello variables in hello table for each of hello parameters tooinclude their value in your custom payload.</span></span>

| <span data-ttu-id="4bec9-148">매개 변수</span><span class="sxs-lookup"><span data-stu-id="4bec9-148">Parameter</span></span> | <span data-ttu-id="4bec9-149">변수</span><span class="sxs-lookup"><span data-stu-id="4bec9-149">Variable</span></span> | <span data-ttu-id="4bec9-150">설명</span><span class="sxs-lookup"><span data-stu-id="4bec9-150">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="4bec9-151">AlertRuleName</span><span class="sxs-lookup"><span data-stu-id="4bec9-151">AlertRuleName</span></span> |<span data-ttu-id="4bec9-152">#alertrulename</span><span class="sxs-lookup"><span data-stu-id="4bec9-152">#alertrulename</span></span> |<span data-ttu-id="4bec9-153">Hello 경고 규칙의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-153">Name of hello alert rule.</span></span> |
| <span data-ttu-id="4bec9-154">AlertThresholdOperator</span><span class="sxs-lookup"><span data-stu-id="4bec9-154">AlertThresholdOperator</span></span> |<span data-ttu-id="4bec9-155">#thresholdoperator</span><span class="sxs-lookup"><span data-stu-id="4bec9-155">#thresholdoperator</span></span> |<span data-ttu-id="4bec9-156">Hello 경고 규칙에 대 한 임계값 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-156">Threshold operator for hello alert rule.</span></span>  <span data-ttu-id="4bec9-157">*보다 큼* 또는 *보다 작음*.</span><span class="sxs-lookup"><span data-stu-id="4bec9-157">*Greater than* or *Less than*.</span></span> |
| <span data-ttu-id="4bec9-158">AlertThresholdValue</span><span class="sxs-lookup"><span data-stu-id="4bec9-158">AlertThresholdValue</span></span> |<span data-ttu-id="4bec9-159">#thresholdvalue</span><span class="sxs-lookup"><span data-stu-id="4bec9-159">#thresholdvalue</span></span> |<span data-ttu-id="4bec9-160">Hello 경고 규칙에 대 한 임계값입니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-160">Threshold value for hello alert rule.</span></span> |
| <span data-ttu-id="4bec9-161">LinkToSearchResults</span><span class="sxs-lookup"><span data-stu-id="4bec9-161">LinkToSearchResults</span></span> |<span data-ttu-id="4bec9-162">#linktosearchresults</span><span class="sxs-lookup"><span data-stu-id="4bec9-162">#linktosearchresults</span></span> |<span data-ttu-id="4bec9-163">Hello 경고를 생성 하는 hello 쿼리에서 hello 레코드를 반환 하는 tooLog 분석 로그 검색에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-163">Link tooLog Analytics log search that returns hello records from hello query that created hello alert.</span></span> |
| <span data-ttu-id="4bec9-164">ResultCount</span><span class="sxs-lookup"><span data-stu-id="4bec9-164">ResultCount</span></span> |<span data-ttu-id="4bec9-165">#searchresultcount</span><span class="sxs-lookup"><span data-stu-id="4bec9-165">#searchresultcount</span></span> |<span data-ttu-id="4bec9-166">Hello 검색 결과에서 레코드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-166">Number of records in hello search results.</span></span> |
| <span data-ttu-id="4bec9-167">SearchIntervalEndtimeUtc</span><span class="sxs-lookup"><span data-stu-id="4bec9-167">SearchIntervalEndtimeUtc</span></span> |<span data-ttu-id="4bec9-168">#searchintervalendtimeutc</span><span class="sxs-lookup"><span data-stu-id="4bec9-168">#searchintervalendtimeutc</span></span> |<span data-ttu-id="4bec9-169">Hello 쿼리 UTC 형식에서에 대 한 종료 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-169">End time for hello query in UTC format.</span></span> |
| <span data-ttu-id="4bec9-170">SearchIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="4bec9-170">SearchIntervalInSeconds</span></span> |<span data-ttu-id="4bec9-171">#searchinterval</span><span class="sxs-lookup"><span data-stu-id="4bec9-171">#searchinterval</span></span> |<span data-ttu-id="4bec9-172">Hello 경고 규칙에 대 한 시간 창입니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-172">Time window for hello alert rule.</span></span> |
| <span data-ttu-id="4bec9-173">SearchIntervalStartTimeUtc</span><span class="sxs-lookup"><span data-stu-id="4bec9-173">SearchIntervalStartTimeUtc</span></span> |<span data-ttu-id="4bec9-174">#searchintervalstarttimeutc</span><span class="sxs-lookup"><span data-stu-id="4bec9-174">#searchintervalstarttimeutc</span></span> |<span data-ttu-id="4bec9-175">Hello 쿼리에 대 한 시간을 UTC 형식에서 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-175">Start time for hello query in UTC format.</span></span> |
| <span data-ttu-id="4bec9-176">SearchQuery</span><span class="sxs-lookup"><span data-stu-id="4bec9-176">SearchQuery</span></span> |<span data-ttu-id="4bec9-177">#searchquery</span><span class="sxs-lookup"><span data-stu-id="4bec9-177">#searchquery</span></span> |<span data-ttu-id="4bec9-178">로그 검색 쿼리 hello 경고 규칙으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-178">Log search query used by hello alert rule.</span></span> |
| <span data-ttu-id="4bec9-179">SearchResults</span><span class="sxs-lookup"><span data-stu-id="4bec9-179">SearchResults</span></span> |<span data-ttu-id="4bec9-180">아래 참조</span><span class="sxs-lookup"><span data-stu-id="4bec9-180">See below</span></span> |<span data-ttu-id="4bec9-181">JSON 형식의 hello 쿼리에서 반환 된 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-181">Records returned by hello query in JSON format.</span></span>  <span data-ttu-id="4bec9-182">제한 된 toohello 먼저 5, 000 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-182">Limited toohello first 5,000 records.</span></span> |
| <span data-ttu-id="4bec9-183">WorkspaceID</span><span class="sxs-lookup"><span data-stu-id="4bec9-183">WorkspaceID</span></span> |<span data-ttu-id="4bec9-184">#workspaceid</span><span class="sxs-lookup"><span data-stu-id="4bec9-184">#workspaceid</span></span> |<span data-ttu-id="4bec9-185">OMS 작업 영역의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-185">ID of your OMS workspace.</span></span> |

<span data-ttu-id="4bec9-186">예를 들어 다음 라는 단일 매개 변수를 포함 하는 사용자 지정 페이로드 hello를 지정할 수 있습니다 *텍스트*합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-186">For example, you might specify hello following custom payload that includes a single parameter called *text*.</span></span>  <span data-ttu-id="4bec9-187">이 webhook 호출 hello 서비스는이 매개 변수를 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-187">hello service that this webhook calls would be expecting this parameter.</span></span>

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

<span data-ttu-id="4bec9-188">이 예에서는 페이로드를 hello 때 다음 같은 toosomething 전송 toohello webhook 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-188">This example payload would resolve toosomething like hello following when sent toohello webhook.</span></span>

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

<span data-ttu-id="4bec9-189">검색 결과 사용자 지정 페이로드를 tooinclude hello hello json 페이로드에서 최상위 속성으로 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-189">tooinclude search results in a custom payload, add hello following line as a top level property in hello json payload.</span></span>  

    "IncludeSearchResults":true

<span data-ttu-id="4bec9-190">예를 들어 방금 hello 경고 이름 및 hello 검색 결과 포함 하는 사용자 지정 페이로드 toocreate hello 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-190">For example, toocreate a custom payload that includes just hello alert name and hello search results, you could use hello following.</span></span> 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


<span data-ttu-id="4bec9-191">외부 서비스 webhook toostart를 사용 하 여 경고 규칙을 만드는 전체 예제를 진행할 수 [toosend 메시지 tooSlack OMS 로그 분석에서에서 경고 webhook 작업을 만들](log-analytics-alerts-webhooks.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-191">You can walk through a complete example of creating an alert rule with a webhook toostart an external service at [Create an alert webhook action in OMS Log Analytics toosend message tooSlack](log-analytics-alerts-webhooks.md).</span></span>

## <a name="runbook-actions"></a><span data-ttu-id="4bec9-192">Runbook 작업</span><span class="sxs-lookup"><span data-stu-id="4bec9-192">Runbook actions</span></span>
<span data-ttu-id="4bec9-193">Runbook 작업은 Azure 자동화에서 Runbook을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-193">Runbook actions start a runbook in Azure Automation.</span></span>  <span data-ttu-id="4bec9-194">주문 toouse 이런이 종류의 동작, hello 있어야 [자동화 솔루션](log-analytics-add-solutions.md) OMS 작업 영역에 설치 및 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-194">In order toouse this type of action, you must have hello [Automation solution](log-analytics-add-solutions.md) installed and configured in your OMS workspace.</span></span>  <span data-ttu-id="4bec9-195">Hello 자동화 솔루션에서에서 구성한 hello 자동화 계정에서 hello runbook에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-195">You can select from hello runbooks in hello automation account that you configured in hello Automation solution.</span></span>

<span data-ttu-id="4bec9-196">Runbook 작업에는 다음 표에 hello에 hello 속성 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-196">Runbook actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="4bec9-197">속성</span><span class="sxs-lookup"><span data-stu-id="4bec9-197">Property</span></span> | <span data-ttu-id="4bec9-198">설명</span><span class="sxs-lookup"><span data-stu-id="4bec9-198">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="4bec9-199">Runbook</span><span class="sxs-lookup"><span data-stu-id="4bec9-199">Runbook</span></span> | <span data-ttu-id="4bec9-200">경고를 만들 때 toostart 되도록 Runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-200">Runbook that you want toostart when an alert is created.</span></span> |
| <span data-ttu-id="4bec9-201">실행</span><span class="sxs-lookup"><span data-stu-id="4bec9-201">Run on</span></span> | <span data-ttu-id="4bec9-202">지정 **Azure** hello 클라우드에서 toorun hello runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-202">Specify **Azure** toorun hello runbook in hello cloud.</span></span>  <span data-ttu-id="4bec9-203">지정 **Hybrid worker** 와 에이전트에서 toorun hello runbook [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-203">Specify **Hybrid worker** toorun hello runbook on an agent with [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) installed.</span></span>  |

<span data-ttu-id="4bec9-204">Runbook 작업을 사용 하 여 hello runbook 시작는 [webhook](../automation/automation-webhooks.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-204">Runbook actions start hello runbook using a [webhook](../automation/automation-webhooks.md).</span></span>  <span data-ttu-id="4bec9-205">Hello 경고 규칙을 만들 때 자동으로 만들어집니다 hello runbook에 대 한 새 webhook hello 이름의 **OMS 경고 재구성** GUID가 차례로 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-205">When you create hello alert rule, it will automatically create a new webhook for hello runbook with hello name **OMS Alert Remediation** followed by a GUID.</span></span>  

<span data-ttu-id="4bec9-206">직접 hello runbook의 모든 매개 변수를 채울 하지만 hello 없습니다 [$WebhookData 매개 변수](../automation/automation-webhooks.md) hello를 만든 hello 로그 검색 결과 포함 하 여 hello 알림의 hello 세부 정보가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-206">You cannot directly populate any parameters of hello runbook, but hello [$WebhookData parameter](../automation/automation-webhooks.md) will include hello details of hello alert, including hello results of hello log search that created it.</span></span>  <span data-ttu-id="4bec9-207">hello runbook toodefine 할 **$WebhookData** 것에 대 한 매개 변수로 tooaccess hello hello 경고의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-207">hello runbook will need toodefine **$WebhookData** as a parameter for it tooaccess hello properties of hello alert.</span></span>  <span data-ttu-id="4bec9-208">hello 경고 데이터는 라는 단일 속성에 대 한 json 형식으로 사용할 수 있는 **SearchResults** hello에 **RequestBody** 속성 **$WebhookData**합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-208">hello alert data is available in json format in a single property called **SearchResults** in hello **RequestBody** property of **$WebhookData**.</span></span>  <span data-ttu-id="4bec9-209">다음 표에 hello hello 속성과 함께이 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-209">This will have with hello properties in hello following table.</span></span>

| <span data-ttu-id="4bec9-210">노드</span><span class="sxs-lookup"><span data-stu-id="4bec9-210">Node</span></span> | <span data-ttu-id="4bec9-211">설명</span><span class="sxs-lookup"><span data-stu-id="4bec9-211">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4bec9-212">id</span><span class="sxs-lookup"><span data-stu-id="4bec9-212">id</span></span> |<span data-ttu-id="4bec9-213">경로 hello 검색의 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-213">Path and GUID of hello search.</span></span> |
| <span data-ttu-id="4bec9-214">__metadata</span><span class="sxs-lookup"><span data-stu-id="4bec9-214">__metadata</span></span> |<span data-ttu-id="4bec9-215">Hello 경고 포함 하 여 hello 레코드의 수 및 hello 검색 결과의 상태에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-215">Information about hello alert including hello number of records and status of hello search results.</span></span> |
| <span data-ttu-id="4bec9-216">값</span><span class="sxs-lookup"><span data-stu-id="4bec9-216">value</span></span> |<span data-ttu-id="4bec9-217">Hello 검색 결과의 각 레코드에 대 한 별도 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-217">Separate entry for each record in hello search results.</span></span>  <span data-ttu-id="4bec9-218">hello 항목의 hello 세부 정보에는 hello 레코드의 hello 속성 및 값과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-218">hello details of hello entry will match hello properties and values of hello record.</span></span> |

<span data-ttu-id="4bec9-219">예를 들어 hello 다음 runbook은 hello 로그 검색에서 반환 되는 hello 레코드를 추출 하 고 각 레코드의 hello 형식을 기반으로 하는 다른 속성을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-219">For example, hello following runbook would extract hello records returned by hello log search  and assign different properties based on hello type of each record.</span></span>  <span data-ttu-id="4bec9-220">변환 하 여 해당 hello runbook 시작 **RequestBody** 에서 json 한다는 PowerShell의 개체와 작동할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-220">Note that hello runbook starts by converting **RequestBody** from json so that it can be worked with as an object in PowerShell.</span></span>

    param ( 
        [object]$WebhookData
    )

    $RequestBody = ConvertFrom-JSON -InputObject $WebhookData.RequestBody
    $Records     = $RequestBody.SearchResults.value

    foreach ($Record in $Records)
    {
        $Computer = $Record.Computer

        if ($Record.Type -eq 'Event')
        {
            $EventNo    = $Record.EventID
            $EventLevel = $Record.EventLevelName
            $EventData  = $Record.EventData
        }

        if ($Record.Type -eq 'Perf')
        {
            $Object    = $Record.ObjectName
            $Counter   = $Record.CounterName
            $Instance  = $Record.InstanceName
            $Value     = $Record.CounterValue
        }
    }


## <a name="next-steps"></a><span data-ttu-id="4bec9-221">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4bec9-221">Next steps</span></span>
- <span data-ttu-id="4bec9-222">경고 규칙을 사용하여 [웹후크를 구성](log-analytics-alerts-webhooks.md) 하는 연습을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-222">Complete a walkthrough for [configuring a webook](log-analytics-alerts-webhooks.md) with an alert rule.</span></span>  
- <span data-ttu-id="4bec9-223">자세한 내용은 어떻게 toowrite [Azure 자동화의 runbook](https://azure.microsoft.com/documentation/services/automation) tooremediate 문제를 경고로 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bec9-223">Learn how toowrite [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) tooremediate problems identified by alerts.</span></span>
