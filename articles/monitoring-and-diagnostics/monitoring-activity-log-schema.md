---
title: "Azure 활동 로그 이벤트 스키마 | Microsoft 문서"
description: "활동 로그로 내보내는 데이터의 이벤트 스키마에 대해 설명합니다."
author: johnkemnetz
manager: robb
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: johnkem
ms.openlocfilehash: a4ceb822e0ec3e1c1dc31ece1db761834e795f6c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-activity-log-event-schema"></a><span data-ttu-id="967d9-103">Azure 활동 로그 이벤트 스키마</span><span class="sxs-lookup"><span data-stu-id="967d9-103">Azure Activity Log event schema</span></span>
<span data-ttu-id="967d9-104">**Azure 활동 로그**는 Azure에서 발생한 모든 구독 수준 이벤트에 대한 정보를 제공하는 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-104">The **Azure Activity Log** is a log that provides insight into any subscription-level events that have occurred in Azure.</span></span> <span data-ttu-id="967d9-105">이 문서에서는 데이터 범주별 이벤트 스키마에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-105">This article describes the event schema per category of data.</span></span>

## <a name="administrative"></a><span data-ttu-id="967d9-106">관리</span><span class="sxs-lookup"><span data-stu-id="967d9-106">Administrative</span></span>
<span data-ttu-id="967d9-107">이 범주에는 Resource Manager를 통해 수행한 모든 만들기, 업데이트, 삭제 및 동작 작업의 레코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-107">This category contains the record of all create, update, delete, and action operations performed through Resource Manager.</span></span> <span data-ttu-id="967d9-108">이 범주에 표시되는 이벤트의 유형의 예로는 "가상 컴퓨터 만들기", "네트워크 보안 그룹 삭제" 등이 있습니다. 사용자나 응용 프로그램이 Resource Manager를 사용하여 취하는 모든 동작은 특정 리소스 종류에 대한 작업으로 모델링됩니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-108">Examples of the types of events you would see in this category include "create virtual machine" and "delete network security group" Every action taken by a user or application using Resource Manager is modeled as an operation on a particular resource type.</span></span> <span data-ttu-id="967d9-109">작업 유형이 쓰기, 삭제 또는 동작이면 해당 작업의 시작 및 성공이나 실패 레코드가 모두 관리 범주에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-109">If the operation type is Write, Delete, or Action, the records of both the start and success or fail of that operation are recorded in the Administrative category.</span></span> <span data-ttu-id="967d9-110">관리 범주에는 구독의 역할 기반 액세스 제어 변경 내용도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-110">The Administrative category also includes any changes to role-based access control in a subscription.</span></span>

### <a name="sample-event"></a><span data-ttu-id="967d9-111">샘플 이벤트</span><span class="sxs-lookup"><span data-stu-id="967d9-111">Sample event</span></span>
```json
{
  "authorization": {
    "action": "microsoft.support/supporttickets/write",
    "role": "Subscription Admin",
    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841"
  },
  "caller": "admin@contoso.com",
  "channels": "Operation",
  "claims": {
    "aud": "https://management.core.windows.net/",
    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
    "iat": "1421876371",
    "nbf": "1421876371",
    "exp": "1421880271",
    "ver": "1.0",
    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
    "puid": "20030000801A118C",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
    "name": "John Smith",
    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
    "appidacr": "2",
    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
    "http://schemas.microsoft.com/claims/authnclassreference": "1"
  },
  "correlationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "description": "",
  "eventDataId": "44ade6b4-3813-45e6-ae27-7420a95fa2f8",
  "eventName": {
    "value": "EndRequest",
    "localizedValue": "End request"
  },
  "httpRequest": {
    "clientRequestId": "27003b25-91d3-418f-8eb1-29e537dcb249",
    "clientIpAddress": "192.168.35.115",
    "method": "PUT"
  },
  "id": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841/events/44ade6b4-3813-45e6-ae27-7420a95fa2f8/ticks/635574752669792776",
  "level": "Informational",
  "resourceGroupName": "MSSupportGroup",
  "resourceProviderName": {
    "value": "microsoft.support",
    "localizedValue": "microsoft.support"
  },
  "resourceUri": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
  "operationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "operationName": {
    "value": "microsoft.support/supporttickets/write",
    "localizedValue": "microsoft.support/supporttickets/write"
  },
  "properties": {
    "statusCode": "Created"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": "Created",
    "localizedValue": "Created (HTTP Status Code: 201)"
  },
  "eventTimestamp": "2015-01-21T22:14:26.9792776Z",
  "submissionTimestamp": "2015-01-21T22:14:39.9936304Z",
  "subscriptionId": "s1"
}
```

