---
title: "Azure Queue 저장소 소개 | Microsoft Docs"
description: "Azure Queue 저장소 소개"
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
ms.openlocfilehash: 4db7552a1b76c89151405c55c8682abbb5326bb6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-queues"></a><span data-ttu-id="18244-103">큐 소개</span><span class="sxs-lookup"><span data-stu-id="18244-103">Introduction to Queues</span></span>

<span data-ttu-id="18244-104">Azure 큐 저장소는 HTTP 또는 HTTPS를 사용하여 인증된 호출을 통해 전 세계 어디에서나 액세스할 수 있는 다수의 메시지를 저장하기 위한 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="18244-104">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="18244-105">단일 큐 메시지의 크기는 최대 64KB일 수 있으며, 하나의 큐에 저장소 계정의 총 용량 제한까지 수백만 개의 메시지가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18244-105">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span>

## <a name="common-uses"></a><span data-ttu-id="18244-106">일반적인 사용</span><span class="sxs-lookup"><span data-stu-id="18244-106">Common uses</span></span>

<span data-ttu-id="18244-107">큐 저장소의 일반적인 사용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="18244-107">Common uses of Queue storage include:</span></span>

* <span data-ttu-id="18244-108">비동기적으로 처리할 작업 백로그 만들기</span><span class="sxs-lookup"><span data-stu-id="18244-108">Creating a backlog of work to process asynchronously</span></span>
* <span data-ttu-id="18244-109">Azure 웹 역할에서 Azure 작업자 역할로 메시지 전달</span><span class="sxs-lookup"><span data-stu-id="18244-109">Passing messages from an Azure web role to an Azure worker role</span></span>

## <a name="queue-service-concepts"></a><span data-ttu-id="18244-110">큐 서비스 개념</span><span class="sxs-lookup"><span data-stu-id="18244-110">Queue service concepts</span></span>

<span data-ttu-id="18244-111">큐 서비스에는 다음 구성 요소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="18244-111">The Queue service contains the following components:</span></span>

![큐 개념](./media/storage-queues-introduction/queue1.png)

* <span data-ttu-id="18244-113">**URL 형식:** 다음 URL 형식을 사용하여 큐에 주소를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18244-113">**URL format:** Queues are addressable using the following URL format:</span></span>   
    <span data-ttu-id="18244-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span><span class="sxs-lookup"><span data-stu-id="18244-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span></span> 
  
    <span data-ttu-id="18244-115">다음 URL은 다이어그램에 있는 큐의 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="18244-115">The following URL addresses a queue in the diagram:</span></span>  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* <span data-ttu-id="18244-116">**저장소 계정:** Azure Storage에 대한 모든 액세스는 저장소 계정을 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="18244-116">**Storage account:** All access to Azure Storage is done through a storage account.</span></span> <span data-ttu-id="18244-117">저장소 계정 용량에 대한 자세한 내용은 [Azure 저장소 확장성 및 성능 목표](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) (영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="18244-117">See [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) for details about storage account capacity.</span></span>

* <span data-ttu-id="18244-118">**큐:** 큐에는 메시지 집합이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="18244-118">**Queue:** A queue contains a set of messages.</span></span> <span data-ttu-id="18244-119">모든 메시지는 큐에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18244-119">All messages must be in a queue.</span></span> <span data-ttu-id="18244-120">큐 이름은 모두 소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18244-120">Note that the queue name must be all lowercase.</span></span> <span data-ttu-id="18244-121">큐의 명명에 대한 자세한 내용은 [큐 및 메타데이터 명명](https://msdn.microsoft.com/library/azure/dd179349.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18244-121">For information on naming queues, see [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

* <span data-ttu-id="18244-122">**메시지:** 최대 64KB인 임의 형식의 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="18244-122">**Message:** A message, in any format, of up to 64 KB.</span></span> <span data-ttu-id="18244-123">메시지가 큐에 남아 있을 수 있는 최대 시간은 7일입니다.</span><span class="sxs-lookup"><span data-stu-id="18244-123">The maximum time that a message can remain in the queue is seven days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18244-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="18244-124">Next steps</span></span>

* [<span data-ttu-id="18244-125">저장소 계정을 만드는</span><span class="sxs-lookup"><span data-stu-id="18244-125">Create a storage account</span></span>](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="18244-126">.NET을 사용하여 큐 시작하기</span><span class="sxs-lookup"><span data-stu-id="18244-126">Getting started with Queues using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
