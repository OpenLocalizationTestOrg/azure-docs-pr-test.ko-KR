---
title: "Azure 활동 로그 경고에 대한 webhook 호출 | Microsoft Docs"
description: "활동 로그 이벤트를 사용자 지정 작업에 대한 다른 서비스로 라우팅할 수 있습니다. 예를 들어 SMS를 전송하거나, 버그를 기록하거나, 채팅/메시징 서비스를 통해 팀에 알릴 수 있습니다."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 64d333d1-7f37-4a00-9d16-dda6e69a113b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: johnkem
ms.openlocfilehash: 341ab32ad0ec691285fbf1537ee298ab30156a5d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a><span data-ttu-id="a26c3-104">Azure 활동 로그 경고에 대한 webhook 호출</span><span class="sxs-lookup"><span data-stu-id="a26c3-104">Call a webhook on Azure Activity Log alerts</span></span>
<span data-ttu-id="a26c3-105">웹후크를 사용하면 사후 처리 또는 사용자 지정 작업을 위해 Azure 경고 알림을 다른 시스템으로 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-105">Webhooks allow you to route an Azure alert notification to other systems for post-processing or custom actions.</span></span> <span data-ttu-id="a26c3-106">SMS 보내기, 버그 기록, 채팅/메시징 서비스를 통한 팀 알림 또는 원하는 수의 다른 작업 수행 등을 처리하는 서비스에 라우팅하도록 웹후크를 경고에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-106">You can use a webhook on an alert to route it to services that send SMS, log bugs, notify a team via chat/messaging services, or do any number of other actions.</span></span> <span data-ttu-id="a26c3-107">이 문서에서는 Azure 활동 로그 경고가 발생될 때 호출되도록 webhook을 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-107">This article describes how to set a webhook to be called when an Azure Activity Log alert fires.</span></span> <span data-ttu-id="a26c3-108">Webhook에 대한 HTTP POST의 페이로드 형태도 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-108">It also shows what the payload for the HTTP POST to a webhook looks like.</span></span> <span data-ttu-id="a26c3-109">한편 Azure 메트릭 경고에 대한 설정과 스키마에 대해서는 [이 페이지를 대신 참조하세요](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="a26c3-109">For information on the setup and schema for an Azure metric alert, [see this page instead](insights-webhooks-alerts.md).</span></span> <span data-ttu-id="a26c3-110">또한 활성화될 때 전자 메일을 보내도록 활동 로그 경고를 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-110">You can also set up an Activity Log alert to send email when activated.</span></span>

> [!NOTE]
> <span data-ttu-id="a26c3-111">이 기능은 현재 미리 보기이며 나중에 제거될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-111">This feature is currently in preview and will be removed at some point in the future.</span></span>
>
>

<span data-ttu-id="a26c3-112">[Azure PowerShell Cmdlet](insights-powershell-samples.md#create-metric-alerts), [플랫폼 간 CLI](insights-cli-samples.md#work-with-alerts) 또는 [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx)를 사용하여 활동 로그 경고를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-112">You can set up an Activity Log alert using the [Azure PowerShell Cmdlets](insights-powershell-samples.md#create-metric-alerts), [Cross-Platform CLI](insights-cli-samples.md#work-with-alerts), or [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span></span> <span data-ttu-id="a26c3-113">현재 Azure Portal에서는 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-113">Currently, you cannot set one up using the Azure portal.</span></span>

## <a name="authenticating-the-webhook"></a><span data-ttu-id="a26c3-114">웹후크 인증</span><span class="sxs-lookup"><span data-stu-id="a26c3-114">Authenticating the webhook</span></span>
<span data-ttu-id="a26c3-115">웹후크는 다음 방법 중 하나를 사용하여 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-115">The webhook can authenticate using either of these methods:</span></span>

1. <span data-ttu-id="a26c3-116">**토큰 기반 인증** - 토큰 ID를 사용하여 webhook URI를 저장합니다. 예를 들면 `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-116">**Token-based authorization** - The webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span></span>
2. <span data-ttu-id="a26c3-117">**기본 인증** - 사용자 이름과 암호를 사용하여 webhook URI를 저장합니다. 예를 들면 `https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-117">**Basic authorization** - The webhook URI is saved with a username and password, for example, `https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span></span>

## <a name="payload-schema"></a><span data-ttu-id="a26c3-118">페이로드 스키마</span><span class="sxs-lookup"><span data-stu-id="a26c3-118">Payload schema</span></span>
<span data-ttu-id="a26c3-119">POST 작업에는 모든 활동 로그 기반 경고에 대해 다음과 같은 JSON 페이로드와 스키마가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-119">The POST operation contains the following JSON payload and schema for all Activity Log-based alerts.</span></span> <span data-ttu-id="a26c3-120">이 스키마는 메트릭 기반 경고에서 사용하는 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-120">This schema is similar to the one used by metric-based alerts.</span></span>

```
{
        "status": "Activated",
        "context": {
                "resourceProviderName": "Microsoft.Web",
                "event": {
                        "$type": "Microsoft.WindowsAzure.Management.Monitoring.Automation.Notifications.GenericNotifications.Datacontracts.InstanceEventContext, Microsoft.WindowsAzure.Management.Mon.Automation",
                        "authorization": {
                                "action": "Microsoft.Web/sites/start/action",
                                "scope": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest"
                        },
                        "eventDataId": "327caaca-08d7-41b1-86d8-27d0a7adb92d",
                        "category": "Administrative",
                        "caller": "myname@mycompany.com",
                        "httpRequest": {
                                "clientRequestId": "f58cead8-c9ed-43af-8710-55e64def208d",
                                "clientIpAddress": "104.43.166.155",
                                "method": "POST"
                        },
                        "status": "Succeeded",
                        "subStatus": "OK",
                        "level": "Informational",
                        "correlationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "eventDescription": "",
                        "operationName": "Microsoft.Web/sites/start/action",
                        "operationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "properties": {
                                "$type": "Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage",
                                "statusCode": "OK",
                                "serviceRequestId": "f7716681-496a-4f5c-8d14-d564bcf54714"
                        }
                },
                "timestamp": "Friday, March 11, 2016 9:13:23 PM",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/alertonevent2",
                "name": "alertonevent2",
                "description": "test alert on event start",
                "conditionType": "Event",
                "subscriptionId": "s1",
                "resourceId": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest",
                "resourceGroupName": "rg1"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```

| <span data-ttu-id="a26c3-121">요소 이름</span><span class="sxs-lookup"><span data-stu-id="a26c3-121">Element Name</span></span> | <span data-ttu-id="a26c3-122">설명</span><span class="sxs-lookup"><span data-stu-id="a26c3-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a26c3-123">status</span><span class="sxs-lookup"><span data-stu-id="a26c3-123">status</span></span> |<span data-ttu-id="a26c3-124">메트릭 경고에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-124">Used for metric alerts.</span></span> <span data-ttu-id="a26c3-125">활동 로그 경고에 대해서는 항상 "activated"로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-125">Always set to "activated" for Activity Log alerts.</span></span> |
| <span data-ttu-id="a26c3-126">context</span><span class="sxs-lookup"><span data-stu-id="a26c3-126">context</span></span> |<span data-ttu-id="a26c3-127">이벤트에 대한 컨텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-127">Context of the event.</span></span> |
| <span data-ttu-id="a26c3-128">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="a26c3-128">resourceProviderName</span></span> |<span data-ttu-id="a26c3-129">영향을 받는 리소스의 리소스 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-129">The resource provider of the impacted resource.</span></span> |
| <span data-ttu-id="a26c3-130">conditionType</span><span class="sxs-lookup"><span data-stu-id="a26c3-130">conditionType</span></span> |<span data-ttu-id="a26c3-131">항상 "Event"입니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-131">Always "Event."</span></span> |
| <span data-ttu-id="a26c3-132">name</span><span class="sxs-lookup"><span data-stu-id="a26c3-132">name</span></span> |<span data-ttu-id="a26c3-133">경고 규칙의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-133">Name of the alert rule.</span></span> |
| <span data-ttu-id="a26c3-134">id</span><span class="sxs-lookup"><span data-stu-id="a26c3-134">id</span></span> |<span data-ttu-id="a26c3-135">경고의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-135">Resource ID of the alert.</span></span> |
| <span data-ttu-id="a26c3-136">설명</span><span class="sxs-lookup"><span data-stu-id="a26c3-136">description</span></span> |<span data-ttu-id="a26c3-137">경고를 만드는 동안 설정되는 경고 설명 입니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-137">Alert description as set during creation of the alert.</span></span> |
| <span data-ttu-id="a26c3-138">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="a26c3-138">subscriptionId</span></span> |<span data-ttu-id="a26c3-139">Azure 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-139">Azure Subscription ID.</span></span> |
| <span data-ttu-id="a26c3-140">timestamp</span><span class="sxs-lookup"><span data-stu-id="a26c3-140">timestamp</span></span> |<span data-ttu-id="a26c3-141">요청을 처리하는 Azure 서비스에서 이벤트를 생성한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-141">Time at which the event was generated by the Azure service that processed the request.</span></span> |
| <span data-ttu-id="a26c3-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="a26c3-142">resourceId</span></span> |<span data-ttu-id="a26c3-143">영향을 받는 리소스의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-143">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="a26c3-144">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="a26c3-144">resourceGroupName</span></span> |<span data-ttu-id="a26c3-145">영향을 받는 리소스의 리소스 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-145">Name of the resource group for the impacted resource</span></span> |
| <span data-ttu-id="a26c3-146">properties</span><span class="sxs-lookup"><span data-stu-id="a26c3-146">properties</span></span> |<span data-ttu-id="a26c3-147">이벤트에 대한 세부 정보를 포함하는 `<Key, Value>` 쌍의 집합(예: `Dictionary<String, String>`)입니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-147">Set of `<Key, Value>` pairs (i.e. `Dictionary<String, String>`) that includes details about the event.</span></span> |
| <span data-ttu-id="a26c3-148">event</span><span class="sxs-lookup"><span data-stu-id="a26c3-148">event</span></span> |<span data-ttu-id="a26c3-149">이벤트에 대한 메타데이터가 포함된 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-149">Element containing metadata about the event.</span></span> |
| <span data-ttu-id="a26c3-150">권한 부여</span><span class="sxs-lookup"><span data-stu-id="a26c3-150">authorization</span></span> |<span data-ttu-id="a26c3-151">이벤트의 RBAC 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-151">The RBAC properties of the event.</span></span> <span data-ttu-id="a26c3-152">여기에는 일반적으로 "action", "role" 및 "scope"가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-152">These usually include the “action”, “role” and the “scope.”</span></span> |
| <span data-ttu-id="a26c3-153">카테고리</span><span class="sxs-lookup"><span data-stu-id="a26c3-153">category</span></span> |<span data-ttu-id="a26c3-154">이벤트의 범주.</span><span class="sxs-lookup"><span data-stu-id="a26c3-154">Category of the event.</span></span> <span data-ttu-id="a26c3-155">지원되는 값으로 Administrative, Alert, Security, ServiceHealth, Recommendation이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-155">Supported values include: Administrative, Alert, Security, ServiceHealth, Recommendation.</span></span> |
| <span data-ttu-id="a26c3-156">caller</span><span class="sxs-lookup"><span data-stu-id="a26c3-156">caller</span></span> |<span data-ttu-id="a26c3-157">가용성에 기반한 작업, UPN 클레임 또는 SPN 클레임을 수행한 사용자의 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-157">Email address of the user who performed the operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="a26c3-158">특정 시스템 호출의 경우 null일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-158">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="a26c3-159">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="a26c3-159">correlationId</span></span> |<span data-ttu-id="a26c3-160">일반적으로 문자열 형식의 GUID.</span><span class="sxs-lookup"><span data-stu-id="a26c3-160">Usually a GUID in string format.</span></span> <span data-ttu-id="a26c3-161">correlationId가 있는 이벤트는 동일한 상위 작업에 속하며 일반적으로 correlationId를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-161">Events with correlationId belong to the same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="a26c3-162">eventDescription</span><span class="sxs-lookup"><span data-stu-id="a26c3-162">eventDescription</span></span> |<span data-ttu-id="a26c3-163">이벤트에 대한 정적 텍스트 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-163">Static text description of the event.</span></span> |
| <span data-ttu-id="a26c3-164">eventDataId</span><span class="sxs-lookup"><span data-stu-id="a26c3-164">eventDataId</span></span> |<span data-ttu-id="a26c3-165">이벤트에 대한 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-165">Unique identifier for the event.</span></span> |
| <span data-ttu-id="a26c3-166">eventSource</span><span class="sxs-lookup"><span data-stu-id="a26c3-166">eventSource</span></span> |<span data-ttu-id="a26c3-167">이벤트를 생성한 Azure 서비스 또는 인프라의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-167">Name of the Azure service or infrastructure that generated the event.</span></span> |
| <span data-ttu-id="a26c3-168">httpRequest</span><span class="sxs-lookup"><span data-stu-id="a26c3-168">httpRequest</span></span> |<span data-ttu-id="a26c3-169">일반적으로 “clientRequestId”, “clientIpAddress” 및 “method”(PUT 등의 HTTP 메서드) 포함</span><span class="sxs-lookup"><span data-stu-id="a26c3-169">Usually includes the “clientRequestId”, “clientIpAddress” and “method” (HTTP method e.g. PUT).</span></span> |
| <span data-ttu-id="a26c3-170">level</span><span class="sxs-lookup"><span data-stu-id="a26c3-170">level</span></span> |<span data-ttu-id="a26c3-171">“Critical”, “Error”, “Warning”, “Informational” 및 “Verbose” 값 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-171">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose.”</span></span> |
| <span data-ttu-id="a26c3-172">operationId</span><span class="sxs-lookup"><span data-stu-id="a26c3-172">operationId</span></span> |<span data-ttu-id="a26c3-173">일반적으로 이벤트 간에 공유되는 GUID로서 단일 작업에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-173">Usually a GUID shared among the events corresponding to single operation.</span></span> |
| <span data-ttu-id="a26c3-174">operationName</span><span class="sxs-lookup"><span data-stu-id="a26c3-174">operationName</span></span> |<span data-ttu-id="a26c3-175">작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-175">Name of the operation.</span></span> |
| <span data-ttu-id="a26c3-176">properties</span><span class="sxs-lookup"><span data-stu-id="a26c3-176">properties</span></span> |<span data-ttu-id="a26c3-177">이벤트의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-177">Properties of the event.</span></span> |
| <span data-ttu-id="a26c3-178">status</span><span class="sxs-lookup"><span data-stu-id="a26c3-178">status</span></span> |<span data-ttu-id="a26c3-179">문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-179">String.</span></span> <span data-ttu-id="a26c3-180">작업의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-180">Status of the operation.</span></span> <span data-ttu-id="a26c3-181">일반적인 값으로 "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved"가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-181">Common values include: "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved".</span></span> |
| <span data-ttu-id="a26c3-182">subStatus</span><span class="sxs-lookup"><span data-stu-id="a26c3-182">subStatus</span></span> |<span data-ttu-id="a26c3-183">일반적으로 해당 REST 호출의 HTTP 상태 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-183">Usually includes the HTTP status code of the corresponding REST call.</span></span> <span data-ttu-id="a26c3-184">하위 상태를 설명하는 다른 문자열을 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-184">It might also include other strings describing a substatus.</span></span> <span data-ttu-id="a26c3-185">일반적인 하위 상태 값으로 OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-185">Common substatus values include: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a26c3-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a26c3-186">Next steps</span></span>
* [<span data-ttu-id="a26c3-187">활동 로그에 대한 자세한 내용</span><span class="sxs-lookup"><span data-stu-id="a26c3-187">Learn more about the Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="a26c3-188">Azure 경고에 대한 Azure Automation 스크립트 실행 (Runbooks)</span><span class="sxs-lookup"><span data-stu-id="a26c3-188">Execute Azure Automation scripts (Runbooks) on Azure alerts</span></span>](http://go.microsoft.com/fwlink/?LinkId=627081)
* <span data-ttu-id="a26c3-189">[논리 앱을 사용하여 Azure 경고에서 Twilio 통해 SMS 보내기](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="a26c3-189">[Use Logic App to send an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="a26c3-190">이 예제는 메트릭 경고를 위한 것이지만 활동 로그 경고도 지원하도록 수정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-190">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span></span>
* <span data-ttu-id="a26c3-191">[논리 앱을 사용하여 Azure 경고에서 Slack 메시지 보내기](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="a26c3-191">[Use Logic App to send a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="a26c3-192">이 예제는 메트릭 경고를 위한 것이지만 활동 로그 경고도 지원하도록 수정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-192">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span></span>
* <span data-ttu-id="a26c3-193">[논리 앱을 사용하여 Azure 경고에서 Azure Queue에 메시지 보내기](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="a26c3-193">[Use Logic App to send a message to an Azure Queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="a26c3-194">이 예제는 메트릭 경고를 위한 것이지만 활동 로그 경고도 지원하도록 수정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a26c3-194">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span></span>
