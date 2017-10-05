---
title: "논리 앱에서 Salesforce 커넥터 사용 방법 알아보기 | Microsoft Docs"
description: "Azure 앱 서비스로 논리 앱을 만듭니다. Salesforce 커넥터는 Salesforce 개체와 함께 작동하는 API를 제공합니다."
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
ms.openlocfilehash: c2e2efd356382df9404f5c4ed54f24758b2cd22b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-salesforce-connector"></a><span data-ttu-id="8610b-104">Salesforce 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="8610b-104">Get started with the Salesforce connector</span></span>
<span data-ttu-id="8610b-105">Salesforce 커넥터는 Salesforce 개체와 함께 작동하는 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8610b-105">The Salesforce Connector provides an API to work with Salesforce objects.</span></span>

<span data-ttu-id="8610b-106">[커넥터](apis-list.md)를 사용하려면 먼저 논리 앱을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8610b-106">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="8610b-107">[지금 논리 앱을 만들어](../logic-apps/logic-apps-create-a-logic-app.md) 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8610b-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-salesforce-connector"></a><span data-ttu-id="8610b-108">Salesforce 커넥터에 연결</span><span class="sxs-lookup"><span data-stu-id="8610b-108">Connect to Salesforce connector</span></span>
<span data-ttu-id="8610b-109">논리 앱에서 서비스에 액세스하려면 먼저 서비스에 대한 *연결*을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8610b-109">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="8610b-110">[연결](connectors-overview.md)은 논리 앱과 다른 서비스 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8610b-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-salesforce-connector"></a><span data-ttu-id="8610b-111">Salesforce 커넥터에 대한 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="8610b-111">Create a connection to Salesforce connector</span></span>
> [!INCLUDE [Steps to create a connection to Salesforce Connector](../../includes/connectors-create-api-salesforce.md)]
> 
> 

## <a name="use-a-salesforce-connector-trigger"></a><span data-ttu-id="8610b-112">Salesforce 커넥터 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="8610b-112">Use a Salesforce connector trigger</span></span>
<span data-ttu-id="8610b-113">트리거는 논리 앱에 정의된 워크플로를 시작하는 데 사용할 수 있는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="8610b-113">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="8610b-114">[트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="8610b-114">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps to create a Salesforce trigger](../../includes/connectors-create-api-salesforce-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="8610b-115">조건 추가</span><span class="sxs-lookup"><span data-stu-id="8610b-115">Add a condition</span></span>
> [!INCLUDE [Steps to create a Salesforce condition](../../includes/connectors-create-api-salesforce-condition.md)]
> 
> 

## <a name="use-a-salesforce-connector-action"></a><span data-ttu-id="8610b-116">Salesforce 커넥터 작업 사용</span><span class="sxs-lookup"><span data-stu-id="8610b-116">Use a Salesforce connector action</span></span>
<span data-ttu-id="8610b-117">작업은 논리 앱에 정의된 워크플로에 의해 수행되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="8610b-117">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="8610b-118">[작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="8610b-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps to create a Salesforce action](../../includes/connectors-create-api-salesforce-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="8610b-119">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="8610b-119">Connector-specific details</span></span>

<span data-ttu-id="8610b-120">[커넥터 세부 정보](/connectors/salesforce/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8610b-120">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/salesforce/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8610b-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8610b-121">Next steps</span></span>
[<span data-ttu-id="8610b-122">논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="8610b-122">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

