---
title: "OMS Log Analytics에서 경고에 대한 응답 | Microsoft Docs"
description: "Log Analytics의 경고는 OMS 저장소의 중요한 정보를 식별하며 문제를 미리 알리거나 작업을 호출하여 문제 해결을 시도합니다.  이 문서에서는 경고 규칙을 만드는 방법을 설명하고 규칙에서 실행할 수 있는 여러 가지 작업을 자세히 설명합니다."
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
ms.openlocfilehash: b8731e1fe48b7d809b113eb5273e3962542b8f34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-actions-to-alert-rules-in-log-analytics"></a><span data-ttu-id="fbe61-104">Log Analytics에서 경고 규칙에 작업 추가</span><span class="sxs-lookup"><span data-stu-id="fbe61-104">Add actions to alert rules in Log Analytics</span></span>
<span data-ttu-id="fbe61-105">[경고가 Log Analytics에서 생성](log-analytics-alerts.md)될 때 하나 이상의 작업을 수행하는 [경고 규칙 구성](log-analytics-alerts.md)의 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-105">When an [alert is created in Log Analytics](log-analytics-alerts.md), you have the option of [configuring the alert rule](log-analytics-alerts.md) to perform one or more actions.</span></span>  <span data-ttu-id="fbe61-106">이 문서에서는 사용 가능한 다양한 작업 및 각 종류를 구성하는 세부 정보를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-106">This article describes the different actions that are available and details on configuring each kind.</span></span>

