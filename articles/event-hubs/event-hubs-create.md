---
title: "Azure 이벤트 허브 aaaCreate | Microsoft Docs"
description: "Azure 이벤트 허브 네임 스페이스 및 hello Azure 포털을 사용 하 여 이벤트 허브 만들기"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: ff99e327-c8db-4354-9040-9c60c51a2191
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: sethm
ms.openlocfilehash: 9a8b7711e2ca7d112e24be19353d43c365ff6935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-hello-azure-portal"></a><span data-ttu-id="3e59b-103">이벤트 허브 네임 스페이스 및 hello Azure 포털을 사용 하 여 이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="3e59b-103">Create an Event Hubs namespace and an event hub using hello Azure portal</span></span>

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="3e59b-104">Event Hubs 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="3e59b-104">Create an Event Hubs namespace</span></span>
1. <span data-ttu-id="3e59b-105">Toohello 로그온 [Azure 포털][Azure portal], 클릭 하 고 **새로** hello에 왼쪽 상단 hello 화면에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e59b-105">Log on toohello [Azure portal][Azure portal], and click **New** at hello top left of hello screen.</span></span>
1. <span data-ttu-id="3e59b-106">**사물 인터넷**을 클릭한 다음 **Event Hubs**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e59b-106">Click **Internet of Things**, and then click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. <span data-ttu-id="3e59b-107">Hello에 **네임 스페이스 만들기** 블레이드에서 네임 스페이스 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e59b-107">In hello **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="3e59b-108">hello 시스템 hello 이름이 사용 가능한 경우 즉시 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e59b-108">hello system immediately checks toosee if hello name is available.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. <span data-ttu-id="3e59b-109">만드는 있는지 hello 네임 스페이스 이름을 사용할 수 있는 되 면 hello 가격 책정 계층 (기본 또는 표준)를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e59b-109">After making sure hello namespace name is available, choose hello pricing tier (Basic or Standard).</span></span> <span data-ttu-id="3e59b-110">또한 toocreate hello 리소스에는 Azure 구독, 리소스 그룹 및 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e59b-110">Also, choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> 
1. <span data-ttu-id="3e59b-111">클릭 **만들기** toocreate hello 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e59b-111">Click **Create** toocreate hello namespace.</span></span> <span data-ttu-id="3e59b-112">Toowait 몇 분 정도 hello 시스템 toofully hello 리소스를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e59b-112">You may have toowait a few minutes for hello system toofully provision hello resources.</span></span>
2. <span data-ttu-id="3e59b-113">네임 스페이스의 hello 포털 목록에서 새로 생성 된 네임 스페이스 hello를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e59b-113">In hello portal list of namespaces, click hello newly created namespace.</span></span>
2. <span data-ttu-id="3e59b-114">**공유 액세스 정책**을 클릭한 후 **RootManageSharedAccessKey**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e59b-114">Click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. <span data-ttu-id="3e59b-115">Hello 복사 단추 toocopy hello 클릭 **RootManageSharedAccessKey** 연결 문자열 toohello 클립보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e59b-115">Click hello copy button toocopy hello **RootManageSharedAccessKey** connection string toohello clipboard.</span></span> <span data-ttu-id="3e59b-116">나중에 toouse 메모장 등의 임시 위치에이 연결 문자열을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e59b-116">Save this connection string in a temporary location, such as Notepad, toouse later.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a><span data-ttu-id="3e59b-117">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="3e59b-117">Create an event hub</span></span>

1. <span data-ttu-id="3e59b-118">Hello 이벤트 허브 네임 스페이스 목록에서 새로 만든 hello 네임 스페이스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e59b-118">In hello Event Hubs namespace list, click hello newly created namespace.</span></span>      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. <span data-ttu-id="3e59b-119">Hello 네임 스페이스 블레이드에서 클릭 **이벤트 허브**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e59b-119">In hello namespace blade, click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. <span data-ttu-id="3e59b-120">Hello 블레이드의 hello 위쪽 클릭 **이벤트 허브 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e59b-120">At hello top of hello blade, click **Add Event Hub**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. <span data-ttu-id="3e59b-121">이벤트 허브의 이름을 입력한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e59b-121">Type a name for your event hub, then click **Create**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub5.png)

<span data-ttu-id="3e59b-122">이벤트 허브 이제 만들어지고 hello 연결 문자열이 toosend 필요 하 고 이벤트를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e59b-122">Your event hub is now created, and you have hello connection strings you need toosend and receive events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e59b-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3e59b-123">Next steps</span></span>
<span data-ttu-id="3e59b-124">다음이 링크를 방문 하는 이벤트 허브에 대해 자세히 toolearn:</span><span class="sxs-lookup"><span data-stu-id="3e59b-124">toolearn more about Event Hubs, visit these links:</span></span>

* [<span data-ttu-id="3e59b-125">이벤트 허브 개요</span><span class="sxs-lookup"><span data-stu-id="3e59b-125">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="3e59b-126">이벤트 허브 API 개요</span><span class="sxs-lookup"><span data-stu-id="3e59b-126">Event Hubs API overview</span></span>](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/