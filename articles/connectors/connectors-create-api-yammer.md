---
title: "Azure Logic Apps에 Yammer 커넥터 추가 | Microsoft Docs"
description: "REST API 매개 변수를 사용하는 Yammer 커넥터 개요"
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
ms.openlocfilehash: c7a213343b4fb2b5a89a5052a459061b404a431c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-yammer-connector"></a><span data-ttu-id="e5daa-103">Yammer 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="e5daa-103">Get started with the Yammer connector</span></span>
<span data-ttu-id="e5daa-104">Yammer에 연결하여 엔터프라이즈 네트워크의 대화에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="e5daa-104">Connect to Yammer to access conversations in your enterprise network.</span></span> <span data-ttu-id="e5daa-105">Yammer를 사용하면 다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5daa-105">With Yammer, you can:</span></span>

* <span data-ttu-id="e5daa-106">Yammer에서 가져온 데이터를 기반으로 비즈니스 흐름을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="e5daa-106">Build your business flow based on the data you get from Yammer.</span></span> 
* <span data-ttu-id="e5daa-107">그룹의 새 메시지 또는 팔로잉의 피드가 있을 때 트리거를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5daa-107">Use triggers for when there is a new message in a group, or a feed your following.</span></span>
* <span data-ttu-id="e5daa-108">메시지 게시, 모든 메시지 가져오기 등의 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5daa-108">Use actions to post a message, get all messages, and more.</span></span> <span data-ttu-id="e5daa-109">이러한 작업을 사용하여 응답을 가져오고 출력을 다른 작업에 사용할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5daa-109">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="e5daa-110">예를 들어 새 메시지가 표시되면 Office 365를 사용하여 메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5daa-110">For example, when a new message appears, you can send an email using Office 365.</span></span>

<span data-ttu-id="e5daa-111">논리 앱을 만들어 시작합니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5daa-111">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-yammer"></a><span data-ttu-id="e5daa-112">Yammer에 대한 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="e5daa-112">Create a connection to Yammer</span></span>
<span data-ttu-id="e5daa-113">Yammer 커넥터를 사용하려면 먼저 **연결**을 만든 다음 이러한 속성에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e5daa-113">To use the Yammer connector, you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="e5daa-114">속성</span><span class="sxs-lookup"><span data-stu-id="e5daa-114">Property</span></span> | <span data-ttu-id="e5daa-115">필수</span><span class="sxs-lookup"><span data-stu-id="e5daa-115">Required</span></span> | <span data-ttu-id="e5daa-116">설명</span><span class="sxs-lookup"><span data-stu-id="e5daa-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e5daa-117">신뢰</span><span class="sxs-lookup"><span data-stu-id="e5daa-117">Token</span></span> |<span data-ttu-id="e5daa-118">예</span><span class="sxs-lookup"><span data-stu-id="e5daa-118">Yes</span></span> |<span data-ttu-id="e5daa-119">Yammer 자격 증명 제공</span><span class="sxs-lookup"><span data-stu-id="e5daa-119">Provide Yammer Credentials</span></span> |

> [!INCLUDE [Steps to create a connection to Yammer](../../includes/connectors-create-api-yammer.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="e5daa-120">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="e5daa-120">Connector-specific details</span></span>

<span data-ttu-id="e5daa-121">[커넥터 세부 정보](/connectors/yammer/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5daa-121">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/yammer/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="e5daa-122">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="e5daa-122">More connectors</span></span>
<span data-ttu-id="e5daa-123">[API 목록](apis-list.md)으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="e5daa-123">Go back to the [APIs list](apis-list.md).</span></span>