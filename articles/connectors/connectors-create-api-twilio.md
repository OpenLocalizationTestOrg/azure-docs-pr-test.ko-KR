---
title: "Azure Logic Apps에 Twilio 커넥터 추가 | Microsoft Docs"
description: "REST API 매개 변수를 사용하는 Twilio 커넥터 개요"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 43116187-4a2f-42e5-9852-a0d62f08c5fc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/19/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a790ac51b0fea7e3fa379d20e0e094e7ce0d7696
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-twilio-connector"></a><span data-ttu-id="31d52-103">Twilio 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="31d52-103">Get started with the Twilio connector</span></span>
<span data-ttu-id="31d52-104">Twilio에 연결하여 전역 SMS, MMS 및 IP 메시지를 보내고 받습니다.</span><span class="sxs-lookup"><span data-stu-id="31d52-104">Connect to Twilio to send and receive global SMS, MMS, and IP messages.</span></span> <span data-ttu-id="31d52-105">Twilio를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31d52-105">With Twilio, you can:</span></span>

* <span data-ttu-id="31d52-106">Twilio에서 가져온 데이터를 기반으로 비즈니스 흐름을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="31d52-106">Build your business flow based on the data you get from Twilio.</span></span> 
* <span data-ttu-id="31d52-107">메시지 가져오기, 메시지 나열 등의 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31d52-107">Use actions that get a message, list messages, and more.</span></span> <span data-ttu-id="31d52-108">이러한 작업을 사용하여 응답을 가져오고 출력을 다른 작업에 사용할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="31d52-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="31d52-109">예를 들어 새 Twilio 메시지를 받은 경우 이 메시지를 가져와 서비스 버스 워크플로에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31d52-109">For example, when  you get a new Twilio message, you can take this message and use it a Service Bus workflow.</span></span> 

<span data-ttu-id="31d52-110">논리 앱을 만들어 시작할 수 있습니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31d52-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-twilio"></a><span data-ttu-id="31d52-111">Twilio에 대한 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="31d52-111">Create a connection to Twilio</span></span>
<span data-ttu-id="31d52-112">논리 앱에 이 커넥터를 추가할 때 다음 Twilio 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="31d52-112">When you add this Connector to your logic apps, enter the following Twilio values:</span></span>

| <span data-ttu-id="31d52-113">속성</span><span class="sxs-lookup"><span data-stu-id="31d52-113">Property</span></span> | <span data-ttu-id="31d52-114">필수</span><span class="sxs-lookup"><span data-stu-id="31d52-114">Required</span></span> | <span data-ttu-id="31d52-115">설명</span><span class="sxs-lookup"><span data-stu-id="31d52-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31d52-116">계정 ID</span><span class="sxs-lookup"><span data-stu-id="31d52-116">Account ID</span></span> |<span data-ttu-id="31d52-117">예</span><span class="sxs-lookup"><span data-stu-id="31d52-117">Yes</span></span> |<span data-ttu-id="31d52-118">Twilio 계정 ID 입력</span><span class="sxs-lookup"><span data-stu-id="31d52-118">Enter your Twilio account ID</span></span> |
| <span data-ttu-id="31d52-119">액세스 토큰</span><span class="sxs-lookup"><span data-stu-id="31d52-119">Access Token</span></span> |<span data-ttu-id="31d52-120">예</span><span class="sxs-lookup"><span data-stu-id="31d52-120">Yes</span></span> |<span data-ttu-id="31d52-121">Twilio 액세스 토큰 입력</span><span class="sxs-lookup"><span data-stu-id="31d52-121">Enter your Twilio access token</span></span> |

> [!INCLUDE [Steps to create a connection to Twilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

<span data-ttu-id="31d52-122">Twilio 액세스 토큰이 없으면 [사용자 ID 및 액세스 토큰](https://www.twilio.com/docs/api/chat/guides/identity)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31d52-122">If you don't have a Twilio access token, see [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="31d52-123">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="31d52-123">Connector-specific details</span></span>

<span data-ttu-id="31d52-124">[커넥터 세부 정보](/connectors/twilio/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31d52-124">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/twilio/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="31d52-125">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="31d52-125">More connectors</span></span>
<span data-ttu-id="31d52-126">[API 목록](apis-list.md)으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="31d52-126">Go back to the [APIs list](apis-list.md).</span></span>