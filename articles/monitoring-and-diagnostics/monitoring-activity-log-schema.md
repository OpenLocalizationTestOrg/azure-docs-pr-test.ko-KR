---
title: "활동 로그 이벤트 스키마 aaaAzure | Microsoft Docs"
description: "Hello 활동 로그에 내보낸 데이터에 대 한 hello 이벤트 스키마 이해"
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
ms.openlocfilehash: dfece949a20a4d9b4e8a4d488c1c34842d87d586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-activity-log-event-schema"></a><span data-ttu-id="7e34c-103">Azure 활동 로그 이벤트 스키마</span><span class="sxs-lookup"><span data-stu-id="7e34c-103">Azure Activity Log event schema</span></span>
<span data-ttu-id="7e34c-104">hello **Azure 활동 로그** Azure에서 발생 한 모든 구독 수준 이벤트에 대 한 정보를 제공 하는 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-104">hello **Azure Activity Log** is a log that provides insight into any subscription-level events that have occurred in Azure.</span></span> <span data-ttu-id="7e34c-105">이 문서에서는 데이터의 범주별 hello 이벤트 스키마를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-105">This article describes hello event schema per category of data.</span></span>

## <a name="administrative"></a><span data-ttu-id="7e34c-106">관리</span><span class="sxs-lookup"><span data-stu-id="7e34c-106">Administrative</span></span>
<span data-ttu-id="7e34c-107">이 범주에 모든 hello 레코드 만들기, 업데이트, 삭제 및 작업 작업이 리소스 관리자를 통해 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-107">This category contains hello record of all create, update, delete, and action operations performed through Resource Manager.</span></span> <span data-ttu-id="7e34c-108">이 범주에 표시 되는 이벤트 유형을 포함 하는 hello의 예로 "가상 컴퓨터 만들기" 및 "삭제" 네트워크 보안 그룹 사용자가 수행한 동작 또는 리소스 관리자를 사용 하 여 응용 프로그램은 특정 리소스 종류에 대 한 작업으로 모델링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-108">Examples of hello types of events you would see in this category include "create virtual machine" and "delete network security group" Every action taken by a user or application using Resource Manager is modeled as an operation on a particular resource type.</span></span> <span data-ttu-id="7e34c-109">Hello 작업 유형이 hello 시작과 성공의 hello 레코드를 삭제 또는 동작을 작성 하거나 hello 관리 범주에 해당 작업의 실패 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-109">If hello operation type is Write, Delete, or Action, hello records of both hello start and success or fail of that operation are recorded in hello Administrative category.</span></span> <span data-ttu-id="7e34c-110">구독에 변경 내용을 toorole 기반 액세스 제어를 관리 범주 hello 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-110">hello Administrative category also includes any changes toorole-based access control in a subscription.</span></span>

### <a name="sample-event"></a><span data-ttu-id="7e34c-111">샘플 이벤트</span><span class="sxs-lookup"><span data-stu-id="7e34c-111">Sample event</span></span>
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

