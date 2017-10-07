---
title: "논리 앱에서 aaaLearn toouse hello Azure 서비스 버스 커넥터 | Microsoft Docs"
description: "Azure 앱 서비스로 논리 앱을 만듭니다. 서비스 버스 toosend tooAzure를 연결 하 고 메시지를 받습니다. 송신 tooqueue 같은 동작을 수행할 tootopic 송신 및 큐에서 받을 구독에서 수신 수 있습니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d6d14f5f-2126-4e33-808e-41de08e6721f
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/02/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c815ac167c3106ade470ce139d119085558a9497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-service-bus-connector"></a><span data-ttu-id="f0fc5-105">Hello Azure 서비스 버스 커넥터와 함께 시작.</span><span class="sxs-lookup"><span data-stu-id="f0fc5-105">Get started with hello Azure Service Bus connector</span></span>
<span data-ttu-id="f0fc5-106">서비스 버스 toosend tooAzure를 연결 하 고 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="f0fc5-106">Connect tooAzure Service Bus toosend and receive messages.</span></span> <span data-ttu-id="f0fc5-107">송신 tooqueue 같은 동작을 수행할 tootopic 송신 및 큐에서 받을 구독에서 수신 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0fc5-107">You can perform actions such as send tooqueue, send tootopic, receive from queue, and receive from subscription.</span></span>

<span data-ttu-id="f0fc5-108">toouse [커넥터](apis-list.md), toocreate 논리 앱을 먼저 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0fc5-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="f0fc5-109">[지금 논리 앱을 만들어](../logic-apps/logic-apps-create-a-logic-app.md) 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0fc5-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooservice-bus"></a><span data-ttu-id="f0fc5-110">버스 tooService 연결</span><span class="sxs-lookup"><span data-stu-id="f0fc5-110">Connect tooService Bus</span></span>
<span data-ttu-id="f0fc5-111">논리 앱에서 모든 서비스에 액세스 하기 전에 먼저 연결 toohello 서비스 toocreate를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0fc5-111">Before your logic app can access any service, you first need toocreate a connection toohello service.</span></span> <span data-ttu-id="f0fc5-112">[연결](connectors-overview.md)은 논리 앱과 다른 서비스 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f0fc5-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

> [!INCLUDE [Steps toocreate a connection tooAzure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a><span data-ttu-id="f0fc5-113">서비스 버스 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="f0fc5-113">Use a Service Bus trigger</span></span>
<span data-ttu-id="f0fc5-114">트리거는 이벤트를 사용 하는 toostart hello 워크플로 논리 앱에 정의 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0fc5-114">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="f0fc5-115">[트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="f0fc5-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a><span data-ttu-id="f0fc5-116">서비스 버스 동작 사용</span><span class="sxs-lookup"><span data-stu-id="f0fc5-116">Use a Service Bus action</span></span>
<span data-ttu-id="f0fc5-117">동작은 논리 앱에 정의 된 hello 워크플로에 의해 수행 되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="f0fc5-117">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="f0fc5-118">[작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="f0fc5-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

[!INCLUDE [Steps toocreate a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a><span data-ttu-id="f0fc5-119">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="f0fc5-119">Connector-specific details</span></span>

<span data-ttu-id="f0fc5-120">모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/servicebus/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f0fc5-120">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/servicebus/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f0fc5-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f0fc5-121">Next steps</span></span>
<span data-ttu-id="f0fc5-122">[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="f0fc5-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

