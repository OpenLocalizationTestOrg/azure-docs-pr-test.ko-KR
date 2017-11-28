---
title: "aaaAdd Azure 논리 앱에서 Twilio 커넥터 hello | Microsoft Docs"
description: "REST API 매개 변수가 있는 hello Twilio 커넥터 개요"
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
ms.openlocfilehash: b2b487f34bc76bee24b4237a71ee767d0d22ff7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twilio-connector"></a><span data-ttu-id="42887-103">Hello Twilio 커넥터와 함께 시작</span><span class="sxs-lookup"><span data-stu-id="42887-103">Get started with hello Twilio connector</span></span>
<span data-ttu-id="42887-104">전역 SMS, MMS, 및 IP 메시지를 주고받을 tooTwilio toosend 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="42887-104">Connect tooTwilio toosend and receive global SMS, MMS, and IP messages.</span></span> <span data-ttu-id="42887-105">Twilio를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42887-105">With Twilio, you can:</span></span>

* <span data-ttu-id="42887-106">Twilio에서 가져오는 hello 데이터를 기반으로 비즈니스 흐름을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="42887-106">Build your business flow based on hello data you get from Twilio.</span></span> 
* <span data-ttu-id="42887-107">메시지 가져오기, 메시지 나열 등의 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="42887-107">Use actions that get a message, list messages, and more.</span></span> <span data-ttu-id="42887-108">이러한 작업 응답을 가져오고 다른 작업에 사용할 수 있는 hello 출력을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="42887-108">These actions get a response, and then make hello output available for other actions.</span></span> <span data-ttu-id="42887-109">예를 들어 새 Twilio 메시지를 받은 경우 이 메시지를 가져와 서비스 버스 워크플로에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42887-109">For example, when  you get a new Twilio message, you can take this message and use it a Service Bus workflow.</span></span> 

<span data-ttu-id="42887-110">논리 앱을 만들어 시작할 수 있습니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="42887-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tootwilio"></a><span data-ttu-id="42887-111">연결 tooTwilio 만들기</span><span class="sxs-lookup"><span data-stu-id="42887-111">Create a connection tooTwilio</span></span>
<span data-ttu-id="42887-112">이 커넥터 tooyour 논리 앱을 추가 하면 hello 다음 Twilio 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="42887-112">When you add this Connector tooyour logic apps, enter hello following Twilio values:</span></span>

| <span data-ttu-id="42887-113">속성</span><span class="sxs-lookup"><span data-stu-id="42887-113">Property</span></span> | <span data-ttu-id="42887-114">필수</span><span class="sxs-lookup"><span data-stu-id="42887-114">Required</span></span> | <span data-ttu-id="42887-115">설명</span><span class="sxs-lookup"><span data-stu-id="42887-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="42887-116">계정 ID</span><span class="sxs-lookup"><span data-stu-id="42887-116">Account ID</span></span> |<span data-ttu-id="42887-117">예</span><span class="sxs-lookup"><span data-stu-id="42887-117">Yes</span></span> |<span data-ttu-id="42887-118">Twilio 계정 ID 입력</span><span class="sxs-lookup"><span data-stu-id="42887-118">Enter your Twilio account ID</span></span> |
| <span data-ttu-id="42887-119">액세스 토큰</span><span class="sxs-lookup"><span data-stu-id="42887-119">Access Token</span></span> |<span data-ttu-id="42887-120">예</span><span class="sxs-lookup"><span data-stu-id="42887-120">Yes</span></span> |<span data-ttu-id="42887-121">Twilio 액세스 토큰 입력</span><span class="sxs-lookup"><span data-stu-id="42887-121">Enter your Twilio access token</span></span> |

> [!INCLUDE [Steps toocreate a connection tooTwilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

<span data-ttu-id="42887-122">Twilio 액세스 토큰이 없으면 [사용자 ID 및 액세스 토큰](https://www.twilio.com/docs/api/chat/guides/identity)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="42887-122">If you don't have a Twilio access token, see [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="42887-123">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="42887-123">Connector-specific details</span></span>

<span data-ttu-id="42887-124">모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/twilio/)합니다.</span><span class="sxs-lookup"><span data-stu-id="42887-124">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/twilio/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="42887-125">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="42887-125">More connectors</span></span>
<span data-ttu-id="42887-126">Toohello 돌아가서 [Api 목록](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="42887-126">Go back toohello [APIs list](apis-list.md).</span></span>