### <a name="property-descriptions"></a><span data-ttu-id="7e34c-112">속성 설명</span><span class="sxs-lookup"><span data-stu-id="7e34c-112">Property descriptions</span></span>
| <span data-ttu-id="7e34c-113">요소 이름</span><span class="sxs-lookup"><span data-stu-id="7e34c-113">Element Name</span></span> | <span data-ttu-id="7e34c-114">설명</span><span class="sxs-lookup"><span data-stu-id="7e34c-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7e34c-115">권한 부여</span><span class="sxs-lookup"><span data-stu-id="7e34c-115">authorization</span></span> |<span data-ttu-id="7e34c-116">Hello 이벤트의 RBAC 속성의 blob입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-116">Blob of RBAC properties of hello event.</span></span> <span data-ttu-id="7e34c-117">일반적으로 hello "action", "role" 및 "범위" 속성이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-117">Usually includes hello “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="7e34c-118">caller</span><span class="sxs-lookup"><span data-stu-id="7e34c-118">caller</span></span> |<span data-ttu-id="7e34c-119">Hello 작업, UPN 클레임 또는 SPN 클레임 가용성에 따라 수행한 hello 사용자의 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-119">Email address of hello user who has performed hello operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="7e34c-120">channels</span><span class="sxs-lookup"><span data-stu-id="7e34c-120">channels</span></span> |<span data-ttu-id="7e34c-121">Hello 다음 값 중 하나: "Admin", "작업이"</span><span class="sxs-lookup"><span data-stu-id="7e34c-121">One of hello following values: “Admin”, “Operation”</span></span> |
| <span data-ttu-id="7e34c-122">claims</span><span class="sxs-lookup"><span data-stu-id="7e34c-122">claims</span></span> |<span data-ttu-id="7e34c-123">Active Directory tooauthenticate hello 사용자 또는 응용 프로그램 tooperform에서 리소스 관리자에서이 작업을 사용 하는 hello JWT 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-123">hello JWT token used by Active Directory tooauthenticate hello user or application tooperform this operation in resource manager.</span></span> |
| <span data-ttu-id="7e34c-124">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="7e34c-124">correlationId</span></span> |<span data-ttu-id="7e34c-125">일반적으로 hello 문자열 형식의 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-125">Usually a GUID in hello string format.</span></span> <span data-ttu-id="7e34c-126">CorrelationId를 공유 하는 이벤트가 속하는지 toohello 같은 uber 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-126">Events that share a correlationId belong toohello same uber action.</span></span> |
| <span data-ttu-id="7e34c-127">설명</span><span class="sxs-lookup"><span data-stu-id="7e34c-127">description</span></span> |<span data-ttu-id="7e34c-128">이벤트의 정적 텍스트 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-128">Static text description of an event.</span></span> |
| <span data-ttu-id="7e34c-129">eventDataId</span><span class="sxs-lookup"><span data-stu-id="7e34c-129">eventDataId</span></span> |<span data-ttu-id="7e34c-130">이벤트의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-130">Unique identifier of an event.</span></span> |
| <span data-ttu-id="7e34c-131">httpRequest</span><span class="sxs-lookup"><span data-stu-id="7e34c-131">httpRequest</span></span> |<span data-ttu-id="7e34c-132">Http 요청 번호를 설명 하는 blob입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-132">Blob describing hello Http Request.</span></span> <span data-ttu-id="7e34c-133">일반적으로 "clientRequestId" hello, "clientIpAddress" 및 "방법" (HTTP 메서드입니다 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-133">Usually includes hello “clientRequestId”, “clientIpAddress” and “method” (HTTP method.</span></span> <span data-ttu-id="7e34c-134">HTTP 메서드) 포함.</span><span class="sxs-lookup"><span data-stu-id="7e34c-134">For example, PUT).</span></span> |
| <span data-ttu-id="7e34c-135">level</span><span class="sxs-lookup"><span data-stu-id="7e34c-135">level</span></span> |<span data-ttu-id="7e34c-136">Hello 이벤트의 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-136">Level of hello event.</span></span> <span data-ttu-id="7e34c-137">Hello 다음 값 중 하나: "Critical", "Error", "Warning", "Informational" 및 "Verbose"</span><span class="sxs-lookup"><span data-stu-id="7e34c-137">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="7e34c-138">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="7e34c-138">resourceGroupName</span></span> |<span data-ttu-id="7e34c-139">Hello에 대 한 hello 리소스 그룹의 이름을 리소스를 저하 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-139">Name of hello resource group for hello impacted resource.</span></span> |
| <span data-ttu-id="7e34c-140">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="7e34c-140">resourceProviderName</span></span> |<span data-ttu-id="7e34c-141">리소스의 영향을 hello에 대 한 hello 리소스 공급자의 이름</span><span class="sxs-lookup"><span data-stu-id="7e34c-141">Name of hello resource provider for hello impacted resource</span></span> |
| <span data-ttu-id="7e34c-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="7e34c-142">resourceId</span></span> |<span data-ttu-id="7e34c-143">Hello의 리소스 id 리소스를 저하 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-143">Resource id of hello impacted resource.</span></span> |
| <span data-ttu-id="7e34c-144">operationId</span><span class="sxs-lookup"><span data-stu-id="7e34c-144">operationId</span></span> |<span data-ttu-id="7e34c-145">Hello 해당 하는 이벤트 tooa 단일 작업 간에 공유 하는 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-145">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="7e34c-146">operationName</span><span class="sxs-lookup"><span data-stu-id="7e34c-146">operationName</span></span> |<span data-ttu-id="7e34c-147">Hello 작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-147">Name of hello operation.</span></span> |
| <span data-ttu-id="7e34c-148">properties</span><span class="sxs-lookup"><span data-stu-id="7e34c-148">properties</span></span> |<span data-ttu-id="7e34c-149">설정 `<Key, Value>` hello 이벤트의 hello 세부 정보를 설명 하는 쌍 (즉, 사전).</span><span class="sxs-lookup"><span data-stu-id="7e34c-149">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="7e34c-150">status</span><span class="sxs-lookup"><span data-stu-id="7e34c-150">status</span></span> |<span data-ttu-id="7e34c-151">Hello 연산의 hello 상태를 설명 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-151">String describing hello status of hello operation.</span></span> <span data-ttu-id="7e34c-152">일반적인 값: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="7e34c-152">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="7e34c-153">subStatus</span><span class="sxs-lookup"><span data-stu-id="7e34c-153">subStatus</span></span> |<span data-ttu-id="7e34c-154">Hello hello 해당 REST 호출의 HTTP 상태 코드는 일반적으로 있지만 이러한 공통 값과 같은 하위 상태를 설명 하는 다른 문자열을 포함할 수도 있습니다: 확인 (HTTP 상태 코드: 200) 작성 (HTTP 상태 코드: 201) 허용 되는, (HTTP 상태 코드: 202), 아니요 콘텐츠 (HTTP 상태 코드: 204), 잘못 된 요청 (HTTP 상태 코드: 400), 찾을 수 없음 (HTTP 상태 코드: 404), 충돌 (HTTP 상태 코드: 409), 내부 서버 오류 (HTTP 상태 코드: 500), 서비스 사용할 수 없음 (HTTP 상태 코드: 503), 게이트웨이 시간 초과 (HTTP 상태 코드: 504).</span><span class="sxs-lookup"><span data-stu-id="7e34c-154">Usually hello HTTP status code of hello corresponding REST call, but can also include other strings describing a substatus, such as these common values: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504).</span></span> |
| <span data-ttu-id="7e34c-155">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="7e34c-155">eventTimestamp</span></span> |<span data-ttu-id="7e34c-156">Hello Azure 서비스 처리 hello에서 hello 이벤트가 생성 된 시점의 타임 스탬프는 해당 하는 hello 이벤트를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-156">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="7e34c-157">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="7e34c-157">submissionTimestamp</span></span> |<span data-ttu-id="7e34c-158">Hello 이벤트를 쿼리 하기 위해 사용할 수 있게 하는 경우 타임 스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-158">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="7e34c-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7e34c-159">subscriptionId</span></span> |<span data-ttu-id="7e34c-160">Azure 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-160">Azure Subscription Id.</span></span> |

## <a name="service-health"></a><span data-ttu-id="7e34c-161">서비스 상태</span><span class="sxs-lookup"><span data-stu-id="7e34c-161">Service health</span></span>
<span data-ttu-id="7e34c-162">이 범주에는 Azure에서 발생 한 모든 서비스 상태 문제의 hello 레코드에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-162">This category contains hello record of any service health incidents that have occurred in Azure.</span></span> <span data-ttu-id="7e34c-163">Hello 유형의이 범주에 표시 되는 이벤트의 예로 "미국 동부에서 SQL Azure 가동 중지 시간이 발생 합니다."</span><span class="sxs-lookup"><span data-stu-id="7e34c-163">An example of hello type of event you would see in this category is "SQL Azure in East US is experiencing downtime."</span></span> <span data-ttu-id="7e34c-164">서비스 상태 이벤트를 가져오는 다섯 가지 종류의: 필요한 작업, 복구 지원, 인시던트, 유지 관리, 정보 또는 보안을 hello 이벤트에 의해 영향을 받게 hello 구독에는 리소스를 사용할 경우에 표시 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-164">Service health events come in five varieties: Action Required, Assisted Recovery, Incident, Maintenance, Information, or Security, and only appear if you have a resource in hello subscription that would be impacted by hello event.</span></span>

