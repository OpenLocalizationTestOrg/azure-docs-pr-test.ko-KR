---
title: "b2b 스키마 추적 aaaCustom 모니터링-Azure 논리 앱 | Microsoft Docs"
description: "Azure 통합 계정에 대 한 트랜잭션 으로부터 사용자 지정 추적 스키마 toomonitor B2B 메시지를 만듭니다."
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
ms.openlocfilehash: 8cf26a43d89f0414a2a8c5ef59d804235afeb5d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-tracking-toomonitor-your-complete-workflow-end-to-end"></a><span data-ttu-id="b2b32-103">전체 워크플로, 종단 간 추적 toomonitor를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="b2b32-103">Enable tracking toomonitor your complete workflow, end-to-end</span></span>
<span data-ttu-id="b2b32-104">기업 간 워크플로의 다양한 부분에 대해 사용할 수 있는 기본 제공 추적(예: AS2 또는 X12 메시지 추적)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-104">There is built-in tracking that you can enable for different parts of your business-to-business workflow, such as tracking AS2 or X12 messages.</span></span> <span data-ttu-id="b2b32-105">논리 앱, BizTalk Server, SQL Server 또는 다른 레이어를 포함 하는 워크플로 만들 때 워크플로의 hello 시작 toohello 끝에서 이벤트를 기록 하는 사용자 지정 추적을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-105">When you create workflows that includes a logic app, BizTalk Server, SQL Server, or any other layer, then you can enable custom tracking that logs events from hello beginning toohello end of your workflow.</span></span> 

<span data-ttu-id="b2b32-106">이 항목에서는 논리 앱 외부 hello 계층에서 사용할 수 있는 사용자 지정 코드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-106">This topic provides custom code that you can use in hello layers outside of your logic app.</span></span> 

## <a name="custom-tracking-schema"></a><span data-ttu-id="b2b32-107">사용자 지정 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="b2b32-107">Custom tracking schema</span></span>
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

