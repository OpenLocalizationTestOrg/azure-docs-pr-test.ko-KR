---
title: "aaaScenario-Azure 함수 및 Azure 서비스 버스를 사용 하 여 논리 앱 트리거 | Microsoft Docs"
description: "Azure 함수 및 Azure 서비스 버스를 사용 하 여 함수 tootrigger 논리 앱 만들기"
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
ms.openlocfilehash: a7b78ebcfe492eee2e08ceeae6b9c5f8ed4717bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a><span data-ttu-id="abac4-103">시나리오: Azure Functions 및 Azure Service Bus를 사용하여 논리 앱 트리거</span><span class="sxs-lookup"><span data-stu-id="abac4-103">Scenario: Trigger a logic app with Azure Functions and Azure Service Bus</span></span>

<span data-ttu-id="abac4-104">장기 실행 수신기 또는 작업 toodeploy 필요할 때 논리 앱에 대 한 Azure 기능 toocreate 트리거를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abac4-104">You can use Azure Functions toocreate a trigger for a logic app when you need toodeploy a long-running listener or task.</span></span> <span data-ttu-id="abac4-105">예를 들어, 큐에서 수신 대기하고 있다가 푸시 트리거로 즉시 논리 앱을 실행하는 함수를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abac4-105">For example, you can create a function that listens in on a queue and then immediately fire a logic app as a push trigger.</span></span>

## <a name="build-hello-logic-app"></a><span data-ttu-id="abac4-106">Hello 논리 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="abac4-106">Build hello logic app</span></span>
<span data-ttu-id="abac4-107">이 예제에서는 함수 toobe 트리거되는 각 논리 앱에 대해 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abac4-107">In this example, you have a function running for each logic app that needs toobe triggered.</span></span> <span data-ttu-id="abac4-108">먼저, HTTP 요청 트리거가 있는 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abac4-108">First, create a logic app that has an HTTP request trigger.</span></span> <span data-ttu-id="abac4-109">hello 함수 큐 메시지를 받을 때마다 해당 끝점을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="abac4-109">hello function calls that endpoint whenever a queue message is received.</span></span>  

1. <span data-ttu-id="abac4-110">논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abac4-110">Create a logic app.</span></span>
2. <span data-ttu-id="abac4-111">선택 hello **수동-HTTP 요청을 받으면** 트리거.</span><span class="sxs-lookup"><span data-stu-id="abac4-111">Select hello **Manual - When an HTTP Request is Received** trigger.</span></span>
   <span data-ttu-id="abac4-112">와 같은 도구를 사용 하 여 hello 큐 메시지와 함께 JSON 스키마 toouse를 지정할 수는 필요에 따라 [jsonschema.net](http://jsonschema.net)합니다.</span><span class="sxs-lookup"><span data-stu-id="abac4-112">Optionally, you can specify a JSON schema toouse with hello queue message by using a tool like [jsonschema.net](http://jsonschema.net).</span></span> <span data-ttu-id="abac4-113">Hello 트리거에서 hello 스키마를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="abac4-113">Paste hello schema in hello trigger.</span></span> <span data-ttu-id="abac4-114">스키마는 hello 모양의 hello 데이터 및 흐름 속성 hello 워크플로 통해 보다 쉽게 이해 하는 hello 디자이너 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abac4-114">Schemas help hello designer understand hello shape of hello data and flow properties more easily through hello workflow.</span></span>
2. <span data-ttu-id="abac4-115">큐 메시지를 받은 후 toooccur 되도록 추가 단계를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="abac4-115">Add any additional steps that you want toooccur after a queue message is received.</span></span> <span data-ttu-id="abac4-116">예를 들어, Office 365로 이메일을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="abac4-116">For example, send an email via Office 365.</span></span>  
3. <span data-ttu-id="abac4-117">Hello 트리거 toothis 논리 앱 hello 논리 앱 toogenerate hello 콜백 URL을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="abac4-117">Save hello logic app toogenerate hello callback URL for hello trigger toothis logic app.</span></span> <span data-ttu-id="abac4-118">hello URL hello 트리거 카드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abac4-118">hello URL appears on hello trigger card.</span></span>

![hello 트리거 카드에 hello 콜백 URL 표시][1]

## <a name="build-hello-function"></a><span data-ttu-id="abac4-120">Hello 함수를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="abac4-120">Build hello function</span></span>
<span data-ttu-id="abac4-121">다음으로 역할을 hello 트리거 toohello 큐에서 수신 하는 함수를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abac4-121">Next, you must create a function that acts as hello trigger and listens toohello queue.</span></span>

1. <span data-ttu-id="abac4-122">Hello에 [Azure 함수 포털](https://functions.azure.com/signin)을 선택 **새 함수**를 클릭 한 hello **ServiceBusQueueTrigger-C#** 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="abac4-122">In hello [Azure Functions portal](https://functions.azure.com/signin), select **New Function**, and then select hello **ServiceBusQueueTrigger - C#** template.</span></span>
   
    ![Azure Functions 포털][2]
2. <span data-ttu-id="abac4-124">Hello 연결 toohello 서비스 버스 큐를 사용 하 여 Azure 서비스 버스 SDK hello 구성 `OnMessageReceive()` 수신기입니다.</span><span class="sxs-lookup"><span data-stu-id="abac4-124">Configure hello connection toohello Service Bus queue, which uses hello Azure Service Bus SDK `OnMessageReceive()` listener.</span></span>
3. <span data-ttu-id="abac4-125">기본 함수 toocall hello 논리가 응용 프로그램 끝점 (앞에서 만든)을 트리거로 hello 큐 메시지를 사용 하 여 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="abac4-125">Write a basic function toocall hello logic app endpoint (created earlier) by using hello queue message as a trigger.</span></span> <span data-ttu-id="abac4-126">함수의 전체 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="abac4-126">Here's a full example of a function.</span></span> <span data-ttu-id="abac4-127">사용 하 여 hello 예제는 `application/json` 메시지 콘텐츠 형식에 필요한 만큼이 유형을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abac4-127">hello example uses an `application/json` message content type, but you can change this type as necessary.</span></span>
   
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

<span data-ttu-id="abac4-128">tootest와 같은 도구를 통해 큐 메시지 추가 [서비스 버스 탐색기](https://github.com/paolosalvatori/ServiceBusExplorer)합니다.</span><span class="sxs-lookup"><span data-stu-id="abac4-128">tootest, add a queue message via a tool like [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span></span> <span data-ttu-id="abac4-129">Hello 함수 hello 메시지를 받은 후에 즉시 실행 하는 hello 논리 앱을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="abac4-129">See hello logic app fire immediately after hello function receives hello message.</span></span>

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