### <a name="sample-event"></a><span data-ttu-id="7e34c-165">샘플 이벤트</span><span class="sxs-lookup"><span data-stu-id="7e34c-165">Sample event</span></span>
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
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a><span data-ttu-id="7e34c-166">속성 설명</span><span class="sxs-lookup"><span data-stu-id="7e34c-166">Property descriptions</span></span>
<span data-ttu-id="7e34c-167">요소 이름</span><span class="sxs-lookup"><span data-stu-id="7e34c-167">Element Name</span></span> | <span data-ttu-id="7e34c-168">설명</span><span class="sxs-lookup"><span data-stu-id="7e34c-168">Description</span></span>
-------- | -----------
<span data-ttu-id="7e34c-169">channels</span><span class="sxs-lookup"><span data-stu-id="7e34c-169">channels</span></span> | <span data-ttu-id="7e34c-170">Hello 다음 값 중 하나: "Admin", "작업이"</span><span class="sxs-lookup"><span data-stu-id="7e34c-170">Is one of hello following values: “Admin”, “Operation”</span></span>
<span data-ttu-id="7e34c-171">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="7e34c-171">correlationId</span></span> | <span data-ttu-id="7e34c-172">일반적으로 hello 문자열 형식의 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-172">Is usually a GUID in hello string format.</span></span> <span data-ttu-id="7e34c-173">같은 uber 작업 대개 공유 toohello 속하는 이벤트는 같은 correlationId hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-173">Events with that belong toohello same uber action usually share hello same correlationId.</span></span>
<span data-ttu-id="7e34c-174">설명</span><span class="sxs-lookup"><span data-stu-id="7e34c-174">description</span></span> | <span data-ttu-id="7e34c-175">Hello 이벤트의 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-175">Description of hello event.</span></span>
<span data-ttu-id="7e34c-176">eventDataId</span><span class="sxs-lookup"><span data-stu-id="7e34c-176">eventDataId</span></span> | <span data-ttu-id="7e34c-177">hello 이벤트의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-177">hello unique identifier of an event.</span></span>
<span data-ttu-id="7e34c-178">eventName</span><span class="sxs-lookup"><span data-stu-id="7e34c-178">eventName</span></span> | <span data-ttu-id="7e34c-179">hello 제목 hello 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-179">hello title of hello event.</span></span>
<span data-ttu-id="7e34c-180">level</span><span class="sxs-lookup"><span data-stu-id="7e34c-180">level</span></span> | <span data-ttu-id="7e34c-181">Hello 이벤트의 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-181">Level of hello event.</span></span> <span data-ttu-id="7e34c-182">Hello 다음 값 중 하나: "Critical", "Error", "Warning", "Informational" 및 "Verbose"</span><span class="sxs-lookup"><span data-stu-id="7e34c-182">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span>
<span data-ttu-id="7e34c-183">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="7e34c-183">resourceProviderName</span></span> | <span data-ttu-id="7e34c-184">리소스의 영향을 hello에 대 한 hello 리소스 공급자의 이름.</span><span class="sxs-lookup"><span data-stu-id="7e34c-184">Name of hello resource provider for hello impacted resource.</span></span> <span data-ttu-id="7e34c-185">알 수 없는 경우 null로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-185">If not known, this will be null.</span></span>
<span data-ttu-id="7e34c-186">resourceType</span><span class="sxs-lookup"><span data-stu-id="7e34c-186">resourceType</span></span>| <span data-ttu-id="7e34c-187">hello hello의 리소스 유형의 리소스를 저하 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-187">hello type of resource of hello impacted resource.</span></span> <span data-ttu-id="7e34c-188">알 수 없는 경우 null로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-188">If not known, this will be null.</span></span>
<span data-ttu-id="7e34c-189">subStatus</span><span class="sxs-lookup"><span data-stu-id="7e34c-189">subStatus</span></span> | <span data-ttu-id="7e34c-190">서비스 상태 이벤트의 경우 대개 null입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-190">Usually null for Service Health events.</span></span>
<span data-ttu-id="7e34c-191">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="7e34c-191">eventTimestamp</span></span> | <span data-ttu-id="7e34c-192">Hello 로그 이벤트를 생성 되었고 toohello 활동 로그를 전송 하는 경우 타임 스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-192">Timestamp when hello log event was generated and submitted toohello Activity Log.</span></span>
<span data-ttu-id="7e34c-193">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="7e34c-193">submissionTimestamp</span></span> |   <span data-ttu-id="7e34c-194">Hello 활동 로그에서에서 제공 된 hello 이벤트 타임 스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-194">Timestamp when hello event became available in hello Activity Log.</span></span>
<span data-ttu-id="7e34c-195">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7e34c-195">subscriptionId</span></span> | <span data-ttu-id="7e34c-196">이 이벤트가 기록 되는 Azure 구독을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-196">hello Azure subscription in which this event was logged.</span></span>
<span data-ttu-id="7e34c-197">status</span><span class="sxs-lookup"><span data-stu-id="7e34c-197">status</span></span> | <span data-ttu-id="7e34c-198">Hello 연산의 hello 상태를 설명 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-198">String describing hello status of hello operation.</span></span> <span data-ttu-id="7e34c-199">일반적인 값으로는 Active, Resolved 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-199">Some common values are: Active, Resolved.</span></span>
<span data-ttu-id="7e34c-200">operationName</span><span class="sxs-lookup"><span data-stu-id="7e34c-200">operationName</span></span> | <span data-ttu-id="7e34c-201">Hello 작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-201">Name of hello operation.</span></span> <span data-ttu-id="7e34c-202">보통 Microsoft.ServiceHealth/incident/action입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-202">Usually Microsoft.ServiceHealth/incident/action.</span></span>
<span data-ttu-id="7e34c-203">카테고리</span><span class="sxs-lookup"><span data-stu-id="7e34c-203">category</span></span> | <span data-ttu-id="7e34c-204">"ServiceHealth"</span><span class="sxs-lookup"><span data-stu-id="7e34c-204">"ServiceHealth"</span></span>
<span data-ttu-id="7e34c-205">resourceId</span><span class="sxs-lookup"><span data-stu-id="7e34c-205">resourceId</span></span> | <span data-ttu-id="7e34c-206">Hello의 리소스 id의 리소스에 영향을 알 수 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="7e34c-206">Resource id of hello impacted resource, if known.</span></span> <span data-ttu-id="7e34c-207">확인되지 않은 경우에는 구독 ID가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-207">Subscription ID is provided otherwise.</span></span>
<span data-ttu-id="7e34c-208">Properties.title</span><span class="sxs-lookup"><span data-stu-id="7e34c-208">Properties.title</span></span> | <span data-ttu-id="7e34c-209">이 통신에 대 한 hello 지역화 된 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-209">hello localized title for this communication.</span></span> <span data-ttu-id="7e34c-210">영어는 hello 기본 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-210">English is hello default language.</span></span>
<span data-ttu-id="7e34c-211">Properties.communication</span><span class="sxs-lookup"><span data-stu-id="7e34c-211">Properties.communication</span></span> | <span data-ttu-id="7e34c-212">hello는 hello 통신할 때 HTML 태그의 세부 정보를 지역화 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-212">hello localized details of hello communication with HTML markup.</span></span> <span data-ttu-id="7e34c-213">영어는 hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-213">English is hello default.</span></span>
<span data-ttu-id="7e34c-214">Properties.incidentType</span><span class="sxs-lookup"><span data-stu-id="7e34c-214">Properties.incidentType</span></span> | <span data-ttu-id="7e34c-215">가능한 값: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span><span class="sxs-lookup"><span data-stu-id="7e34c-215">Possible values: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span></span>
<span data-ttu-id="7e34c-216">Properties.trackingId</span><span class="sxs-lookup"><span data-stu-id="7e34c-216">Properties.trackingId</span></span> | <span data-ttu-id="7e34c-217">이 이벤트와 연결 된 hello 인시던트를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-217">Identifies hello incident this event is associated with.</span></span> <span data-ttu-id="7e34c-218">이 toocorrelate hello 이벤트 관련된 tooan 인시던트에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-218">Use this toocorrelate hello events related tooan incident.</span></span>
<span data-ttu-id="7e34c-219">Properties.impactedServices</span><span class="sxs-lookup"><span data-stu-id="7e34c-219">Properties.impactedServices</span></span> | <span data-ttu-id="7e34c-220">Hello 서비스 및 hello 인시던트의 영향을 미치는 영역을 설명 하는 이스케이프 된 JSON blob입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-220">An escaped JSON blob which describes hello services and regions that are impacted by hello incident.</span></span> <span data-ttu-id="7e34c-221">각각 ServiceName과 ImpactedRegions 목록을 포함하는 서비스 목록으로, 각 ImpactedRegions에는 RegionName이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-221">A list of Services, each of which has a ServiceName and a list of ImpactedRegions, each of which has a RegionName.</span></span>
<span data-ttu-id="7e34c-222">Properties.defaultLanguageTitle</span><span class="sxs-lookup"><span data-stu-id="7e34c-222">Properties.defaultLanguageTitle</span></span> | <span data-ttu-id="7e34c-223">영어로 hello 통신</span><span class="sxs-lookup"><span data-stu-id="7e34c-223">hello communication in English</span></span>
<span data-ttu-id="7e34c-224">Properties.defaultLanguageContent</span><span class="sxs-lookup"><span data-stu-id="7e34c-224">Properties.defaultLanguageContent</span></span> | <span data-ttu-id="7e34c-225">html 태그 또는 일반 텍스트 영어로 hello 통신</span><span class="sxs-lookup"><span data-stu-id="7e34c-225">hello communication in English as either html markup or plain text</span></span>
<span data-ttu-id="7e34c-226">Properties.stage</span><span class="sxs-lookup"><span data-stu-id="7e34c-226">Properties.stage</span></span> | <span data-ttu-id="7e34c-227">AssistedRecovery, ActionRequired, Information, Incident, Security에 대해 가능한 값: Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="7e34c-227">Possible values for AssistedRecovery, ActionRequired, Information, Incident, Security: are Active, Resolved.</span></span> <span data-ttu-id="7e34c-228">Maintenance에 대해 가능한 값: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete</span><span class="sxs-lookup"><span data-stu-id="7e34c-228">For Maintenance they are: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete</span></span>
<span data-ttu-id="7e34c-229">Properties.communicationId</span><span class="sxs-lookup"><span data-stu-id="7e34c-229">Properties.communicationId</span></span> | <span data-ttu-id="7e34c-230">이 이벤트는 연결 된 hello 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-230">hello communication this event is associated.</span></span>

