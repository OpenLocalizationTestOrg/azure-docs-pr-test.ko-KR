---
title: "aaaLearn 어떻게 toouse hello 논리 앱의 SharePoint Online 커넥터 | Microsoft Docs"
description: "논리 앱 hello SharePoint Online 커넥터와 함께 toomange에 목록을 만들고 SharePoint 합니다."
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
ms.openlocfilehash: fc2f2745f0d174eae6165e84fd8b6656b0aac44b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sharepoint-online-connector"></a><span data-ttu-id="b449c-103">SharePoint Online 커넥터 hello 시작</span><span class="sxs-lookup"><span data-stu-id="b449c-103">Get started with hello SharePoint Online connector</span></span>
<span data-ttu-id="b449c-104">SharePoint 목록 hello SharePoint Online 커넥터 toomanage를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b449c-104">Use hello SharePoint Online connector toomanage SharePoint lists.</span></span>  

<span data-ttu-id="b449c-105">toouse [커넥터](apis-list.md), toocreate 논리 앱을 먼저 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b449c-105">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="b449c-106">[지금 논리 앱을 만들어](../logic-apps/logic-apps-create-a-logic-app.md) 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b449c-106">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosharepoint-online"></a><span data-ttu-id="b449c-107">TooSharePoint 온라인 연결</span><span class="sxs-lookup"><span data-stu-id="b449c-107">Connect tooSharePoint Online</span></span>
<span data-ttu-id="b449c-108">Toocreate 먼저 논리 앱에서 모든 서비스에 액세스 하기 전에 *연결* toohello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b449c-108">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="b449c-109">[연결](connectors-overview.md)은 논리 앱과 다른 서비스 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b449c-109">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-toosharepoint-online"></a><span data-ttu-id="b449c-110">연결 tooSharePoint 온라인 만들기</span><span class="sxs-lookup"><span data-stu-id="b449c-110">Create a connection tooSharePoint Online</span></span>
> [!INCLUDE [Steps toocreate a connection tooSharePoint](../../includes/connectors-create-api-sharepointonline.md)]


## <a name="use-a-sharepoint-online-trigger"></a><span data-ttu-id="b449c-111">SharePoint Online 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="b449c-111">Use a SharePoint Online trigger</span></span>
<span data-ttu-id="b449c-112">트리거는 이벤트를 사용 하는 toostart hello 워크플로 논리 앱에 정의 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b449c-112">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="b449c-113">[트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="b449c-113">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate a SharePoint Online trigger](../../includes/connectors-create-api-sharepointonline-trigger.md)]


## <a name="use-a-sharepoint-online-action"></a><span data-ttu-id="b449c-114">SharePoint Online 작업 사용</span><span class="sxs-lookup"><span data-stu-id="b449c-114">Use a SharePoint Online action</span></span>
<span data-ttu-id="b449c-115">동작은 논리 앱에 정의 된 hello 워크플로에 의해 수행 되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b449c-115">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="b449c-116">[작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="b449c-116">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate a SharePoint Online action](../../includes/connectors-create-api-sharepointonline-action.md)]


## <a name="connector-specific-details"></a><span data-ttu-id="b449c-117">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="b449c-117">Connector-specific details</span></span>

<span data-ttu-id="b449c-118">모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/sharepoint/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b449c-118">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sharepoint/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b449c-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b449c-119">Next Steps</span></span>
[<span data-ttu-id="b449c-120">논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="b449c-120">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