### <a name="property-descriptions"></a><span data-ttu-id="967d9-112">속성 설명</span><span class="sxs-lookup"><span data-stu-id="967d9-112">Property descriptions</span></span>
| <span data-ttu-id="967d9-113">요소 이름</span><span class="sxs-lookup"><span data-stu-id="967d9-113">Element Name</span></span> | <span data-ttu-id="967d9-114">설명</span><span class="sxs-lookup"><span data-stu-id="967d9-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="967d9-115">authorization</span><span class="sxs-lookup"><span data-stu-id="967d9-115">authorization</span></span> |<span data-ttu-id="967d9-116">이벤트의 RBAC 속성 Blob입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-116">Blob of RBAC properties of the event.</span></span> <span data-ttu-id="967d9-117">일반적으로 "action", "role" 및 "scope" 속성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-117">Usually includes the “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="967d9-118">caller</span><span class="sxs-lookup"><span data-stu-id="967d9-118">caller</span></span> |<span data-ttu-id="967d9-119">가용성을 기반으로 작업, UPN 클레임 또는 SPN 클레임을 수행한 사용자의 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-119">Email address of the user who has performed the operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="967d9-120">channels</span><span class="sxs-lookup"><span data-stu-id="967d9-120">channels</span></span> |<span data-ttu-id="967d9-121">"Admin", "Operation" 값 중 하나여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-121">One of the following values: “Admin”, “Operation”</span></span> |
| <span data-ttu-id="967d9-122">claims</span><span class="sxs-lookup"><span data-stu-id="967d9-122">claims</span></span> |<span data-ttu-id="967d9-123">Resource Manager에서 이 작업을 수행하기 위해 사용자 또는 응용 프로그램을 인증하는 데 Active Directory에서 사용하는 JWT 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-123">The JWT token used by Active Directory to authenticate the user or application to perform this operation in resource manager.</span></span> |
| <span data-ttu-id="967d9-124">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="967d9-124">correlationId</span></span> |<span data-ttu-id="967d9-125">일반적으로 문자열 형식의 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-125">Usually a GUID in the string format.</span></span> <span data-ttu-id="967d9-126">동일한 uber 작업에 속하는 correlationId를 공유하는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-126">Events that share a correlationId belong to the same uber action.</span></span> |
| <span data-ttu-id="967d9-127">설명</span><span class="sxs-lookup"><span data-stu-id="967d9-127">description</span></span> |<span data-ttu-id="967d9-128">이벤트의 정적 텍스트 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-128">Static text description of an event.</span></span> |
| <span data-ttu-id="967d9-129">eventDataId</span><span class="sxs-lookup"><span data-stu-id="967d9-129">eventDataId</span></span> |<span data-ttu-id="967d9-130">이벤트의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-130">Unique identifier of an event.</span></span> |
| <span data-ttu-id="967d9-131">httpRequest</span><span class="sxs-lookup"><span data-stu-id="967d9-131">httpRequest</span></span> |<span data-ttu-id="967d9-132">Http 요청을 설명하는 Blob입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-132">Blob describing the Http Request.</span></span> <span data-ttu-id="967d9-133">일반적으로 "clientRequestId", "clientIpAddress" 및 "method"(PUT 등의</span><span class="sxs-lookup"><span data-stu-id="967d9-133">Usually includes the “clientRequestId”, “clientIpAddress” and “method” (HTTP method.</span></span> <span data-ttu-id="967d9-134">HTTP 메서드) 포함.</span><span class="sxs-lookup"><span data-stu-id="967d9-134">For example, PUT).</span></span> |
| <span data-ttu-id="967d9-135">최소 수준</span><span class="sxs-lookup"><span data-stu-id="967d9-135">level</span></span> |<span data-ttu-id="967d9-136">이벤트의 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-136">Level of the event.</span></span> <span data-ttu-id="967d9-137">다음 값 중 하나: “Critical”, “Error”, “Warning”, “Informational” 및 “Verbose”</span><span class="sxs-lookup"><span data-stu-id="967d9-137">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="967d9-138">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="967d9-138">resourceGroupName</span></span> |<span data-ttu-id="967d9-139">영향을 받는 리소스의 리소스 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-139">Name of the resource group for the impacted resource.</span></span> |
| <span data-ttu-id="967d9-140">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="967d9-140">resourceProviderName</span></span> |<span data-ttu-id="967d9-141">영향을 받는 리소스의 리소스 공급자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-141">Name of the resource provider for the impacted resource</span></span> |
| <span data-ttu-id="967d9-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="967d9-142">resourceId</span></span> |<span data-ttu-id="967d9-143">영향을 받는 리소스의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-143">Resource id of the impacted resource.</span></span> |
| <span data-ttu-id="967d9-144">operationId</span><span class="sxs-lookup"><span data-stu-id="967d9-144">operationId</span></span> |<span data-ttu-id="967d9-145">단일 작업에 해당하는 이벤트 간에 공유되는 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-145">A GUID shared among the events that correspond to a single operation.</span></span> |
| <span data-ttu-id="967d9-146">operationName</span><span class="sxs-lookup"><span data-stu-id="967d9-146">operationName</span></span> |<span data-ttu-id="967d9-147">작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-147">Name of the operation.</span></span> |
| <span data-ttu-id="967d9-148">properties</span><span class="sxs-lookup"><span data-stu-id="967d9-148">properties</span></span> |<span data-ttu-id="967d9-149">이벤트에 대한 세부 정보를 설명하는 `<Key, Value>` 쌍의 집합(즉, 사전)입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-149">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span></span> |
| <span data-ttu-id="967d9-150">status</span><span class="sxs-lookup"><span data-stu-id="967d9-150">status</span></span> |<span data-ttu-id="967d9-151">작업의 상태를 설명하는 문자열.</span><span class="sxs-lookup"><span data-stu-id="967d9-151">String describing the status of the operation.</span></span> <span data-ttu-id="967d9-152">일반적인 값: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="967d9-152">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="967d9-153">subStatus</span><span class="sxs-lookup"><span data-stu-id="967d9-153">subStatus</span></span> |<span data-ttu-id="967d9-154">일반적으로 해당 REST 호출의 HTTP 상태 코드이지만 다음과 같이 하위 상태를 설명하는 다른 문자열을 포함할 수 있습니다. 예를 들어 이러한 일반적인 값은 다음과 같습니다. OK(HTTP 상태 코드: 200), Created(HTTP 상태 코드: 201), Accepted(HTTP 상태 코드: 202), No Content(HTTP 상태 코드: 204), Bad Request(HTTP 상태 코드: 400), Not Found(HTTP 상태 코드: 404), Conflict(HTTP 상태 코드: 409), Internal Server Error(HTTP 상태 코드: 500), Service Unavailable(HTTP 상태 코드:503), Gateway Timeout(HTTP 상태 코드: 504).</span><span class="sxs-lookup"><span data-stu-id="967d9-154">Usually the HTTP status code of the corresponding REST call, but can also include other strings describing a substatus, such as these common values: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504).</span></span> |
| <span data-ttu-id="967d9-155">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="967d9-155">eventTimestamp</span></span> |<span data-ttu-id="967d9-156">이벤트에 해당하는 요청을 처리한 Azure 서비스에 의해 이벤트가 생성된 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-156">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="967d9-157">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="967d9-157">submissionTimestamp</span></span> |<span data-ttu-id="967d9-158">이벤트를 쿼리할 수 있게 되는 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-158">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="967d9-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="967d9-159">subscriptionId</span></span> |<span data-ttu-id="967d9-160">Azure 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-160">Azure Subscription Id.</span></span> |