## <a name="alert"></a><span data-ttu-id="7e34c-231">경고</span><span class="sxs-lookup"><span data-stu-id="7e34c-231">Alert</span></span>
<span data-ttu-id="7e34c-232">이 범주는 hello 레코드의 Azure 경고의 모든 정품 인증을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-232">This category contains hello record of all activations of Azure alerts.</span></span> <span data-ttu-id="7e34c-233">Hello 유형의이 범주에 표시 되는 이벤트의 예로 "CPU (%)에서 myVM은 되었으며 80 hello에 대 한 지난 5 분"</span><span class="sxs-lookup"><span data-stu-id="7e34c-233">An example of hello type of event you would see in this category is "CPU % on myVM has been over 80 for hello past 5 minutes."</span></span> <span data-ttu-id="7e34c-234">다수의 Azure 시스템에서 경고 개념이 사용됩니다. 일종의 규칙을 정의하여 조건이 해당 규칙과 일치하면 알림을 수신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-234">A variety of Azure systems have an alerting concept -- you can define a rule of some sort and receive a notification when conditions match that rule.</span></span> <span data-ttu-id="7e34c-235">될 때마다 지원 되는 Azure 경고 유형 '활성화,' 또는 hello 조건이 충족된 toogenerate 알림을, hello 정품 인증에 대 한 기록을 hello 활동 로그의 toothis 범주 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-235">Each time a supported Azure alert type 'activates,' or hello conditions are met toogenerate a notification, a record of hello activation is also pushed toothis category of hello Activity Log.</span></span>

