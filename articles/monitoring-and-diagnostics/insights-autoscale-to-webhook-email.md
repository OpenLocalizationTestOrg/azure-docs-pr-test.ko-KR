---
title: "크기 자동 조정 작업을 사용하여 전자 메일 및 webhook 경고 알림 보내기 | Microsoft Docs"
description: "Azure Monitor에서 크기 자동 조정 작업을 사용하여 웹 URL을 호출하거나 전자 메일을 보내는 방법에 대해 알아봅니다. "
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
ms.openlocfilehash: 16caf14028494800e9259f0296c292b606d0210a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-autoscale-actions-to-send-email-and-webhook-alert-notifications-in-azure-monitor"></a><span data-ttu-id="bd491-104">크기 자동 조정 작업을 사용하여 Azure Monitor에서 전자 메일 및 webhook 경고 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="bd491-104">Use autoscale actions to send email and webhook alert notifications in Azure Monitor</span></span>
<span data-ttu-id="bd491-105">이 문서에서는 Azure에서 크기 자동 조정 작업을 기준으로 특정 웹 URL을 호출하거나 전자 메일을 보낼 수 있도록 트리거를 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-105">This article shows you how set up triggers so that you can call specific web URLs or send emails based on autoscale actions in Azure.</span></span>  

## <a name="webhooks"></a><span data-ttu-id="bd491-106">Webhook</span><span class="sxs-lookup"><span data-stu-id="bd491-106">Webhooks</span></span>
<span data-ttu-id="bd491-107">Webhook를 사용하면 사후 처리 또는 사용자 지정 알림을 위해 Azure 경고 알림을 다른 시스템으로 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-107">Webhooks allow you to route the Azure alert notifications to other systems for post-processing or custom notifications.</span></span> <span data-ttu-id="bd491-108">예를 들어 수신 웹 요청을 처리할 수 있는 서비스로 경고를 라우팅하여 SMS를 보내거나 버그를 기록하거나 채팅 또는 메시징 서비스를 사용해 팀에게 알리는 등의 작업을 수행할 수 있습니다. Webhook URI는 유효한 HTTP 또는 HTTPS 끝점이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-108">For example, routing the alert to services that can handle an incoming web request to send SMS, log bugs, notify a team using chat or messaging services, etc. The webhook URI must be a valid HTTP or HTTPS endpoint.</span></span>

## <a name="email"></a><span data-ttu-id="bd491-109">Email</span><span class="sxs-lookup"><span data-stu-id="bd491-109">Email</span></span>
<span data-ttu-id="bd491-110">모든 유효한 전자 메일 주소로 전자 메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-110">Email can be sent to any valid email address.</span></span> <span data-ttu-id="bd491-111">규칙이 실행되고 있는 구독의 관리자와 공동 관리자도 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-111">Administrators and co-administrators of the subscription where the rule is running will also be notified.</span></span>

## <a name="cloud-services-and-web-apps"></a><span data-ttu-id="bd491-112">클라우드 서비스 및 웹 앱</span><span class="sxs-lookup"><span data-stu-id="bd491-112">Cloud Services and Web Apps</span></span>
<span data-ttu-id="bd491-113">Azure 포털에서 클라우드 서비스 및 서버 팜(웹 앱)에 대해 옵트인(opt in)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-113">You can opt-in from the Azure portal for Cloud Services and Server Farms (Web Apps).</span></span>

* <span data-ttu-id="bd491-114">**배율 기준** 메트릭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-114">Choose the **scale by** metric.</span></span>