## <a name="service-health"></a><span data-ttu-id="967d9-161">서비스 상태</span><span class="sxs-lookup"><span data-stu-id="967d9-161">Service health</span></span>
<span data-ttu-id="967d9-162">이 범주에는 Azure에서 발생한 모든 서비스 상태 관련 인시던트의 레코드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-162">This category contains the record of any service health incidents that have occurred in Azure.</span></span> <span data-ttu-id="967d9-163">이 범주에 표시되는 이벤트 유형의 예로는 "미국 동부의 SQL Azure가 가동 중지 상태입니다." 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-163">An example of the type of event you would see in this category is "SQL Azure in East US is experiencing downtime."</span></span> <span data-ttu-id="967d9-164">서비스 상태 이벤트는 작업 필요, 복구 지원, 인시던트, 유지 관리, 정보 또는 보안의 5가지 중 하나이며 구독에 이벤트의 영향을 받는 리소스가 있는 경우에만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-164">Service health events come in five varieties: Action Required, Assisted Recovery, Incident, Maintenance, Information, or Security, and only appear if you have a resource in the subscription that would be impacted by the event.</span></span>

### <a name="sample-event"></a><span data-ttu-id="967d9-165">샘플 이벤트</span><span class="sxs-lookup"><span data-stu-id="967d9-165">Sample event</span></span>
```json
{
  "channels": "Admin",
  "correlationId": "c550176b-8f52-4380-bdc5-36c1b59d3a44",
  "description": "Active: Network Infrastructure - UK South",
  "eventDataId": "c5bc4514-6642-2be3-453e-c6a67841b073",
  "eventName": {
      "value": null
  },
  "category": {
      "value": "ServiceHealth",
      "localizedValue": "Service Health"
  },
  "eventTimestamp": "2017-07-20T23:30:14.8022297Z",
  "id": "/subscriptions/mySubscriptionID/events/c5bc4514-6642-2be3-453e-c6a67841b073/ticks/636361902148022297",
  "level": "Warning",
  "operationName": {
      "value": "Microsoft.ServiceHealth/incident/action",
      "localizedValue": "Microsoft.ServiceHealth/incident/action"
  },
  "resourceProviderName": {
      "value": null
  },
  "resourceType": {
      "value": null,
      "localizedValue": ""
  },
  "resourceId": "/subscriptions/mySubscriptionID",
  "status": {
      "value": "Active",
      "localizedValue": "Active"
  },
  "subStatus": {
      "value": null
  },
  "submissionTimestamp": "2017-07-20T23:30:34.7431946Z",
  "subscriptionId": "mySubscriptionID",
  "properties": {
    "title": "Network Infrastructure - UK South",
    "service": "Service Fabric",
    "region": "UK South",
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited to App Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows to mitigate the impact. The next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited to App Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows to mitigate the impact. The next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a><span data-ttu-id="967d9-166">속성 설명</span><span class="sxs-lookup"><span data-stu-id="967d9-166">Property descriptions</span></span>
<span data-ttu-id="967d9-167">요소 이름</span><span class="sxs-lookup"><span data-stu-id="967d9-167">Element Name</span></span> | <span data-ttu-id="967d9-168">설명</span><span class="sxs-lookup"><span data-stu-id="967d9-168">Description</span></span>
-------- | -----------
<span data-ttu-id="967d9-169">channels</span><span class="sxs-lookup"><span data-stu-id="967d9-169">channels</span></span> | <span data-ttu-id="967d9-170">“Admin”, “Operation” 값 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-170">Is one of the following values: “Admin”, “Operation”</span></span>
<span data-ttu-id="967d9-171">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="967d9-171">correlationId</span></span> | <span data-ttu-id="967d9-172">일반적으로 문자열 형식의 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-172">Is usually a GUID in the string format.</span></span> <span data-ttu-id="967d9-173">동일한 uber 작업에 속하는 이벤트는 일반적으로 동일한 correlationId를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-173">Events with that belong to the same uber action usually share the same correlationId.</span></span>
<span data-ttu-id="967d9-174">설명</span><span class="sxs-lookup"><span data-stu-id="967d9-174">description</span></span> | <span data-ttu-id="967d9-175">이벤트의 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-175">Description of the event.</span></span>
<span data-ttu-id="967d9-176">eventDataId</span><span class="sxs-lookup"><span data-stu-id="967d9-176">eventDataId</span></span> | <span data-ttu-id="967d9-177">이벤트의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-177">The unique identifier of an event.</span></span>
<span data-ttu-id="967d9-178">eventName</span><span class="sxs-lookup"><span data-stu-id="967d9-178">eventName</span></span> | <span data-ttu-id="967d9-179">이벤트의 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-179">The title of the event.</span></span>
<span data-ttu-id="967d9-180">level</span><span class="sxs-lookup"><span data-stu-id="967d9-180">level</span></span> | <span data-ttu-id="967d9-181">이벤트의 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-181">Level of the event.</span></span> <span data-ttu-id="967d9-182">다음 값 중 하나: “Critical”, “Error”, “Warning”, “Informational” 및 “Verbose”</span><span class="sxs-lookup"><span data-stu-id="967d9-182">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span>
<span data-ttu-id="967d9-183">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="967d9-183">resourceProviderName</span></span> | <span data-ttu-id="967d9-184">영향을 받는 리소스의 리소스 공급자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-184">Name of the resource provider for the impacted resource.</span></span> <span data-ttu-id="967d9-185">알 수 없는 경우 null로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-185">If not known, this will be null.</span></span>
<span data-ttu-id="967d9-186">resourceType</span><span class="sxs-lookup"><span data-stu-id="967d9-186">resourceType</span></span>| <span data-ttu-id="967d9-187">영향을 받는 리소스의 리소스 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-187">The type of resource of the impacted resource.</span></span> <span data-ttu-id="967d9-188">알 수 없는 경우 null로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-188">If not known, this will be null.</span></span>
<span data-ttu-id="967d9-189">subStatus</span><span class="sxs-lookup"><span data-stu-id="967d9-189">subStatus</span></span> | <span data-ttu-id="967d9-190">서비스 상태 이벤트의 경우 대개 null입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-190">Usually null for Service Health events.</span></span>
<span data-ttu-id="967d9-191">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="967d9-191">eventTimestamp</span></span> | <span data-ttu-id="967d9-192">로그 이벤트가 생성되어 활동 로그로 제출된 시간의 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-192">Timestamp when the log event was generated and submitted to the Activity Log.</span></span>
<span data-ttu-id="967d9-193">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="967d9-193">submissionTimestamp</span></span> |   <span data-ttu-id="967d9-194">활동 로그에서 이벤트를 사용할 수 있게 된 시간의 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-194">Timestamp when the event became available in the Activity Log.</span></span>
<span data-ttu-id="967d9-195">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="967d9-195">subscriptionId</span></span> | <span data-ttu-id="967d9-196">이 이벤트가 로깅된 Azure 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-196">The Azure subscription in which this event was logged.</span></span>
<span data-ttu-id="967d9-197">status</span><span class="sxs-lookup"><span data-stu-id="967d9-197">status</span></span> | <span data-ttu-id="967d9-198">작업의 상태를 설명하는 문자열.</span><span class="sxs-lookup"><span data-stu-id="967d9-198">String describing the status of the operation.</span></span> <span data-ttu-id="967d9-199">일반적인 값으로는 Active, Resolved 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-199">Some common values are: Active, Resolved.</span></span>
<span data-ttu-id="967d9-200">operationName</span><span class="sxs-lookup"><span data-stu-id="967d9-200">operationName</span></span> | <span data-ttu-id="967d9-201">작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-201">Name of the operation.</span></span> <span data-ttu-id="967d9-202">보통 Microsoft.ServiceHealth/incident/action입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-202">Usually Microsoft.ServiceHealth/incident/action.</span></span>
<span data-ttu-id="967d9-203">카테고리</span><span class="sxs-lookup"><span data-stu-id="967d9-203">category</span></span> | <span data-ttu-id="967d9-204">"ServiceHealth"</span><span class="sxs-lookup"><span data-stu-id="967d9-204">"ServiceHealth"</span></span>
<span data-ttu-id="967d9-205">resourceId</span><span class="sxs-lookup"><span data-stu-id="967d9-205">resourceId</span></span> | <span data-ttu-id="967d9-206">영향을 받는 리소스의 리소스 ID(확인된 경우)입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-206">Resource id of the impacted resource, if known.</span></span> <span data-ttu-id="967d9-207">확인되지 않은 경우에는 구독 ID가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-207">Subscription ID is provided otherwise.</span></span>
<span data-ttu-id="967d9-208">Properties.title</span><span class="sxs-lookup"><span data-stu-id="967d9-208">Properties.title</span></span> | <span data-ttu-id="967d9-209">이 통신에 대한 지역화된 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-209">The localized title for this communication.</span></span> <span data-ttu-id="967d9-210">기본 언어는 영어입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-210">English is the default language.</span></span>
<span data-ttu-id="967d9-211">Properties.communication</span><span class="sxs-lookup"><span data-stu-id="967d9-211">Properties.communication</span></span> | <span data-ttu-id="967d9-212">HTML 태그와 통신에 대한 지역화된 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-212">The localized details of the communication with HTML markup.</span></span> <span data-ttu-id="967d9-213">기본값은 영어입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-213">English is the default.</span></span>
<span data-ttu-id="967d9-214">Properties.incidentType</span><span class="sxs-lookup"><span data-stu-id="967d9-214">Properties.incidentType</span></span> | <span data-ttu-id="967d9-215">가능한 값: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span><span class="sxs-lookup"><span data-stu-id="967d9-215">Possible values: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span></span>
<span data-ttu-id="967d9-216">Properties.trackingId</span><span class="sxs-lookup"><span data-stu-id="967d9-216">Properties.trackingId</span></span> | <span data-ttu-id="967d9-217">이 이벤트가 연결된 인시던트를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-217">Identifies the incident this event is associated with.</span></span> <span data-ttu-id="967d9-218">인시던트와 관련된 이벤트를 상호 연결할 때 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-218">Use this to correlate the events related to an incident.</span></span>
<span data-ttu-id="967d9-219">Properties.impactedServices</span><span class="sxs-lookup"><span data-stu-id="967d9-219">Properties.impactedServices</span></span> | <span data-ttu-id="967d9-220">인시던트에 의해 영향을 받는 서비스 및 지역을 설명하는 이스케이프된 JSON Blob입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-220">An escaped JSON blob which describes the services and regions that are impacted by the incident.</span></span> <span data-ttu-id="967d9-221">각각 ServiceName과 ImpactedRegions 목록을 포함하는 서비스 목록으로, 각 ImpactedRegions에는 RegionName이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-221">A list of Services, each of which has a ServiceName and a list of ImpactedRegions, each of which has a RegionName.</span></span>
<span data-ttu-id="967d9-222">Properties.defaultLanguageTitle</span><span class="sxs-lookup"><span data-stu-id="967d9-222">Properties.defaultLanguageTitle</span></span> | <span data-ttu-id="967d9-223">통신은 영어로 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-223">The communication in English</span></span>
<span data-ttu-id="967d9-224">Properties.defaultLanguageContent</span><span class="sxs-lookup"><span data-stu-id="967d9-224">Properties.defaultLanguageContent</span></span> | <span data-ttu-id="967d9-225">영어로 통신은 html 태그 또는 일반 텍스트로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-225">The communication in English as either html markup or plain text</span></span>
<span data-ttu-id="967d9-226">Properties.stage</span><span class="sxs-lookup"><span data-stu-id="967d9-226">Properties.stage</span></span> | <span data-ttu-id="967d9-227">AssistedRecovery, ActionRequired, Information, Incident, Security에 대해 가능한 값: Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="967d9-227">Possible values for AssistedRecovery, ActionRequired, Information, Incident, Security: are Active, Resolved.</span></span> <span data-ttu-id="967d9-228">Maintenance에 대해 가능한 값: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete</span><span class="sxs-lookup"><span data-stu-id="967d9-228">For Maintenance they are: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete</span></span>
<span data-ttu-id="967d9-229">Properties.communicationId</span><span class="sxs-lookup"><span data-stu-id="967d9-229">Properties.communicationId</span></span> | <span data-ttu-id="967d9-230">이 이벤트가 연결된 통신입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-230">The communication this event is associated.</span></span>

## <a name="alert"></a><span data-ttu-id="967d9-231">경고</span><span class="sxs-lookup"><span data-stu-id="967d9-231">Alert</span></span>
<span data-ttu-id="967d9-232">이 범주에는 모든 Azure 경고 활성화의 레코드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-232">This category contains the record of all activations of Azure alerts.</span></span> <span data-ttu-id="967d9-233">이 범주에 표시되는 이벤트 유형의 예로는 "지난 5분 동안 myVM의 CPU 사용률이 80%를 초과했습니다." 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-233">An example of the type of event you would see in this category is "CPU % on myVM has been over 80 for the past 5 minutes."</span></span> <span data-ttu-id="967d9-234">다수의 Azure 시스템에서 경고 개념이 사용됩니다. 일종의 규칙을 정의하여 조건이 해당 규칙과 일치하면 알림을 수신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-234">A variety of Azure systems have an alerting concept -- you can define a rule of some sort and receive a notification when conditions match that rule.</span></span> <span data-ttu-id="967d9-235">지원되는 Azure 경고 유형이 '활성화'되거나 알림 생성을 위한 조건이 충족될 때마다 활성화 레코드도 이 활동 로그 범주로 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-235">Each time a supported Azure alert type 'activates,' or the conditions are met to generate a notification, a record of the activation is also pushed to this category of the Activity Log.</span></span>

### <a name="sample-event"></a><span data-ttu-id="967d9-236">샘플 이벤트</span><span class="sxs-lookup"><span data-stu-id="967d9-236">Sample event</span></span>

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in the last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
  "eventDataId": "149d4baf-53dc-4cf4-9e29-17de37405cd9",
  "eventName": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "category": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle/events/149d4baf-53dc-4cf4-9e29-17de37405cd9/ticks/636362258535221920",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "Microsoft.ClassicCompute",
    "localizedValue": "Microsoft.ClassicCompute"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle",
  "resourceType": {
    "value": "Microsoft.ClassicCompute/domainNames/slots/roles",
    "localizedValue": "Microsoft.ClassicCompute/domainNames/slots/roles"
  },
  "operationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "operationName": {
    "value": "Microsoft.Insights/AlertRules/Resolved/Action",
    "localizedValue": "Microsoft.Insights/AlertRules/Resolved/Action"
  },
  "properties": {
    "RuleUri": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert",
    "RuleName": "myalert",
    "RuleDescription": "",
    "Threshold": "100000",
    "WindowSizeInMinutes": "5",
    "Aggregation": "Average",
    "Operator": "LessThan",
    "MetricName": "Disk read",
    "MetricUnit": "Count"
  },
  "status": {
    "value": "Resolved",
    "localizedValue": "Resolved"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T09:24:13.522192Z",
  "submissionTimestamp": "2017-07-21T09:24:15.6578651Z",
  "subscriptionId": "mySubscriptionID"
}
```