### <a name="sample-event"></a><span data-ttu-id="7e34c-236">샘플 이벤트</span><span class="sxs-lookup"><span data-stu-id="7e34c-236">Sample event</span></span>

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in hello last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
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

### <a name="property-descriptions"></a><span data-ttu-id="7e34c-237">속성 설명</span><span class="sxs-lookup"><span data-stu-id="7e34c-237">Property descriptions</span></span>
| <span data-ttu-id="7e34c-238">요소 이름</span><span class="sxs-lookup"><span data-stu-id="7e34c-238">Element Name</span></span> | <span data-ttu-id="7e34c-239">설명</span><span class="sxs-lookup"><span data-stu-id="7e34c-239">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7e34c-240">caller</span><span class="sxs-lookup"><span data-stu-id="7e34c-240">caller</span></span> | <span data-ttu-id="7e34c-241">Always Microsoft.Insights/alertRules</span><span class="sxs-lookup"><span data-stu-id="7e34c-241">Always Microsoft.Insights/alertRules</span></span> |
| <span data-ttu-id="7e34c-242">channels</span><span class="sxs-lookup"><span data-stu-id="7e34c-242">channels</span></span> | <span data-ttu-id="7e34c-243">항상 "Admin, Operation"입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-243">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="7e34c-244">claims</span><span class="sxs-lookup"><span data-stu-id="7e34c-244">claims</span></span> | <span data-ttu-id="7e34c-245">Hello SPN (서비스 사용자 이름) 또는 리소스에 대 한 형식의 hello 경고 엔진이 사용 하 여 JSON blob입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-245">JSON blob with hello SPN (service principal name), or resource type, of hello alert engine.</span></span> |
| <span data-ttu-id="7e34c-246">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="7e34c-246">correlationId</span></span> | <span data-ttu-id="7e34c-247">Hello 문자열 형식의 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-247">A GUID in hello string format.</span></span> |
| <span data-ttu-id="7e34c-248">설명</span><span class="sxs-lookup"><span data-stu-id="7e34c-248">description</span></span> |<span data-ttu-id="7e34c-249">Hello 경고 이벤트의 정적 텍스트 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-249">Static text description of hello alert event.</span></span> |
| <span data-ttu-id="7e34c-250">eventDataId</span><span class="sxs-lookup"><span data-stu-id="7e34c-250">eventDataId</span></span> |<span data-ttu-id="7e34c-251">Hello 경고 이벤트의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-251">Unique identifier of hello alert event.</span></span> |
| <span data-ttu-id="7e34c-252">level</span><span class="sxs-lookup"><span data-stu-id="7e34c-252">level</span></span> |<span data-ttu-id="7e34c-253">Hello 이벤트의 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-253">Level of hello event.</span></span> <span data-ttu-id="7e34c-254">Hello 다음 값 중 하나: "Critical", "Error", "Warning", "Informational" 및 "Verbose"</span><span class="sxs-lookup"><span data-stu-id="7e34c-254">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="7e34c-255">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="7e34c-255">resourceGroupName</span></span> |<span data-ttu-id="7e34c-256">Hello에 대 한 hello 리소스 그룹의 이름을 메트릭 경고 이면 리소스는 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-256">Name of hello resource group for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="7e34c-257">다른 경고 유형에 대 한 자체 hello 경고가 포함 된 hello 리소스 그룹의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-257">For other alert types, this is hello name of hello resource group that contains hello alert itself.</span></span> |
| <span data-ttu-id="7e34c-258">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="7e34c-258">resourceProviderName</span></span> |<span data-ttu-id="7e34c-259">Hello에 대 한 hello 리소스 공급자의 이름 메트릭 경고 이면 리소스는 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-259">Name of hello resource provider for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="7e34c-260">다른 경고 유형에 대 한 자체 hello 경고에 대 한 hello 리소스 공급자의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-260">For other alert types, this is hello name of hello resource provider for hello alert itself.</span></span> |
| <span data-ttu-id="7e34c-261">resourceId</span><span class="sxs-lookup"><span data-stu-id="7e34c-261">resourceId</span></span> | <span data-ttu-id="7e34c-262">Hello에 대 한 hello 리소스 ID의 이름 메트릭 경고 이면 리소스는 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-262">Name of hello resource ID for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="7e34c-263">다른 경고 유형에 대 한 hello 경고 리소스 자체의 hello 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-263">For other alert types, this is hello resource ID of hello alert resource itself.</span></span> |
| <span data-ttu-id="7e34c-264">operationId</span><span class="sxs-lookup"><span data-stu-id="7e34c-264">operationId</span></span> |<span data-ttu-id="7e34c-265">Hello 해당 하는 이벤트 tooa 단일 작업 간에 공유 하는 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-265">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="7e34c-266">operationName</span><span class="sxs-lookup"><span data-stu-id="7e34c-266">operationName</span></span> |<span data-ttu-id="7e34c-267">Hello 작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-267">Name of hello operation.</span></span> |
| <span data-ttu-id="7e34c-268">properties</span><span class="sxs-lookup"><span data-stu-id="7e34c-268">properties</span></span> |<span data-ttu-id="7e34c-269">설정 `<Key, Value>` hello 이벤트의 hello 세부 정보를 설명 하는 쌍 (즉, 사전).</span><span class="sxs-lookup"><span data-stu-id="7e34c-269">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="7e34c-270">status</span><span class="sxs-lookup"><span data-stu-id="7e34c-270">status</span></span> |<span data-ttu-id="7e34c-271">Hello 연산의 hello 상태를 설명 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-271">String describing hello status of hello operation.</span></span> <span data-ttu-id="7e34c-272">일반적인 값: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="7e34c-272">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="7e34c-273">subStatus</span><span class="sxs-lookup"><span data-stu-id="7e34c-273">subStatus</span></span> | <span data-ttu-id="7e34c-274">경고의 경우 대개 null입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-274">Usually null for alerts.</span></span> |
| <span data-ttu-id="7e34c-275">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="7e34c-275">eventTimestamp</span></span> |<span data-ttu-id="7e34c-276">Hello Azure 서비스 처리 hello에서 hello 이벤트가 생성 된 시점의 타임 스탬프는 해당 하는 hello 이벤트를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-276">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="7e34c-277">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="7e34c-277">submissionTimestamp</span></span> |<span data-ttu-id="7e34c-278">Hello 이벤트를 쿼리 하기 위해 사용할 수 있게 하는 경우 타임 스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-278">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="7e34c-279">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7e34c-279">subscriptionId</span></span> |<span data-ttu-id="7e34c-280">Azure 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-280">Azure Subscription Id.</span></span> |

