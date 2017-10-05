---
title: "활동 로그 경고에 사용된 웹후크 스키마 이해 | Microsoft Docs"
description: "활동 로그 경고가 활성화될 때 웹후크 URL에 게시되는 JSON 스키마에 대해 알아봅니다."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: 75c71bcd16573d4f4dd3377c623aa9b414aa3906
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a><span data-ttu-id="38dc7-103">Azure 활동 로그 경고에 대한 웹후크</span><span class="sxs-lookup"><span data-stu-id="38dc7-103">Webhooks for Azure activity log alerts</span></span>
<span data-ttu-id="38dc7-104">작업 그룹 정의의 일부로 활동 로그 경고 알림을 받도록 웹후크 끝점을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-104">As part of the definition of an action group, you can configure webhook endpoints to receive activity log alert notifications.</span></span> <span data-ttu-id="38dc7-105">웹후크를 사용하면 사후 처리 또는 사용자 지정 작업을 위해 이러한 알림을 다른 시스템으로 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-105">With webhooks, you can route these notifications to other systems for post-processing or custom actions.</span></span> <span data-ttu-id="38dc7-106">이 문서는 Webhook에 대한 HTTP POST의 페이로드 형태를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-106">This article shows what the payload for the HTTP POST to a webhook looks like.</span></span>

<span data-ttu-id="38dc7-107">활동 로그 경고에 대한 자세한 내용은 [Azure 활동 로그 알림을 만드는](monitoring-activity-log-alerts.md) 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="38dc7-107">For more information on activity log alerts, see how to [create Azure activity log alerts](monitoring-activity-log-alerts.md).</span></span>

<span data-ttu-id="38dc7-108">작업 그룹에 대한 자세한 내용은 [작업 그룹을 만드는](monitoring-action-groups.md) 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="38dc7-108">For information on action groups, see how to [create action groups](monitoring-action-groups.md).</span></span>

## <a name="authenticate-the-webhook"></a><span data-ttu-id="38dc7-109">웹후크 인증</span><span class="sxs-lookup"><span data-stu-id="38dc7-109">Authenticate the webhook</span></span>
<span data-ttu-id="38dc7-110">웹후크는 인증을 위해 토큰 기반 인증을 선택적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-110">The webhook can optionally use token-based authorization for authentication.</span></span> <span data-ttu-id="38dc7-111">웹후크 URI는 토큰 ID를 통해 저장됩니다. 예: `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span><span class="sxs-lookup"><span data-stu-id="38dc7-111">The webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span></span>

## <a name="payload-schema"></a><span data-ttu-id="38dc7-112">페이로드 스키마</span><span class="sxs-lookup"><span data-stu-id="38dc7-112">Payload schema</span></span>
<span data-ttu-id="38dc7-113">POST 작업에 포함된 JSON 페이로드는 페이로드 data.context.activityLog.eventSource 필드에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-113">The JSON payload contained in the POST operation differs based on the payload's data.context.activityLog.eventSource field.</span></span>

###<a name="common"></a><span data-ttu-id="38dc7-114">일반</span><span class="sxs-lookup"><span data-stu-id="38dc7-114">Common</span></span>
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "channels": "Operation",
                "correlationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "eventSource": "Administrative",
                "eventTimestamp": "2017-03-29T15:43:08.0019532+00:00",
                "eventDataId": "8195a56a-85de-4663-943e-1a2bf401ad94",
                "level": "Informational",
                "operationName": "Microsoft.Insights/actionGroups/write",
                "operationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "status": "Started",
                "subStatus": "",
                "subscriptionId": "52c65f65-0518-4d37-9719-7dbbfc68c57a",
                "submissionTimestamp": "2017-03-29T15:43:20.3863637+00:00",
                ...
            }
        },
        "properties": {}
    }
}
```
###<a name="administrative"></a><span data-ttu-id="38dc7-115">관리</span><span class="sxs-lookup"><span data-stu-id="38dc7-115">Administrative</span></span>
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "authorization": {
                    "action": "Microsoft.Insights/actionGroups/write",
                    "scope": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions"
                },
                "claims": "{...}",
                "caller": "me@contoso.com",
                "description": "",
                "httpRequest": "{...}",
                "resourceId": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions",
                "resourceGroupName": "CONTOSO-TEST",
                "resourceProviderName": "Microsoft.Insights",
                "resourceType": "Microsoft.Insights/actionGroups"
            }
        },
        "properties": {}
    }
}

```
###<a name="servicehealth"></a><span data-ttu-id="38dc7-116">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="38dc7-116">ServiceHealth</span></span>
```json
{
    "schemaId": "unknown",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "properties": {
                    "title": "...",
                    "service": "...",
                    "region": "...",
                    "communication": "...",
                    "incidentType": "Incident",
                    "trackingId": "...",
                    "groupId": "...",
                    "impactStartTime": "3/29/2017 3:43:21 PM",
                    "impactMitigationTime": "3/29/2017 3:43:21 PM",
                    "eventCreationTime": "3/29/2017 3:43:21 PM",
                    "impactedServices": "[{...}]",
                    "defaultLanguageTitle": "...",
                    "defaultLanguageContent": "...",
                    "stage": "Active",
                    "communicationId": "...",
                    "version": "0.1"
                }
            }
        },
        "properties": {}
    }
}
```

