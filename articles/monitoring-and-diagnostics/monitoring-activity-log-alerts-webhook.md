---
title: "활동 로그 경고에 사용 된 aaaUnderstand hello webhook 스키마 | Microsoft Docs"
description: "Hello는 활동 로그 경고가 활성화 되는 경우 tooa webhook URL에 게시 하는 JSON의 hello 스키마에 알아봅니다."
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
ms.openlocfilehash: 75562e0589222d3e392ea73eacfd7414a422d115
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a><span data-ttu-id="74ec1-103">Azure 활동 로그 경고에 대한 웹후크</span><span class="sxs-lookup"><span data-stu-id="74ec1-103">Webhooks for Azure activity log alerts</span></span>
<span data-ttu-id="74ec1-104">작업 그룹 hello 정의의 일부로 webhook 끝점 tooreceive 활동 로그 경고 알림을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-104">As part of hello definition of an action group, you can configure webhook endpoints tooreceive activity log alert notifications.</span></span> <span data-ttu-id="74ec1-105">Webhook을 사용자 지정 또는 후 처리 작업에 대 한 이러한 알림을 tooother 시스템을 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-105">With webhooks, you can route these notifications tooother systems for post-processing or custom actions.</span></span> <span data-ttu-id="74ec1-106">이 문서에서는 다음과 같은 hello HTTP POST tooa webhook에 대 한 어떤 hello 페이로드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-106">This article shows what hello payload for hello HTTP POST tooa webhook looks like.</span></span>