### <a name="properties-field-per-alert-type"></a><span data-ttu-id="7e34c-281">경고 유형별 속성 필드</span><span class="sxs-lookup"><span data-stu-id="7e34c-281">Properties field per alert type</span></span>
<span data-ttu-id="7e34c-282">hello 속성 필드 hello 경고 이벤트의 hello 소스에 따라 다른 값이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-282">hello properties field will contain different values depending on hello source of hello alert event.</span></span> <span data-ttu-id="7e34c-283">일반적으로 사용되는 두 경고 이벤트 공급자는 활동 로그 경고와 메트릭 경고입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-283">Two common alert event providers are Activity Log alerts and metric alerts.</span></span>

#### <a name="properties-for-activity-log-alerts"></a><span data-ttu-id="7e34c-284">활동 로그 경고의 속성</span><span class="sxs-lookup"><span data-stu-id="7e34c-284">Properties for Activity Log alerts</span></span>
| <span data-ttu-id="7e34c-285">요소 이름</span><span class="sxs-lookup"><span data-stu-id="7e34c-285">Element Name</span></span> | <span data-ttu-id="7e34c-286">설명</span><span class="sxs-lookup"><span data-stu-id="7e34c-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7e34c-287">properties.subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7e34c-287">properties.subscriptionId</span></span> | <span data-ttu-id="7e34c-288">hello 활성화이 활동 로그 경고 규칙 toobe를 일으킨 hello 활동 로그 이벤트를 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-288">hello subscription ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="7e34c-289">properties.eventDataId</span><span class="sxs-lookup"><span data-stu-id="7e34c-289">properties.eventDataId</span></span> | <span data-ttu-id="7e34c-290">활성화 되는이 활동 로그 경고 규칙 toobe를 일으킨 hello 활동 로그 이벤트에서 hello 이벤트 데이터 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-290">hello event data ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="7e34c-291">properties.resourceGroup</span><span class="sxs-lookup"><span data-stu-id="7e34c-291">properties.resourceGroup</span></span> | <span data-ttu-id="7e34c-292">hello 리소스 그룹에서 활성화 되는이 활동 로그 경고 규칙 toobe를 일으킨 hello 활동 로그 이벤트.</span><span class="sxs-lookup"><span data-stu-id="7e34c-292">hello resource group from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="7e34c-293">properties.resourceId</span><span class="sxs-lookup"><span data-stu-id="7e34c-293">properties.resourceId</span></span> | <span data-ttu-id="7e34c-294">활성화 되는이 활동 로그 경고 규칙 toobe를 일으킨 hello 활동 로그 이벤트에서 hello 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-294">hello resource ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="7e34c-295">properties.eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="7e34c-295">properties.eventTimestamp</span></span> | <span data-ttu-id="7e34c-296">활성화 되는이 활동 로그 경고 규칙 toobe를 일으킨 hello 활동 로그 이벤트의 hello 이벤트 타임 스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-296">hello event timestamp of hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="7e34c-297">properties.operationName</span><span class="sxs-lookup"><span data-stu-id="7e34c-297">properties.operationName</span></span> | <span data-ttu-id="7e34c-298">활성화 되는이 활동 로그 경고 규칙 toobe를 일으킨 hello 활동 로그 이벤트 hello 작업 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-298">hello operation name from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="7e34c-299">properties.status</span><span class="sxs-lookup"><span data-stu-id="7e34c-299">properties.status</span></span> | <span data-ttu-id="7e34c-300">활성화 되는이 활동 로그 경고 규칙 toobe를 일으킨 hello 활동 로그 이벤트에서 hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-300">hello status from hello activity log event which caused this activity log alert rule toobe activated.</span></span>|

