---
title: "aaaLearn toouse 논리 앱에서 Salesforce 커넥터 hello | Microsoft Docs"
description: "Azure 앱 서비스로 논리 앱을 만듭니다. Salesforce 커넥터 hello는 API toowork Salesforce 개체를 제공합니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 54fe5af8-7d2a-4da8-94e7-15d029e029bf
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/05/2016
ms.author: mandia; ladocs
ms.openlocfilehash: b14b41fa8a4648b4f0090472dc0f9575bf13a2ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-salesforce-connector"></a><span data-ttu-id="b3382-104">Hello Salesforce 커넥터와 함께 시작</span><span class="sxs-lookup"><span data-stu-id="b3382-104">Get started with hello Salesforce connector</span></span>
<span data-ttu-id="b3382-105">Salesforce 커넥터 hello는 API toowork Salesforce 개체를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b3382-105">hello Salesforce Connector provides an API toowork with Salesforce objects.</span></span>

<span data-ttu-id="b3382-106">toouse [커넥터](apis-list.md), toocreate 논리 앱을 먼저 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3382-106">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="b3382-107">[지금 논리 앱을 만들어](../logic-apps/logic-apps-create-a-logic-app.md) 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3382-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosalesforce-connector"></a><span data-ttu-id="b3382-108">TooSalesforce 커넥터에 연결</span><span class="sxs-lookup"><span data-stu-id="b3382-108">Connect tooSalesforce connector</span></span>
<span data-ttu-id="b3382-109">Toocreate 먼저 논리 앱에서 모든 서비스에 액세스 하기 전에 *연결* toohello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b3382-109">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="b3382-110">[연결](connectors-overview.md)은 논리 앱과 다른 서비스 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b3382-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-toosalesforce-connector"></a><span data-ttu-id="b3382-111">연결 tooSalesforce 커넥터 만들기</span><span class="sxs-lookup"><span data-stu-id="b3382-111">Create a connection tooSalesforce connector</span></span>
> [!INCLUDE [Steps toocreate a connection tooSalesforce Connector](../../includes/connectors-create-api-salesforce.md)]
> 
> 

## <a name="use-a-salesforce-connector-trigger"></a><span data-ttu-id="b3382-112">Salesforce 커넥터 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="b3382-112">Use a Salesforce connector trigger</span></span>
<span data-ttu-id="b3382-113">트리거는 이벤트를 사용 하는 toostart hello 워크플로 논리 앱에 정의 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3382-113">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="b3382-114">[트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="b3382-114">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps toocreate a Salesforce trigger](../../includes/connectors-create-api-salesforce-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="b3382-115">조건 추가</span><span class="sxs-lookup"><span data-stu-id="b3382-115">Add a condition</span></span>
> [!INCLUDE [Steps toocreate a Salesforce condition](../../includes/connectors-create-api-salesforce-condition.md)]
> 
> 

## <a name="use-a-salesforce-connector-action"></a><span data-ttu-id="b3382-116">Salesforce 커넥터 작업 사용</span><span class="sxs-lookup"><span data-stu-id="b3382-116">Use a Salesforce connector action</span></span>
<span data-ttu-id="b3382-117">동작은 논리 앱에 정의 된 hello 워크플로에 의해 수행 되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b3382-117">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="b3382-118">[작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="b3382-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps toocreate a Salesforce action](../../includes/connectors-create-api-salesforce-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="b3382-119">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="b3382-119">Connector-specific details</span></span>

<span data-ttu-id="b3382-120">모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/salesforce/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3382-120">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/salesforce/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b3382-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b3382-121">Next steps</span></span>
[<span data-ttu-id="b3382-122">논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="b3382-122">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