<span data-ttu-id="38dc7-117">서비스 상태 알림 활동 로그 경고에 대한 특정 스키마 세부 정보는 [서비스 상태 알림](monitoring-service-notifications.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="38dc7-117">For specific schema details on service health notification activity log alerts, see [Service health notifications](monitoring-service-notifications.md).</span></span>

<span data-ttu-id="38dc7-118">다른 모든 활동 로그 경고에 대한 특정 스키마 세부 정보는 [Azure 활동 로그 개요](monitoring-overview-activity-logs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="38dc7-118">For specific schema details on all other activity log alerts, see [Overview of the Azure activity log](monitoring-overview-activity-logs.md).</span></span>

| <span data-ttu-id="38dc7-119">요소 이름</span><span class="sxs-lookup"><span data-stu-id="38dc7-119">Element name</span></span> | <span data-ttu-id="38dc7-120">설명</span><span class="sxs-lookup"><span data-stu-id="38dc7-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="38dc7-121">status</span><span class="sxs-lookup"><span data-stu-id="38dc7-121">status</span></span> |<span data-ttu-id="38dc7-122">메트릭 경고에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-122">Used for metric alerts.</span></span> <span data-ttu-id="38dc7-123">활동 로그 경고에 대해서는 항상 “activated”로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-123">Always set to "activated" for activity log alerts.</span></span> |
| <span data-ttu-id="38dc7-124">context</span><span class="sxs-lookup"><span data-stu-id="38dc7-124">context</span></span> |<span data-ttu-id="38dc7-125">이벤트에 대한 컨텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-125">Context of the event.</span></span> |
| <span data-ttu-id="38dc7-126">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="38dc7-126">resourceProviderName</span></span> |<span data-ttu-id="38dc7-127">영향을 받는 리소스의 리소스 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-127">The resource provider of the impacted resource.</span></span> |
| <span data-ttu-id="38dc7-128">conditionType</span><span class="sxs-lookup"><span data-stu-id="38dc7-128">conditionType</span></span> |<span data-ttu-id="38dc7-129">항상 "Event"입니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-129">Always "Event."</span></span> |
| <span data-ttu-id="38dc7-130">name</span><span class="sxs-lookup"><span data-stu-id="38dc7-130">name</span></span> |<span data-ttu-id="38dc7-131">경고 규칙의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-131">Name of the alert rule.</span></span> |
| <span data-ttu-id="38dc7-132">id</span><span class="sxs-lookup"><span data-stu-id="38dc7-132">id</span></span> |<span data-ttu-id="38dc7-133">경고의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-133">Resource ID of the alert.</span></span> |
| <span data-ttu-id="38dc7-134">설명</span><span class="sxs-lookup"><span data-stu-id="38dc7-134">description</span></span> |<span data-ttu-id="38dc7-135">경고를 만들 때 설정하는 경고 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-135">Alert description set when the alert is created.</span></span> |
| <span data-ttu-id="38dc7-136">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="38dc7-136">subscriptionId</span></span> |<span data-ttu-id="38dc7-137">Azure 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-137">Azure subscription ID.</span></span> |
| <span data-ttu-id="38dc7-138">timestamp</span><span class="sxs-lookup"><span data-stu-id="38dc7-138">timestamp</span></span> |<span data-ttu-id="38dc7-139">요청을 처리하는 Azure 서비스에서 이벤트를 생성한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-139">Time at which the event was generated by the Azure service that processed the request.</span></span> |
| <span data-ttu-id="38dc7-140">resourceId</span><span class="sxs-lookup"><span data-stu-id="38dc7-140">resourceId</span></span> |<span data-ttu-id="38dc7-141">영향을 받는 리소스의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-141">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="38dc7-142">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="38dc7-142">resourceGroupName</span></span> |<span data-ttu-id="38dc7-143">영향을 받는 리소스의 리소스 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-143">Name of the resource group for the impacted resource.</span></span> |
| <span data-ttu-id="38dc7-144">properties</span><span class="sxs-lookup"><span data-stu-id="38dc7-144">properties</span></span> |<span data-ttu-id="38dc7-145">이벤트에 대한 세부 정보를 포함하는 `<Key, Value>` 쌍의 집합(즉, `Dictionary<String, String>`)입니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-145">Set of `<Key, Value>` pairs (that is, `Dictionary<String, String>`) that includes details about the event.</span></span> |
| <span data-ttu-id="38dc7-146">event</span><span class="sxs-lookup"><span data-stu-id="38dc7-146">event</span></span> |<span data-ttu-id="38dc7-147">이벤트에 대한 메타데이터가 포함된 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-147">Element that contains metadata about the event.</span></span> |
| <span data-ttu-id="38dc7-148">권한 부여</span><span class="sxs-lookup"><span data-stu-id="38dc7-148">authorization</span></span> |<span data-ttu-id="38dc7-149">이벤트의 역할 기반 액세스 제어 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-149">The Role-Based Access Control properties of the event.</span></span> <span data-ttu-id="38dc7-150">이러한 속성에는 일반적으로 action, role 및 scope이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-150">These properties usually include the action, the role, and the scope.</span></span> |
| <span data-ttu-id="38dc7-151">카테고리</span><span class="sxs-lookup"><span data-stu-id="38dc7-151">category</span></span> |<span data-ttu-id="38dc7-152">이벤트의 범주.</span><span class="sxs-lookup"><span data-stu-id="38dc7-152">Category of the event.</span></span> <span data-ttu-id="38dc7-153">지원되는 값으로 Administrative, Alert, Security, ServiceHealth, Recommendation이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-153">Supported values include Administrative, Alert, Security, ServiceHealth, and Recommendation.</span></span> |
| <span data-ttu-id="38dc7-154">caller</span><span class="sxs-lookup"><span data-stu-id="38dc7-154">caller</span></span> |<span data-ttu-id="38dc7-155">가용성에 기반한 작업, UPN 클레임 또는 SPN 클레임을 수행한 사용자의 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-155">Email address of the user who performed the operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="38dc7-156">특정 시스템 호출의 경우 null일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-156">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="38dc7-157">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="38dc7-157">correlationId</span></span> |<span data-ttu-id="38dc7-158">일반적으로 문자열 형식의 GUID.</span><span class="sxs-lookup"><span data-stu-id="38dc7-158">Usually a GUID in string format.</span></span> <span data-ttu-id="38dc7-159">correlationId가 있는 이벤트는 동일한 상위 작업에 속하며 일반적으로 correlationId를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-159">Events with correlationId belong to the same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="38dc7-160">eventDescription</span><span class="sxs-lookup"><span data-stu-id="38dc7-160">eventDescription</span></span> |<span data-ttu-id="38dc7-161">이벤트에 대한 정적 텍스트 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-161">Static text description of the event.</span></span> |
| <span data-ttu-id="38dc7-162">eventDataId</span><span class="sxs-lookup"><span data-stu-id="38dc7-162">eventDataId</span></span> |<span data-ttu-id="38dc7-163">이벤트에 대한 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-163">Unique identifier for the event.</span></span> |
| <span data-ttu-id="38dc7-164">eventSource</span><span class="sxs-lookup"><span data-stu-id="38dc7-164">eventSource</span></span> |<span data-ttu-id="38dc7-165">이벤트를 생성한 Azure 서비스 또는 인프라의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-165">Name of the Azure service or infrastructure that generated the event.</span></span> |
| <span data-ttu-id="38dc7-166">httpRequest</span><span class="sxs-lookup"><span data-stu-id="38dc7-166">httpRequest</span></span> |<span data-ttu-id="38dc7-167">요청은 일반적으로 clientRequestId, clientIpAddress 및 HTTP 메서드(예: PUT)를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-167">The request usually includes the clientRequestId, clientIpAddress, and HTTP method (for example, PUT).</span></span> |
| <span data-ttu-id="38dc7-168">level</span><span class="sxs-lookup"><span data-stu-id="38dc7-168">level</span></span> |<span data-ttu-id="38dc7-169">Critical, Error, Warning, Informational 및 Verbose 값 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-169">One of the following values: Critical, Error, Warning, Informational, and Verbose.</span></span> |
| <span data-ttu-id="38dc7-170">operationId</span><span class="sxs-lookup"><span data-stu-id="38dc7-170">operationId</span></span> |<span data-ttu-id="38dc7-171">일반적으로 이벤트 간에 공유되는 GUID로서 단일 작업에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-171">Usually a GUID shared among the events corresponding to single operation.</span></span> |
| <span data-ttu-id="38dc7-172">operationName</span><span class="sxs-lookup"><span data-stu-id="38dc7-172">operationName</span></span> |<span data-ttu-id="38dc7-173">작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-173">Name of the operation.</span></span> |
| <span data-ttu-id="38dc7-174">properties</span><span class="sxs-lookup"><span data-stu-id="38dc7-174">properties</span></span> |<span data-ttu-id="38dc7-175">이벤트의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-175">Properties of the event.</span></span> |
| <span data-ttu-id="38dc7-176">status</span><span class="sxs-lookup"><span data-stu-id="38dc7-176">status</span></span> |<span data-ttu-id="38dc7-177">문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-177">String.</span></span> <span data-ttu-id="38dc7-178">작업의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-178">Status of the operation.</span></span> <span data-ttu-id="38dc7-179">일반적인 값으로 Started, In Progress, Succeeded, Failed, Active 및 Resolved가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-179">Common values include Started, In Progress, Succeeded, Failed, Active, and Resolved.</span></span> |
| <span data-ttu-id="38dc7-180">subStatus</span><span class="sxs-lookup"><span data-stu-id="38dc7-180">subStatus</span></span> |<span data-ttu-id="38dc7-181">일반적으로 해당 REST 호출의 HTTP 상태 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-181">Usually includes the HTTP status code of the corresponding REST call.</span></span> <span data-ttu-id="38dc7-182">하위 상태를 설명하는 다른 문자열을 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-182">It might also include other strings that describe a substatus.</span></span> <span data-ttu-id="38dc7-183">일반적인 하위 상태 값으로 OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503) 및 Gateway Timeout (HTTP Status Code: 504)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-183">Common substatus values include OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), and Gateway Timeout (HTTP Status Code: 504).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="38dc7-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="38dc7-184">Next steps</span></span>
* <span data-ttu-id="38dc7-185">[활동 로그에 대해 자세히 알아보세요](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="38dc7-185">[Learn more about the activity log](monitoring-overview-activity-logs.md).</span></span>
* <span data-ttu-id="38dc7-186">[Azure 경고에 대한 Azure Automation 스크립트(Runbook)를 실행하세요](http://go.microsoft.com/fwlink/?LinkId=627081).</span><span class="sxs-lookup"><span data-stu-id="38dc7-186">[Execute Azure automation scripts (Runbooks) on Azure alerts](http://go.microsoft.com/fwlink/?LinkId=627081).</span></span>
* <span data-ttu-id="38dc7-187">[논리 앱을 사용하여 Azure 경고에서 Twilio를 통해 SMS를 보냅니다](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="38dc7-187">[Use a logic app to send an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="38dc7-188">이 예제는 메트릭 경고를 위한 것이지만 활동 로그 경고도 지원하도록 수정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-188">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
* <span data-ttu-id="38dc7-189">[논리 앱을 사용하여 Azure 경고에서 Slack 메시지를 보냅니다](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="38dc7-189">[Use a logic app to send a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="38dc7-190">이 예제는 메트릭 경고를 위한 것이지만 활동 로그 경고도 지원하도록 수정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-190">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
* <span data-ttu-id="38dc7-191">[논리 앱을 사용하여 Azure 경고에서 Azure Queue에 메시지를 보냅니다](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="38dc7-191">[Use a logic app to send a message to an Azure queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="38dc7-192">이 예제는 메트릭 경고를 위한 것이지만 활동 로그 경고도 지원하도록 수정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38dc7-192">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
