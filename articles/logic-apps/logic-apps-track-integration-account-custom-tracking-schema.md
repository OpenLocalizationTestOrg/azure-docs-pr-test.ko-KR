---
title: "B2B 모니터링을 위한 사용자 지정 추적 스키마 - Azure Logic Apps | Microsoft Docs"
description: "사용자 지정 추적 스키마를 만들어 Azure 통합 계정의 트랜잭션에서 B2B 메시지를 모니터링합니다."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 433ae852-a833-44d3-a3c3-14cca33403a2
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b71a4938dde2a71f1ce29403af7aa9101358d64c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-tracking-to-monitor-your-complete-workflow-end-to-end"></a><span data-ttu-id="06c98-103">추적을 사용하도록 설정하여 종단 간, 전체 워크플로 모니터링</span><span class="sxs-lookup"><span data-stu-id="06c98-103">Enable tracking to monitor your complete workflow, end-to-end</span></span>
<span data-ttu-id="06c98-104">기업 간 워크플로의 다양한 부분에 대해 사용할 수 있는 기본 제공 추적(예: AS2 또는 X12 메시지 추적)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-104">There is built-in tracking that you can enable for different parts of your business-to-business workflow, such as tracking AS2 or X12 messages.</span></span> <span data-ttu-id="06c98-105">논리 앱, BizTalk Server, SQL Server 또는 다른 계층을 포함하는 워크플로를 만들 경우 워크플로의 시작부터 끝까지 이벤트를 기록하는 사용자 지정 추적을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-105">When you create workflows that includes a logic app, BizTalk Server, SQL Server, or any other layer, then you can enable custom tracking that logs events from the beginning to the end of your workflow.</span></span> 

<span data-ttu-id="06c98-106">이 항목에서는 논리 앱 외부의 계층에서 사용할 수 있는 사용자 지정 코드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-106">This topic provides custom code that you can use in the layers outside of your logic app.</span></span> 

## <a name="custom-tracking-schema"></a><span data-ttu-id="06c98-107">사용자 지정 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="06c98-107">Custom tracking schema</span></span>
````java

        {
            "sourceType": "",
            "source": {

            "workflow": {
                "systemId": ""
            },
            "runInstance": {
                "runId": ""
            },
            "operation": {
                "operationName": "",
                "repeatItemScopeName": "",
                "repeatItemIndex": "",
                "trackingId": "",
                "correlationId": "",
                "clientRequestId": ""
                }
            },
            "events": [
            {
                "eventLevel": "",
                "eventTime": "",
                "recordType": "",
                "record": {                
                }
            }
         ]
      }

````

