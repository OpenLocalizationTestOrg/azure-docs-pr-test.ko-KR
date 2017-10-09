---
title: "큐 저장소 aaaIntroduction tooAzure | Microsoft Docs"
description: "소개 tooAzure 큐 저장소"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: robinsh
ms.openlocfilehash: 669effedff7beedde8a119c350a2a70edafedcf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooqueues"></a><span data-ttu-id="66a10-103">소개 tooQueues</span><span class="sxs-lookup"><span data-stu-id="66a10-103">Introduction tooQueues</span></span>

<span data-ttu-id="66a10-104">Azure 큐 저장소는 많은 수의 액세스할 수 있는에서 아무 곳 이나 HTTP 또는 HTTPS를 사용 하 여 인증 된 호출을 통해 hello world에 메시지를 저장 하기 위한 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="66a10-104">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="66a10-105">단일 큐 메시지의 크기 (kb) too64 될 수 있습니다 및 큐 수많은 메시지 저장소 계정의 toohello 총 용량 한계를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66a10-105">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

## <a name="common-uses"></a><span data-ttu-id="66a10-106">일반적인 사용</span><span class="sxs-lookup"><span data-stu-id="66a10-106">Common uses</span></span>

<span data-ttu-id="66a10-107">큐 저장소의 일반적인 사용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="66a10-107">Common uses of Queue storage include:</span></span>

* <span data-ttu-id="66a10-108">작업 tooprocess의 백로그를 비동기적으로 만들기</span><span class="sxs-lookup"><span data-stu-id="66a10-108">Creating a backlog of work tooprocess asynchronously</span></span>
* <span data-ttu-id="66a10-109">Azure 웹 역할 tooan Azure 작업자 역할에서 메시지를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="66a10-109">Passing messages from an Azure web role tooan Azure worker role</span></span>

## <a name="queue-service-concepts"></a><span data-ttu-id="66a10-110">큐 서비스 개념</span><span class="sxs-lookup"><span data-stu-id="66a10-110">Queue service concepts</span></span>

<span data-ttu-id="66a10-111">hello를 큐 서비스는 hello를 다음과 같은 구성 요소가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66a10-111">hello Queue service contains hello following components:</span></span>

![큐 개념](./media/storage-queues-introduction/queue1.png)

* <span data-ttu-id="66a10-113">**URL 형식:** 큐는 주소 지정 가능한 URL 형식에 따라 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="66a10-113">**URL format:** Queues are addressable using hello following URL format:</span></span>   
    <span data-ttu-id="66a10-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span><span class="sxs-lookup"><span data-stu-id="66a10-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span></span> 
  
    <span data-ttu-id="66a10-115">url hello hello 다이어그램의 큐를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66a10-115">hello following URL addresses a queue in hello diagram:</span></span>  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* <span data-ttu-id="66a10-116">**저장소 계정:** 저장소 계정을 통해 모든 액세스 tooAzure 저장소 작업은 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a10-116">**Storage account:** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="66a10-117">저장소 계정 용량에 대한 자세한 내용은 [Azure 저장소 확장성 및 성능 목표](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) (영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="66a10-117">See [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) for details about storage account capacity.</span></span>

* <span data-ttu-id="66a10-118">**큐:** 큐에는 메시지 집합이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a10-118">**Queue:** A queue contains a set of messages.</span></span> <span data-ttu-id="66a10-119">모든 메시지는 큐에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66a10-119">All messages must be in a queue.</span></span> <span data-ttu-id="66a10-120">Note 해당 hello 큐 이름은 모두 소문자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66a10-120">Note that hello queue name must be all lowercase.</span></span> <span data-ttu-id="66a10-121">큐의 명명에 대한 자세한 내용은 [큐 및 메타데이터 명명](https://msdn.microsoft.com/library/azure/dd179349.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66a10-121">For information on naming queues, see [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

* <span data-ttu-id="66a10-122">**메시지:** A 메시지, 모든 형식으로의 too64 KB를 합니다.</span><span class="sxs-lookup"><span data-stu-id="66a10-122">**Message:** A message, in any format, of up too64 KB.</span></span> <span data-ttu-id="66a10-123">hello 메시지 hello 큐에 남아 있을 수 있는 최대 시간은 7 일입니다.</span><span class="sxs-lookup"><span data-stu-id="66a10-123">hello maximum time that a message can remain in hello queue is seven days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66a10-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="66a10-124">Next steps</span></span>

* [<span data-ttu-id="66a10-125">저장소 계정을 만드는</span><span class="sxs-lookup"><span data-stu-id="66a10-125">Create a storage account</span></span>](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="66a10-126">.NET을 사용하여 큐 시작하기</span><span class="sxs-lookup"><span data-stu-id="66a10-126">Getting started with Queues using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
