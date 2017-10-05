---
title: "JSON으로 워크플로 정의 - Azure Logic Apps | Microsoft Docs"
description: "JSON에서 논리 앱용 워크플로 정의를 작성하는 방법"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 03/29/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 7f9e5a10066df8a464c285273e77a85c0d562ebb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a><span data-ttu-id="4a3e5-103">JSON을 사용하여 논리 앱용 워크플로 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="4a3e5-103">Create workflow definitions for logic apps using JSON</span></span>

<span data-ttu-id="4a3e5-104">간단하고 선언적인 JSON 언어로 [Azure Logic Apps](logic-apps-what-are-logic-apps.md)에 대한 워크플로 정의를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-104">You can create workflow definitions for [Azure Logic Apps](logic-apps-what-are-logic-apps.md) with simple, declarative JSON language.</span></span> <span data-ttu-id="4a3e5-105">아직 없는 경우 [Logic App Designer에서 첫 번째 논리 앱을 만드는 방법](logic-apps-create-a-logic-app.md)을 먼저 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-105">If you haven't already, first review [how to create your first logic app with Logic App Designer](logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="4a3e5-106">또한 [워크플로 정의 언어에 대한 전체 참조](http://aka.ms/logicappsdocs)도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-106">Also, see the [full reference for the Workflow Definition Language](http://aka.ms/logicappsdocs).</span></span>

## <a name="repeat-steps-over-a-list"></a><span data-ttu-id="4a3e5-107">목록에 대한 단계 반복</span><span class="sxs-lookup"><span data-stu-id="4a3e5-107">Repeat steps over a list</span></span>

<span data-ttu-id="4a3e5-108">최대 10,000개의 항목이 포함된 배열을 반복하고 각 항목에 대해 작업을 수행하고 [foreach 형식](logic-apps-loops-and-scopes.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-108">To iterate through an array that has up to 10,000 items and perform an action for each item, use the [foreach type](logic-apps-loops-and-scopes.md).</span></span>

## <a name="handle-failures-if-something-goes-wrong"></a><span data-ttu-id="4a3e5-109">문제가 발생한 경우의 오류 처리</span><span class="sxs-lookup"><span data-stu-id="4a3e5-109">Handle failures if something goes wrong</span></span>

<span data-ttu-id="4a3e5-110">일반적으로 하나 이상의 호출이 실패한 *경우에 한해* 일부 논리를 실행하는 *재구성 단계*를 포함하기를 원합니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-110">Usually, you want to include a *remediation step* — some logic that executes *if and only if* one or more of your calls fail.</span></span> <span data-ttu-id="4a3e5-111">이 예제에서는 다양한 위치에서 데이터를 가져오지만 호출이 실패한 경우에는 나중에 오류를 추적할 수 있는 곳에 메시지를 게시하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-111">This example gets data from various places, but if the call fails, we want to POST a message somewhere so we can track down that failure later:</span></span>  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "postToErrorMessageQueue": {
      "type": "ApiConnection",
      "inputs": "...",
      "runAfter": {
        "readData": [
          "Failed"
        ]
      }
    }
  },
  "outputs": {}
}
```

<span data-ttu-id="4a3e5-112">`readData`가 `Failed`한 후에만 `postToErrorMessageQueue`가 실행되도록 지정하려면 `runAfter` 속성을 사용합니다. 예를 들어 가능한 값 목록을 지정하려면 `runAfter`는 `["Succeeded", "Failed"]`일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-112">To specify that `postToErrorMessageQueue` only runs after `readData` has `Failed`, use the `runAfter` property, for example, to specify a list of possible values, so that `runAfter` could be `["Succeeded", "Failed"]`.</span></span>

<span data-ttu-id="4a3e5-113">마지막으로, 이제 오류를 처리했으므로 더 이상 실행을 `Failed`로 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-113">Finally, because this example now handles the error, we no longer mark the run as `Failed`.</span></span> <span data-ttu-id="4a3e5-114">이 예제에서는 오류 처리를 위한 단계를 추가했으므로 한 단계가 `Failed`하더라도 실행은 `Succeeded`합니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-114">Because we added the step for handling this failure in this example, the run has `Succeeded` although one step `Failed`.</span></span>

## <a name="execute-two-or-more-steps-in-parallel"></a><span data-ttu-id="4a3e5-115">둘 이상의 단계를 병렬로 실행</span><span class="sxs-lookup"><span data-stu-id="4a3e5-115">Execute two or more steps in parallel</span></span>

<span data-ttu-id="4a3e5-116">여러 작업을 병렬로 실행하려면 `runAfter` 속성은 런타임 시 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-116">To run multiple actions in parallel, the `runAfter` property must be equivalent at runtime.</span></span> 

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "kind": "http",
      "type": "Request"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

<span data-ttu-id="4a3e5-117">이 예제에서는 `branch1` 및 `branch2` 모두 `readData` 후에 실행되도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-117">In this example, both `branch1` and `branch2` are set to run after `readData`.</span></span> <span data-ttu-id="4a3e5-118">따라서 두 분기가 병렬로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-118">As a result, both branches run in parallel.</span></span> <span data-ttu-id="4a3e5-119">두 분기에 대한 타임스탬프는 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-119">The timestamp for both branches is identical.</span></span>

![병렬](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a><span data-ttu-id="4a3e5-121">두 병렬 분기의 조인</span><span class="sxs-lookup"><span data-stu-id="4a3e5-121">Join two parallel branches</span></span>

<span data-ttu-id="4a3e5-122">이전 예제에서처럼 `runAfter` 속성에 항목을 추가하여 병렬로 실행하도록 설정된 두 가지 작업을 조인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-122">You can join two actions that are set to run in parallel by adding items to the `runAfter` property as in the previous example.</span></span>

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-04-01-preview/workflowdefinition.json#",
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {}
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "join": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "branch1": [
          "Succeeded"
        ],
        "branch2": [
          "Succeeded"
        ]
      }
    }
  },
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "Http",
      "inputs": {
        "schema": {}
      }
    }
  },
  "contentVersion": "1.0.0.0",
  "outputs": {}
}
```

