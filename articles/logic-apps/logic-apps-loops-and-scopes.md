---
title: "워크플로에서 루프와 범위 만들기 및 데이터 분리 - Azure Logic Apps | Microsoft Docs"
description: "Azure Logic Apps에서 루프를 만들어 데이터를 반복하거나, 작업을 범위로 그룹화하거나, 데이터를 분리하여 더 많은 워크플로를 시작합니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 75b52eeb-23a7-47dd-a42f-1351c6dfebdc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 413a2ba9107ca259ed577825bf0a17ff5622f1ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="logic-apps-loops-scopes-and-debatching"></a><span data-ttu-id="81ad4-103">논리 앱 루프, 범위 및 분할</span><span class="sxs-lookup"><span data-stu-id="81ad4-103">Logic Apps Loops, Scopes, and Debatching</span></span>
  
<span data-ttu-id="81ad4-104">논리 앱은 워크플로 내에서 배열, 컬렉션, 일괄 처리 작업 및 루프를 다양한 방법으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-104">Logic Apps provides a number of ways to work with arrays, collections, batches, and loops within a workflow.</span></span>
  
## <a name="foreach-loop-and-arrays"></a><span data-ttu-id="81ad4-105">ForEach 루프 및 배열</span><span class="sxs-lookup"><span data-stu-id="81ad4-105">ForEach loop and arrays</span></span>
  
<span data-ttu-id="81ad4-106">논리 앱을 사용하면 데이터 집합을 반복하고 각 항목에 대해 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-106">Logic Apps allows you to loop over a set of data and perform an action for each item.</span></span>  <span data-ttu-id="81ad4-107">이는 `foreach` 작업을 통해 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-107">This is possible via the `foreach` action.</span></span>  <span data-ttu-id="81ad4-108">디자이너에서 ForEach 루프를 추가하도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-108">In the designer, you can specify to add a for each loop.</span></span>  <span data-ttu-id="81ad4-109">반복하려는 배열을 선택한 후 작업 추가를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-109">After selecting the array you wish to iterate over, you can begin adding actions.</span></span>  <span data-ttu-id="81ad4-110">현재는 ForEach 루프당 하나의 작업으로만 제한되지만 이러한 제한이 향후 몇 주 후에는 변경될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-110">Currently you are limited to only one action per foreach loop, but this restriction will be lifted in the coming weeks.</span></span>  <span data-ttu-id="81ad4-111">일단 루프 내에 들어오면 배열의 각 값에 나오는 항목을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-111">Once within the loop you can begin to specify what should occur at each value of the array.</span></span>

<span data-ttu-id="81ad4-112">코드 보기를 사용하는 경우 아래와 같이 각 루프에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-112">If using code-view, you can specify a for each loop like below.</span></span>  <span data-ttu-id="81ad4-113">다음은 'microsoft.com'을 포함하는 각 전자 메일 주소에 대해 전자 메일을 보내는 각 루프의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-113">This is an example of a for each loop that sends an email for each email address that contains 'microsoft.com':</span></span>

``` json
{
    "email_filter": {
        "type": "query",
        "inputs": {
            "from": "@triggerBody()['emails']",
            "where": "@contains(item()['email'], 'microsoft.com')"
        }
    },
    "forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "actions": {
            "send_email": {
                "type": "ApiConnection",
                "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                },
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                },
                }
            }
        },
        "runAfter":{
            "email_filter": [ "Succeeded" ]
        }
    }
}
```
  
  <span data-ttu-id="81ad4-114">`foreach` 작업은 5,000개 행까지 배열을 반복할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-114">A `foreach` action can iterate over arrays up to 5,000 rows.</span></span>  <span data-ttu-id="81ad4-115">각 반복은 기본적으로 병렬로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-115">Each iteration will execute in parallel by default.</span></span>  

### <a name="sequential-foreach-loops"></a><span data-ttu-id="81ad4-116">순차적 ForEach 루프</span><span class="sxs-lookup"><span data-stu-id="81ad4-116">Sequential ForEach loops</span></span>

