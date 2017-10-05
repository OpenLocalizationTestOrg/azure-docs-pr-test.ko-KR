---
title: "2016년 6월 1일 스키마 업데이트 - Azure Logic Apps | Microsoft Docs"
description: "스키마 버전 2016-06-01로 Azure Logic Apps에 대한 JSON 정의 만들기"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 349d57e8-f62b-4ec6-a92f-a6e0242d6c0e
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/25/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 43df04d6478e44c82c88b17d916cfc9fe4afc03e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a><span data-ttu-id="98fb3-103">Azure Logic Apps에 대한 스키마 업데이트 - 2016년 6월 1일</span><span class="sxs-lookup"><span data-stu-id="98fb3-103">Schema updates for Azure Logic Apps - June 1, 2016</span></span>

<span data-ttu-id="98fb3-104">Azure Logic Apps에 대한 새 스키마 및 API 버전에 논리 앱의 안정성 및 사용 편의성을 개선하는 향상된 주요 기능이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier to use:</span></span>

* <span data-ttu-id="98fb3-105">[범위](#scopes)를 통해 작업 컬렉션으로 작업을 그룹화 또는 중첩시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-105">[Scopes](#scopes) let you group or nest actions as a collection of actions.</span></span>
* <span data-ttu-id="98fb3-106">[조건과 루프](#conditions-loops)는 최고 수준의 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-106">[Conditions and loops](#conditions-loops) are now first-class actions.</span></span>
* <span data-ttu-id="98fb3-107">`dependsOn`를 대체하는 `runAfter` 속성이 있는 작업을 실행하기 위한 보다 정확한 정렬</span><span class="sxs-lookup"><span data-stu-id="98fb3-107">More precise ordering for running actions with the `runAfter` property, replacing `dependsOn`</span></span>

<span data-ttu-id="98fb3-108">2015년 8월 1일 미리 보기 스키마에서 2016년 6월 1일 스키마로 논리 앱을 업그레이드하려면 [업그레이드 섹션을 확인합니다.](##upgrade-your-schema)</span><span class="sxs-lookup"><span data-stu-id="98fb3-108">To upgrade your logic apps from the August 1, 2015 preview schema to the June 1, 2016 schema, [check out the upgrade section](##upgrade-your-schema).</span></span>

<a name="scopes"></a>
## <a name="scopes"></a><span data-ttu-id="98fb3-109">범위</span><span class="sxs-lookup"><span data-stu-id="98fb3-109">Scopes</span></span>

<span data-ttu-id="98fb3-110">이 스키마는 작업을 함께 그룹화하거나 작업을 서로 중첩시킬 수 있는 범위를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-110">This schema includes scopes, which let you group actions together, or nest actions inside each other.</span></span> <span data-ttu-id="98fb3-111">예를 들어 조건은 다른 조건을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-111">For example, a condition can contain another condition.</span></span> <span data-ttu-id="98fb3-112">[범위 구문](../logic-apps/logic-apps-loops-and-scopes.md)에 대해 자세히 알아보거나 기본 범위 예제를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="98fb3-112">Learn more about [scope syntax](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic scope example:</span></span>

```
{
    "actions": {
        "My_Scope": {
            "type": "scope",
            "actions": {                
                "Http": {
                    "inputs": {
                        "method": "GET",
                        "uri": "http://www.bing.com"
                    },
                    "runAfter": {},
                    "type": "Http"
                }
            }
        }
    }
}
```

<a name="conditions-loops"></a>
## <a name="conditions-and-loops-changes"></a><span data-ttu-id="98fb3-113">조건 및 루프 변경</span><span class="sxs-lookup"><span data-stu-id="98fb3-113">Conditions and loops changes</span></span>

<span data-ttu-id="98fb3-114">이전 버전의 스키마에서 조건과 루프는 단일 작업과 관련된 매개 변수였습니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-114">In previous schema versions, conditions and loops were parameters associated with a single action.</span></span> <span data-ttu-id="98fb3-115">이 스키마는 이 제한 사항을 해제하므로 조건과 루프가 작업 유형으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-115">This schema lifts this limitation, so conditions and loops now appear as action types.</span></span> <span data-ttu-id="98fb3-116">[루프 및 범위](../logic-apps/logic-apps-loops-and-scopes.md)에 대해 자세히 알아보거나 조건 작업에 대한 기본 예제를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="98fb3-116">Learn more about [loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic example for a condition action:</span></span>

```
{
    "If_trigger_is_some-trigger": {
        "type": "If",
        "expression": "@equals(triggerBody(), 'some-trigger')",
        "runAfter": { },
        "actions": {
            "Http_2": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://www.bing.com"
                },
                "runAfter": {},
                "type": "Http"
            }
        },
        "else": 
        {
            "if_trigger_is_another-trigger": "..."
        }      
    }
}
```

<a name="run-after"></a>
## <a name="runafter-property"></a><span data-ttu-id="98fb3-117">'runAfter' 속성</span><span class="sxs-lookup"><span data-stu-id="98fb3-117">'runAfter' property</span></span>

<span data-ttu-id="98fb3-118">`runAfter` 속성은 `dependsOn`을 대체하며 이전 작업의 상태에 따라 작업의 실행 순서를 지정할 때 더 높은 정확도를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-118">The `runAfter` property replaces `dependsOn`, providing more precision when you specify the run order for actions based on the status of previous actions.</span></span>

<span data-ttu-id="98fb3-119">`dependsOn` 속성은 이전 작업을 성공하거나 실패 또는 건너뛰었는지에 따라 작업을 몇 번 실행하려는지에 관계 없이 "작업을 실행하고 성공했습니다"와 동의어입니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-119">The `dependsOn` property was synonymous with "the action ran and was successful", no matter how many times you wanted to execute an action, based on whether the previous action was successful, failed, or skipped.</span></span> <span data-ttu-id="98fb3-120">`runAfter` 속성은 개체가 실행된 후 모든 작업 이름을 지정하는 개체로 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-120">The `runAfter` property provides that flexibility as an object that specifies all the action names after which the object runs.</span></span> <span data-ttu-id="98fb3-121">또한 이 속성은 트리거로 허용 가능한 상태 배열도 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-121">This property also defines an array of statuses that are acceptable as triggers.</span></span> <span data-ttu-id="98fb3-122">예를 들어 A단계가 성공하고 B단계가 성공하거나 실패한 후에 실행하려는 경우 이 `runAfter` 속성을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-122">For example, if you wanted to run after step A succeeds and also after step B succeeds or fails, you construct this `runAfter` property:</span></span>

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a><span data-ttu-id="98fb3-123">스키마 업그레이드</span><span class="sxs-lookup"><span data-stu-id="98fb3-123">Upgrade your schema</span></span>

<span data-ttu-id="98fb3-124">새롭게 스키마로 업그레이드하려면 몇 가지 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-124">Upgrading to the new schema only takes a few steps.</span></span> <span data-ttu-id="98fb3-125">업그레이드 프로세스에는 업그레이드 스크립트를 실행하고 새 논리 앱으로 저장하며 원하는 경우 잠재적으로 이전 논리 앱을 덮어쓰는 과정이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-125">The upgrade process includes running the upgrade script, saving as a new logic app, and if you want, possibly overwriting the previous logic app.</span></span>

1. <span data-ttu-id="98fb3-126">Azure Portal에서 논리 앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-126">In the Azure portal, open your logic app.</span></span>

2. <span data-ttu-id="98fb3-127">**개요**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-127">Go to **Overview**.</span></span> <span data-ttu-id="98fb3-128">논리 앱 도구 모음에서 **스키마 업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-128">On the logic app toolbar, choose **Update Schema**.</span></span>
   
    ![스키마 업데이트 선택][1]
   
    <span data-ttu-id="98fb3-130">업그레이드된 정의가 반환되며 필요할 경우 리소스 정의에 복사 및 붙여넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-130">The upgraded definition is returned, which you can copy and paste into a resource definition if necessary.</span></span> 
    <span data-ttu-id="98fb3-131">하지만 업그레이드된 논리 앱에서 모든 연결 참조가 유효하도록 **다른 이름으로 저장**을 사용하는 것이 **좋습니다**.</span><span class="sxs-lookup"><span data-stu-id="98fb3-131">However, we **strongly recommend** you choose **Save As** to make sure that all connection references are valid in the upgraded logic app.</span></span>

3. <span data-ttu-id="98fb3-132">업그레이드 블레이드 도구 모음에서 **다른 이름으로 저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-132">In the upgrade blade toolbar, choose **Save As**.</span></span>

4. <span data-ttu-id="98fb3-133">논리 앱 및 상태를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-133">Enter the logic name and status.</span></span> <span data-ttu-id="98fb3-134">업그레이드된 논리 앱을 배포하려면 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-134">To deploy your upgraded logic app, choose **Create**.</span></span>

5. <span data-ttu-id="98fb3-135">업그레이드된 논리 앱이 예상대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-135">Confirm that your upgraded logic app works as expected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="98fb3-136">수동 또는 요청 트리거를 사용하는 경우 콜백 URL이 새 논리 앱에서 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-136">If you are using a manual or request trigger, the callback URL changes in your new logic app.</span></span> <span data-ttu-id="98fb3-137">새 URL을 테스트하여 종단 간 환경이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-137">Test the new URL to make sure the end-to-end experience works.</span></span> <span data-ttu-id="98fb3-138">이전 URL을 유지하기 위해 기존 논리 앱에 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-138">To preserve previous URLs, you can clone over your existing logic app.</span></span>

6. <span data-ttu-id="98fb3-139">*선택 사항* 이전 논리 앱을 새 스키마 버전으로 덮어쓰려면 도구 모음에서 **스키마 업데이트** 옆에 있는 **복제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-139">*Optional* To overwrite your previous logic app with the new schema version, on the toolbar, choose **Clone**, next to **Update Schema**.</span></span> <span data-ttu-id="98fb3-140">동일한 리소스 ID를 유지하거나 논리 앱의 트리거 URL을 요청하려는 경우에만 이 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-140">This step is necessary only if you want to keep the same resource ID or request trigger URL of your logic app.</span></span>

### <a name="upgrade-tool-notes"></a><span data-ttu-id="98fb3-141">업그레이드 도구 정보</span><span class="sxs-lookup"><span data-stu-id="98fb3-141">Upgrade tool notes</span></span>

#### <a name="mapping-conditions"></a><span data-ttu-id="98fb3-142">매핑 조건</span><span class="sxs-lookup"><span data-stu-id="98fb3-142">Mapping conditions</span></span>

<span data-ttu-id="98fb3-143">업그레이드된 정의에서 도구는 true 및 false 분기 작업을 범위로 함께 그룹화하는 최고의 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-143">In the upgraded definition, the tool makes a best effort at grouping true and false branch actions together as a scope.</span></span> <span data-ttu-id="98fb3-144">특히 디자이너 패턴 `@equals(actions('a').status, 'Skipped')`은 `else` 작업으로 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-144">Specifically, the designer pattern of `@equals(actions('a').status, 'Skipped')` should appear as an `else` action.</span></span> <span data-ttu-id="98fb3-145">그러나 이 도구가 인식할 수 없는 패턴을 검색하는 경우 true와 false 분기 모두에 별도의 조건을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-145">However, if the tool detects unrecognizable patterns, the tool might create separate conditions for both the true and the false branch.</span></span> <span data-ttu-id="98fb3-146">필요에 따라 업그레이드 후 작업을 다시 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-146">You can remap actions after upgrading, if necessary.</span></span>

#### <a name="foreach-loop-with-condition"></a><span data-ttu-id="98fb3-147">조건이 있는 'foreach' 루프</span><span class="sxs-lookup"><span data-stu-id="98fb3-147">'foreach' loop with condition</span></span>

<span data-ttu-id="98fb3-148">새 스키마에서는 필터 작업을 사용하여 `foreach` 루프의 패턴을 항목당 조건으로 복제할 수 있지만 이러한 변경은 업그레이드할 때 자동으로 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-148">In the new schema, you can use the filter action to replicate the pattern of a `foreach` loop with a condition per item, but this change should automatically happen when you upgrade.</span></span> <span data-ttu-id="98fb3-149">조건은 조건과 일치하는 항목의 배열만 반환하는 foreach 루프 이전에 필터 동작이 되고 해당 배열은 foreach 작업으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-149">The condition becomes a filter action before the foreach loop for returning only an array of items that match the condition, and that array is passed into the foreach action.</span></span> <span data-ttu-id="98fb3-150">이에 대한 예제는 [루프 및 범위](../logic-apps/logic-apps-loops-and-scopes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98fb3-150">For an example, see [Loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md).</span></span>

#### <a name="resource-tags"></a><span data-ttu-id="98fb3-151">리소스 태그</span><span class="sxs-lookup"><span data-stu-id="98fb3-151">Resource tags</span></span>

<span data-ttu-id="98fb3-152">업그레이드한 후에는 리소스 태그가 제거되므로 업그레이드된 워크플로에 대해 재설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-152">After you upgrade, resource tags are removed, so you must reset them for the upgraded workflow.</span></span>

## <a name="other-changes"></a><span data-ttu-id="98fb3-153">기타 변경 내용</span><span class="sxs-lookup"><span data-stu-id="98fb3-153">Other changes</span></span>

### <a name="renamed-manual-trigger-to-request-trigger"></a><span data-ttu-id="98fb3-154">'manual' 트리거를 'request' 트리거로 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="98fb3-154">Renamed 'manual' trigger to 'request' trigger</span></span>

<span data-ttu-id="98fb3-155">`manual` 트리거 형식이 사용되지 않고 `http` 종류를 사용하여 이름이 `request`로 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-155">The `manual` trigger type was deprecated and renamed to `request` with type `http`.</span></span> <span data-ttu-id="98fb3-156">이러한 변경은 트리거가 구축하는 데 사용되는 패턴의 종류와 더욱 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-156">This change creates more consistency for the kind of pattern that the trigger is used to build.</span></span>

### <a name="new-filter-action"></a><span data-ttu-id="98fb3-157">새 '필터' 작업</span><span class="sxs-lookup"><span data-stu-id="98fb3-157">New 'filter' action</span></span>

<span data-ttu-id="98fb3-158">대규모 배열을 소규모 항목 집합으로 하위 필터링하려면 새 `filter` 형식은 배열 및 조건을 허용하고 각 항목에 대해 조건을 평가한 후 해당 조건에 맞는 항목이 포함된 배열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-158">To filter a large array down to a smaller set of items, the new `filter` type accepts an array and a condition, evaluates the condition for each item, and returns an array with items meeting the condition.</span></span>

### <a name="restrictions-for-foreach-and-until-actions"></a><span data-ttu-id="98fb3-159">'foreach' 및 'until' 작업에 대한 제한 사항</span><span class="sxs-lookup"><span data-stu-id="98fb3-159">Restrictions for 'foreach' and 'until' actions</span></span>

<span data-ttu-id="98fb3-160">`foreach` 및 `until` 루프는 한 번의 작업으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-160">The `foreach` and `until` loop are restricted to a single action.</span></span>

### <a name="new-trackedproperties-for-actions"></a><span data-ttu-id="98fb3-161">작업에 대한 새 'trackedProperties'</span><span class="sxs-lookup"><span data-stu-id="98fb3-161">New 'trackedProperties' for actions</span></span>

<span data-ttu-id="98fb3-162">작업에는 `runAfter` 및 `type` 속성의 형제인 `trackedProperties`이라는 추가 속성이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-162">Actions can now have an additional property called `trackedProperties`, which is sibling to the `runAfter` and `type` properties.</span></span> <span data-ttu-id="98fb3-163">이 개체는 워크플로의 일부로 내보내고 Azure 진단 원격 분석에 포함할 특정 작업 입력 또는 출력을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="98fb3-163">This object specifies certain action inputs or outputs that you want to include in the Azure Diagnostic telemetry, emitted as part of a workflow.</span></span> <span data-ttu-id="98fb3-164">예:</span><span class="sxs-lookup"><span data-stu-id="98fb3-164">For example:</span></span>

```
{                
    "Http": {
        "inputs": {
            "method": "GET",
            "uri": "http://www.bing.com"
        },
        "runAfter": {},
        "type": "Http",
        "trackedProperties": {
            "responseCode": "@action().outputs.statusCode",
            "uri": "@action().inputs.uri"
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="98fb3-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="98fb3-165">Next Steps</span></span>
* [<span data-ttu-id="98fb3-166">논리 앱용 워크플로 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="98fb3-166">Create workflow definitions for logic apps</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="98fb3-167">논리 앱용 배포 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="98fb3-167">Create deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
