---
title: "aaaUse 자동 크기 조정 작업 toosend 전자 메일 및 webhook 경고 알림입니다. | Microsoft Docs"
description: "Toouse 자동 크기 조정 작업 toocall 웹 Url 또는 Azure 모니터에서 전자 메일 알림을 보내는 방법을 참조 하십시오. "
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: eb9a4c98-0894-488c-8ee8-5df0065d094f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: ancav
ms.openlocfilehash: f611a18f5a808412fbdd0c89e3addb36437064c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-autoscale-actions-toosend-email-and-webhook-alert-notifications-in-azure-monitor"></a><span data-ttu-id="21898-104">Azure 모니터에서 자동 크기 조정 작업 toosend 전자 메일 및 webhook 경고 알림 사용</span><span class="sxs-lookup"><span data-stu-id="21898-104">Use autoscale actions toosend email and webhook alert notifications in Azure Monitor</span></span>
<span data-ttu-id="21898-105">이 문서에서는 Azure에서 크기 자동 조정 작업을 기준으로 특정 웹 URL을 호출하거나 전자 메일을 보낼 수 있도록 트리거를 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="21898-105">This article shows you how set up triggers so that you can call specific web URLs or send emails based on autoscale actions in Azure.</span></span>  

## <a name="webhooks"></a><span data-ttu-id="21898-106">Webhook</span><span class="sxs-lookup"><span data-stu-id="21898-106">Webhooks</span></span>
<span data-ttu-id="21898-107">Webhook 사후 처리 또는 사용자 지정 알림을 tooroute hello Azure 경고 알림 tooother 시스템을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="21898-107">Webhooks allow you tooroute hello Azure alert notifications tooother systems for post-processing or custom notifications.</span></span> <span data-ttu-id="21898-108">예를 들어는 들어오는 웹 요청 toosend SMS, 로그 버그를 처리할 수 있는 라우팅 hello 경고 tooservices 팀 채팅을 사용 하 여 또는 메시징 서비스 알림, 등 hello webhook URI는 유효한 HTTP 또는 HTTPS 끝점 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21898-108">For example, routing hello alert tooservices that can handle an incoming web request toosend SMS, log bugs, notify a team using chat or messaging services, etc. hello webhook URI must be a valid HTTP or HTTPS endpoint.</span></span>

## <a name="email"></a><span data-ttu-id="21898-109">Email</span><span class="sxs-lookup"><span data-stu-id="21898-109">Email</span></span>
<span data-ttu-id="21898-110">전자 메일 tooany 유효한 전자 메일 주소를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21898-110">Email can be sent tooany valid email address.</span></span> <span data-ttu-id="21898-111">관리자와 hello 규칙 실행 되 고 있는 hello 구독의 공동 관리자 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21898-111">Administrators and co-administrators of hello subscription where hello rule is running will also be notified.</span></span>

## <a name="cloud-services-and-web-apps"></a><span data-ttu-id="21898-112">클라우드 서비스 및 웹 앱</span><span class="sxs-lookup"><span data-stu-id="21898-112">Cloud Services and Web Apps</span></span>
<span data-ttu-id="21898-113">있습니다 수 옵트인 hello Azure 포털에서에서 클라우드 서비스 및 서버 팜 (웹 앱).</span><span class="sxs-lookup"><span data-stu-id="21898-113">You can opt-in from hello Azure portal for Cloud Services and Server Farms (Web Apps).</span></span>

* <span data-ttu-id="21898-114">Hello 선택 **하 여 확장할** 메트릭.</span><span class="sxs-lookup"><span data-stu-id="21898-114">Choose hello **scale by** metric.</span></span>

