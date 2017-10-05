---
title: "논리 앱에서 SharePoint Online 커넥터 사용 방법 알아보기 | Microsoft Docs"
description: "SharePoint Online 커넥터를 사용하여 논리 앱을 만들고 SharePoint에서 목록을 관리합니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: e0ec3149-507a-409d-8e7b-d5fbded006ce
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/19/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 96fc1347604c0c6cc2c2463a5dbd83b560183a16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sharepoint-online-connector"></a><span data-ttu-id="95e2f-103">SharePoint Online 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="95e2f-103">Get started with the SharePoint Online connector</span></span>
<span data-ttu-id="95e2f-104">SharePoint Online 커넥터를 사용하여 SharePoint 목록을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="95e2f-104">Use the SharePoint Online connector to manage SharePoint lists.</span></span>  

<span data-ttu-id="95e2f-105">[커넥터](apis-list.md)를 사용하려면 먼저 논리 앱을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95e2f-105">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="95e2f-106">[지금 논리 앱을 만들어](../logic-apps/logic-apps-create-a-logic-app.md) 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e2f-106">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-sharepoint-online"></a><span data-ttu-id="95e2f-107">SharePoint Online에 연결</span><span class="sxs-lookup"><span data-stu-id="95e2f-107">Connect to SharePoint Online</span></span>
<span data-ttu-id="95e2f-108">논리 앱에서 서비스에 액세스하려면 먼저 서비스에 대한 *연결*을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95e2f-108">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="95e2f-109">[연결](connectors-overview.md)은 논리 앱과 다른 서비스 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="95e2f-109">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-sharepoint-online"></a><span data-ttu-id="95e2f-110">SharePoint Online에 대한 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="95e2f-110">Create a connection to SharePoint Online</span></span>
> [!INCLUDE [Steps to create a connection to SharePoint](../../includes/connectors-create-api-sharepointonline.md)]


## <a name="use-a-sharepoint-online-trigger"></a><span data-ttu-id="95e2f-111">SharePoint Online 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="95e2f-111">Use a SharePoint Online trigger</span></span>
<span data-ttu-id="95e2f-112">트리거는 논리 앱에 정의된 워크플로를 시작하는 데 사용할 수 있는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="95e2f-112">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="95e2f-113">[트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="95e2f-113">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create a SharePoint Online trigger](../../includes/connectors-create-api-sharepointonline-trigger.md)]


## <a name="use-a-sharepoint-online-action"></a><span data-ttu-id="95e2f-114">SharePoint Online 작업 사용</span><span class="sxs-lookup"><span data-stu-id="95e2f-114">Use a SharePoint Online action</span></span>
<span data-ttu-id="95e2f-115">작업은 논리 앱에 정의된 워크플로에 의해 수행되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="95e2f-115">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="95e2f-116">[작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="95e2f-116">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create a SharePoint Online action](../../includes/connectors-create-api-sharepointonline-action.md)]


## <a name="connector-specific-details"></a><span data-ttu-id="95e2f-117">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="95e2f-117">Connector-specific details</span></span>

<span data-ttu-id="95e2f-118">[커넥터 세부 정보](/connectors/sharepoint/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e2f-118">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sharepoint/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="95e2f-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="95e2f-119">Next Steps</span></span>
[<span data-ttu-id="95e2f-120">논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="95e2f-120">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