### <a name="property-descriptions"></a><span data-ttu-id="967d9-237">속성 설명</span><span class="sxs-lookup"><span data-stu-id="967d9-237">Property descriptions</span></span>
| <span data-ttu-id="967d9-238">요소 이름</span><span class="sxs-lookup"><span data-stu-id="967d9-238">Element Name</span></span> | <span data-ttu-id="967d9-239">설명</span><span class="sxs-lookup"><span data-stu-id="967d9-239">Description</span></span> |
| --- | --- |
| <span data-ttu-id="967d9-240">caller</span><span class="sxs-lookup"><span data-stu-id="967d9-240">caller</span></span> | <span data-ttu-id="967d9-241">Always Microsoft.Insights/alertRules</span><span class="sxs-lookup"><span data-stu-id="967d9-241">Always Microsoft.Insights/alertRules</span></span> |
| <span data-ttu-id="967d9-242">channels</span><span class="sxs-lookup"><span data-stu-id="967d9-242">channels</span></span> | <span data-ttu-id="967d9-243">항상 "Admin, Operation"입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-243">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="967d9-244">claims</span><span class="sxs-lookup"><span data-stu-id="967d9-244">claims</span></span> | <span data-ttu-id="967d9-245">경고 엔진의 SPN(서비스 사용자 이름) 또는 리소스 종류가 포함된 JSON Blob입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-245">JSON blob with the SPN (service principal name), or resource type, of the alert engine.</span></span> |
| <span data-ttu-id="967d9-246">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="967d9-246">correlationId</span></span> | <span data-ttu-id="967d9-247">문자열 형식의 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-247">A GUID in the string format.</span></span> |
| <span data-ttu-id="967d9-248">설명</span><span class="sxs-lookup"><span data-stu-id="967d9-248">description</span></span> |<span data-ttu-id="967d9-249">경고 이벤트의 정적 텍스트 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-249">Static text description of the alert event.</span></span> |
| <span data-ttu-id="967d9-250">eventDataId</span><span class="sxs-lookup"><span data-stu-id="967d9-250">eventDataId</span></span> |<span data-ttu-id="967d9-251">경고 이벤트의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-251">Unique identifier of the alert event.</span></span> |
| <span data-ttu-id="967d9-252">level</span><span class="sxs-lookup"><span data-stu-id="967d9-252">level</span></span> |<span data-ttu-id="967d9-253">이벤트의 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-253">Level of the event.</span></span> <span data-ttu-id="967d9-254">다음 값 중 하나: “Critical”, “Error”, “Warning”, “Informational” 및 “Verbose”</span><span class="sxs-lookup"><span data-stu-id="967d9-254">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="967d9-255">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="967d9-255">resourceGroupName</span></span> |<span data-ttu-id="967d9-256">메트릭 경고의 경우 영향을 받는 리소스의 리소스 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-256">Name of the resource group for the impacted resource if it is a metric alert.</span></span> <span data-ttu-id="967d9-257">기타 경고 유형의 경우에는 경고 자체가 포함된 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-257">For other alert types, this is the name of the resource group that contains the alert itself.</span></span> |
| <span data-ttu-id="967d9-258">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="967d9-258">resourceProviderName</span></span> |<span data-ttu-id="967d9-259">메트릭 경고의 경우 영향을 받는 리소스의 리소스 공급자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-259">Name of the resource provider for the impacted resource if it is a metric alert.</span></span> <span data-ttu-id="967d9-260">기타 경고 유형의 경우에는 경고 자체의 리소스 공급자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-260">For other alert types, this is the name of the resource provider for the alert itself.</span></span> |
| <span data-ttu-id="967d9-261">resourceId</span><span class="sxs-lookup"><span data-stu-id="967d9-261">resourceId</span></span> | <span data-ttu-id="967d9-262">메트릭 경고의 경우 영향을 받는 리소스의 리소스 ID 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-262">Name of the resource ID for the impacted resource if it is a metric alert.</span></span> <span data-ttu-id="967d9-263">기타 경고 유형의 경우에는 경고 리소스 자체의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-263">For other alert types, this is the resource ID of the alert resource itself.</span></span> |
| <span data-ttu-id="967d9-264">operationId</span><span class="sxs-lookup"><span data-stu-id="967d9-264">operationId</span></span> |<span data-ttu-id="967d9-265">단일 작업에 해당하는 이벤트 간에 공유되는 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-265">A GUID shared among the events that correspond to a single operation.</span></span> |
| <span data-ttu-id="967d9-266">operationName</span><span class="sxs-lookup"><span data-stu-id="967d9-266">operationName</span></span> |<span data-ttu-id="967d9-267">작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-267">Name of the operation.</span></span> |
| <span data-ttu-id="967d9-268">properties</span><span class="sxs-lookup"><span data-stu-id="967d9-268">properties</span></span> |<span data-ttu-id="967d9-269">이벤트에 대한 세부 정보를 설명하는 `<Key, Value>` 쌍의 집합(즉, 사전)입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-269">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span></span> |
| <span data-ttu-id="967d9-270">status</span><span class="sxs-lookup"><span data-stu-id="967d9-270">status</span></span> |<span data-ttu-id="967d9-271">작업의 상태를 설명하는 문자열.</span><span class="sxs-lookup"><span data-stu-id="967d9-271">String describing the status of the operation.</span></span> <span data-ttu-id="967d9-272">일반적인 값: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="967d9-272">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="967d9-273">subStatus</span><span class="sxs-lookup"><span data-stu-id="967d9-273">subStatus</span></span> | <span data-ttu-id="967d9-274">경고의 경우 대개 null입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-274">Usually null for alerts.</span></span> |
| <span data-ttu-id="967d9-275">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="967d9-275">eventTimestamp</span></span> |<span data-ttu-id="967d9-276">이벤트에 해당하는 요청을 처리한 Azure 서비스에 의해 이벤트가 생성된 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-276">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="967d9-277">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="967d9-277">submissionTimestamp</span></span> |<span data-ttu-id="967d9-278">이벤트를 쿼리할 수 있게 되는 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-278">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="967d9-279">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="967d9-279">subscriptionId</span></span> |<span data-ttu-id="967d9-280">Azure 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-280">Azure Subscription Id.</span></span> |

