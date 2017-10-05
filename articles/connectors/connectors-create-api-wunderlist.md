---
title: "Azure Logic Apps의 Wunderlist 커넥터 | Microsoft Docs"
description: "Wunderlist에 대한 연결을 만들고 이 연결을 사용하여 Logic Apps에서 워크플로를 작성합니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: e4773ecf-3ad3-44b4-a1b5-ee5f58baeadd
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 899110992cc52ca5edf1706320fd5570473de784
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-wunderlist-connector"></a><span data-ttu-id="48c06-103">Wunderlist 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="48c06-103">Get started with the Wunderlist connector</span></span>
<span data-ttu-id="48c06-104">Wunderlist는 사람들이 작업할 수 있도록 할 일 목록 및 작업 관리자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="48c06-104">Wunderlist provide a todo list and task manager to help people get their stuff done.</span></span>  <span data-ttu-id="48c06-105">친구와 식료품 목록 공유하거나 프로젝트에 대해 작업하고 휴가를 계획할 경우 Wunderlist를 사용하여 할 일을 쉽게 캡처하고 공유하며 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48c06-105">Whether you’re sharing a grocery list with a loved one, working on a project, or planning a vacation, Wunderlist makes it easy to capture, share, and complete your to¬dos.</span></span> <span data-ttu-id="48c06-106">Wunderlist는 어디에서든 모든 작업에 액세스할 수 있도록 전화, 태블릿 및 컴퓨터 간을 즉시 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="48c06-106">Wunderlist instantly syncs between your phone, tablet and computer, so you can access all your tasks from anywhere.</span></span>

<span data-ttu-id="48c06-107">논리 앱을 만들어 시작합니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="48c06-107">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-wunderlist"></a><span data-ttu-id="48c06-108">Wunderlist에 대한 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="48c06-108">Create a connection to Wunderlist</span></span>
<span data-ttu-id="48c06-109">Wunderlist로 논리 앱을 만들려면 먼저 **연결**을 만든 후에 다음 속성에 대한 세부 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c06-109">To create Logic apps with Wunderlist, you must first create a **connection** then provide the details for the following properties:</span></span>

| <span data-ttu-id="48c06-110">속성</span><span class="sxs-lookup"><span data-stu-id="48c06-110">Property</span></span> | <span data-ttu-id="48c06-111">필수</span><span class="sxs-lookup"><span data-stu-id="48c06-111">Required</span></span> | <span data-ttu-id="48c06-112">설명</span><span class="sxs-lookup"><span data-stu-id="48c06-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="48c06-113">신뢰</span><span class="sxs-lookup"><span data-stu-id="48c06-113">Token</span></span> |<span data-ttu-id="48c06-114">예</span><span class="sxs-lookup"><span data-stu-id="48c06-114">Yes</span></span> |<span data-ttu-id="48c06-115">Wunderlist 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="48c06-115">Provide Wunderlist Credentials</span></span> |

<span data-ttu-id="48c06-116">연결을 만든 후에 사용하여 작업을 실행하고 트리거에 대한 수신을 대기할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48c06-116">After you create the connection, you can use it to execute the actions and listen for the triggers.</span></span>

> [!INCLUDE [Steps to create a connection to Wunderlist](../../includes/connectors-create-api-wunderlist.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="48c06-117">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="48c06-117">Connector-specific details</span></span>

<span data-ttu-id="48c06-118">[커넥터 세부 정보](/connectors/wunderlist/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48c06-118">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/wunderlist/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="48c06-119">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="48c06-119">More connectors</span></span>
<span data-ttu-id="48c06-120">[API 목록](apis-list.md)으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="48c06-120">Go back to the [APIs list](apis-list.md).</span></span>