| <span data-ttu-id="b2b32-108">속성</span><span class="sxs-lookup"><span data-stu-id="b2b32-108">Property</span></span> | <span data-ttu-id="b2b32-109">형식</span><span class="sxs-lookup"><span data-stu-id="b2b32-109">Type</span></span> | <span data-ttu-id="b2b32-110">설명</span><span class="sxs-lookup"><span data-stu-id="b2b32-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2b32-111">sourceType</span><span class="sxs-lookup"><span data-stu-id="b2b32-111">sourceType</span></span> |   | <span data-ttu-id="b2b32-112">실행 하는 hello 원본의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-112">Type of hello run source.</span></span> <span data-ttu-id="b2b32-113">허용되는 값은**Microsoft.Logic/workflows** 및 **custom**입니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-113">Allowed values are **Microsoft.Logic/workflows** and **custom**.</span></span> <span data-ttu-id="b2b32-114">(필수)</span><span class="sxs-lookup"><span data-stu-id="b2b32-114">(Mandatory)</span></span> |
| <span data-ttu-id="b2b32-115">원본</span><span class="sxs-lookup"><span data-stu-id="b2b32-115">Source</span></span> |   | <span data-ttu-id="b2b32-116">Hello 소스 형식이 면 **Microsoft.Logic/workflows**, hello 소스 정보 toofollow이이 스키마를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-116">If hello source type is **Microsoft.Logic/workflows**, hello source information needs toofollow this schema.</span></span> <span data-ttu-id="b2b32-117">Hello 소스 형식이 면 **사용자 지정**, hello 스키마는 JToken는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-117">If hello source type is **custom**, hello schema is a JToken.</span></span> <span data-ttu-id="b2b32-118">(필수)</span><span class="sxs-lookup"><span data-stu-id="b2b32-118">(Mandatory)</span></span> |
| <span data-ttu-id="b2b32-119">systemId</span><span class="sxs-lookup"><span data-stu-id="b2b32-119">systemId</span></span> | <span data-ttu-id="b2b32-120">문자열</span><span class="sxs-lookup"><span data-stu-id="b2b32-120">String</span></span> | <span data-ttu-id="b2b32-121">논리 앱 시스템 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-121">Logic app system ID.</span></span> <span data-ttu-id="b2b32-122">(필수)</span><span class="sxs-lookup"><span data-stu-id="b2b32-122">(Mandatory)</span></span> |
| <span data-ttu-id="b2b32-123">runId</span><span class="sxs-lookup"><span data-stu-id="b2b32-123">runId</span></span> | <span data-ttu-id="b2b32-124">string</span><span class="sxs-lookup"><span data-stu-id="b2b32-124">String</span></span> | <span data-ttu-id="b2b32-125">논리 앱 실행 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-125">Logic app run ID.</span></span> <span data-ttu-id="b2b32-126">(필수)</span><span class="sxs-lookup"><span data-stu-id="b2b32-126">(Mandatory)</span></span> |
| <span data-ttu-id="b2b32-127">operationName</span><span class="sxs-lookup"><span data-stu-id="b2b32-127">operationName</span></span> | <span data-ttu-id="b2b32-128">문자열</span><span class="sxs-lookup"><span data-stu-id="b2b32-128">String</span></span> | <span data-ttu-id="b2b32-129">Hello 작업 (예: 동작 또는 트리거)의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-129">Name of hello operation (for example, action or trigger).</span></span> <span data-ttu-id="b2b32-130">(필수)</span><span class="sxs-lookup"><span data-stu-id="b2b32-130">(Mandatory)</span></span> |
| <span data-ttu-id="b2b32-131">repeatItemScopeName</span><span class="sxs-lookup"><span data-stu-id="b2b32-131">repeatItemScopeName</span></span> | <span data-ttu-id="b2b32-132">문자열</span><span class="sxs-lookup"><span data-stu-id="b2b32-132">String</span></span> | <span data-ttu-id="b2b32-133">Hello 작업 내에 있으면 항목 이름을 반복는 `foreach` / `until` 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-133">Repeat item name if hello action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="b2b32-134">(필수)</span><span class="sxs-lookup"><span data-stu-id="b2b32-134">(Mandatory)</span></span> |
| <span data-ttu-id="b2b32-135">repeatItemIndex</span><span class="sxs-lookup"><span data-stu-id="b2b32-135">repeatItemIndex</span></span> | <span data-ttu-id="b2b32-136">Integer</span><span class="sxs-lookup"><span data-stu-id="b2b32-136">Integer</span></span> | <span data-ttu-id="b2b32-137">Hello 동작 내 인지는 `foreach` / `until` 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-137">Whether hello action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="b2b32-138">Hello 반복된 항목 인덱스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-138">Indicates hello repeated item index.</span></span> <span data-ttu-id="b2b32-139">(필수)</span><span class="sxs-lookup"><span data-stu-id="b2b32-139">(Mandatory)</span></span> |
| <span data-ttu-id="b2b32-140">trackingId</span><span class="sxs-lookup"><span data-stu-id="b2b32-140">trackingId</span></span> | <span data-ttu-id="b2b32-141">문자열</span><span class="sxs-lookup"><span data-stu-id="b2b32-141">String</span></span> | <span data-ttu-id="b2b32-142">ID, toocorrelate hello 메시지를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-142">Tracking ID, toocorrelate hello messages.</span></span> <span data-ttu-id="b2b32-143">(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="b2b32-143">(Optional)</span></span> |
| <span data-ttu-id="b2b32-144">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="b2b32-144">correlationId</span></span> | <span data-ttu-id="b2b32-145">문자열</span><span class="sxs-lookup"><span data-stu-id="b2b32-145">String</span></span> | <span data-ttu-id="b2b32-146">Toocorrelate hello 메시지의 상관 관계 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-146">Correlation ID, toocorrelate hello messages.</span></span> <span data-ttu-id="b2b32-147">(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="b2b32-147">(Optional)</span></span> |
| <span data-ttu-id="b2b32-148">clientRequestId</span><span class="sxs-lookup"><span data-stu-id="b2b32-148">clientRequestId</span></span> | <span data-ttu-id="b2b32-149">문자열</span><span class="sxs-lookup"><span data-stu-id="b2b32-149">String</span></span> | <span data-ttu-id="b2b32-150">클라이언트는 toocorrelate 메시지 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-150">Client can populate it toocorrelate messages.</span></span> <span data-ttu-id="b2b32-151">(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="b2b32-151">(Optional)</span></span> |
| <span data-ttu-id="b2b32-152">eventLevel</span><span class="sxs-lookup"><span data-stu-id="b2b32-152">eventLevel</span></span> |   | <span data-ttu-id="b2b32-153">Hello 이벤트의 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-153">Level of hello event.</span></span> <span data-ttu-id="b2b32-154">(필수)</span><span class="sxs-lookup"><span data-stu-id="b2b32-154">(Mandatory)</span></span> |
| <span data-ttu-id="b2b32-155">eventTime</span><span class="sxs-lookup"><span data-stu-id="b2b32-155">eventTime</span></span> |   | <span data-ttu-id="b2b32-156">UTC 형식 YYYY-m M-DDTHH:MM:SS.00000Z hello 이벤트 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-156">Time of hello event, in UTC format YYYY-MM-DDTHH:MM:SS.00000Z.</span></span> <span data-ttu-id="b2b32-157">(필수)</span><span class="sxs-lookup"><span data-stu-id="b2b32-157">(Mandatory)</span></span> |
| <span data-ttu-id="b2b32-158">recordType</span><span class="sxs-lookup"><span data-stu-id="b2b32-158">recordType</span></span> |   | <span data-ttu-id="b2b32-159">Hello 추적 레코드의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-159">Type of hello track record.</span></span> <span data-ttu-id="b2b32-160">허용되는 값은 **custom**입니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-160">Allowed value is **custom**.</span></span> <span data-ttu-id="b2b32-161">(필수)</span><span class="sxs-lookup"><span data-stu-id="b2b32-161">(Mandatory)</span></span> |
| <span data-ttu-id="b2b32-162">record</span><span class="sxs-lookup"><span data-stu-id="b2b32-162">record</span></span> |   | <span data-ttu-id="b2b32-163">사용자 지정 레코드 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-163">Custom record type.</span></span> <span data-ttu-id="b2b32-164">허용된 형식은 JToken입니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-164">Allowed format is JToken.</span></span> <span data-ttu-id="b2b32-165">(필수)</span><span class="sxs-lookup"><span data-stu-id="b2b32-165">(Mandatory)</span></span> |

## <a name="b2b-protocol-tracking-schemas"></a><span data-ttu-id="b2b32-166">B2B 프로토콜 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="b2b32-166">B2B protocol tracking schemas</span></span>
<span data-ttu-id="b2b32-167">스키마를 추적하는 B2B 프로토콜에 대한 정보는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2b32-167">For information about B2B protocol tracking schemas, see:</span></span>
* [<span data-ttu-id="b2b32-168">AS2 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="b2b32-168">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [<span data-ttu-id="b2b32-169">X12 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="b2b32-169">X12 tracking schemas</span></span>](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="b2b32-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b2b32-170">Next steps</span></span>
* <span data-ttu-id="b2b32-171">[B2B 메시지 모니터링](logic-apps-monitor-b2b-message.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-171">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="b2b32-172">에 대 한 자세한 내용은 [hello Operations Management Suite 포털에서 B2B 메시지를 추적](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-172">Learn about [tracking B2B messages in hello Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>
* <span data-ttu-id="b2b32-173">Hello에 대 한 자세한 [엔터프라이즈 통합 팩](../logic-apps/logic-apps-enterprise-integration-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b2b32-173">Learn more about hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>
