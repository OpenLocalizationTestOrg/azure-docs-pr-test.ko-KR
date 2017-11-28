---
title: "논리 앱에서 aaaAdd hello Facebook 커넥터 | Microsoft Docs"
description: "REST API 매개 변수를 사용 하는 hello Facebook 커넥터 개요"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: f4d6f0ed-c09b-488c-be1c-8cf2b5b1d4b8
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/07/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 962c6ed5d36e465de9d485d50e5c6dca6d44f470
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-facebook-connector"></a><span data-ttu-id="8b8f6-103">Hello Facebook 커넥터와 함께 시작</span><span class="sxs-lookup"><span data-stu-id="8b8f6-103">Get started with hello Facebook connector</span></span>
<span data-ttu-id="8b8f6-104">TooFacebook 연결 및 tooa 타임 라인 게시를 공급 하는 페이지 등 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b8f6-104">Connect tooFacebook and post tooa timeline, get a page feed, and more.</span></span> <span data-ttu-id="8b8f6-105">Facebook을 사용하면 다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b8f6-105">With Facebook, you can:</span></span>

* <span data-ttu-id="8b8f6-106">Facebook에서 받아야 하는 hello 데이터를 기반으로 비즈니스 흐름을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b8f6-106">Build your business flow based on hello data you get from Facebook.</span></span> 
* <span data-ttu-id="8b8f6-107">새 게시를 수신할 때 트리거를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8b8f6-107">Use a trigger when a new post is received.</span></span>
* <span data-ttu-id="8b8f6-108">사용 하 여 작업 tooyour 타임 라인을 게시 하는 피드, 페이지 및 기타 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8b8f6-108">Use actions that post tooyour timeline, get a page feed, and more.</span></span> <span data-ttu-id="8b8f6-109">이러한 작업 응답을 가져오고 다른 작업에 사용할 수 있는 hello 출력을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b8f6-109">These actions get a response, and then make hello output available for other actions.</span></span> <span data-ttu-id="8b8f6-110">예를 들어, 일정에는 새 게시 되는 경우에 해당 게시물 걸릴 고 tooyour Twitter 피드를 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b8f6-110">For example, when there is a new post on your timeline, you can take that post and push it tooyour Twitter feed.</span></span> 

<span data-ttu-id="8b8f6-111">이제 논리 앱을 만들어 시작할 수 있습니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b8f6-111">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-toofacebook"></a><span data-ttu-id="8b8f6-112">연결 tooFacebook 만들기</span><span class="sxs-lookup"><span data-stu-id="8b8f6-112">Create a connection tooFacebook</span></span>
<span data-ttu-id="8b8f6-113">이 커넥터 tooyour 논리 앱을 추가 하면 논리 앱 tooconnect tooyour Facebook에 권한을 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b8f6-113">When you add this connector tooyour logic apps, you must authorize logic apps tooconnect tooyour Facebook.</span></span>

1. <span data-ttu-id="8b8f6-114">Facebook 계정 tooyour에 로그인</span><span class="sxs-lookup"><span data-stu-id="8b8f6-114">Sign in tooyour Facebook account</span></span>
2. <span data-ttu-id="8b8f6-115">선택 **Authorize**, 논리 앱 tooconnect 허용 하 고 여 Facebook을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b8f6-115">Select **Authorize**, and allow your logic apps tooconnect and use your Facebook.</span></span> 

> [!INCLUDE [Steps toocreate a connection tooFacebook](../../includes/connectors-create-api-facebook.md)]
> 


## <a name="connector-specific-details"></a><span data-ttu-id="8b8f6-116">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="8b8f6-116">Connector-specific details</span></span>

<span data-ttu-id="8b8f6-117">모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/facebook/)합니다.</span><span class="sxs-lookup"><span data-stu-id="8b8f6-117">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/facebook/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="8b8f6-118">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="8b8f6-118">More connectors</span></span>
<span data-ttu-id="8b8f6-119">Toohello 돌아가서 [Api 목록](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8b8f6-119">Go back toohello [APIs list](apis-list.md).</span></span>