![배율 기준](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a><span data-ttu-id="21898-116">가상 컴퓨터 확장 집합</span><span class="sxs-lookup"><span data-stu-id="21898-116">Virtual Machine scale sets</span></span>
<span data-ttu-id="21898-117">Resource Manager(가상 컴퓨터 확장 집합)로 만든 새 가상 컴퓨터의 경우 REST API, Resource Manager 템플릿, PowerShell 및 CLI를 사용하여 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21898-117">For newer Virtual Machines created with Resource Manager (Virtual Machine scale sets), you can configure this using REST API, Resource Manager templates, PowerShell, and CLI.</span></span> <span data-ttu-id="21898-118">포털 인터페이스는 아직 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="21898-118">A portal interface is not yet available.</span></span>
<span data-ttu-id="21898-119">Hello REST API 또는 리소스 관리자 템플릿을 사용 하는 경우 다음 옵션 hello로 hello 알림을 요소를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="21898-119">When using hello REST API or Resource Manager template, include hello notifications element with hello following options.</span></span>

```
"notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": false,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]
```
| <span data-ttu-id="21898-120">필드</span><span class="sxs-lookup"><span data-stu-id="21898-120">Field</span></span> | <span data-ttu-id="21898-121">필수?</span><span class="sxs-lookup"><span data-stu-id="21898-121">Mandatory?</span></span> | <span data-ttu-id="21898-122">설명</span><span class="sxs-lookup"><span data-stu-id="21898-122">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21898-123">operation</span><span class="sxs-lookup"><span data-stu-id="21898-123">operation</span></span> |<span data-ttu-id="21898-124">yes</span><span class="sxs-lookup"><span data-stu-id="21898-124">yes</span></span> |<span data-ttu-id="21898-125">값은 "Scale"이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21898-125">value must be "Scale"</span></span> |
| <span data-ttu-id="21898-126">sendToSubscriptionAdministrator</span><span class="sxs-lookup"><span data-stu-id="21898-126">sendToSubscriptionAdministrator</span></span> |<span data-ttu-id="21898-127">yes</span><span class="sxs-lookup"><span data-stu-id="21898-127">yes</span></span> |<span data-ttu-id="21898-128">값은 "true" 또는 "false"여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21898-128">value must be "true" or "false"</span></span> |
| <span data-ttu-id="21898-129">sendToSubscriptionCoAdministrators</span><span class="sxs-lookup"><span data-stu-id="21898-129">sendToSubscriptionCoAdministrators</span></span> |<span data-ttu-id="21898-130">yes</span><span class="sxs-lookup"><span data-stu-id="21898-130">yes</span></span> |<span data-ttu-id="21898-131">값은 "true" 또는 "false"여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21898-131">value must be "true" or "false"</span></span> |
| <span data-ttu-id="21898-132">customEmails</span><span class="sxs-lookup"><span data-stu-id="21898-132">customEmails</span></span> |<span data-ttu-id="21898-133">yes</span><span class="sxs-lookup"><span data-stu-id="21898-133">yes</span></span> |<span data-ttu-id="21898-134">값에 null [] 또는 전자 메일 문자열 배열을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21898-134">value can be null [] or string array of emails</span></span> |
| <span data-ttu-id="21898-135">Webhook</span><span class="sxs-lookup"><span data-stu-id="21898-135">webhooks</span></span> |<span data-ttu-id="21898-136">yes</span><span class="sxs-lookup"><span data-stu-id="21898-136">yes</span></span> |<span data-ttu-id="21898-137">값은 null이거나 올바른 URI일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21898-137">value can be null or valid Uri</span></span> |
| <span data-ttu-id="21898-138">serviceUri</span><span class="sxs-lookup"><span data-stu-id="21898-138">serviceUri</span></span> |<span data-ttu-id="21898-139">yes</span><span class="sxs-lookup"><span data-stu-id="21898-139">yes</span></span> |<span data-ttu-id="21898-140">유효한 https URI</span><span class="sxs-lookup"><span data-stu-id="21898-140">a valid https Uri</span></span> |
| <span data-ttu-id="21898-141">properties</span><span class="sxs-lookup"><span data-stu-id="21898-141">properties</span></span> |<span data-ttu-id="21898-142">yes</span><span class="sxs-lookup"><span data-stu-id="21898-142">yes</span></span> |<span data-ttu-id="21898-143">값은 비어 있거나{} 키-값 쌍을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21898-143">value must be empty {} or can contain key-value pairs</span></span> |

## <a name="authentication-in-webhooks"></a><span data-ttu-id="21898-144">Webhook의 인증</span><span class="sxs-lookup"><span data-stu-id="21898-144">Authentication in webhooks</span></span>
<span data-ttu-id="21898-145">hello webhook 토큰 기반 인증을 사용 하 여 쿼리 매개 변수로 토큰 ID를 가진 hello webhook URI를 저장할 위치를 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21898-145">hello webhook can authenticate using token-based authentication, where you save hello webhook URI with a token ID as a query parameter.</span></span> <span data-ttu-id="21898-146">예를 들어 https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue입니다.</span><span class="sxs-lookup"><span data-stu-id="21898-146">For example, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span></span>

## <a name="autoscale-notification-webhook-payload-schema"></a><span data-ttu-id="21898-147">크기 자동 조정 알림 Webhook 페이로드 스키마</span><span class="sxs-lookup"><span data-stu-id="21898-147">Autoscale notification webhook payload schema</span></span>
<span data-ttu-id="21898-148">Hello 자동 크기 조정 알림 생성 되 면 hello 다음과 같은 메타 데이터에에서 연결 되어 hello webhook 페이로드:</span><span class="sxs-lookup"><span data-stu-id="21898-148">When hello autoscale notification is generated, hello following metadata is included in hello webhook payload:</span></span>

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' toocapacity '2'",
                "subscriptionId": "s1",
                "resourceGroupName": "rg1",
                "resourceName": "MyCSRole",
                "resourceType": "microsoft.classiccompute/domainnames/slots/roles",
                "resourceId": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService/slots/Production/roles/MyCSRole",
                "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService",
                "oldCapacity": "3",
                "newCapacity": "2"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```


| <span data-ttu-id="21898-149">필드</span><span class="sxs-lookup"><span data-stu-id="21898-149">Field</span></span> | <span data-ttu-id="21898-150">필수?</span><span class="sxs-lookup"><span data-stu-id="21898-150">Mandatory?</span></span> | <span data-ttu-id="21898-151">설명</span><span class="sxs-lookup"><span data-stu-id="21898-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21898-152">status</span><span class="sxs-lookup"><span data-stu-id="21898-152">status</span></span> |<span data-ttu-id="21898-153">yes</span><span class="sxs-lookup"><span data-stu-id="21898-153">yes</span></span> |<span data-ttu-id="21898-154">자동 크기 조정 작업 생성 했음을 나타내는 hello 상태</span><span class="sxs-lookup"><span data-stu-id="21898-154">hello status that indicates that an autoscale action was generated</span></span> |
| <span data-ttu-id="21898-155">operation</span><span class="sxs-lookup"><span data-stu-id="21898-155">operation</span></span> |<span data-ttu-id="21898-156">yes</span><span class="sxs-lookup"><span data-stu-id="21898-156">yes</span></span> |<span data-ttu-id="21898-157">인스턴스가 증가하면 "규모 확장"되고 인스턴스가 감소하면 "규모 감축"됩니다.</span><span class="sxs-lookup"><span data-stu-id="21898-157">For an increase of instances, it will be "Scale Out" and for a decrease in instances, it will be "Scale In"</span></span> |
| <span data-ttu-id="21898-158">context</span><span class="sxs-lookup"><span data-stu-id="21898-158">context</span></span> |<span data-ttu-id="21898-159">yes</span><span class="sxs-lookup"><span data-stu-id="21898-159">yes</span></span> |<span data-ttu-id="21898-160">hello 자동 크기 조정 작업 컨텍스트</span><span class="sxs-lookup"><span data-stu-id="21898-160">hello autoscale action context</span></span> |
| <span data-ttu-id="21898-161">timestamp</span><span class="sxs-lookup"><span data-stu-id="21898-161">timestamp</span></span> |<span data-ttu-id="21898-162">yes</span><span class="sxs-lookup"><span data-stu-id="21898-162">yes</span></span> |<span data-ttu-id="21898-163">Hello 자동 크기 조정 작업 트리거 되었을 때의 타임 스탬프</span><span class="sxs-lookup"><span data-stu-id="21898-163">Time stamp when hello autoscale action was triggered</span></span> |
| <span data-ttu-id="21898-164">id</span><span class="sxs-lookup"><span data-stu-id="21898-164">id</span></span> |<span data-ttu-id="21898-165">예</span><span class="sxs-lookup"><span data-stu-id="21898-165">Yes</span></span> |<span data-ttu-id="21898-166">Hello 자동 크기 조정 설정의 리소스 관리자 ID</span><span class="sxs-lookup"><span data-stu-id="21898-166">Resource Manager ID of hello autoscale setting</span></span> |
| <span data-ttu-id="21898-167">name</span><span class="sxs-lookup"><span data-stu-id="21898-167">name</span></span> |<span data-ttu-id="21898-168">예</span><span class="sxs-lookup"><span data-stu-id="21898-168">Yes</span></span> |<span data-ttu-id="21898-169">hello 자동 크기 조정 설정의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="21898-169">hello name of hello autoscale setting</span></span> |
| <span data-ttu-id="21898-170">세부 정보</span><span class="sxs-lookup"><span data-stu-id="21898-170">details</span></span> |<span data-ttu-id="21898-171">예</span><span class="sxs-lookup"><span data-stu-id="21898-171">Yes</span></span> |<span data-ttu-id="21898-172">자동 크기 조정 서비스 hello hello 동작의 설명에는 적용 하 고 hello hello 인스턴스 수 변경</span><span class="sxs-lookup"><span data-stu-id="21898-172">Explanation of hello action that hello autoscale service took and hello change in hello instance count</span></span> |
| <span data-ttu-id="21898-173">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="21898-173">subscriptionId</span></span> |<span data-ttu-id="21898-174">예</span><span class="sxs-lookup"><span data-stu-id="21898-174">Yes</span></span> |<span data-ttu-id="21898-175">크기가 조정 되는 hello 대상 리소스의 구독 ID</span><span class="sxs-lookup"><span data-stu-id="21898-175">Subscription ID of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="21898-176">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="21898-176">resourceGroupName</span></span> |<span data-ttu-id="21898-177">예</span><span class="sxs-lookup"><span data-stu-id="21898-177">Yes</span></span> |<span data-ttu-id="21898-178">크기가 조정 되는 hello 대상 리소스의 리소스 그룹 이름</span><span class="sxs-lookup"><span data-stu-id="21898-178">Resource Group name of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="21898-179">resourceName</span><span class="sxs-lookup"><span data-stu-id="21898-179">resourceName</span></span> |<span data-ttu-id="21898-180">예</span><span class="sxs-lookup"><span data-stu-id="21898-180">Yes</span></span> |<span data-ttu-id="21898-181">크기가 조정 되는 hello 대상 리소스의 이름</span><span class="sxs-lookup"><span data-stu-id="21898-181">Name of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="21898-182">resourceType</span><span class="sxs-lookup"><span data-stu-id="21898-182">resourceType</span></span> |<span data-ttu-id="21898-183">예</span><span class="sxs-lookup"><span data-stu-id="21898-183">Yes</span></span> |<span data-ttu-id="21898-184">지원 되는 세 가지 값 hello: "microsoft.classiccompute/domainnames/slots/roles"-클라우드 서비스 역할과 가상 컴퓨터 크기 집합 "microsoft.compute/virtualmachinescalesets"-"microsoft.web/serverfarms"-웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="21898-184">hello three supported values: "microsoft.classiccompute/domainnames/slots/roles" - Cloud Service roles, "microsoft.compute/virtualmachinescalesets" - Virtual Machine Scale Sets,  and "Microsoft.Web/serverfarms" - Web App</span></span> |
| <span data-ttu-id="21898-185">resourceId</span><span class="sxs-lookup"><span data-stu-id="21898-185">resourceId</span></span> |<span data-ttu-id="21898-186">예</span><span class="sxs-lookup"><span data-stu-id="21898-186">Yes</span></span> |<span data-ttu-id="21898-187">크기가 조정 되는 hello 대상 리소스의 리소스 관리자 ID</span><span class="sxs-lookup"><span data-stu-id="21898-187">Resource Manager ID of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="21898-188">portalLink</span><span class="sxs-lookup"><span data-stu-id="21898-188">portalLink</span></span> |<span data-ttu-id="21898-189">예</span><span class="sxs-lookup"><span data-stu-id="21898-189">Yes</span></span> |<span data-ttu-id="21898-190">Azure 포털 링크 toohello hello 대상 리소스의 요약 페이지</span><span class="sxs-lookup"><span data-stu-id="21898-190">Azure portal link toohello summary page of hello target resource</span></span> |
| <span data-ttu-id="21898-191">oldCapacity</span><span class="sxs-lookup"><span data-stu-id="21898-191">oldCapacity</span></span> |<span data-ttu-id="21898-192">예</span><span class="sxs-lookup"><span data-stu-id="21898-192">Yes</span></span> |<span data-ttu-id="21898-193">hello 현재 (이전) 인스턴스 수가 자동 크기 조정 크기 조정 작업 시간</span><span class="sxs-lookup"><span data-stu-id="21898-193">hello current (old) instance count when Autoscale took a scale action</span></span> |
| <span data-ttu-id="21898-194">newCapacity</span><span class="sxs-lookup"><span data-stu-id="21898-194">newCapacity</span></span> |<span data-ttu-id="21898-195">예</span><span class="sxs-lookup"><span data-stu-id="21898-195">Yes</span></span> |<span data-ttu-id="21898-196">자동 크기 조정 hello 리소스를 너무 확장 있다는 hello 새 인스턴스 수</span><span class="sxs-lookup"><span data-stu-id="21898-196">hello new instance count that Autoscale scaled hello resource too</span></span>|
| <span data-ttu-id="21898-197">properties</span><span class="sxs-lookup"><span data-stu-id="21898-197">Properties</span></span> |<span data-ttu-id="21898-198">아니요</span><span class="sxs-lookup"><span data-stu-id="21898-198">No</span></span> |<span data-ttu-id="21898-199">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="21898-199">Optional.</span></span> <span data-ttu-id="21898-200"><키, 값> 쌍 집합(예: Dictionary <문자열, 문자열>).</span><span class="sxs-lookup"><span data-stu-id="21898-200">Set of <Key, Value> pairs (for example,  Dictionary <String, String>).</span></span> <span data-ttu-id="21898-201">hello 속성 필드는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="21898-201">hello properties field is optional.</span></span> <span data-ttu-id="21898-202">사용자 지정 사용자 인터페이스 또는 논리 앱 기반 워크플로 hello 페이로드를 사용 하 여 전달할 수 있는 키와 값을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21898-202">In a custom user interface  or Logic app based workflow, you can enter keys and values that can be passed using hello payload.</span></span> <span data-ttu-id="21898-203">사용자 지정 속성 toopass 다시 toohello 보내는 webhook 호출 하는 다른 방법은 것 toouse hello webhook (쿼리 매개 변수)으로 자체 URI</span><span class="sxs-lookup"><span data-stu-id="21898-203">An alternate way toopass custom properties back toohello outgoing webhook call is toouse hello webhook URI itself (as query parameters)</span></span> |
