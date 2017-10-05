---
title: "Azure Logic Apps의 Trello 커넥터 | Microsoft Docs"
description: "Azure 앱 서비스로 논리 앱을 만듭니다. Trello는 회사 및 집에서 모든 프로젝트를 통해 큐브 뷰를 제공합니다.  쉽고 무료로 유연하며 시각적인 방법으로 프로젝트를 관리하고 무엇이든 구성할 수 있습니다.  Trello에 연결하여 보드, 목록 및 카드 관리"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: fe7a4377-5c24-4f72-ab1a-6d9d23e8d895
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 526a14710f24ee4a4b61a11873aa6caa0b47dc10
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-trello-connector"></a><span data-ttu-id="191a0-106">Trello 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="191a0-106">Get started with the Trello connector</span></span>
<span data-ttu-id="191a0-107">Trello는 회사 및 집에서 모든 프로젝트를 통해 큐브 뷰를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="191a0-107">Trello gives you perspective over all your projects, at work and at home.</span></span>  <span data-ttu-id="191a0-108">쉽고 무료로 유연하며 시각적인 방법으로 프로젝트를 관리하고 무엇이든 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="191a0-108">It is an easy, free, flexible, and visual way to manage your projects and organize anything.</span></span>  <span data-ttu-id="191a0-109">Trello에 연결하여 보드, 목록 및 카드를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="191a0-109">Connect to Trello to manage your boards, lists and cards.</span></span>

<span data-ttu-id="191a0-110">논리 앱을 만들어 시작할 수 있습니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="191a0-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-trello"></a><span data-ttu-id="191a0-111">Trello에 대한 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="191a0-111">Create a connection to Trello</span></span>
<span data-ttu-id="191a0-112">Trello로 논리 앱을 만들려면 먼저 **연결**을 만든 후에 다음 속성에 대한 세부 정보를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="191a0-112">To create Logic apps with Trello, first create a **connection**, and enter the details for the following properties:</span></span>

| <span data-ttu-id="191a0-113">속성</span><span class="sxs-lookup"><span data-stu-id="191a0-113">Property</span></span> | <span data-ttu-id="191a0-114">필수</span><span class="sxs-lookup"><span data-stu-id="191a0-114">Required</span></span> | <span data-ttu-id="191a0-115">설명</span><span class="sxs-lookup"><span data-stu-id="191a0-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="191a0-116">신뢰</span><span class="sxs-lookup"><span data-stu-id="191a0-116">Token</span></span> |<span data-ttu-id="191a0-117">예</span><span class="sxs-lookup"><span data-stu-id="191a0-117">Yes</span></span> |<span data-ttu-id="191a0-118">Trello 자격 증명 제공</span><span class="sxs-lookup"><span data-stu-id="191a0-118">Provide Trello Credentials</span></span> |

<span data-ttu-id="191a0-119">연결을 만든 후에 사용하여 작업을 실행하고 트리거에 대한 수신을 대기할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="191a0-119">After you create the connection, you can use it to execute the actions and listen for the triggers.</span></span>

> [!INCLUDE [Steps to create a connection to Trello](../../includes/connectors-create-api-trello.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="191a0-120">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="191a0-120">Connector-specific details</span></span>

<span data-ttu-id="191a0-121">[커넥터 세부 정보](/connectors/trello/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="191a0-121">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/trello/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="191a0-122">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="191a0-122">More connectors</span></span>
<span data-ttu-id="191a0-123">[API 목록](apis-list.md)으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="191a0-123">Go back to the [APIs list](apis-list.md).</span></span>