### <a name="properties-field-per-alert-type"></a><span data-ttu-id="967d9-281">경고 유형별 속성 필드</span><span class="sxs-lookup"><span data-stu-id="967d9-281">Properties field per alert type</span></span>
<span data-ttu-id="967d9-282">속성 필드에는 경고 이벤트의 원본에 따라 다른 값이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-282">The properties field will contain different values depending on the source of the alert event.</span></span> <span data-ttu-id="967d9-283">일반적으로 사용되는 두 경고 이벤트 공급자는 활동 로그 경고와 메트릭 경고입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-283">Two common alert event providers are Activity Log alerts and metric alerts.</span></span>

#### <a name="properties-for-activity-log-alerts"></a><span data-ttu-id="967d9-284">활동 로그 경고의 속성</span><span class="sxs-lookup"><span data-stu-id="967d9-284">Properties for Activity Log alerts</span></span>
| <span data-ttu-id="967d9-285">요소 이름</span><span class="sxs-lookup"><span data-stu-id="967d9-285">Element Name</span></span> | <span data-ttu-id="967d9-286">설명</span><span class="sxs-lookup"><span data-stu-id="967d9-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="967d9-287">properties.subscriptionId</span><span class="sxs-lookup"><span data-stu-id="967d9-287">properties.subscriptionId</span></span> | <span data-ttu-id="967d9-288">이 활동 로그 경고 규칙을 활성화한 활동 로그 이벤트의 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-288">The subscription ID from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="967d9-289">properties.eventDataId</span><span class="sxs-lookup"><span data-stu-id="967d9-289">properties.eventDataId</span></span> | <span data-ttu-id="967d9-290">이 활동 로그 경고 규칙을 활성화한 활동 로그 이벤트의 이벤트 데이터 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-290">The event data ID from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="967d9-291">properties.resourceGroup</span><span class="sxs-lookup"><span data-stu-id="967d9-291">properties.resourceGroup</span></span> | <span data-ttu-id="967d9-292">이 활동 로그 경고 규칙을 활성화한 활동 로그 이벤트의 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-292">The resource group from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="967d9-293">properties.resourceId</span><span class="sxs-lookup"><span data-stu-id="967d9-293">properties.resourceId</span></span> | <span data-ttu-id="967d9-294">이 활동 로그 경고 규칙을 활성화한 활동 로그 이벤트의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-294">The resource ID from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="967d9-295">properties.eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="967d9-295">properties.eventTimestamp</span></span> | <span data-ttu-id="967d9-296">이 활동 로그 경고 규칙을 활성화한 활동 로그 이벤트의 이벤트 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-296">The event timestamp of the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="967d9-297">properties.operationName</span><span class="sxs-lookup"><span data-stu-id="967d9-297">properties.operationName</span></span> | <span data-ttu-id="967d9-298">이 활동 로그 경고 규칙을 활성화한 활동 로그 이벤트의 작업 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-298">The operation name from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="967d9-299">properties.status</span><span class="sxs-lookup"><span data-stu-id="967d9-299">properties.status</span></span> | <span data-ttu-id="967d9-300">이 활동 로그 경고 규칙을 활성화한 활동 로그 이벤트의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-300">The status from the activity log event which caused this activity log alert rule to be activated.</span></span>|

