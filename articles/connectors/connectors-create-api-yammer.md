---
title: "aaaAdd hello Azure 논리 앱에서 Yammer 커넥터 | Microsoft Docs"
description: "REST API 매개 변수가 있는 hello Yammer 커넥터 개요"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5ae0827-fbb3-45ec-8f45-ad1cc2e7eccc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: be75df770a8062d839926dff8c0195d2647f78d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-yammer-connector"></a><span data-ttu-id="56498-103">Hello Yammer 커넥터와 함께 시작</span><span class="sxs-lookup"><span data-stu-id="56498-103">Get started with hello Yammer connector</span></span>
<span data-ttu-id="56498-104">엔터프라이즈 네트워크의 tooYammer tooaccess 대화를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="56498-104">Connect tooYammer tooaccess conversations in your enterprise network.</span></span> <span data-ttu-id="56498-105">Yammer를 사용하면 다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56498-105">With Yammer, you can:</span></span>

* <span data-ttu-id="56498-106">Yammer에서 받아야 하는 hello 데이터를 기반으로 비즈니스 흐름을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="56498-106">Build your business flow based on hello data you get from Yammer.</span></span> 
* <span data-ttu-id="56498-107">그룹의 새 메시지 또는 팔로잉의 피드가 있을 때 트리거를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="56498-107">Use triggers for when there is a new message in a group, or a feed your following.</span></span>
* <span data-ttu-id="56498-108">모든 메시지 및 가져올를 작업 toopost 메시지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="56498-108">Use actions toopost a message, get all messages, and more.</span></span> <span data-ttu-id="56498-109">이러한 작업 응답을 가져오고 다른 작업에 사용할 수 있는 hello 출력을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="56498-109">These actions get a response, and then make hello output available for other actions.</span></span> <span data-ttu-id="56498-110">예를 들어 새 메시지가 표시되면 Office 365를 사용하여 메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56498-110">For example, when a new message appears, you can send an email using Office 365.</span></span>

<span data-ttu-id="56498-111">논리 앱을 만들어 시작합니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56498-111">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tooyammer"></a><span data-ttu-id="56498-112">연결 tooYammer 만들기</span><span class="sxs-lookup"><span data-stu-id="56498-112">Create a connection tooYammer</span></span>
<span data-ttu-id="56498-113">toouse hello Yammer 커넥터를 처음 만들면는 **연결** 다음 이러한 속성에 대 한 hello 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="56498-113">toouse hello Yammer connector, you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="56498-114">속성</span><span class="sxs-lookup"><span data-stu-id="56498-114">Property</span></span> | <span data-ttu-id="56498-115">필수</span><span class="sxs-lookup"><span data-stu-id="56498-115">Required</span></span> | <span data-ttu-id="56498-116">설명</span><span class="sxs-lookup"><span data-stu-id="56498-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="56498-117">신뢰</span><span class="sxs-lookup"><span data-stu-id="56498-117">Token</span></span> |<span data-ttu-id="56498-118">예</span><span class="sxs-lookup"><span data-stu-id="56498-118">Yes</span></span> |<span data-ttu-id="56498-119">Yammer 자격 증명 제공</span><span class="sxs-lookup"><span data-stu-id="56498-119">Provide Yammer Credentials</span></span> |

> [!INCLUDE [Steps toocreate a connection tooYammer](../../includes/connectors-create-api-yammer.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="56498-120">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="56498-120">Connector-specific details</span></span>

<span data-ttu-id="56498-121">모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/yammer/)합니다.</span><span class="sxs-lookup"><span data-stu-id="56498-121">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/yammer/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="56498-122">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="56498-122">More connectors</span></span>
<span data-ttu-id="56498-123">Toohello 돌아가서 [Api 목록](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="56498-123">Go back toohello [APIs list](apis-list.md).</span></span>
