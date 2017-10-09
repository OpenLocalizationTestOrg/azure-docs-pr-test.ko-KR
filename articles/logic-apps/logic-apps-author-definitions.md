---
title: "json-Azure 논리 앱 워크플로 aaaDefine | Microsoft Docs"
description: "어떻게 논리 앱에 대 한 json에서 toowrite 워크플로 정의"
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
ms.openlocfilehash: 0d69d334ecee9c3e7f8684cfde68ef0e85280358
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a><span data-ttu-id="e0d1f-103">JSON을 사용하여 논리 앱용 워크플로 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="e0d1f-103">Create workflow definitions for logic apps using JSON</span></span>

<span data-ttu-id="e0d1f-104">간단하고 선언적인 JSON 언어로 [Azure Logic Apps](logic-apps-what-are-logic-apps.md)에 대한 워크플로 정의를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-104">You can create workflow definitions for [Azure Logic Apps](logic-apps-what-are-logic-apps.md) with simple, declarative JSON language.</span></span> <span data-ttu-id="e0d1f-105">아직 하지 않는 경우 먼저 검토 [어떻게 toocreate 논리가 응용 프로그램 디자이너를 사용 하 여 첫 번째 논리 앱](logic-apps-create-a-logic-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-105">If you haven't already, first review [how toocreate your first logic app with Logic App Designer](logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="e0d1f-106">참고: hello [hello 워크플로 정의 언어에 대 한 참조를 전체](http://aka.ms/logicappsdocs)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-106">Also, see hello [full reference for hello Workflow Definition Language](http://aka.ms/logicappsdocs).</span></span>

## <a name="repeat-steps-over-a-list"></a><span data-ttu-id="e0d1f-107">목록에 대한 단계 반복</span><span class="sxs-lookup"><span data-stu-id="e0d1f-107">Repeat steps over a list</span></span>