#### <a name="properties-for-metric-alerts"></a><span data-ttu-id="967d9-301">메트릭 경고의 속성</span><span class="sxs-lookup"><span data-stu-id="967d9-301">Properties for metric alerts</span></span>
| <span data-ttu-id="967d9-302">요소 이름</span><span class="sxs-lookup"><span data-stu-id="967d9-302">Element Name</span></span> | <span data-ttu-id="967d9-303">설명</span><span class="sxs-lookup"><span data-stu-id="967d9-303">Description</span></span> |
| --- | --- |
| <span data-ttu-id="967d9-304">properties.RuleUri</span><span class="sxs-lookup"><span data-stu-id="967d9-304">properties.RuleUri</span></span> | <span data-ttu-id="967d9-305">메트릭 경고 규칙 자체의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-305">Resource ID of the metric alert rule itself.</span></span> |
| <span data-ttu-id="967d9-306">properties.RuleName</span><span class="sxs-lookup"><span data-stu-id="967d9-306">properties.RuleName</span></span> | <span data-ttu-id="967d9-307">메트릭 경고 규칙의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-307">The name of the metric alert rule.</span></span> |
| <span data-ttu-id="967d9-308">properties.RuleDescription</span><span class="sxs-lookup"><span data-stu-id="967d9-308">properties.RuleDescription</span></span> | <span data-ttu-id="967d9-309">경고 규칙에 정의된 메트릭 경고 규칙의 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-309">The description of the metric alert rule (as defined in the alert rule).</span></span> |
| <span data-ttu-id="967d9-310">properties.Threshold</span><span class="sxs-lookup"><span data-stu-id="967d9-310">properties.Threshold</span></span> | <span data-ttu-id="967d9-311">메트릭 경고 규칙의 평가에 사용되는 임계값입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-311">The threshold value used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="967d9-312">properties.WindowSizeInMinutes</span><span class="sxs-lookup"><span data-stu-id="967d9-312">properties.WindowSizeInMinutes</span></span> | <span data-ttu-id="967d9-313">메트릭 경고 규칙의 평가에 사용되는 창 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-313">The window size used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="967d9-314">properties.Aggregation</span><span class="sxs-lookup"><span data-stu-id="967d9-314">properties.Aggregation</span></span> | <span data-ttu-id="967d9-315">메트릭 경고 규칙에 정의된 집계 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-315">The aggregation type defined in the metric alert rule.</span></span> |
| <span data-ttu-id="967d9-316">properties.Operator</span><span class="sxs-lookup"><span data-stu-id="967d9-316">properties.Operator</span></span> | <span data-ttu-id="967d9-317">메트릭 경고 규칙의 평가에 사용되는 조건부 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-317">The conditional operator used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="967d9-318">properties.MetricName</span><span class="sxs-lookup"><span data-stu-id="967d9-318">properties.MetricName</span></span> | <span data-ttu-id="967d9-319">메트릭 경고 규칙의 평가에 사용되는 메트릭의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-319">The metric name of the metric used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="967d9-320">properties.MetricUnit</span><span class="sxs-lookup"><span data-stu-id="967d9-320">properties.MetricUnit</span></span> | <span data-ttu-id="967d9-321">메트릭 경고 규칙의 평가에 사용되는 메트릭의 메트릭 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-321">The metric unit for the metric used in the evaluation of the metric alert rule.</span></span> |