| <span data-ttu-id="fbe61-107">작업</span><span class="sxs-lookup"><span data-stu-id="fbe61-107">Action</span></span> | <span data-ttu-id="fbe61-108">설명</span><span class="sxs-lookup"><span data-stu-id="fbe61-108">Description</span></span> |
|:--|:--|
| [<span data-ttu-id="fbe61-109">Email</span><span class="sxs-lookup"><span data-stu-id="fbe61-109">Email</span></span>](#email-actions) | <span data-ttu-id="fbe61-110">한 명 이상의 수신자에게 경고의 세부 정보가 포함된 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-110">Send an e-mail with the details of the alert to one or more recipients.</span></span> |
| [<span data-ttu-id="fbe61-111">웹후크</span><span class="sxs-lookup"><span data-stu-id="fbe61-111">Webhook</span></span>](#webhook-actions) | <span data-ttu-id="fbe61-112">단일 HTTP POST 요청을 통해 외부 프로세스를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-112">Invoke an external process through a single HTTP POST request.</span></span> |
| [<span data-ttu-id="fbe61-113">Runbook</span><span class="sxs-lookup"><span data-stu-id="fbe61-113">Runbook</span></span>](#runbook-actions) | <span data-ttu-id="fbe61-114">Azure Automation에서 Runbook을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-114">Start a runbook in Azure Automation.</span></span> |


## <a name="email-actions"></a><span data-ttu-id="fbe61-115">전자 메일 작업</span><span class="sxs-lookup"><span data-stu-id="fbe61-115">Email actions</span></span>
<span data-ttu-id="fbe61-116">전자 메일 작업은 한 명 이상의 수신자에게 경고의 세부 정보가 포함된 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-116">Email actions send an e-mail with the details of the alert to one or more recipients.</span></span>  <span data-ttu-id="fbe61-117">메일의 제목을 지정할 수 있지만 그 내용은 Log Analytics이 구성한 표준 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-117">You can specify the subject of the mail, but it's content is a standard format constructed by Log Analytics.</span></span>  <span data-ttu-id="fbe61-118">메일은 로그 검색에서 반환된 10개까지의 레코드에 대한 세부 정보 외에 경고의 이름과 같은 요약 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-118">It includes summary information such as the name of the alert in addition to details of up to ten records returned by the log search.</span></span>  <span data-ttu-id="fbe61-119">또한 쿼리에서 전체 레코드 집합을 반환할 Log Analytics의 로그 검색에 대한 링크를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-119">It also includes a link to a log search in Log Analytics that will return the entire set of records from that query.</span></span>   <span data-ttu-id="fbe61-120">메일의 보낸 사람은 *Microsoft Operations Management Suite Team &lt;noreply@oms.microsoft.com&gt;*입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-120">The sender of the mail is *Microsoft Operations Management Suite Team &lt;noreply@oms.microsoft.com&gt;*.</span></span> 

<span data-ttu-id="fbe61-121">전자 메일 작업에는 다음 표의 속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-121">Email actions require the properties in the following table.</span></span>

| <span data-ttu-id="fbe61-122">속성</span><span class="sxs-lookup"><span data-stu-id="fbe61-122">Property</span></span> | <span data-ttu-id="fbe61-123">설명</span><span class="sxs-lookup"><span data-stu-id="fbe61-123">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="fbe61-124">제목</span><span class="sxs-lookup"><span data-stu-id="fbe61-124">Subject</span></span> |<span data-ttu-id="fbe61-125">전자 메일의 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-125">Subject in the email.</span></span>  <span data-ttu-id="fbe61-126">메일의 본문을 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-126">You cannot modify the body of the mail.</span></span> |
| <span data-ttu-id="fbe61-127">받는 사람</span><span class="sxs-lookup"><span data-stu-id="fbe61-127">Recipients</span></span> |<span data-ttu-id="fbe61-128">모든 전자 메일 받는 사람의 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-128">Addresses of all e-mail recipients.</span></span>  <span data-ttu-id="fbe61-129">둘 이상의 주소를 지정하는 경우 주소를 세미콜론(;)으로 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-129">If you specify more than one address, then separate the addresses with a semicolon (;).</span></span> |


## <a name="webhook-actions"></a><span data-ttu-id="fbe61-130">웹후크 작업</span><span class="sxs-lookup"><span data-stu-id="fbe61-130">Webhook actions</span></span>

<span data-ttu-id="fbe61-131">웹후크 작업을 사용하여 단일 HTTP POST 요청을 통해 외부 프로세스를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-131">Webhook actions allow you to invoke an external process through a single HTTP POST request.</span></span>  <span data-ttu-id="fbe61-132">호출 중인 서비스는 웹후크를 지원하고 수신하는 페이로드를 사용하는 방법을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-132">The service being called should support webhooks and determine how it will use any payload it receives.</span></span>  <span data-ttu-id="fbe61-133">또한 요청이 API에서 이해하는 형식으로 되어 있다면 웹후크를 명시적으로 지원하지 않는 REST API를 호출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-133">You could also call a REST API that doesn't specifically support webhooks as long as the request is in a format that the API understands.</span></span>  <span data-ttu-id="fbe61-134">경고에 대한 응답으로 웹후크를 사용하는 예는 [Slack](http://slack.com)에서 메시지를 보내거나 [PagerDuty](http://pagerduty.com/)에서 인시던트를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-134">Examples of using a webhook in response to an alert are sending a message in [Slack](http://slack.com) or creating an incident in [PagerDuty](http://pagerduty.com/).</span></span>  <span data-ttu-id="fbe61-135">Slack을 호출하는 웹후크를 사용하여 경고 규칙을 생성하는 전체 연습은 [Log Analytics 경고의 웹후크](log-analytics-alerts-webhooks.md)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-135">A complete walkthrough of creating an alert rule with a webhook to call Slack is available at [Webhooks in Log Analytics alerts](log-analytics-alerts-webhooks.md).</span></span>

<span data-ttu-id="fbe61-136">웹후크 작업에는 다음 표의 속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-136">Webhook actions require the properties in the following table.</span></span>

| <span data-ttu-id="fbe61-137">속성</span><span class="sxs-lookup"><span data-stu-id="fbe61-137">Property</span></span> | <span data-ttu-id="fbe61-138">설명</span><span class="sxs-lookup"><span data-stu-id="fbe61-138">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="fbe61-139">Webhook URL</span><span class="sxs-lookup"><span data-stu-id="fbe61-139">Webhook URL</span></span> |<span data-ttu-id="fbe61-140">웹후크의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-140">The URL of the webhook.</span></span> |
| <span data-ttu-id="fbe61-141">사용자 지정 JSON 페이로드</span><span class="sxs-lookup"><span data-stu-id="fbe61-141">Custom JSON payload</span></span> |<span data-ttu-id="fbe61-142">웹후크와 함께 보낼 사용자 지정 페이로드입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-142">Custom payload to send with the webhook.</span></span>  <span data-ttu-id="fbe61-143">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbe61-143">See below for details.</span></span> |


<span data-ttu-id="fbe61-144">웹후크는 URL 및 외부 서비스에 보낸 데이터인 JSON 형식의 페이로드를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-144">Webhooks include a URL and a payload formatted in JSON that is the data sent to the external service.</span></span>  <span data-ttu-id="fbe61-145">기본적으로 페이로드는 다음 표의 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-145">By default, the payload will include the values in the following table.</span></span>  <span data-ttu-id="fbe61-146">이 페이로드를 자신만의 사용자 지정 페이로드로 바꾸도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-146">You can choose to replace this payload with a custom one of your own.</span></span>  <span data-ttu-id="fbe61-147">그러한 경우 각 매개 변수에 대한 표의 변수를 사용하여 해당 값을 사용자 지정 페이로드에 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-147">In that case you can use the variables in the table for each of the parameters to include their value in your custom payload.</span></span>

| <span data-ttu-id="fbe61-148">매개 변수</span><span class="sxs-lookup"><span data-stu-id="fbe61-148">Parameter</span></span> | <span data-ttu-id="fbe61-149">변수</span><span class="sxs-lookup"><span data-stu-id="fbe61-149">Variable</span></span> | <span data-ttu-id="fbe61-150">설명</span><span class="sxs-lookup"><span data-stu-id="fbe61-150">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="fbe61-151">AlertRuleName</span><span class="sxs-lookup"><span data-stu-id="fbe61-151">AlertRuleName</span></span> |<span data-ttu-id="fbe61-152">#alertrulename</span><span class="sxs-lookup"><span data-stu-id="fbe61-152">#alertrulename</span></span> |<span data-ttu-id="fbe61-153">경고 규칙의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-153">Name of the alert rule.</span></span> |
| <span data-ttu-id="fbe61-154">AlertThresholdOperator</span><span class="sxs-lookup"><span data-stu-id="fbe61-154">AlertThresholdOperator</span></span> |<span data-ttu-id="fbe61-155">#thresholdoperator</span><span class="sxs-lookup"><span data-stu-id="fbe61-155">#thresholdoperator</span></span> |<span data-ttu-id="fbe61-156">경고 규칙에 대한 임계값 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-156">Threshold operator for the alert rule.</span></span>  <span data-ttu-id="fbe61-157">*보다 큼* 또는 *보다 작음*.</span><span class="sxs-lookup"><span data-stu-id="fbe61-157">*Greater than* or *Less than*.</span></span> |
| <span data-ttu-id="fbe61-158">AlertThresholdValue</span><span class="sxs-lookup"><span data-stu-id="fbe61-158">AlertThresholdValue</span></span> |<span data-ttu-id="fbe61-159">#thresholdvalue</span><span class="sxs-lookup"><span data-stu-id="fbe61-159">#thresholdvalue</span></span> |<span data-ttu-id="fbe61-160">경고 규칙에 대한 임계값입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-160">Threshold value for the alert rule.</span></span> |
| <span data-ttu-id="fbe61-161">LinkToSearchResults</span><span class="sxs-lookup"><span data-stu-id="fbe61-161">LinkToSearchResults</span></span> |<span data-ttu-id="fbe61-162">#linktosearchresults</span><span class="sxs-lookup"><span data-stu-id="fbe61-162">#linktosearchresults</span></span> |<span data-ttu-id="fbe61-163">경고를 생성한 쿼리에서 레코드를 반환하는 Log Analytics 로그 검색에 대한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-163">Link to Log Analytics log search that returns the records from the query that created the alert.</span></span> |
| <span data-ttu-id="fbe61-164">ResultCount</span><span class="sxs-lookup"><span data-stu-id="fbe61-164">ResultCount</span></span> |<span data-ttu-id="fbe61-165">#searchresultcount</span><span class="sxs-lookup"><span data-stu-id="fbe61-165">#searchresultcount</span></span> |<span data-ttu-id="fbe61-166">검색 결과의 레코드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-166">Number of records in the search results.</span></span> |
| <span data-ttu-id="fbe61-167">SearchIntervalEndtimeUtc</span><span class="sxs-lookup"><span data-stu-id="fbe61-167">SearchIntervalEndtimeUtc</span></span> |<span data-ttu-id="fbe61-168">#searchintervalendtimeutc</span><span class="sxs-lookup"><span data-stu-id="fbe61-168">#searchintervalendtimeutc</span></span> |<span data-ttu-id="fbe61-169">UTC 형식의 쿼리에 대한 종료 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-169">End time for the query in UTC format.</span></span> |
| <span data-ttu-id="fbe61-170">SearchIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="fbe61-170">SearchIntervalInSeconds</span></span> |<span data-ttu-id="fbe61-171">#searchinterval</span><span class="sxs-lookup"><span data-stu-id="fbe61-171">#searchinterval</span></span> |<span data-ttu-id="fbe61-172">경고 규칙에 대한 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-172">Time window for the alert rule.</span></span> |
| <span data-ttu-id="fbe61-173">SearchIntervalStartTimeUtc</span><span class="sxs-lookup"><span data-stu-id="fbe61-173">SearchIntervalStartTimeUtc</span></span> |<span data-ttu-id="fbe61-174">#searchintervalstarttimeutc</span><span class="sxs-lookup"><span data-stu-id="fbe61-174">#searchintervalstarttimeutc</span></span> |<span data-ttu-id="fbe61-175">UTC 형식의 쿼리에 대한 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-175">Start time for the query in UTC format.</span></span> |
| <span data-ttu-id="fbe61-176">SearchQuery</span><span class="sxs-lookup"><span data-stu-id="fbe61-176">SearchQuery</span></span> |<span data-ttu-id="fbe61-177">#searchquery</span><span class="sxs-lookup"><span data-stu-id="fbe61-177">#searchquery</span></span> |<span data-ttu-id="fbe61-178">경고 규칙에서 사용하는 로그 검색 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-178">Log search query used by the alert rule.</span></span> |
| <span data-ttu-id="fbe61-179">SearchResults</span><span class="sxs-lookup"><span data-stu-id="fbe61-179">SearchResults</span></span> |<span data-ttu-id="fbe61-180">아래 참조</span><span class="sxs-lookup"><span data-stu-id="fbe61-180">See below</span></span> |<span data-ttu-id="fbe61-181">JSON 형식의 쿼리에서 반환된 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-181">Records returned by the query in JSON format.</span></span>  <span data-ttu-id="fbe61-182">처음 5,000 개의 레코드로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-182">Limited to the first 5,000 records.</span></span> |
| <span data-ttu-id="fbe61-183">WorkspaceID</span><span class="sxs-lookup"><span data-stu-id="fbe61-183">WorkspaceID</span></span> |<span data-ttu-id="fbe61-184">#workspaceid</span><span class="sxs-lookup"><span data-stu-id="fbe61-184">#workspaceid</span></span> |<span data-ttu-id="fbe61-185">OMS 작업 영역의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-185">ID of your OMS workspace.</span></span> |

<span data-ttu-id="fbe61-186">예를 들어 *text*라는 단일 매개변수를 포함하는 다음과 같은 사용자 지정 페이로드를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-186">For example, you might specify the following custom payload that includes a single parameter called *text*.</span></span>  <span data-ttu-id="fbe61-187">이 웹후크가 호출하는 서비스는 이 매개 변수를 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-187">The service that this webhook calls would be expecting this parameter.</span></span>

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

<span data-ttu-id="fbe61-188">이 예제 페이로드는 웹후크에 보낼 때 다음과 같은 내용으로 확인될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-188">This example payload would resolve to something like the following when sent to the webhook.</span></span>

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

<span data-ttu-id="fbe61-189">검색 결과를 사용자 지정 페이로드에 포함하려면 JSON 페이로드의 최상위 속성으로 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-189">To include search results in a custom payload, add the following line as a top level property in the json payload.</span></span>  

    "IncludeSearchResults":true

<span data-ttu-id="fbe61-190">예를 들어 경고 이름과 검색 결과만 포함하는 사용자 지정 페이로드를 만들려면 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-190">For example, to create a custom payload that includes just the alert name and the search results, you could use the following.</span></span> 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


<span data-ttu-id="fbe61-191">웹후크를 통해 경고 규칙을 생성하여 [OMS Log Analytics에서 Slack에 메시지를 보내는 경고 웹후크 작업 만들기](log-analytics-alerts-webhooks.md)에서 외부 서비스를 시작하는 전체 예제를 연습할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-191">You can walk through a complete example of creating an alert rule with a webhook to start an external service at [Create an alert webhook action in OMS Log Analytics to send message to Slack](log-analytics-alerts-webhooks.md).</span></span>

## <a name="runbook-actions"></a><span data-ttu-id="fbe61-192">Runbook 작업</span><span class="sxs-lookup"><span data-stu-id="fbe61-192">Runbook actions</span></span>
<span data-ttu-id="fbe61-193">Runbook 작업은 Azure 자동화에서 Runbook을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-193">Runbook actions start a runbook in Azure Automation.</span></span>  <span data-ttu-id="fbe61-194">이 유형의 작업을 사용하려면 OMS 작업 영역에 [자동화 솔루션](log-analytics-add-solutions.md) 을 설치하고 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-194">In order to use this type of action, you must have the [Automation solution](log-analytics-add-solutions.md) installed and configured in your OMS workspace.</span></span>  <span data-ttu-id="fbe61-195">자동화 솔루션에서 구성한 자동화 계정의 Runbook 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-195">You can select from the runbooks in the automation account that you configured in the Automation solution.</span></span>

<span data-ttu-id="fbe61-196">Runbook 작업에는 다음 표의 속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-196">Runbook actions require the properties in the following table.</span></span>

| <span data-ttu-id="fbe61-197">속성</span><span class="sxs-lookup"><span data-stu-id="fbe61-197">Property</span></span> | <span data-ttu-id="fbe61-198">설명</span><span class="sxs-lookup"><span data-stu-id="fbe61-198">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="fbe61-199">Runbook</span><span class="sxs-lookup"><span data-stu-id="fbe61-199">Runbook</span></span> | <span data-ttu-id="fbe61-200">경고가 생성될 때 시작하려는 Runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-200">Runbook that you want to start when an alert is created.</span></span> |
| <span data-ttu-id="fbe61-201">실행</span><span class="sxs-lookup"><span data-stu-id="fbe61-201">Run on</span></span> | <span data-ttu-id="fbe61-202">클라우드에서 Runbook을 실행하려면 **Azure**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-202">Specify **Azure** to run the runbook in the cloud.</span></span>  <span data-ttu-id="fbe61-203">[Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md )가 설치된 에이전트에서 Runbook을 실행할 **Hybrid Worker**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-203">Specify **Hybrid worker** to run the runbook on an agent with [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) installed.</span></span>  |

<span data-ttu-id="fbe61-204">Runbook 작업은 [웹후크](../automation/automation-webhooks.md)를 사용하여 Runbook을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-204">Runbook actions start the runbook using a [webhook](../automation/automation-webhooks.md).</span></span>  <span data-ttu-id="fbe61-205">경고 규칙을 만들 때 이름 **OMS 경고 수정** 에 이어 GUID를 가진 Runbook에 대해 새 웹후크가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-205">When you create the alert rule, it will automatically create a new webhook for the runbook with the name **OMS Alert Remediation** followed by a GUID.</span></span>  

<span data-ttu-id="fbe61-206">Runbook의 매개 변수를 직접 채울 수는 없으나 [$WebhookData 매개 변수](../automation/automation-webhooks.md)는 해당 경고를 생성한 로그 검색의 결과를 포함한 경고의 세부 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-206">You cannot directly populate any parameters of the runbook, but the [$WebhookData parameter](../automation/automation-webhooks.md) will include the details of the alert, including the results of the log search that created it.</span></span>  <span data-ttu-id="fbe61-207">Runbook이 경고의 속성에 액세스하려면 **$WebhookData**를 매개 변수로 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-207">The runbook will need to define **$WebhookData** as a parameter for it to access the properties of the alert.</span></span>  <span data-ttu-id="fbe61-208">이 경고는 **$WebhookData**의 **RequestBody** 속성에서 **SearchResults**라고 하는 단일 속성에서 json 형식으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-208">The alert data is available in json format in a single property called **SearchResults** in the **RequestBody** property of **$WebhookData**.</span></span>  <span data-ttu-id="fbe61-209">이 항목은 다음 표의 속성을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-209">This will have with the properties in the following table.</span></span>

| <span data-ttu-id="fbe61-210">노드</span><span class="sxs-lookup"><span data-stu-id="fbe61-210">Node</span></span> | <span data-ttu-id="fbe61-211">설명</span><span class="sxs-lookup"><span data-stu-id="fbe61-211">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="fbe61-212">id</span><span class="sxs-lookup"><span data-stu-id="fbe61-212">id</span></span> |<span data-ttu-id="fbe61-213">경로와, 검색의 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-213">Path and GUID of the search.</span></span> |
| <span data-ttu-id="fbe61-214">__metadata</span><span class="sxs-lookup"><span data-stu-id="fbe61-214">__metadata</span></span> |<span data-ttu-id="fbe61-215">레코드 수 및 검색 결과 상태를 포함하는 경고 관련 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-215">Information about the alert including the number of records and status of the search results.</span></span> |
| <span data-ttu-id="fbe61-216">value</span><span class="sxs-lookup"><span data-stu-id="fbe61-216">value</span></span> |<span data-ttu-id="fbe61-217">검색 결과의 각 레코드에 대해 개별 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-217">Separate entry for each record in the search results.</span></span>  <span data-ttu-id="fbe61-218">항목의 상세 정보는 레코드의 속성 및 값과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-218">The details of the entry will match the properties and values of the record.</span></span> |

<span data-ttu-id="fbe61-219">예를 들어, 다음 Runbook은 로그 검색에서 반환된 레코드를 추출하고 각 레코드 유형에 따라 서로 다른 속성을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-219">For example, the following runbook would extract the records returned by the log search  and assign different properties based on the type of each record.</span></span>  <span data-ttu-id="fbe61-220">Runbook은 JSON에서 **RequestBody**를 변환하여 시작되므로 PowerShell의 개체로 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-220">Note that the runbook starts by converting **RequestBody** from json so that it can be worked with as an object in PowerShell.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="fbe61-221">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fbe61-221">Next steps</span></span>
- <span data-ttu-id="fbe61-222">경고 규칙을 사용하여 [웹후크를 구성](log-analytics-alerts-webhooks.md) 하는 연습을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-222">Complete a walkthrough for [configuring a webook](log-analytics-alerts-webhooks.md) with an alert rule.</span></span>  
- <span data-ttu-id="fbe61-223">경고에 의해 식별된 문제를 수정하는 [Azure 자동화의 Runbook](https://azure.microsoft.com/documentation/services/automation) 을 작성하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fbe61-223">Learn how to write [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) to remediate problems identified by alerts.</span></span>