![배율 기준](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a><span data-ttu-id="bd491-116">가상 컴퓨터 확장 집합</span><span class="sxs-lookup"><span data-stu-id="bd491-116">Virtual Machine scale sets</span></span>
<span data-ttu-id="bd491-117">Resource Manager(가상 컴퓨터 확장 집합)로 만든 새 가상 컴퓨터의 경우 REST API, Resource Manager 템플릿, PowerShell 및 CLI를 사용하여 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-117">For newer Virtual Machines created with Resource Manager (Virtual Machine scale sets), you can configure this using REST API, Resource Manager templates, PowerShell, and CLI.</span></span> <span data-ttu-id="bd491-118">포털 인터페이스는 아직 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-118">A portal interface is not yet available.</span></span>
<span data-ttu-id="bd491-119">REST API 또는 Resource Manager 템플릿을 사용하는 경우 다음 옵션으로 알림 요소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-119">When using the REST API or Resource Manager template, include the notifications element with the following options.</span></span>

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
| <span data-ttu-id="bd491-120">필드</span><span class="sxs-lookup"><span data-stu-id="bd491-120">Field</span></span> | <span data-ttu-id="bd491-121">필수?</span><span class="sxs-lookup"><span data-stu-id="bd491-121">Mandatory?</span></span> | <span data-ttu-id="bd491-122">설명</span><span class="sxs-lookup"><span data-stu-id="bd491-122">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bd491-123">operation</span><span class="sxs-lookup"><span data-stu-id="bd491-123">operation</span></span> |<span data-ttu-id="bd491-124">yes</span><span class="sxs-lookup"><span data-stu-id="bd491-124">yes</span></span> |<span data-ttu-id="bd491-125">값은 "Scale"이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-125">value must be "Scale"</span></span> |
| <span data-ttu-id="bd491-126">sendToSubscriptionAdministrator</span><span class="sxs-lookup"><span data-stu-id="bd491-126">sendToSubscriptionAdministrator</span></span> |<span data-ttu-id="bd491-127">yes</span><span class="sxs-lookup"><span data-stu-id="bd491-127">yes</span></span> |<span data-ttu-id="bd491-128">값은 "true" 또는 "false"여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-128">value must be "true" or "false"</span></span> |
| <span data-ttu-id="bd491-129">sendToSubscriptionCoAdministrators</span><span class="sxs-lookup"><span data-stu-id="bd491-129">sendToSubscriptionCoAdministrators</span></span> |<span data-ttu-id="bd491-130">yes</span><span class="sxs-lookup"><span data-stu-id="bd491-130">yes</span></span> |<span data-ttu-id="bd491-131">값은 "true" 또는 "false"여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-131">value must be "true" or "false"</span></span> |
| <span data-ttu-id="bd491-132">customEmails</span><span class="sxs-lookup"><span data-stu-id="bd491-132">customEmails</span></span> |<span data-ttu-id="bd491-133">yes</span><span class="sxs-lookup"><span data-stu-id="bd491-133">yes</span></span> |<span data-ttu-id="bd491-134">값에 null [] 또는 전자 메일 문자열 배열을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-134">value can be null [] or string array of emails</span></span> |
| <span data-ttu-id="bd491-135">Webhook</span><span class="sxs-lookup"><span data-stu-id="bd491-135">webhooks</span></span> |<span data-ttu-id="bd491-136">yes</span><span class="sxs-lookup"><span data-stu-id="bd491-136">yes</span></span> |<span data-ttu-id="bd491-137">값은 null이거나 올바른 URI일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-137">value can be null or valid Uri</span></span> |
| <span data-ttu-id="bd491-138">serviceUri</span><span class="sxs-lookup"><span data-stu-id="bd491-138">serviceUri</span></span> |<span data-ttu-id="bd491-139">yes</span><span class="sxs-lookup"><span data-stu-id="bd491-139">yes</span></span> |<span data-ttu-id="bd491-140">유효한 https URI</span><span class="sxs-lookup"><span data-stu-id="bd491-140">a valid https Uri</span></span> |
| <span data-ttu-id="bd491-141">properties</span><span class="sxs-lookup"><span data-stu-id="bd491-141">properties</span></span> |<span data-ttu-id="bd491-142">yes</span><span class="sxs-lookup"><span data-stu-id="bd491-142">yes</span></span> |<span data-ttu-id="bd491-143">값은 비어 있거나{} 키-값 쌍을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-143">value must be empty {} or can contain key-value pairs</span></span> |

## <a name="authentication-in-webhooks"></a><span data-ttu-id="bd491-144">Webhook의 인증</span><span class="sxs-lookup"><span data-stu-id="bd491-144">Authentication in webhooks</span></span>
<span data-ttu-id="bd491-145">웹후크는 토큰 ID를 쿼리 매개 변수로 사용해서 웹후크 URI를 저장하는 토큰 기반 인증을 사용하여 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-145">The webhook can authenticate using token-based authentication, where you save the webhook URI with a token ID as a query parameter.</span></span> <span data-ttu-id="bd491-146">예를 들어 https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue입니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-146">For example, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span></span>

## <a name="autoscale-notification-webhook-payload-schema"></a><span data-ttu-id="bd491-147">크기 자동 조정 알림 Webhook 페이로드 스키마</span><span class="sxs-lookup"><span data-stu-id="bd491-147">Autoscale notification webhook payload schema</span></span>
<span data-ttu-id="bd491-148">크기 자동 조정 알림이 생성될 때는 다음 메타데이터가 Webhook 페이로드에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-148">When the autoscale notification is generated, the following metadata is included in the webhook payload:</span></span>

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' to capacity '2'",
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


| <span data-ttu-id="bd491-149">필드</span><span class="sxs-lookup"><span data-stu-id="bd491-149">Field</span></span> | <span data-ttu-id="bd491-150">필수?</span><span class="sxs-lookup"><span data-stu-id="bd491-150">Mandatory?</span></span> | <span data-ttu-id="bd491-151">설명</span><span class="sxs-lookup"><span data-stu-id="bd491-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bd491-152">status</span><span class="sxs-lookup"><span data-stu-id="bd491-152">status</span></span> |<span data-ttu-id="bd491-153">yes</span><span class="sxs-lookup"><span data-stu-id="bd491-153">yes</span></span> |<span data-ttu-id="bd491-154">크기 자동 조정 작업이 생성되었음을 나타내는 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-154">The status that indicates that an autoscale action was generated</span></span> |
| <span data-ttu-id="bd491-155">operation</span><span class="sxs-lookup"><span data-stu-id="bd491-155">operation</span></span> |<span data-ttu-id="bd491-156">yes</span><span class="sxs-lookup"><span data-stu-id="bd491-156">yes</span></span> |<span data-ttu-id="bd491-157">인스턴스가 증가하면 "규모 확장"되고 인스턴스가 감소하면 "규모 감축"됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-157">For an increase of instances, it will be "Scale Out" and for a decrease in instances, it will be "Scale In"</span></span> |
| <span data-ttu-id="bd491-158">context</span><span class="sxs-lookup"><span data-stu-id="bd491-158">context</span></span> |<span data-ttu-id="bd491-159">yes</span><span class="sxs-lookup"><span data-stu-id="bd491-159">yes</span></span> |<span data-ttu-id="bd491-160">크기 자동 조정 작업 컨텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-160">The autoscale action context</span></span> |
| <span data-ttu-id="bd491-161">timestamp</span><span class="sxs-lookup"><span data-stu-id="bd491-161">timestamp</span></span> |<span data-ttu-id="bd491-162">yes</span><span class="sxs-lookup"><span data-stu-id="bd491-162">yes</span></span> |<span data-ttu-id="bd491-163">크기 자동 조정 작업이 트리거된 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-163">Time stamp when the autoscale action was triggered</span></span> |
| <span data-ttu-id="bd491-164">id</span><span class="sxs-lookup"><span data-stu-id="bd491-164">id</span></span> |<span data-ttu-id="bd491-165">yes</span><span class="sxs-lookup"><span data-stu-id="bd491-165">Yes</span></span> |<span data-ttu-id="bd491-166">자동 크기 조정 설정의 Resource Manager ID</span><span class="sxs-lookup"><span data-stu-id="bd491-166">Resource Manager ID of the autoscale setting</span></span> |
| <span data-ttu-id="bd491-167">name</span><span class="sxs-lookup"><span data-stu-id="bd491-167">name</span></span> |<span data-ttu-id="bd491-168">yes</span><span class="sxs-lookup"><span data-stu-id="bd491-168">Yes</span></span> |<span data-ttu-id="bd491-169">크기 자동 조정 설정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-169">The name of the autoscale setting</span></span> |
| <span data-ttu-id="bd491-170">세부 정보</span><span class="sxs-lookup"><span data-stu-id="bd491-170">details</span></span> |<span data-ttu-id="bd491-171">yes</span><span class="sxs-lookup"><span data-stu-id="bd491-171">Yes</span></span> |<span data-ttu-id="bd491-172">크기 자동 조정 서비스가 수행한 작업에 대한 설명 및 인스턴스 수의 변경 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-172">Explanation of the action that the autoscale service took and the change in the instance count</span></span> |
| <span data-ttu-id="bd491-173">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="bd491-173">subscriptionId</span></span> |<span data-ttu-id="bd491-174">yes</span><span class="sxs-lookup"><span data-stu-id="bd491-174">Yes</span></span> |<span data-ttu-id="bd491-175">크기 조정 중인 대상 리소스의 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-175">Subscription ID of the target resource that is being scaled</span></span> |
| <span data-ttu-id="bd491-176">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="bd491-176">resourceGroupName</span></span> |<span data-ttu-id="bd491-177">yes</span><span class="sxs-lookup"><span data-stu-id="bd491-177">Yes</span></span> |<span data-ttu-id="bd491-178">크기 조정 중인 대상 리소스의 리소스 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-178">Resource Group name of the target resource that is being scaled</span></span> |
| <span data-ttu-id="bd491-179">resourceName</span><span class="sxs-lookup"><span data-stu-id="bd491-179">resourceName</span></span> |<span data-ttu-id="bd491-180">yes</span><span class="sxs-lookup"><span data-stu-id="bd491-180">Yes</span></span> |<span data-ttu-id="bd491-181">크기 조정 중인 대상 리소스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-181">Name of the target resource that is being scaled</span></span> |
| <span data-ttu-id="bd491-182">resourceType</span><span class="sxs-lookup"><span data-stu-id="bd491-182">resourceType</span></span> |<span data-ttu-id="bd491-183">예</span><span class="sxs-lookup"><span data-stu-id="bd491-183">Yes</span></span> |<span data-ttu-id="bd491-184">다음의 세 값이 지원됩니다. "microsoft.classiccompute/domainnames/slots/roles" - Cloud Service 역할/"microsoft.compute/virtualmachinescalesets" - 가상 컴퓨터 확장 집합/"Microsoft.Web/serverfarms" - Web App</span><span class="sxs-lookup"><span data-stu-id="bd491-184">The three supported values: "microsoft.classiccompute/domainnames/slots/roles" - Cloud Service roles, "microsoft.compute/virtualmachinescalesets" - Virtual Machine Scale Sets,  and "Microsoft.Web/serverfarms" - Web App</span></span> |
| <span data-ttu-id="bd491-185">resourceId</span><span class="sxs-lookup"><span data-stu-id="bd491-185">resourceId</span></span> |<span data-ttu-id="bd491-186">yes</span><span class="sxs-lookup"><span data-stu-id="bd491-186">Yes</span></span> |<span data-ttu-id="bd491-187">크기 조정 중인 대상 리소스의 Resource Manager ID</span><span class="sxs-lookup"><span data-stu-id="bd491-187">Resource Manager ID of the target resource that is being scaled</span></span> |
| <span data-ttu-id="bd491-188">portalLink</span><span class="sxs-lookup"><span data-stu-id="bd491-188">portalLink</span></span> |<span data-ttu-id="bd491-189">yes</span><span class="sxs-lookup"><span data-stu-id="bd491-189">Yes</span></span> |<span data-ttu-id="bd491-190">대상 리소스의 요약 페이지에 대한 Azure 포털 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-190">Azure portal link to the summary page of the target resource</span></span> |
| <span data-ttu-id="bd491-191">oldCapacity</span><span class="sxs-lookup"><span data-stu-id="bd491-191">oldCapacity</span></span> |<span data-ttu-id="bd491-192">yes</span><span class="sxs-lookup"><span data-stu-id="bd491-192">Yes</span></span> |<span data-ttu-id="bd491-193">크기 자동 조정에서 크기 조정 작업을 수행한 현재(이전) 인스턴스 수입니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-193">The current (old) instance count when Autoscale took a scale action</span></span> |
| <span data-ttu-id="bd491-194">newCapacity</span><span class="sxs-lookup"><span data-stu-id="bd491-194">newCapacity</span></span> |<span data-ttu-id="bd491-195">yes</span><span class="sxs-lookup"><span data-stu-id="bd491-195">Yes</span></span> |<span data-ttu-id="bd491-196">크기 자동 조정에서 리소스 크기를 조정한 새 인스턴스 수입니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-196">The new instance count that Autoscale scaled the resource to</span></span> |
| <span data-ttu-id="bd491-197">properties</span><span class="sxs-lookup"><span data-stu-id="bd491-197">Properties</span></span> |<span data-ttu-id="bd491-198">아니요</span><span class="sxs-lookup"><span data-stu-id="bd491-198">No</span></span> |<span data-ttu-id="bd491-199">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-199">Optional.</span></span> <span data-ttu-id="bd491-200"><키, 값> 쌍 집합(예: Dictionary <문자열, 문자열>).</span><span class="sxs-lookup"><span data-stu-id="bd491-200">Set of <Key, Value> pairs (for example,  Dictionary <String, String>).</span></span> <span data-ttu-id="bd491-201">속성 필드는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-201">The properties field is optional.</span></span> <span data-ttu-id="bd491-202">사용자 지정 사용자 인터페이스 또는 논리 앱 기반 워크플로에서는 페이로드를 사용하여 전달할 수 있는 키와 값을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-202">In a custom user interface  or Logic app based workflow, you can enter keys and values that can be passed using the payload.</span></span> <span data-ttu-id="bd491-203">Webhook URI 자체를 쿼리 매개 변수로 사용하여 발신 Webhook 호출로 사용자 지정 속성을 다시 전달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd491-203">An alternate way to pass custom properties back to the outgoing webhook call is to use the webhook URI itself (as query parameters)</span></span> |