## <a name="autoscale"></a><span data-ttu-id="967d9-322">Autoscale</span><span class="sxs-lookup"><span data-stu-id="967d9-322">Autoscale</span></span>
<span data-ttu-id="967d9-323">이 범주에는 구독에서 정의한 자동 크기 조정 설정을 기준으로 하는 자동 크기 조정 엔진 작업 관련 이벤트의 레코드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-323">This category contains the record of any events related to the operation of the autoscale engine based on any autoscale settings you have defined in your subscription.</span></span> <span data-ttu-id="967d9-324">이 범주에 표시되는 이벤트 유형의 예로는 "자동 크기 조정 강화 동작이 실패했습니다." 등이 있습니다</span><span class="sxs-lookup"><span data-stu-id="967d9-324">An example of the type of event you would see in this category is "Autoscale scale up action failed."</span></span> <span data-ttu-id="967d9-325">자동 크기 조정을 사용하면 자동 크기 조정 설정을 사용하여 시간 및/또는 로드(메트릭) 데이터를 기준으로 지원되는 리소스 종류의 인스턴스 수를 자동으로 규모 확장하거나 규모 감축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-325">Using autoscale, you can automatically scale out or scale in the number of instances in a supported resource type based on time of day and/or load (metric) data using an autoscale setting.</span></span> <span data-ttu-id="967d9-326">강화 또는 규모 축소 조건이 충족되면 시작 이벤트와 성공 또는 실패 이벤트가 이 범주에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-326">When the conditions are met to scale up or down, the start and succeeded or failed events will be recorded in this category.</span></span>

### <a name="sample-event"></a><span data-ttu-id="967d9-327">샘플 이벤트</span><span class="sxs-lookup"><span data-stu-id="967d9-327">Sample event</span></span>
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "The autoscale engine attempting to scale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count to 2 instances count.",
  "eventDataId": "a5b92075-1de9-42f1-b52e-6f3e4945a7c7",
  "eventName": {
    "value": "AutoscaleAction",
    "localizedValue": "AutoscaleAction"
  },
  "category": {
    "value": "Autoscale",
    "localizedValue": "Autoscale"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup/events/a5b92075-1de9-42f1-b52e-6f3e4945a7c7/ticks/636361956518681572",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "microsoft.insights",
    "localizedValue": "microsoft.insights"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup",
  "resourceType": {
    "value": "microsoft.insights/autoscalesettings",
    "localizedValue": "microsoft.insights/autoscalesettings"
  },
  "operationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "operationName": {
    "value": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action",
    "localizedValue": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action"
  },
  "properties": {
    "Description": "The autoscale engine attempting to scale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count to 2 instances count.",
    "ResourceName": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource",
    "OldInstancesCount": "3",
    "NewInstancesCount": "2",
    "LastScaleActionTime": "Fri, 21 Jul 2017 01:00:51 GMT"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T01:00:51.8681572Z",
  "submissionTimestamp": "2017-07-21T01:00:52.3008754Z",
  "subscriptionId": "mySubscriptionID"
}