![병렬](media/logic-apps-author-definitions/join.png)

## <a name="map-list-items-to-a-different-configuration"></a><span data-ttu-id="4a3e5-124">목록 항목을 다른 구성에 매핑</span><span class="sxs-lookup"><span data-stu-id="4a3e5-124">Map list items to a different configuration</span></span>

<span data-ttu-id="4a3e5-125">다음으로 속성의 값을 기반으로 다른 콘텐츠를 가져오는 경우를 다루겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-125">Next, let's say that we want to get different content based on the value of a property.</span></span> <span data-ttu-id="4a3e5-126">매개 변수를 대상으로 하는 값의 맵을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-126">We can create a map of values to destinations as a parameter:</span></span>  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "specialCategories": {
      "defaultValue": [
        "science",
        "google",
        "microsoft",
        "robots",
        "NSA"
      ],
      "type": "Array"
    },
    "destinationMap": {
      "defaultValue": {
        "science": "http://www.nasa.gov",
        "microsoft": "https://www.microsoft.com/en-us/default.aspx",
        "google": "https://www.google.com",
        "robots": "https://en.wikipedia.org/wiki/Robot",
        "NSA": "https://www.nsa.gov/"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "http"
    }
  },
  "actions": {
    "getArticles": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "https://ajax.googleapis.com/ajax/services/feed/load?v=1.0&q=http://feeds.wired.com/wired/index"
      }
    },
    "forEachArticle": {
      "type": "foreach",
      "foreach": "@body('getArticles').responseData.feed.entries",
      "actions": {
        "ifGreater": {
          "type": "if",
          "expression": "@greater(length(intersection(item().categories, parameters('specialCategories'))), 0)",
          "actions": {
            "getSpecialPage": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('destinationMap')[first(intersection(item().categories, parameters('specialCategories')))]"
              }
            }
          }
        }
      },
      "runAfter": {
        "getArticles": [
          "Succeeded"
        ]
      }
    }
  }
}
```

<span data-ttu-id="4a3e5-127">이 경우 먼저 문서 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-127">In this case, we first get a list of articles.</span></span> <span data-ttu-id="4a3e5-128">매개 변수로 정의된 범주에 따라, 두 번째 단계에서는 콘텐츠를 가져오기 위한 URL을 조회하는 맵을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-128">Based on the category that was defined as a parameter, the second step uses a map to look up the URL for getting the content.</span></span>

<span data-ttu-id="4a3e5-129">경우에 따라 다음을 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-129">Some times to note here:</span></span> 

*   <span data-ttu-id="4a3e5-130">[`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) 함수는 해당 범주가 알려진 정의된 범주 중 하나와 일치하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-130">The [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) function checks whether the category matches one of the known defined categories.</span></span>

