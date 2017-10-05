---
title: "시나리오 - Azure Functions 및 Azure Service Bus를 사용하여 논리 앱 트리거 | Microsoft Docs"
description: "Azure Functions 및 Azure Service Bus를 사용하여 논리 앱을 트리거하는 함수 만들기"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 19cbd921-7071-4221-ab86-b44d0fc0ecef
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/23/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 088f10bc32dd492f82f0a10a7e5829e76f588758
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a><span data-ttu-id="f90ad-103">시나리오: Azure Functions 및 Azure Service Bus를 사용하여 논리 앱 트리거</span><span class="sxs-lookup"><span data-stu-id="f90ad-103">Scenario: Trigger a logic app with Azure Functions and Azure Service Bus</span></span>

<span data-ttu-id="f90ad-104">Azure Functions로 장기 실행 수신기 또는 작업을 배포하는 데 필요한 논리 앱용 트리거를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f90ad-104">You can use Azure Functions to create a trigger for a logic app when you need to deploy a long-running listener or task.</span></span> <span data-ttu-id="f90ad-105">예를 들어, 큐에서 수신 대기하고 있다가 푸시 트리거로 즉시 논리 앱을 실행하는 함수를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f90ad-105">For example, you can create a function that listens in on a queue and then immediately fire a logic app as a push trigger.</span></span>

## <a name="build-the-logic-app"></a><span data-ttu-id="f90ad-106">논리 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="f90ad-106">Build the logic app</span></span>
<span data-ttu-id="f90ad-107">이 예에는 트리거할 필요가 있는 각 논리 앱에 대해 실행되는 함수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f90ad-107">In this example, you have a function running for each logic app that needs to be triggered.</span></span> <span data-ttu-id="f90ad-108">먼저, HTTP 요청 트리거가 있는 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f90ad-108">First, create a logic app that has an HTTP request trigger.</span></span> <span data-ttu-id="f90ad-109">이 함수는 큐 메시지를 수신할 때마다 끝점을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ad-109">The function calls that endpoint whenever a queue message is received.</span></span>  

1. <span data-ttu-id="f90ad-110">논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f90ad-110">Create a logic app.</span></span>
2. <span data-ttu-id="f90ad-111">**수동 – HTTP 요청을 받은 경우** 트리거를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ad-111">Select the **Manual - When an HTTP Request is Received** trigger.</span></span>
   <span data-ttu-id="f90ad-112">또는, [jsonschema.net](http://jsonschema.net)과 같은 도구로 큐 메시지와 함께 사용할 JSON 스키마를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f90ad-112">Optionally, you can specify a JSON schema to use with the queue message by using a tool like [jsonschema.net](http://jsonschema.net).</span></span> <span data-ttu-id="f90ad-113">트리거에 스키마를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f90ad-113">Paste the schema in the trigger.</span></span> <span data-ttu-id="f90ad-114">스키마는 디자이너가 데이터의 형태를 이해하고 워크플로에서 속성이 쉽게 흐를 수 있도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="f90ad-114">Schemas help the designer understand the shape of the data and flow properties more easily through the workflow.</span></span>
2. <span data-ttu-id="f90ad-115">큐 메시지를 수신한 후 실행하기를 원하는 추가 절차를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ad-115">Add any additional steps that you want to occur after a queue message is received.</span></span> <span data-ttu-id="f90ad-116">예를 들어, Office 365로 이메일을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ad-116">For example, send an email via Office 365.</span></span>  
3. <span data-ttu-id="f90ad-117">논리 앱을 저장하여 이 논리 앱에 트리거에 대한 콜백 URL을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ad-117">Save the logic app to generate the callback URL for the trigger to this logic app.</span></span> <span data-ttu-id="f90ad-118">URL은 트리거 카드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f90ad-118">The URL appears on the trigger card.</span></span>

![트리거 카드에 나타나는 콜백 URL][1]

## <a name="build-the-function"></a><span data-ttu-id="f90ad-120">함수 빌드</span><span class="sxs-lookup"><span data-stu-id="f90ad-120">Build the function</span></span>
<span data-ttu-id="f90ad-121">다음으로 트리거로 작동하고 큐에 수신 대기하는 함수를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ad-121">Next, you must create a function that acts as the trigger and listens to the queue.</span></span>

1. <span data-ttu-id="f90ad-122">[Azure Functions 포털](https://functions.azure.com/signin)에서 **새 함수**를 선택한 다음 **ServiceBusQueueTrigger - C#** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ad-122">In the [Azure Functions portal](https://functions.azure.com/signin), select **New Function**, and then select the **ServiceBusQueueTrigger - C#** template.</span></span>
   
    ![Azure Functions 포털][2]
2. <span data-ttu-id="f90ad-124">Service Bus 큐에 대한 연결이 Azure Service Bus SDK `OnMessageReceive()` 수신기를 사용하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ad-124">Configure the connection to the Service Bus queue, which uses the Azure Service Bus SDK `OnMessageReceive()` listener.</span></span>
3. <span data-ttu-id="f90ad-125">큐 메시지를 트리거로 사용하여 (앞서 만든) 논리 앱 끝점을 호출하는 기본 함수를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ad-125">Write a basic function to call the logic app endpoint (created earlier) by using the queue message as a trigger.</span></span> <span data-ttu-id="f90ad-126">함수의 전체 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f90ad-126">Here's a full example of a function.</span></span> <span data-ttu-id="f90ad-127">이 예제는 `application/json` 메시지 콘텐츠 형식을 사용하지만 필요에 따라 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f90ad-127">The example uses an `application/json` message content type, but you can change this type as necessary.</span></span>
   
   ```
   using System;
   using System.Threading.Tasks;
   using System.Net.Http;
   using System.Text;
   
   private static string logicAppUri = @"https://prod-05.westus.logic.azure.com:443/.........";
   
   public static void Run(string myQueueItem, TraceWriter log)
   {
   
       log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
       using (var client = new HttpClient())
       {
           var response = client.PostAsync(logicAppUri, new StringContent(myQueueItem, Encoding.UTF8, "application/json")).Result;
       }
   }
   ```

<span data-ttu-id="f90ad-128">테스트를 하려면 [서비스 버스 탐색기](https://github.com/paolosalvatori/ServiceBusExplorer)등의 도구로 큐 메시지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ad-128">To test, add a queue message via a tool like [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span></span> <span data-ttu-id="f90ad-129">함수가 메시지를 받는 즉시 논리 앱이 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ad-129">See the logic app fire immediately after the function receives the message.</span></span>

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