<span data-ttu-id="74ec1-107">활동 로그 경고에 대 한 자세한 내용은 참조 방법을 너무[Azure 활동 로그 알림을 만들](monitoring-activity-log-alerts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-107">For more information on activity log alerts, see how too[create Azure activity log alerts](monitoring-activity-log-alerts.md).</span></span>

<span data-ttu-id="74ec1-108">동작 그룹에 대 한 자세한 내용은 참조 방법을 너무[동작 그룹을 만들](monitoring-action-groups.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-108">For information on action groups, see how too[create action groups](monitoring-action-groups.md).</span></span>

## <a name="authenticate-hello-webhook"></a><span data-ttu-id="74ec1-109">Hello webhook 인증</span><span class="sxs-lookup"><span data-stu-id="74ec1-109">Authenticate hello webhook</span></span>
<span data-ttu-id="74ec1-110">선택적으로 hello webhook 인증에 대 한 토큰 기반 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-110">hello webhook can optionally use token-based authorization for authentication.</span></span> <span data-ttu-id="74ec1-111">토큰 ID와 함께 URI 예를 들어 저장 하는 webhook hello `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`합니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-111">hello webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span></span>

## <a name="payload-schema"></a><span data-ttu-id="74ec1-112">페이로드 스키마</span><span class="sxs-lookup"><span data-stu-id="74ec1-112">Payload schema</span></span>
<span data-ttu-id="74ec1-113">hello POST 작업에에서 포함 된 hello JSON 페이로드 hello 페이로드 data.context.activityLog.eventSource 필드에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-113">hello JSON payload contained in hello POST operation differs based on hello payload's data.context.activityLog.eventSource field.</span></span>

###<a name="common"></a><span data-ttu-id="74ec1-114">일반</span><span class="sxs-lookup"><span data-stu-id="74ec1-114">Common</span></span>
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
###<a name="administrative"></a><span data-ttu-id="74ec1-115">관리</span><span class="sxs-lookup"><span data-stu-id="74ec1-115">Administrative</span></span>
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
###<a name="servicehealth"></a><span data-ttu-id="74ec1-116">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="74ec1-116">ServiceHealth</span></span>
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

<span data-ttu-id="74ec1-117">서비스 상태 알림 활동 로그 경고에 대한 특정 스키마 세부 정보는 [서비스 상태 알림](monitoring-service-notifications.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74ec1-117">For specific schema details on service health notification activity log alerts, see [Service health notifications](monitoring-service-notifications.md).</span></span>

<span data-ttu-id="74ec1-118">다른 모든 활동 로그 경고 세부 정보를 특정 스키마를 참조 하십시오. [hello Azure 활동 로그 간략하게](monitoring-overview-activity-logs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-118">For specific schema details on all other activity log alerts, see [Overview of hello Azure activity log](monitoring-overview-activity-logs.md).</span></span>

| <span data-ttu-id="74ec1-119">요소 이름</span><span class="sxs-lookup"><span data-stu-id="74ec1-119">Element name</span></span> | <span data-ttu-id="74ec1-120">설명</span><span class="sxs-lookup"><span data-stu-id="74ec1-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="74ec1-121">status</span><span class="sxs-lookup"><span data-stu-id="74ec1-121">status</span></span> |<span data-ttu-id="74ec1-122">메트릭 경고에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-122">Used for metric alerts.</span></span> <span data-ttu-id="74ec1-123">항상 너무 "활성화 된" 작업 로그 경고에 대 한 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-123">Always set too"activated" for activity log alerts.</span></span> |
| <span data-ttu-id="74ec1-124">context</span><span class="sxs-lookup"><span data-stu-id="74ec1-124">context</span></span> |<span data-ttu-id="74ec1-125">Hello 이벤트의 컨텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-125">Context of hello event.</span></span> |
| <span data-ttu-id="74ec1-126">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="74ec1-126">resourceProviderName</span></span> |<span data-ttu-id="74ec1-127">hello 리소스 공급자의 hello 리소스를 저하 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-127">hello resource provider of hello impacted resource.</span></span> |
| <span data-ttu-id="74ec1-128">conditionType</span><span class="sxs-lookup"><span data-stu-id="74ec1-128">conditionType</span></span> |<span data-ttu-id="74ec1-129">항상 "Event"입니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-129">Always "Event."</span></span> |
| <span data-ttu-id="74ec1-130">name</span><span class="sxs-lookup"><span data-stu-id="74ec1-130">name</span></span> |<span data-ttu-id="74ec1-131">Hello 경고 규칙의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-131">Name of hello alert rule.</span></span> |
| <span data-ttu-id="74ec1-132">id</span><span class="sxs-lookup"><span data-stu-id="74ec1-132">id</span></span> |<span data-ttu-id="74ec1-133">Hello 경고의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-133">Resource ID of hello alert.</span></span> |
| <span data-ttu-id="74ec1-134">설명</span><span class="sxs-lookup"><span data-stu-id="74ec1-134">description</span></span> |<span data-ttu-id="74ec1-135">경고 설명 hello 경고를 만들 때 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-135">Alert description set when hello alert is created.</span></span> |
| <span data-ttu-id="74ec1-136">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="74ec1-136">subscriptionId</span></span> |<span data-ttu-id="74ec1-137">Azure 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-137">Azure subscription ID.</span></span> |
| <span data-ttu-id="74ec1-138">timestamp</span><span class="sxs-lookup"><span data-stu-id="74ec1-138">timestamp</span></span> |<span data-ttu-id="74ec1-139">hello 이벤트가 hello hello 요청을 처리 하는 Azure 서비스에서 생성 된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-139">Time at which hello event was generated by hello Azure service that processed hello request.</span></span> |
| <span data-ttu-id="74ec1-140">resourceId</span><span class="sxs-lookup"><span data-stu-id="74ec1-140">resourceId</span></span> |<span data-ttu-id="74ec1-141">Hello의 리소스 ID 리소스를 저하 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-141">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="74ec1-142">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="74ec1-142">resourceGroupName</span></span> |<span data-ttu-id="74ec1-143">Hello에 대 한 hello 리소스 그룹의 이름을 리소스를 저하 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-143">Name of hello resource group for hello impacted resource.</span></span> |
| <span data-ttu-id="74ec1-144">properties</span><span class="sxs-lookup"><span data-stu-id="74ec1-144">properties</span></span> |<span data-ttu-id="74ec1-145">설정 `<Key, Value>` 쌍 (즉, `Dictionary<String, String>`) hello 이벤트에 대 한 세부 정보를 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-145">Set of `<Key, Value>` pairs (that is, `Dictionary<String, String>`) that includes details about hello event.</span></span> |
| <span data-ttu-id="74ec1-146">event</span><span class="sxs-lookup"><span data-stu-id="74ec1-146">event</span></span> |<span data-ttu-id="74ec1-147">Hello 이벤트에 대 한 메타 데이터가 포함 된 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-147">Element that contains metadata about hello event.</span></span> |
| <span data-ttu-id="74ec1-148">권한 부여</span><span class="sxs-lookup"><span data-stu-id="74ec1-148">authorization</span></span> |<span data-ttu-id="74ec1-149">hello hello 이벤트의 역할 기반 액세스 제어 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-149">hello Role-Based Access Control properties of hello event.</span></span> <span data-ttu-id="74ec1-150">이러한 속성에는 일반적으로 hello 작업과 hello 역할 hello 범위 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-150">These properties usually include hello action, hello role, and hello scope.</span></span> |
| <span data-ttu-id="74ec1-151">카테고리</span><span class="sxs-lookup"><span data-stu-id="74ec1-151">category</span></span> |<span data-ttu-id="74ec1-152">Hello 이벤트의 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-152">Category of hello event.</span></span> <span data-ttu-id="74ec1-153">지원되는 값으로 Administrative, Alert, Security, ServiceHealth, Recommendation이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-153">Supported values include Administrative, Alert, Security, ServiceHealth, and Recommendation.</span></span> |
| <span data-ttu-id="74ec1-154">caller</span><span class="sxs-lookup"><span data-stu-id="74ec1-154">caller</span></span> |<span data-ttu-id="74ec1-155">Hello 작업, UPN 클레임 또는 SPN 클레임 가용성에 따라 수행한 hello 사용자의 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-155">Email address of hello user who performed hello operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="74ec1-156">특정 시스템 호출의 경우 null일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-156">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="74ec1-157">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="74ec1-157">correlationId</span></span> |<span data-ttu-id="74ec1-158">일반적으로 문자열 형식의 GUID.</span><span class="sxs-lookup"><span data-stu-id="74ec1-158">Usually a GUID in string format.</span></span> <span data-ttu-id="74ec1-159">상관 관계 Id와 함께 이벤트 속해 toohello 같은 더 큰 작업 하 고 일반적으로 correlationId를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-159">Events with correlationId belong toohello same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="74ec1-160">eventDescription</span><span class="sxs-lookup"><span data-stu-id="74ec1-160">eventDescription</span></span> |<span data-ttu-id="74ec1-161">Hello 이벤트의 정적 텍스트 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-161">Static text description of hello event.</span></span> |
| <span data-ttu-id="74ec1-162">eventDataId</span><span class="sxs-lookup"><span data-stu-id="74ec1-162">eventDataId</span></span> |<span data-ttu-id="74ec1-163">Hello 이벤트에 대 한 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-163">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="74ec1-164">eventSource</span><span class="sxs-lookup"><span data-stu-id="74ec1-164">eventSource</span></span> |<span data-ttu-id="74ec1-165">이름에 해당 생성 된 hello 이벤트 인프라 또는 Azure 서비스 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-165">Name of hello Azure service or infrastructure that generated hello event.</span></span> |
| <span data-ttu-id="74ec1-166">httpRequest</span><span class="sxs-lookup"><span data-stu-id="74ec1-166">httpRequest</span></span> |<span data-ttu-id="74ec1-167">hello 요청 일반적으로 hello clientRequestId, 포함 clientIpAddress, HTTP 메서드 (예를 들어 PUT).</span><span class="sxs-lookup"><span data-stu-id="74ec1-167">hello request usually includes hello clientRequestId, clientIpAddress, and HTTP method (for example, PUT).</span></span> |
| <span data-ttu-id="74ec1-168">level</span><span class="sxs-lookup"><span data-stu-id="74ec1-168">level</span></span> |<span data-ttu-id="74ec1-169">Hello 다음 값 중 하나: 중요, 오류, 경고, 정보, 및 자세한 정보 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-169">One of hello following values: Critical, Error, Warning, Informational, and Verbose.</span></span> |
| <span data-ttu-id="74ec1-170">operationId</span><span class="sxs-lookup"><span data-stu-id="74ec1-170">operationId</span></span> |<span data-ttu-id="74ec1-171">일반적으로 GUID toosingle 작업에 해당 하는 hello 이벤트 간에 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-171">Usually a GUID shared among hello events corresponding toosingle operation.</span></span> |
| <span data-ttu-id="74ec1-172">operationName</span><span class="sxs-lookup"><span data-stu-id="74ec1-172">operationName</span></span> |<span data-ttu-id="74ec1-173">Hello 작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-173">Name of hello operation.</span></span> |
| <span data-ttu-id="74ec1-174">properties</span><span class="sxs-lookup"><span data-stu-id="74ec1-174">properties</span></span> |<span data-ttu-id="74ec1-175">Hello 이벤트의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-175">Properties of hello event.</span></span> |
| <span data-ttu-id="74ec1-176">status</span><span class="sxs-lookup"><span data-stu-id="74ec1-176">status</span></span> |<span data-ttu-id="74ec1-177">문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-177">String.</span></span> <span data-ttu-id="74ec1-178">Hello 작업의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-178">Status of hello operation.</span></span> <span data-ttu-id="74ec1-179">일반적인 값으로 Started, In Progress, Succeeded, Failed, Active 및 Resolved가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-179">Common values include Started, In Progress, Succeeded, Failed, Active, and Resolved.</span></span> |
| <span data-ttu-id="74ec1-180">subStatus</span><span class="sxs-lookup"><span data-stu-id="74ec1-180">subStatus</span></span> |<span data-ttu-id="74ec1-181">일반적으로 hello 해당 REST 호출의 hello HTTP 상태 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-181">Usually includes hello HTTP status code of hello corresponding REST call.</span></span> <span data-ttu-id="74ec1-182">하위 상태를 설명하는 다른 문자열을 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-182">It might also include other strings that describe a substatus.</span></span> <span data-ttu-id="74ec1-183">일반적인 하위 상태 값으로 OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503) 및 Gateway Timeout (HTTP Status Code: 504)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-183">Common substatus values include OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), and Gateway Timeout (HTTP Status Code: 504).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="74ec1-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="74ec1-184">Next steps</span></span>
* <span data-ttu-id="74ec1-185">[Hello 활동 로그에 대 한 자세한](monitoring-overview-activity-logs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-185">[Learn more about hello activity log](monitoring-overview-activity-logs.md).</span></span>
* <span data-ttu-id="74ec1-186">[Azure 경고에 대한 Azure Automation 스크립트(Runbook)를 실행하세요](http://go.microsoft.com/fwlink/?LinkId=627081).</span><span class="sxs-lookup"><span data-stu-id="74ec1-186">[Execute Azure automation scripts (Runbooks) on Azure alerts](http://go.microsoft.com/fwlink/?LinkId=627081).</span></span>
* <span data-ttu-id="74ec1-187">[Azure 경고에서 논리 앱 toosend Twilio 통해 SMS를 사용 하 여](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)합니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-187">[Use a logic app toosend an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="74ec1-188">이 예제는 메트릭 경고에 대 한 활동 로그 경고와 수정 된 toowork 수 없지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-188">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
* <span data-ttu-id="74ec1-189">[논리 앱 toosend Azure 경고에서 Slack 메시지를 사용 하 여](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)합니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-189">[Use a logic app toosend a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="74ec1-190">이 예제는 메트릭 경고에 대 한 활동 로그 경고와 수정 된 toowork 수 없지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-190">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
* <span data-ttu-id="74ec1-191">[Azure 경고에서 큐에 메시지 tooan Azure 논리 앱 toosend를 사용 하 여](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)합니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-191">[Use a logic app toosend a message tooan Azure queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="74ec1-192">이 예제는 메트릭 경고에 대 한 활동 로그 경고와 수정 된 toowork 수 없지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ec1-192">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