*   <span data-ttu-id="4a3e5-131">범주를 가져온 후에는 대괄호를 사용하여 맵에서 항목을 끌어올 수 있습니다. `parameters[...]`</span><span class="sxs-lookup"><span data-stu-id="4a3e5-131">After we get the category, we can pull the item from the map using square brackets: `parameters[...]`</span></span>

## <a name="process-strings"></a><span data-ttu-id="4a3e5-132">문자열 처리</span><span class="sxs-lookup"><span data-stu-id="4a3e5-132">Process strings</span></span>

<span data-ttu-id="4a3e5-133">문자열을 조작하기 위해 다양한 함수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-133">You can use various functions to manipulate strings.</span></span> <span data-ttu-id="4a3e5-134">예를 들어 시스템으로 전달하고자 하는 문자열이 있지만 문자 인코딩을 위한 적절한 처리에 자신이 없다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-134">For example, suppose we have a string that we want to pass to a system, but we aren't confident about proper handling for character encoding.</span></span> <span data-ttu-id="4a3e5-135">하나의 옵션은 이 문자열을 base64 인코딩하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-135">One option is to base64 encode this string.</span></span> <span data-ttu-id="4a3e5-136">그러나 URL에서 이스케이프를 방지하기 위해 몇 문자를 대체할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-136">However, to avoid escaping in a URL, we are going to replace a few characters.</span></span> 