<span data-ttu-id="e0d1f-108">가 too10, 000 항목 최대 고 각 항목에 대 한 작업 수행을 hello를 사용 하 여 배열 통한 tooiterate [foreach 유형](logic-apps-loops-and-scopes.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-108">tooiterate through an array that has up too10,000 items and perform an action for each item, use hello [foreach type](logic-apps-loops-and-scopes.md).</span></span>

## <a name="handle-failures-if-something-goes-wrong"></a><span data-ttu-id="e0d1f-109">문제가 발생한 경우의 오류 처리</span><span class="sxs-lookup"><span data-stu-id="e0d1f-109">Handle failures if something goes wrong</span></span>

<span data-ttu-id="e0d1f-110">원하는 tooinclude 일반적으로 *재구성 단계* -를 실행 하는 일부 논리 *경우에* 하나 이상의 호출이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-110">Usually, you want tooinclude a *remediation step* — some logic that executes *if and only if* one or more of your calls fail.</span></span> <span data-ttu-id="e0d1f-111">이 예제에서는 다양 한 위치에서 데이터를 가져옵니다 하지만 hello 호출이 실패 한 경우 원하는 tooPOST 메시지 어딘가에 나중에 해당 오류를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-111">This example gets data from various places, but if hello call fails, we want tooPOST a message somewhere so we can track down that failure later:</span></span>  

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

<span data-ttu-id="e0d1f-112">toospecify 하 `postToErrorMessageQueue` 에 실행 `readData` 가 `Failed`, hello를 사용 하 여 `runAfter` 속성에 가능한 값 목록은 toospecify 예를 들어 있도록 `runAfter` 수 `["Succeeded", "Failed"]`합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-112">toospecify that `postToErrorMessageQueue` only runs after `readData` has `Failed`, use hello `runAfter` property, for example, toospecify a list of possible values, so that `runAfter` could be `["Succeeded", "Failed"]`.</span></span>

<span data-ttu-id="e0d1f-113">마지막으로,이 예제에서는 이제 hello 오류를 처리 하기 때문에에서는 더 이상 표시로 실행 하는 hello `Failed`합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-113">Finally, because this example now handles hello error, we no longer mark hello run as `Failed`.</span></span> <span data-ttu-id="e0d1f-114">이 예제에서이 오류를 처리 하기 위한 hello 단계를 추가 했습니다 있기 때문에 실행 하는 hello 포함 `Succeeded` 있지만 한 번 `Failed`합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-114">Because we added hello step for handling this failure in this example, hello run has `Succeeded` although one step `Failed`.</span></span>

## <a name="execute-two-or-more-steps-in-parallel"></a><span data-ttu-id="e0d1f-115">둘 이상의 단계를 병렬로 실행</span><span class="sxs-lookup"><span data-stu-id="e0d1f-115">Execute two or more steps in parallel</span></span>

<span data-ttu-id="e0d1f-116">toorun 병렬로 여러 동작 hello `runAfter` 속성이 런타임 시 동등한 형식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-116">toorun multiple actions in parallel, hello `runAfter` property must be equivalent at runtime.</span></span> 

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

<span data-ttu-id="e0d1f-117">이 예제에서는 모두 `branch1` 및 `branch2` 후 toorun 설정 `readData`합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-117">In this example, both `branch1` and `branch2` are set toorun after `readData`.</span></span> <span data-ttu-id="e0d1f-118">따라서 두 분기가 병렬로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-118">As a result, both branches run in parallel.</span></span> <span data-ttu-id="e0d1f-119">양쪽 분기에 대 한 hello 타임 스탬프는 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-119">hello timestamp for both branches is identical.</span></span>

![병렬](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a><span data-ttu-id="e0d1f-121">두 병렬 분기의 조인</span><span class="sxs-lookup"><span data-stu-id="e0d1f-121">Join two parallel branches</span></span>

<span data-ttu-id="e0d1f-122">항목 toohello를 추가 하 여 toorun 동시에 설정 된 두 가지 동작을 조인할 수 `runAfter` hello 이전 예제와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-122">You can join two actions that are set toorun in parallel by adding items toohello `runAfter` property as in hello previous example.</span></span>

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

## <a name="map-list-items-tooa-different-configuration"></a><span data-ttu-id="e0d1f-124">맵 목록 항목 tooa 다른 구성</span><span class="sxs-lookup"><span data-stu-id="e0d1f-124">Map list items tooa different configuration</span></span>

<span data-ttu-id="e0d1f-125">그런 다음, hello 속성 값에 따라 tooget 다른 내용을 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-125">Next, let's say that we want tooget different content based on hello value of a property.</span></span> <span data-ttu-id="e0d1f-126">매개 변수로 값 toodestinations의 맵을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-126">We can create a map of values toodestinations as a parameter:</span></span>  

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

<span data-ttu-id="e0d1f-127">이 경우 먼저 문서 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-127">In this case, we first get a list of articles.</span></span> <span data-ttu-id="e0d1f-128">매개 변수로 정의 된 hello 범주에 따라, 두 번째 단계 hello hello 콘텐츠를 가져오기 위한 hello URL 맵 toolook를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-128">Based on hello category that was defined as a parameter, hello second step uses a map toolook up hello URL for getting hello content.</span></span>

<span data-ttu-id="e0d1f-129">일부 시간 toonote:</span><span class="sxs-lookup"><span data-stu-id="e0d1f-129">Some times toonote here:</span></span> 

*   <span data-ttu-id="e0d1f-130">hello [ `intersection()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) 함수 hello 범주 hello 알려진 정의 된 범주 중 하 나와 일치 하는 지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-130">hello [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) function checks whether hello category matches one of hello known defined categories.</span></span>

*   <span data-ttu-id="e0d1f-131">Hello 범주 구했습니다 후 대괄호를 사용 하 여 hello 맵에서 hello 항목을 끌어올 수 있습니다.`parameters[...]`</span><span class="sxs-lookup"><span data-stu-id="e0d1f-131">After we get hello category, we can pull hello item from hello map using square brackets: `parameters[...]`</span></span>

## <a name="process-strings"></a><span data-ttu-id="e0d1f-132">문자열 처리</span><span class="sxs-lookup"><span data-stu-id="e0d1f-132">Process strings</span></span>

<span data-ttu-id="e0d1f-133">다양 한 기능 toomanipulate 문자열을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-133">You can use various functions toomanipulate strings.</span></span> <span data-ttu-id="e0d1f-134">예를 들어 toopass tooa 시스템 원하는 하지만 문자 인코딩에 대 한 적절 한 처리에 대 한 확신 하지 못해 문자열로 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-134">For example, suppose we have a string that we want toopass tooa system, but we aren't confident about proper handling for character encoding.</span></span> <span data-ttu-id="e0d1f-135">한 가지 방법은 toobase64이이 문자열을 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-135">One option is toobase64 encode this string.</span></span> <span data-ttu-id="e0d1f-136">그러나 URL에서 이스케이프 tooavoid 하겠습니다 tooreplace 일부 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-136">However, tooavoid escaping in a URL, we are going tooreplace a few characters.</span></span> 

<span data-ttu-id="e0d1f-137">또한 hello 처음 5 문자가 사용 되지 않는 있으므로 hello 순서 이름 부분 문자열이 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-137">We also want a substring of hello order's name because hello first five characters are not used.</span></span>

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

<span data-ttu-id="e0d1f-138">Toooutside 내에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-138">Working from inside toooutside:</span></span>

1. <span data-ttu-id="e0d1f-139">Hello 가져오기 [ `length()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) hello orderer 이름에 대 한 하므로 구했습니다 다시 hello 총 문자 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-139">Get hello [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) for hello orderer's name, so we get back hello total number of characters.</span></span>

2. <span data-ttu-id="e0d1f-140">더 짧은 문자열을 원하므로 5를 뺍니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-140">Subtract 5 because we want a shorter string.</span></span>

3. <span data-ttu-id="e0d1f-141">Hello, 내용이 [ `substring()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-141">Actually, take hello [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span></span> <span data-ttu-id="e0d1f-142">인덱스에서 시작 `5` hello hello 문자열의 나머지 부분을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-142">We start at index `5` and go hello remainder of hello string.</span></span>

4. <span data-ttu-id="e0d1f-143">이 부분 문자열 tooa 변환 [ `base64()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-143">Convert this substring tooa [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) string.</span></span>

5. <span data-ttu-id="e0d1f-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)모든 hello `+` 와 문자 `-` 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all hello `+` characters with `-` characters.</span></span>

6. <span data-ttu-id="e0d1f-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)모든 hello `/` 와 문자 `_` 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all hello `/` characters with `_` characters.</span></span>

## <a name="work-with-date-times"></a><span data-ttu-id="e0d1f-146">날짜 시간을 사용한 작업</span><span class="sxs-lookup"><span data-stu-id="e0d1f-146">Work with Date Times</span></span>

<span data-ttu-id="e0d1f-147">날짜 시간 자연스럽 게 지원 하지 않는 데이터 원본의 toopull 데이터를 시도할 경우에 특히 유용할 수 있습니다 *트리거*합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-147">Date Times can be useful, particularly when you are trying toopull data from a data source that doesn't naturally support *triggers*.</span></span> <span data-ttu-id="e0d1f-148">날짜 시간은 다양한 단계에 소요되는 시간을 파악하는 데에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-148">You can also use Date Times for finding how long various steps are taking.</span></span>

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

<span data-ttu-id="e0d1f-149">이 예제에서는 hello 추출 `startTime` hello 이전 단계에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-149">In this example, we extract hello `startTime` from hello previous step.</span></span> <span data-ttu-id="e0d1f-150">그런 다음 hello 현재 시간을 가져올 하 고 1 초를 뺍니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-150">Then we get hello current time, and subtract one second:</span></span>

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

<span data-ttu-id="e0d1f-151">`minutes` 또는 `hours`와 같은 다른 시간 단위를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-151">You can use other units of time, like `minutes` or `hours`.</span></span> <span data-ttu-id="e0d1f-152">마지막으로 이 두 값을 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-152">Finally, we can compare these two values.</span></span> <span data-ttu-id="e0d1f-153">Hello 첫 번째 값이 2 초 이상 hello 두 번째 값 보다 작으면 경과한 hello 먼저 주문을 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-153">If hello first value is less than hello second value, then more than one second has passed since hello order was first placed.</span></span>

<span data-ttu-id="e0d1f-154">tooformat 날짜, 문자열 포맷터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-154">tooformat dates, we can use string formatters.</span></span> <span data-ttu-id="e0d1f-155">예를 들어, tooget hello RFC1123 사용 하 여 [ `utcnow('r')` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-155">For example, tooget hello RFC1123, we use [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span> <span data-ttu-id="e0d1f-156">날짜 서식 지정에 대 한 toolearn 참조 [워크플로 정의 언어](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-156">toolearn about date formatting, see [Workflow Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span>

## <a name="deployment-parameters-for-different-environments"></a><span data-ttu-id="e0d1f-157">다른 환경에 대한 배포 매개 변수</span><span class="sxs-lookup"><span data-stu-id="e0d1f-157">Deployment parameters for different environments</span></span>

<span data-ttu-id="e0d1f-158">일반적으로 배포 주기는 배포 환경, 스테이징 환경 및 프로덕션 환경으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-158">Commonly, deployment lifecycles have a development environment, a staging environment, and a production environment.</span></span> <span data-ttu-id="e0d1f-159">예를 들어 사용할 수 있습니다 이러한 환경 모두에서 동일한 정의 hello 하지만 서로 다른 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-159">For example, you might use hello same definition in all these environments but use different databases.</span></span> <span data-ttu-id="e0d1f-160">마찬가지로, toouse 경우가 고가용성에 대 한 서로 다른 영역에서 동일한 정의 hello 하지만 각 논리 앱 인스턴스 tootalk toothat 지역의 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-160">Likewise, you might want toouse hello same definition across different regions for high availability but want each logic app instance tootalk toothat region's database.</span></span>
<span data-ttu-id="e0d1f-161">이 시나리오에서 매개 변수에서 다른 *런타임* 를 대신 사용 해야 hello `trigger()` hello 이전 예제와 같이 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-161">This scenario differs from taking parameters at *runtime* where instead, you should use hello `trigger()` function as in hello previous example.</span></span>

<span data-ttu-id="e0d1f-162">다음 예제와 같은 기본적인 정의로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-162">You can start with a basic definition like this example:</span></span>

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

<span data-ttu-id="e0d1f-163">실제 hello에 `PUT` hello 매개 변수를 제공할 수 있습니다 hello 논리 앱에 대 한 요청 `uri`합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-163">In hello actual `PUT` request for hello logic apps, you can provide hello parameter `uri`.</span></span> <span data-ttu-id="e0d1f-164">기본값을 더 이상 존재 하기 때문에이 매개 변수를 hello 논리가 응용 프로그램 페이로드에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-164">Because a default value no longer exists, hello logic app payload requires this parameter:</span></span>

```
{
    "properties": {},
        "definition": {
          // Use hello definition from above here
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

<span data-ttu-id="e0d1f-165">각 환경에 hello에 대 한 다른 값을 제공할 수 있습니다 `connection` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-165">In each environment, you can provide a different value for hello `connection` parameter.</span></span> 

<span data-ttu-id="e0d1f-166">만들기 및 논리 앱 관리에 대 한 옵션을 hello 모든 hello 참조 [REST API 문서](https://msdn.microsoft.com/library/azure/mt643787.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d1f-166">For all hello options that you have for creating and managing logic apps, see hello [REST API documentation](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span></span> 