```

### <a name="property-descriptions"></a><span data-ttu-id="967d9-328">속성 설명</span><span class="sxs-lookup"><span data-stu-id="967d9-328">Property descriptions</span></span>
| <span data-ttu-id="967d9-329">요소 이름</span><span class="sxs-lookup"><span data-stu-id="967d9-329">Element Name</span></span> | <span data-ttu-id="967d9-330">설명</span><span class="sxs-lookup"><span data-stu-id="967d9-330">Description</span></span> |
| --- | --- |
| <span data-ttu-id="967d9-331">caller</span><span class="sxs-lookup"><span data-stu-id="967d9-331">caller</span></span> | <span data-ttu-id="967d9-332">항상 Microsoft.Insights/autoscaleSettings입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-332">Always Microsoft.Insights/autoscaleSettings</span></span> |
| <span data-ttu-id="967d9-333">channels</span><span class="sxs-lookup"><span data-stu-id="967d9-333">channels</span></span> | <span data-ttu-id="967d9-334">항상 "Admin, Operation"입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-334">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="967d9-335">claims</span><span class="sxs-lookup"><span data-stu-id="967d9-335">claims</span></span> | <span data-ttu-id="967d9-336">자동 크기 조정 엔진의 SPN(서비스 사용자 이름) 또는 리소스 종류가 포함된 JSON Blob입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-336">JSON blob with the SPN (service principal name), or resource type, of the autoscale engine.</span></span> |
| <span data-ttu-id="967d9-337">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="967d9-337">correlationId</span></span> | <span data-ttu-id="967d9-338">문자열 형식의 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-338">A GUID in the string format.</span></span> |
| <span data-ttu-id="967d9-339">설명</span><span class="sxs-lookup"><span data-stu-id="967d9-339">description</span></span> |<span data-ttu-id="967d9-340">자동 크기 조정 이벤트의 정적 텍스트 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-340">Static text description of the autoscale event.</span></span> |
| <span data-ttu-id="967d9-341">eventDataId</span><span class="sxs-lookup"><span data-stu-id="967d9-341">eventDataId</span></span> |<span data-ttu-id="967d9-342">자동 크기 조정 이벤트의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-342">Unique identifier of the autoscale event.</span></span> |
| <span data-ttu-id="967d9-343">level</span><span class="sxs-lookup"><span data-stu-id="967d9-343">level</span></span> |<span data-ttu-id="967d9-344">이벤트의 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-344">Level of the event.</span></span> <span data-ttu-id="967d9-345">다음 값 중 하나: “Critical”, “Error”, “Warning”, “Informational” 및 “Verbose”</span><span class="sxs-lookup"><span data-stu-id="967d9-345">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="967d9-346">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="967d9-346">resourceGroupName</span></span> |<span data-ttu-id="967d9-347">자동 크기 조정 설정의 리소스 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-347">Name of the resource group for the autoscale setting.</span></span> |
| <span data-ttu-id="967d9-348">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="967d9-348">resourceProviderName</span></span> |<span data-ttu-id="967d9-349">자동 크기 조정 설정의 리소스 공급자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-349">Name of the resource provider for the autoscale setting.</span></span> |
| <span data-ttu-id="967d9-350">resourceId</span><span class="sxs-lookup"><span data-stu-id="967d9-350">resourceId</span></span> |<span data-ttu-id="967d9-351">자동 크기 조정 설정의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-351">Resource id of the autoscale setting.</span></span> |
| <span data-ttu-id="967d9-352">operationId</span><span class="sxs-lookup"><span data-stu-id="967d9-352">operationId</span></span> |<span data-ttu-id="967d9-353">단일 작업에 해당하는 이벤트 간에 공유되는 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-353">A GUID shared among the events that correspond to a single operation.</span></span> |
| <span data-ttu-id="967d9-354">operationName</span><span class="sxs-lookup"><span data-stu-id="967d9-354">operationName</span></span> |<span data-ttu-id="967d9-355">작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-355">Name of the operation.</span></span> |
| <span data-ttu-id="967d9-356">properties</span><span class="sxs-lookup"><span data-stu-id="967d9-356">properties</span></span> |<span data-ttu-id="967d9-357">이벤트에 대한 세부 정보를 설명하는 `<Key, Value>` 쌍의 집합(즉, 사전)입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-357">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span></span> |
| <span data-ttu-id="967d9-358">properties.Description</span><span class="sxs-lookup"><span data-stu-id="967d9-358">properties.Description</span></span> | <span data-ttu-id="967d9-359">자동 크기 조정 엔진이 수행 중이었던 작업의 자세한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-359">Detailed description of what the autoscale engine was doing.</span></span> |
| <span data-ttu-id="967d9-360">properties.ResourceName</span><span class="sxs-lookup"><span data-stu-id="967d9-360">properties.ResourceName</span></span> | <span data-ttu-id="967d9-361">영향을 받는 리소스(크기 조정 동작을 수행 중이었던 리소스)의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-361">Resource ID of the impacted resource (the resource on which the scale action was being performed)</span></span> |
| <span data-ttu-id="967d9-362">properties.OldInstancesCount</span><span class="sxs-lookup"><span data-stu-id="967d9-362">properties.OldInstancesCount</span></span> | <span data-ttu-id="967d9-363">자동 크기 조정 동작이 적용되기 전의 인스턴스 수입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-363">The number of instances before the autoscale action took effect.</span></span> |
| <span data-ttu-id="967d9-364">properties.NewInstancesCount</span><span class="sxs-lookup"><span data-stu-id="967d9-364">properties.NewInstancesCount</span></span> | <span data-ttu-id="967d9-365">자동 크기 조정 동작이 적용된 후의 인스턴스 수입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-365">The number of instances after the autoscale action took effect.</span></span> |
| <span data-ttu-id="967d9-366">properties.LastScaleActionTime</span><span class="sxs-lookup"><span data-stu-id="967d9-366">properties.LastScaleActionTime</span></span> | <span data-ttu-id="967d9-367">자동 크기 조정이 수행된 시간의 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-367">The timestamp of when the autoscale action occurred.</span></span> |
| <span data-ttu-id="967d9-368">status</span><span class="sxs-lookup"><span data-stu-id="967d9-368">status</span></span> |<span data-ttu-id="967d9-369">작업의 상태를 설명하는 문자열.</span><span class="sxs-lookup"><span data-stu-id="967d9-369">String describing the status of the operation.</span></span> <span data-ttu-id="967d9-370">일반적인 값: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="967d9-370">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="967d9-371">subStatus</span><span class="sxs-lookup"><span data-stu-id="967d9-371">subStatus</span></span> | <span data-ttu-id="967d9-372">자동 크기 조정의 경우 대개 null입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-372">Usually null for autoscale.</span></span> |
| <span data-ttu-id="967d9-373">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="967d9-373">eventTimestamp</span></span> |<span data-ttu-id="967d9-374">이벤트에 해당하는 요청을 처리한 Azure 서비스에 의해 이벤트가 생성된 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-374">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="967d9-375">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="967d9-375">submissionTimestamp</span></span> |<span data-ttu-id="967d9-376">이벤트를 쿼리할 수 있게 되는 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-376">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="967d9-377">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="967d9-377">subscriptionId</span></span> |<span data-ttu-id="967d9-378">Azure 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="967d9-378">Azure Subscription Id.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="967d9-379">다음 단계</span><span class="sxs-lookup"><span data-stu-id="967d9-379">Next steps</span></span>
* [<span data-ttu-id="967d9-380">활동 로그(이전의 감사 로그)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="967d9-380">Learn more about the Activity Log (formerly Audit Logs)</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="967d9-381">Azure 활동 로그를 Event Hubs로 스트림</span><span class="sxs-lookup"><span data-stu-id="967d9-381">Stream the Azure Activity Log to Event Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