<span data-ttu-id="4a3e5-137">또한 첫 5자는 사용되지 않으므로 명령 이름의 하위 문자열을 원합니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-137">We also want a substring of the order's name because the first five characters are not used.</span></span>

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1",
        "orderer": "NAME=Contoso"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{replace(replace(base64(substring(parameters('order').orderer,5,sub(length(parameters('order').orderer), 5) )),'+','-') ,'/' ,'_' )}"
      }
    }
  },
  "outputs": {}
}
```

<span data-ttu-id="4a3e5-138">내부에서 외부로 작업:</span><span class="sxs-lookup"><span data-stu-id="4a3e5-138">Working from inside to outside:</span></span>

1. <span data-ttu-id="4a3e5-139">명령자 이름의 [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length)를 가져오므로 전체 문자 수를 다시 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-139">Get the [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) for the orderer's name, so we get back the total number of characters.</span></span>

2. <span data-ttu-id="4a3e5-140">더 짧은 문자열을 원하므로 5를 뺍니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-140">Subtract 5 because we want a shorter string.</span></span>

3. <span data-ttu-id="4a3e5-141">실제로 [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring)을(를) 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-141">Actually, take the [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span></span> <span data-ttu-id="4a3e5-142">인덱스 `5` 에서 시작하여 문자열의 나머지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-142">We start at index `5` and go the remainder of the string.</span></span>

4. <span data-ttu-id="4a3e5-143">이 하위 문자열을 [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) 문자열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-143">Convert this substring to a [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) string.</span></span>

5. <span data-ttu-id="4a3e5-144">모든 `+` 문자를 `-` 문자로 [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)합니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all the `+` characters with `-` characters.</span></span>

6. <span data-ttu-id="4a3e5-145">모든 `/` 문자를 `_` 문자로 [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)합니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all the `/` characters with `_` characters.</span></span>

## <a name="work-with-date-times"></a><span data-ttu-id="4a3e5-146">날짜 시간을 사용한 작업</span><span class="sxs-lookup"><span data-stu-id="4a3e5-146">Work with Date Times</span></span>

<span data-ttu-id="4a3e5-147">날짜 시간은 자연스럽게 *트리거*를 지원하지 않는 데이터 원본에서 데이터를 가져오려고 할 때 특히 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-147">Date Times can be useful, particularly when you are trying to pull data from a data source that doesn't naturally support *triggers*.</span></span> <span data-ttu-id="4a3e5-148">날짜 시간은 다양한 단계에 소요되는 시간을 파악하는 데에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-148">You can also use Date Times for finding how long various steps are taking.</span></span>

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{parameters('order').id}"
      }
    },
    "ifTimingWarning": {
      "type": "If",
      "expression": "@less(actions('order').startTime,addseconds(utcNow(),-1))",
      "actions": {
        "timingWarning": {
          "type": "Http",
          "inputs": {
            "method": "GET",
            "uri": "http://www.example.com/?recordLongOrderTime=@{parameters('order').id}&currentTime=@{utcNow('r')}"
          }
        }
      },
      "runAfter": {
        "order": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

<span data-ttu-id="4a3e5-149">이 예제에서는 이전 단계의 `startTime`을(를) 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-149">In this example, we extract the `startTime` from the previous step.</span></span> <span data-ttu-id="4a3e5-150">그런 다음 현재 시간 가져오고 1초를 뺍니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-150">Then we get the current time, and subtract one second:</span></span>

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

<span data-ttu-id="4a3e5-151">`minutes` 또는 `hours`와 같은 다른 시간 단위를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-151">You can use other units of time, like `minutes` or `hours`.</span></span> <span data-ttu-id="4a3e5-152">마지막으로 이 두 값을 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-152">Finally, we can compare these two values.</span></span> <span data-ttu-id="4a3e5-153">첫 번째 값이 두 번째 값보다 작은 경우에는 명령이 처음으로 배치된 후 1초 이상의 시간이 경과된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-153">If the first value is less than the second value, then more than one second has passed since the order was first placed.</span></span>

<span data-ttu-id="4a3e5-154">날짜에 서식을 지정하려면 문자열 포맷터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-154">To format dates, we can use string formatters.</span></span> <span data-ttu-id="4a3e5-155">예를 들어 RFC1123을 얻으려면 [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-155">For example, to get the RFC1123, we use [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span> <span data-ttu-id="4a3e5-156">날짜 서식 지정에 대해 알아보려면 [워크플로 정의 언어](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-156">To learn about date formatting, see [Workflow Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span>

## <a name="deployment-parameters-for-different-environments"></a><span data-ttu-id="4a3e5-157">다른 환경에 대한 배포 매개 변수</span><span class="sxs-lookup"><span data-stu-id="4a3e5-157">Deployment parameters for different environments</span></span>

<span data-ttu-id="4a3e5-158">일반적으로 배포 주기는 배포 환경, 스테이징 환경 및 프로덕션 환경으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-158">Commonly, deployment lifecycles have a development environment, a staging environment, and a production environment.</span></span> <span data-ttu-id="4a3e5-159">예를 들어, 이러한 모든 환경에서 동일한 정의를 사용하지만 다른 데이터베이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-159">For example, you might use the same definition in all these environments but use different databases.</span></span> <span data-ttu-id="4a3e5-160">마찬가지로, 높은 가용성을 위해 다양한 하위 지역에 걸쳐 동일한 정의를 사용하고자 하지만 해당 하위 지역의 데이터베이스와 통신하는 각각의 논리 앱 인스턴스를 원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-160">Likewise, you might want to use the same definition across different regions for high availability but want each logic app instance to talk to that region's database.</span></span>
<span data-ttu-id="4a3e5-161">이 시나리오는 대신 *런타임*에 매개 변수를 사용하는 것과 다르며 이전 예제와 같이 `trigger()` 함수를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-161">This scenario differs from taking parameters at *runtime* where instead, you should use the `trigger()` function as in the previous example.</span></span>

<span data-ttu-id="4a3e5-162">다음 예제와 같은 기본적인 정의로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-162">You can start with a basic definition like this example:</span></span>

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "uri": {
            "type": "string"
        }
    },
    "triggers": {
        "request": {
          "type": "request",
          "kind": "http"
        }
    },
    "actions": {
        "readData": {
            "type": "Http",
            "inputs": {
                "method": "GET",
                "uri": "@parameters('uri')"
            }
        }
    },
    "outputs": {}
}
```

<span data-ttu-id="4a3e5-163">논리 앱에 대한 실제 `PUT` 요청에서 매개 변수 `uri`를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-163">In the actual `PUT` request for the logic apps, you can provide the parameter `uri`.</span></span> <span data-ttu-id="4a3e5-164">기본값이 더 이상 존재하지 않으므로 논리 앱 페이로드에 이 매개 변수가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-164">Because a default value no longer exists, the logic app payload requires this parameter:</span></span>

```
{
    "properties": {},
        "definition": {
          // Use the definition from above here
        },
        "parameters": {
            "connection": {
                "value": "https://my.connection.that.is.per.enviornment"
            }
        }
    },
    "location": "westus"
}
``` 

<span data-ttu-id="4a3e5-165">각 환경에서 `connection` 매개 변수에 대해 다른 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-165">In each environment, you can provide a different value for the `connection` parameter.</span></span> 

<span data-ttu-id="4a3e5-166">논리 앱 만들기 및 관리에 대해 포함할 모든 옵션은 [REST API 설명서](https://msdn.microsoft.com/library/azure/mt643787.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a3e5-166">For all the options that you have for creating and managing logic apps, see the [REST API documentation](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span></span> 