| <span data-ttu-id="06c98-108">속성</span><span class="sxs-lookup"><span data-stu-id="06c98-108">Property</span></span> | <span data-ttu-id="06c98-109">형식</span><span class="sxs-lookup"><span data-stu-id="06c98-109">Type</span></span> | <span data-ttu-id="06c98-110">설명</span><span class="sxs-lookup"><span data-stu-id="06c98-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="06c98-111">sourceType</span><span class="sxs-lookup"><span data-stu-id="06c98-111">sourceType</span></span> |   | <span data-ttu-id="06c98-112">실행 원본의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-112">Type of the run source.</span></span> <span data-ttu-id="06c98-113">허용되는 값은**Microsoft.Logic/workflows** 및 **custom**입니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-113">Allowed values are **Microsoft.Logic/workflows** and **custom**.</span></span> <span data-ttu-id="06c98-114">(필수)</span><span class="sxs-lookup"><span data-stu-id="06c98-114">(Mandatory)</span></span> |
| <span data-ttu-id="06c98-115">원본</span><span class="sxs-lookup"><span data-stu-id="06c98-115">Source</span></span> |   | <span data-ttu-id="06c98-116">소스 형식이 **Microsoft.Logic/workflows**이면 소스 정보는 이 스키마를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-116">If the source type is **Microsoft.Logic/workflows**, the source information needs to follow this schema.</span></span> <span data-ttu-id="06c98-117">소스 형식이 **custom**이면 스키마는 JToken입니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-117">If the source type is **custom**, the schema is a JToken.</span></span> <span data-ttu-id="06c98-118">(필수)</span><span class="sxs-lookup"><span data-stu-id="06c98-118">(Mandatory)</span></span> |
| <span data-ttu-id="06c98-119">systemId</span><span class="sxs-lookup"><span data-stu-id="06c98-119">systemId</span></span> | <span data-ttu-id="06c98-120">문자열</span><span class="sxs-lookup"><span data-stu-id="06c98-120">String</span></span> | <span data-ttu-id="06c98-121">논리 앱 시스템 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-121">Logic app system ID.</span></span> <span data-ttu-id="06c98-122">(필수)</span><span class="sxs-lookup"><span data-stu-id="06c98-122">(Mandatory)</span></span> |
| <span data-ttu-id="06c98-123">runId</span><span class="sxs-lookup"><span data-stu-id="06c98-123">runId</span></span> | <span data-ttu-id="06c98-124">string</span><span class="sxs-lookup"><span data-stu-id="06c98-124">String</span></span> | <span data-ttu-id="06c98-125">논리 앱 실행 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-125">Logic app run ID.</span></span> <span data-ttu-id="06c98-126">(필수)</span><span class="sxs-lookup"><span data-stu-id="06c98-126">(Mandatory)</span></span> |
| <span data-ttu-id="06c98-127">operationName</span><span class="sxs-lookup"><span data-stu-id="06c98-127">operationName</span></span> | <span data-ttu-id="06c98-128">문자열</span><span class="sxs-lookup"><span data-stu-id="06c98-128">String</span></span> | <span data-ttu-id="06c98-129">작업의 이름(예: action 또는 trigger)입니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-129">Name of the operation (for example, action or trigger).</span></span> <span data-ttu-id="06c98-130">(필수)</span><span class="sxs-lookup"><span data-stu-id="06c98-130">(Mandatory)</span></span> |
| <span data-ttu-id="06c98-131">repeatItemScopeName</span><span class="sxs-lookup"><span data-stu-id="06c98-131">repeatItemScopeName</span></span> | <span data-ttu-id="06c98-132">string</span><span class="sxs-lookup"><span data-stu-id="06c98-132">String</span></span> | <span data-ttu-id="06c98-133">작업이 `foreach`/`until` 루프에 있으면 아이템 이름을 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-133">Repeat item name if the action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="06c98-134">(필수)</span><span class="sxs-lookup"><span data-stu-id="06c98-134">(Mandatory)</span></span> |
| <span data-ttu-id="06c98-135">repeatItemIndex</span><span class="sxs-lookup"><span data-stu-id="06c98-135">repeatItemIndex</span></span> | <span data-ttu-id="06c98-136">Integer</span><span class="sxs-lookup"><span data-stu-id="06c98-136">Integer</span></span> | <span data-ttu-id="06c98-137">작업이 `foreach`/`until` 루프에 있는지의 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-137">Whether the action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="06c98-138">반복된 항목 인덱스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-138">Indicates the repeated item index.</span></span> <span data-ttu-id="06c98-139">(필수)</span><span class="sxs-lookup"><span data-stu-id="06c98-139">(Mandatory)</span></span> |
| <span data-ttu-id="06c98-140">trackingId</span><span class="sxs-lookup"><span data-stu-id="06c98-140">trackingId</span></span> | <span data-ttu-id="06c98-141">string</span><span class="sxs-lookup"><span data-stu-id="06c98-141">String</span></span> | <span data-ttu-id="06c98-142">메시지에 상호 연결할 추적 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-142">Tracking ID, to correlate the messages.</span></span> <span data-ttu-id="06c98-143">(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="06c98-143">(Optional)</span></span> |
| <span data-ttu-id="06c98-144">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="06c98-144">correlationId</span></span> | <span data-ttu-id="06c98-145">문자열</span><span class="sxs-lookup"><span data-stu-id="06c98-145">String</span></span> | <span data-ttu-id="06c98-146">메시지에 상호 연결할 상관 관계 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-146">Correlation ID, to correlate the messages.</span></span> <span data-ttu-id="06c98-147">(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="06c98-147">(Optional)</span></span> |
| <span data-ttu-id="06c98-148">clientRequestId</span><span class="sxs-lookup"><span data-stu-id="06c98-148">clientRequestId</span></span> | <span data-ttu-id="06c98-149">string</span><span class="sxs-lookup"><span data-stu-id="06c98-149">String</span></span> | <span data-ttu-id="06c98-150">클라이언트는 메시지에 상호 연결하기 위해 이 항목을 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-150">Client can populate it to correlate messages.</span></span> <span data-ttu-id="06c98-151">(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="06c98-151">(Optional)</span></span> |
| <span data-ttu-id="06c98-152">eventLevel</span><span class="sxs-lookup"><span data-stu-id="06c98-152">eventLevel</span></span> |   | <span data-ttu-id="06c98-153">이벤트의 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-153">Level of the event.</span></span> <span data-ttu-id="06c98-154">(필수)</span><span class="sxs-lookup"><span data-stu-id="06c98-154">(Mandatory)</span></span> |
| <span data-ttu-id="06c98-155">eventTime</span><span class="sxs-lookup"><span data-stu-id="06c98-155">eventTime</span></span> |   | <span data-ttu-id="06c98-156">UTC 형식 YYYY-MM-DDTHH:MM:SS.00000Z의 이벤트 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-156">Time of the event, in UTC format YYYY-MM-DDTHH:MM:SS.00000Z.</span></span> <span data-ttu-id="06c98-157">(필수)</span><span class="sxs-lookup"><span data-stu-id="06c98-157">(Mandatory)</span></span> |
| <span data-ttu-id="06c98-158">recordType</span><span class="sxs-lookup"><span data-stu-id="06c98-158">recordType</span></span> |   | <span data-ttu-id="06c98-159">트랙 레코드의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-159">Type of the track record.</span></span> <span data-ttu-id="06c98-160">허용되는 값은 **custom**입니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-160">Allowed value is **custom**.</span></span> <span data-ttu-id="06c98-161">(필수)</span><span class="sxs-lookup"><span data-stu-id="06c98-161">(Mandatory)</span></span> |
| <span data-ttu-id="06c98-162">record</span><span class="sxs-lookup"><span data-stu-id="06c98-162">record</span></span> |   | <span data-ttu-id="06c98-163">사용자 지정 레코드 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-163">Custom record type.</span></span> <span data-ttu-id="06c98-164">허용된 형식은 JToken입니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-164">Allowed format is JToken.</span></span> <span data-ttu-id="06c98-165">(필수)</span><span class="sxs-lookup"><span data-stu-id="06c98-165">(Mandatory)</span></span> |

## <a name="b2b-protocol-tracking-schemas"></a><span data-ttu-id="06c98-166">B2B 프로토콜 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="06c98-166">B2B protocol tracking schemas</span></span>
<span data-ttu-id="06c98-167">스키마를 추적하는 B2B 프로토콜에 대한 정보는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06c98-167">For information about B2B protocol tracking schemas, see:</span></span>
* [<span data-ttu-id="06c98-168">AS2 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="06c98-168">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [<span data-ttu-id="06c98-169">X12 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="06c98-169">X12 tracking schemas</span></span>](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="06c98-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="06c98-170">Next steps</span></span>
* <span data-ttu-id="06c98-171">[B2B 메시지 모니터링](logic-apps-monitor-b2b-message.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-171">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="06c98-172">[Operations Management Suite에서 B2B 메시지 추적하기](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-172">Learn about [tracking B2B messages in the Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>
* <span data-ttu-id="06c98-173">[엔터프라이즈 통합 팩](../logic-apps/logic-apps-enterprise-integration-overview.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="06c98-173">Learn more about the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>