#### <a name="properties-for-metric-alerts"></a><span data-ttu-id="7e34c-301">메트릭 경고의 속성</span><span class="sxs-lookup"><span data-stu-id="7e34c-301">Properties for metric alerts</span></span>
| <span data-ttu-id="7e34c-302">요소 이름</span><span class="sxs-lookup"><span data-stu-id="7e34c-302">Element Name</span></span> | <span data-ttu-id="7e34c-303">설명</span><span class="sxs-lookup"><span data-stu-id="7e34c-303">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7e34c-304">properties.RuleUri</span><span class="sxs-lookup"><span data-stu-id="7e34c-304">properties.RuleUri</span></span> | <span data-ttu-id="7e34c-305">Hello 메트릭 경고 규칙 자체의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-305">Resource ID of hello metric alert rule itself.</span></span> |
| <span data-ttu-id="7e34c-306">properties.RuleName</span><span class="sxs-lookup"><span data-stu-id="7e34c-306">properties.RuleName</span></span> | <span data-ttu-id="7e34c-307">hello 메트릭 경고 규칙의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-307">hello name of hello metric alert rule.</span></span> |
| <span data-ttu-id="7e34c-308">properties.RuleDescription</span><span class="sxs-lookup"><span data-stu-id="7e34c-308">properties.RuleDescription</span></span> | <span data-ttu-id="7e34c-309">hello 경고 규칙에 정의 된) (대로 hello 메트릭 경고 규칙의 hello 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-309">hello description of hello metric alert rule (as defined in hello alert rule).</span></span> |
| <span data-ttu-id="7e34c-310">properties.Threshold</span><span class="sxs-lookup"><span data-stu-id="7e34c-310">properties.Threshold</span></span> | <span data-ttu-id="7e34c-311">hello 임계값 hello 메트릭 경고 규칙의 hello 평가에 사용 된입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-311">hello threshold value used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="7e34c-312">properties.WindowSizeInMinutes</span><span class="sxs-lookup"><span data-stu-id="7e34c-312">properties.WindowSizeInMinutes</span></span> | <span data-ttu-id="7e34c-313">hello 메트릭 경고 규칙의 hello 평가에 사용 된 hello 창 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-313">hello window size used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="7e34c-314">properties.Aggregation</span><span class="sxs-lookup"><span data-stu-id="7e34c-314">properties.Aggregation</span></span> | <span data-ttu-id="7e34c-315">hello 메트릭 경고 규칙에 정의 된 hello 집계 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-315">hello aggregation type defined in hello metric alert rule.</span></span> |
| <span data-ttu-id="7e34c-316">properties.Operator</span><span class="sxs-lookup"><span data-stu-id="7e34c-316">properties.Operator</span></span> | <span data-ttu-id="7e34c-317">hello 메트릭 경고 규칙의 hello 평가에 사용 된 hello 조건부 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-317">hello conditional operator used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="7e34c-318">properties.MetricName</span><span class="sxs-lookup"><span data-stu-id="7e34c-318">properties.MetricName</span></span> | <span data-ttu-id="7e34c-319">hello hello 메트릭 경고 규칙의 hello 평가에 사용 된 hello 메트릭의 메트릭 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-319">hello metric name of hello metric used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="7e34c-320">properties.MetricUnit</span><span class="sxs-lookup"><span data-stu-id="7e34c-320">properties.MetricUnit</span></span> | <span data-ttu-id="7e34c-321">hello hello 메트릭 경고 규칙의 hello 평가에 사용 된 hello 메트릭의 메트릭 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-321">hello metric unit for hello metric used in hello evaluation of hello metric alert rule.</span></span> |

## <a name="autoscale"></a><span data-ttu-id="7e34c-322">Autoscale</span><span class="sxs-lookup"><span data-stu-id="7e34c-322">Autoscale</span></span>
<span data-ttu-id="7e34c-323">이 범주에는 구독에 정의 된 자동 크기 조정 설정에 따라 hello 자동 크기 조정 엔진의 모든 이벤트 관련된 toohello 연산의 hello 레코드에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-323">This category contains hello record of any events related toohello operation of hello autoscale engine based on any autoscale settings you have defined in your subscription.</span></span> <span data-ttu-id="7e34c-324">Hello 유형의이 범주에 표시 되는 이벤트의 예로 "자동 크기 조정 수직 확장 작업이 실패 했습니다.."</span><span class="sxs-lookup"><span data-stu-id="7e34c-324">An example of hello type of event you would see in this category is "Autoscale scale up action failed."</span></span> <span data-ttu-id="7e34c-325">자동 크기 조정을 사용 하 여 자동으로 확장 하거나 수의 크기를 조정 hello는 지원 되는 리소스 형식에 있는 인스턴스의 수는 자동 크기 조정 설정을 사용 하 여 날짜 및/또는 부하 (메트릭) 데이터는 시간에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-325">Using autoscale, you can automatically scale out or scale in hello number of instances in a supported resource type based on time of day and/or load (metric) data using an autoscale setting.</span></span> <span data-ttu-id="7e34c-326">Hello 조건이 충족 되 면 tooscale 위나 아래로 시작 hello 및 성공 또는 실패 한 이벤트는이 범주에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-326">When hello conditions are met tooscale up or down, hello start and succeeded or failed events will be recorded in this category.</span></span>

### <a name="sample-event"></a><span data-ttu-id="7e34c-327">샘플 이벤트</span><span class="sxs-lookup"><span data-stu-id="7e34c-327">Sample event</span></span>
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
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
    "Description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
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

### <a name="property-descriptions"></a><span data-ttu-id="7e34c-328">속성 설명</span><span class="sxs-lookup"><span data-stu-id="7e34c-328">Property descriptions</span></span>
| <span data-ttu-id="7e34c-329">요소 이름</span><span class="sxs-lookup"><span data-stu-id="7e34c-329">Element Name</span></span> | <span data-ttu-id="7e34c-330">설명</span><span class="sxs-lookup"><span data-stu-id="7e34c-330">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7e34c-331">caller</span><span class="sxs-lookup"><span data-stu-id="7e34c-331">caller</span></span> | <span data-ttu-id="7e34c-332">항상 Microsoft.Insights/autoscaleSettings입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-332">Always Microsoft.Insights/autoscaleSettings</span></span> |
| <span data-ttu-id="7e34c-333">channels</span><span class="sxs-lookup"><span data-stu-id="7e34c-333">channels</span></span> | <span data-ttu-id="7e34c-334">항상 "Admin, Operation"입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-334">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="7e34c-335">claims</span><span class="sxs-lookup"><span data-stu-id="7e34c-335">claims</span></span> | <span data-ttu-id="7e34c-336">Hello hello 자동 크기 조정 엔진의 SPN (서비스 사용자 이름) 또는 리소스 유형 사용 하 여 JSON blob입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-336">JSON blob with hello SPN (service principal name), or resource type, of hello autoscale engine.</span></span> |
| <span data-ttu-id="7e34c-337">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="7e34c-337">correlationId</span></span> | <span data-ttu-id="7e34c-338">Hello 문자열 형식의 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-338">A GUID in hello string format.</span></span> |
| <span data-ttu-id="7e34c-339">설명</span><span class="sxs-lookup"><span data-stu-id="7e34c-339">description</span></span> |<span data-ttu-id="7e34c-340">Hello 자동 크기 조정 이벤트의 정적 텍스트 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-340">Static text description of hello autoscale event.</span></span> |
| <span data-ttu-id="7e34c-341">eventDataId</span><span class="sxs-lookup"><span data-stu-id="7e34c-341">eventDataId</span></span> |<span data-ttu-id="7e34c-342">Hello 자동 크기 조정 이벤트의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-342">Unique identifier of hello autoscale event.</span></span> |
| <span data-ttu-id="7e34c-343">level</span><span class="sxs-lookup"><span data-stu-id="7e34c-343">level</span></span> |<span data-ttu-id="7e34c-344">Hello 이벤트의 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-344">Level of hello event.</span></span> <span data-ttu-id="7e34c-345">Hello 다음 값 중 하나: "Critical", "Error", "Warning", "Informational" 및 "Verbose"</span><span class="sxs-lookup"><span data-stu-id="7e34c-345">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="7e34c-346">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="7e34c-346">resourceGroupName</span></span> |<span data-ttu-id="7e34c-347">Hello 자동 크기 조정 설정에 대 한 hello 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-347">Name of hello resource group for hello autoscale setting.</span></span> |
| <span data-ttu-id="7e34c-348">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="7e34c-348">resourceProviderName</span></span> |<span data-ttu-id="7e34c-349">Hello 자동 크기 조정 설정에 대 한 hello 리소스 공급자의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-349">Name of hello resource provider for hello autoscale setting.</span></span> |
| <span data-ttu-id="7e34c-350">resourceId</span><span class="sxs-lookup"><span data-stu-id="7e34c-350">resourceId</span></span> |<span data-ttu-id="7e34c-351">Hello 자동 크기 조정 설정의 리소스 id입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-351">Resource id of hello autoscale setting.</span></span> |
| <span data-ttu-id="7e34c-352">operationId</span><span class="sxs-lookup"><span data-stu-id="7e34c-352">operationId</span></span> |<span data-ttu-id="7e34c-353">Hello 해당 하는 이벤트 tooa 단일 작업 간에 공유 하는 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-353">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="7e34c-354">operationName</span><span class="sxs-lookup"><span data-stu-id="7e34c-354">operationName</span></span> |<span data-ttu-id="7e34c-355">Hello 작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-355">Name of hello operation.</span></span> |
| <span data-ttu-id="7e34c-356">properties</span><span class="sxs-lookup"><span data-stu-id="7e34c-356">properties</span></span> |<span data-ttu-id="7e34c-357">설정 `<Key, Value>` hello 이벤트의 hello 세부 정보를 설명 하는 쌍 (즉, 사전).</span><span class="sxs-lookup"><span data-stu-id="7e34c-357">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="7e34c-358">properties.Description</span><span class="sxs-lookup"><span data-stu-id="7e34c-358">properties.Description</span></span> | <span data-ttu-id="7e34c-359">어떤 hello 자동 크기 조정 엔진에 수행 되 던의 자세한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-359">Detailed description of what hello autoscale engine was doing.</span></span> |
| <span data-ttu-id="7e34c-360">properties.ResourceName</span><span class="sxs-lookup"><span data-stu-id="7e34c-360">properties.ResourceName</span></span> | <span data-ttu-id="7e34c-361">리소스의 영향을 hello의 리소스 ID (리소스 크기 조정 작업이 수행 되 고 있는 hello에 hello)</span><span class="sxs-lookup"><span data-stu-id="7e34c-361">Resource ID of hello impacted resource (hello resource on which hello scale action was being performed)</span></span> |
| <span data-ttu-id="7e34c-362">properties.OldInstancesCount</span><span class="sxs-lookup"><span data-stu-id="7e34c-362">properties.OldInstancesCount</span></span> | <span data-ttu-id="7e34c-363">hello hello 자동 크기 조정 작업 전에 인스턴스 수에 적용이 될 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-363">hello number of instances before hello autoscale action took effect.</span></span> |
| <span data-ttu-id="7e34c-364">properties.NewInstancesCount</span><span class="sxs-lookup"><span data-stu-id="7e34c-364">properties.NewInstancesCount</span></span> | <span data-ttu-id="7e34c-365">hello 자동 크기 조정 작업에 적용 될 후 인스턴스의 hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-365">hello number of instances after hello autoscale action took effect.</span></span> |
| <span data-ttu-id="7e34c-366">properties.LastScaleActionTime</span><span class="sxs-lookup"><span data-stu-id="7e34c-366">properties.LastScaleActionTime</span></span> | <span data-ttu-id="7e34c-367">hello 자동 크기 조정 작업이 발생 했을 때의 타임 스탬프를 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-367">hello timestamp of when hello autoscale action occurred.</span></span> |
| <span data-ttu-id="7e34c-368">status</span><span class="sxs-lookup"><span data-stu-id="7e34c-368">status</span></span> |<span data-ttu-id="7e34c-369">Hello 연산의 hello 상태를 설명 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-369">String describing hello status of hello operation.</span></span> <span data-ttu-id="7e34c-370">일반적인 값: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="7e34c-370">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="7e34c-371">subStatus</span><span class="sxs-lookup"><span data-stu-id="7e34c-371">subStatus</span></span> | <span data-ttu-id="7e34c-372">자동 크기 조정의 경우 대개 null입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-372">Usually null for autoscale.</span></span> |
| <span data-ttu-id="7e34c-373">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="7e34c-373">eventTimestamp</span></span> |<span data-ttu-id="7e34c-374">Hello Azure 서비스 처리 hello에서 hello 이벤트가 생성 된 시점의 타임 스탬프는 해당 하는 hello 이벤트를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-374">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="7e34c-375">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="7e34c-375">submissionTimestamp</span></span> |<span data-ttu-id="7e34c-376">Hello 이벤트를 쿼리 하기 위해 사용할 수 있게 하는 경우 타임 스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-376">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="7e34c-377">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7e34c-377">subscriptionId</span></span> |<span data-ttu-id="7e34c-378">Azure 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="7e34c-378">Azure Subscription Id.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7e34c-379">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7e34c-379">Next steps</span></span>
* [<span data-ttu-id="7e34c-380">활동 로그 (이전의 감사 로그) hello에 대 한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="7e34c-380">Learn more about hello Activity Log (formerly Audit Logs)</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="7e34c-381">Hello Azure 활동 로그 tooEvent 허브 스트림</span><span class="sxs-lookup"><span data-stu-id="7e34c-381">Stream hello Azure Activity Log tooEvent Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