<span data-ttu-id="81ad4-117">순차적으로 실행하는 foreach 루프를 사용 하도록 설정하려면 `Sequential` 작업 옵션을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-117">To enable a foreach loop to execute sequentially, the `Sequential` operation option should be added.</span></span>

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a><span data-ttu-id="81ad4-118">Until 루프</span><span class="sxs-lookup"><span data-stu-id="81ad4-118">Until loop</span></span>
  
  <span data-ttu-id="81ad4-119">조건이 충족될 때까지 작업 또는 일련의 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-119">You can perform an action or series of actions until a condition is met.</span></span>  <span data-ttu-id="81ad4-120">이에 대한 가장 일반적인 시나리오는 원하는 응답을 얻을 때까지 끝점을 호출하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-120">The most common scenario for this is calling an endpoint until you get the response you are looking for.</span></span>  <span data-ttu-id="81ad4-121">디자이너에서 Until 루프를 추가하도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-121">In the designer, you can specify to add an until loop.</span></span>  <span data-ttu-id="81ad4-122">이 루프 내에 작업을 추가한 후에 루프 한도 뿐만 아니라 종료 조건을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-122">After adding actions inside the loop, you can set the exit condition, as well as the loop limits.</span></span>  <span data-ttu-id="81ad4-123">루프 주기 사이에는 1분의 지연이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-123">There is a 1 minute delay between loop cycles.</span></span>
  
  <span data-ttu-id="81ad4-124">코드 보기를 사용하는 경우 아래와 같이 Until 루프를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-124">If using code-view, you can specify an until loop like below.</span></span>  <span data-ttu-id="81ad4-125">다음은 응답 본문 값이 'Completed'가 될 때까지 HTTP 끝점을 호출하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-125">This is an example of calling an HTTP endpoint until the response body has the value 'Completed'.</span></span>  <span data-ttu-id="81ad4-126">다음과 같은 경우에 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-126">It will complete when either</span></span> 
  
  * <span data-ttu-id="81ad4-127">HTTP 응답의 상태가 'Completed'임</span><span class="sxs-lookup"><span data-stu-id="81ad4-127">HTTP Response has status of 'Completed'</span></span>
  * <span data-ttu-id="81ad4-128">1시간 동안 시도됨</span><span class="sxs-lookup"><span data-stu-id="81ad4-128">It has tried for 1 hour</span></span>
  * <span data-ttu-id="81ad4-129">100번 반복됨</span><span class="sxs-lookup"><span data-stu-id="81ad4-129">It has looped 100 times</span></span>
  
  ``` json
  {
      "until_successful":{
        "type": "until",
        "expression": "@equals(actions('http')['status'], 'Completed')",
        "limit": {
            "count": 100,
            "timeout": "PT1H"
        },
        "actions": {
            "create_resource": {
                "type": "http",
                "inputs": {
                    "url": "http://provisionRseource.com",
                    "body": {
                        "resourceId": "@triggerBody()"
                    }
                }
            }
        }
      }
  }
  ```
  
## <a name="spliton-and-debatching"></a><span data-ttu-id="81ad4-130">SplitOn 및 분리</span><span class="sxs-lookup"><span data-stu-id="81ad4-130">SplitOn and debatching</span></span>

<span data-ttu-id="81ad4-131">경우에 따라 트리거가 항목당 워크플로를 분리하고 시작하려는 항목 배열을 수신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-131">Sometimes a trigger may receive an array of items that you want to debatch and start a workflow per item.</span></span>  <span data-ttu-id="81ad4-132">이 작업은 `spliton` 명령을 통해 수행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-132">This can be accomplished via the `spliton` command.</span></span>  <span data-ttu-id="81ad4-133">기본적으로 트리거 swagger가 배열에 해당하는 페이로드를 지정하는 경우 `spliton`이 추가되고 항목당 실행이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-133">By default, if your trigger swagger specifies a payload that is an array, a `spliton` will be added and start a run per item.</span></span>  <span data-ttu-id="81ad4-134">SplitOn만 트리거로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-134">SplitOn can only be added to a trigger.</span></span>  <span data-ttu-id="81ad4-135">정의 코드 보기에서 수동으로 구성하거나 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-135">This can be manually configured or overridden in definition code-view.</span></span>  <span data-ttu-id="81ad4-136">현재 SplitOn은 배열을 최대 5,000개의 항목으로 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-136">Currently SplitOn can debatch arrays up to 5,000 items.</span></span>  <span data-ttu-id="81ad4-137">`spliton`을 포함할 수 없으며 동기 응답 패턴도 구현할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-137">You cannot have a `spliton` and also implement the synchronous response pattern.</span></span>  <span data-ttu-id="81ad4-138">`spliton` 외에도 `response` 작업이 있는 호출된 모든 워크플로는 비동기식으로 실행되고 즉각적인 `202 Accepted` 응답을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-138">Any workflow called that has a `response` action in addition to `spliton` will run asynchronously and send an immediate `202 Accepted` response.</span></span>  

<span data-ttu-id="81ad4-139">다음 예제와 같이 코드 보기에서 SplitOn을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-139">SplitOn can be specified in code-view as the following example.</span></span>  <span data-ttu-id="81ad4-140">이렇게 하면 항목의 배열이 수신되고 각 행에서 분리됩니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-140">This receives an array of items and debatches on each row.</span></span>

```
{
    "myDebatchTrigger": {
        "type": "Http",
        "inputs": {
            "url": "http://getNewCustomers",
        },
        "recurrence": {
            "frequencey": "Second",
            "interval": 15
        },
        "spliton": "@triggerBody()['rows']"
    }
}
```

## <a name="scopes"></a><span data-ttu-id="81ad4-141">범위</span><span class="sxs-lookup"><span data-stu-id="81ad4-141">Scopes</span></span>

<span data-ttu-id="81ad4-142">범위를 사용하여 일련의 작업을 함께 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-142">It is possible to group a series of actions together using a scope.</span></span>  <span data-ttu-id="81ad4-143">이 기능은 예외 처리를 구현하는 데 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-143">This is particularly useful for implementing exception handling.</span></span>  <span data-ttu-id="81ad4-144">디자이너에서 새 범위를 추가하고 내부에 작업을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-144">In the designer you can add a new scope, and begin adding any actions inside of it.</span></span>  <span data-ttu-id="81ad4-145">다음과 같이 코드 보기에서 범위를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81ad4-145">You can define scopes in code-view like the following:</span></span>


```
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```