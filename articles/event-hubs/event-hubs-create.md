---
title: "Azure 이벤트 허브 만들기 | Microsoft Docs"
description: "Azure Portal을 사용하여 Azure Event Hubs 네임스페이스 및 이벤트 허브 만들기"
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
ms.openlocfilehash: 816bf1426704d3391550e80c0700f1b011683a94
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-the-azure-portal"></a><span data-ttu-id="3d054-103">Azure Portal을 사용하여 Event Hubs 네임스페이스 및 이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="3d054-103">Create an Event Hubs namespace and an event hub using the Azure portal</span></span>

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="3d054-104">Event Hubs 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="3d054-104">Create an Event Hubs namespace</span></span>
1. <span data-ttu-id="3d054-105">[Azure Portal][Azure portal]에 로그온하고 화면 왼쪽 위에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3d054-105">Log on to the [Azure portal][Azure portal], and click **New** at the top left of the screen.</span></span>
1. <span data-ttu-id="3d054-106">**사물 인터넷**을 클릭한 다음 **Event Hubs**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3d054-106">Click **Internet of Things**, and then click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. <span data-ttu-id="3d054-107">**네임스페이스 만들기** 블레이드에서 네임스페이스 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3d054-107">In the **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="3d054-108">시스템에서 사용 가능한 이름인지 즉시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3d054-108">The system immediately checks to see if the name is available.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. <span data-ttu-id="3d054-109">네임스페이스 이름을 사용할 수 있게 설정한 후 가격 책정 계층(기본 또는 표준)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3d054-109">After making sure the namespace name is available, choose the pricing tier (Basic or Standard).</span></span> <span data-ttu-id="3d054-110">또한 리소스를 만들 Azure 구독, 리소스 그룹 및 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3d054-110">Also, choose an Azure subscription, resource group, and location in which to create the resource.</span></span> 
1. <span data-ttu-id="3d054-111">**만들기** 를 클릭하여 네임스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d054-111">Click **Create** to create the namespace.</span></span> <span data-ttu-id="3d054-112">시스템에서 리소스를 완전히 프로비전하기까지 몇 분 동안 기다려야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d054-112">You may have to wait a few minutes for the system to fully provision the resources.</span></span>
2. <span data-ttu-id="3d054-113">네임스페이스 포털 목록에서 새로 만든 네임스페이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3d054-113">In the portal list of namespaces, click the newly created namespace.</span></span>
2. <span data-ttu-id="3d054-114">**공유 액세스 정책**을 클릭한 후 **RootManageSharedAccessKey**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3d054-114">Click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. <span data-ttu-id="3d054-115">복사 단추를 클릭하여 클립보드에 대한 **RootManageSharedAccessKey** 연결 문자열을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3d054-115">Click the copy button to copy the **RootManageSharedAccessKey** connection string to the clipboard.</span></span> <span data-ttu-id="3d054-116">나중에 사용하기 위해 이 연결 문자열을 임시 위치(예: 메모장)에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3d054-116">Save this connection string in a temporary location, such as Notepad, to use later.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a><span data-ttu-id="3d054-117">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="3d054-117">Create an event hub</span></span>

1. <span data-ttu-id="3d054-118">Event Hubs 네임스페이스 목록에서 새로 만든 네임스페이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3d054-118">In the Event Hubs namespace list, click the newly created namespace.</span></span>      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. <span data-ttu-id="3d054-119">네임스페이스 블레이드에서 **Event Hubs**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3d054-119">In the namespace blade, click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. <span data-ttu-id="3d054-120">블레이드의 위쪽에서 **Event Hub 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3d054-120">At the top of the blade, click **Add Event Hub**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. <span data-ttu-id="3d054-121">이벤트 허브의 이름을 입력한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3d054-121">Type a name for your event hub, then click **Create**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub5.png)

<span data-ttu-id="3d054-122">이제 이벤트 허브가 생성되었고 이벤트를 보내고 받는 데 필요한 연결 문자열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d054-122">Your event hub is now created, and you have the connection strings you need to send and receive events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d054-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3d054-123">Next steps</span></span>
<span data-ttu-id="3d054-124">Event Hubs에 대한 자세한 내용은 다음 링크를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="3d054-124">To learn more about Event Hubs, visit these links:</span></span>

* [<span data-ttu-id="3d054-125">이벤트 허브 개요</span><span class="sxs-lookup"><span data-stu-id="3d054-125">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="3d054-126">이벤트 허브 API 개요</span><span class="sxs-lookup"><span data-stu-id="3d054-126">Event Hubs API overview</span></span>](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/