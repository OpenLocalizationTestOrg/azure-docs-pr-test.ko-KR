---
title: "Azure Service Fabric 신뢰할 수 있는 상태 관리자 및 신뢰할 수 있는 컬렉션 내부 | Microsoft Docs"
description: "신뢰할 수 있는 컬렉션 개념 및 Azure Service Fabric의 디자인에 대해 자세히 알아봅니다."
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: d607449a16e886337ab1bd96213fbb4231124353
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a><span data-ttu-id="f0b13-103">Azure Service Fabric 신뢰할 수 있는 상태 관리자 및 신뢰할 수 있는 컬렉션 내부</span><span class="sxs-lookup"><span data-stu-id="f0b13-103">Azure Service Fabric Reliable State Manager and Reliable Collection internals</span></span>
<span data-ttu-id="f0b13-104">이 문서에서는 신뢰할 수 있는 상태 관리자 및 신뢰할 수 있는 컬렉션 내부를 탐구하여 핵심 구성 요소가 백그라운드에서 어떻게 작동하는지 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="f0b13-104">This document delves inside Reliable State Manager and Reliable Collections to see how core components work behind the scenes.</span></span>

> [!NOTE]
> <span data-ttu-id="f0b13-105">이 문서는 진행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b13-105">This document is work in-progress.</span></span> <span data-ttu-id="f0b13-106">이 문서에 의견을 추가하여 자세히 알고 싶은 항목을 알려주세요.</span><span class="sxs-lookup"><span data-stu-id="f0b13-106">Add comments to this article to tell us what topic you would like to learn more about.</span></span>
>

##  <a name="local-persistence-model-log-and-checkpoint"></a><span data-ttu-id="f0b13-107">로컬 지속성 모델: 로그 및 검사점</span><span class="sxs-lookup"><span data-stu-id="f0b13-107">Local persistence model: log and checkpoint</span></span>
<span data-ttu-id="f0b13-108">신뢰할 수 있는 상태 관리자와 신뢰할 수 있는 컬렉션은 로그 및 검사점이라고 하는 지속성 모델을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f0b13-108">The Reliable State Manager and Reliable Collections follow a persistence model that is called Log and Checkpoint.</span></span>
<span data-ttu-id="f0b13-109">이 모델에서 각 상태 변경은 먼저 디스크에 기록된 후 메모리에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b13-109">In this model, each state change is logged on disk first and then applied in memory.</span></span>
<span data-ttu-id="f0b13-110">전체 상태 자체는 가끔씩만 유지됩니다.(즉,</span><span class="sxs-lookup"><span data-stu-id="f0b13-110">The complete state itself is persisted only occasionally (a.k.a.</span></span> <span data-ttu-id="f0b13-111">검사점).</span><span class="sxs-lookup"><span data-stu-id="f0b13-111">Checkpoint).</span></span>
<span data-ttu-id="f0b13-112">이를 통해 성능 향상을 위해 델타가 디스크에 대한 순차 추가 전용 쓰기로 변환된다는 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b13-112">The benefit is that deltas are turned into sequential append-only writes on disk for improved performance.</span></span>

<span data-ttu-id="f0b13-113">로그 및 검사점 모델을 보다 잘 이해하기 위해 먼저 무한 디스크 시나리오를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b13-113">To better understand the Log and Checkpoint model, let’s first look at the infinite disk scenario.</span></span>
<span data-ttu-id="f0b13-114">신뢰할 수 있는 상태 관리자는 복제되기 전에 모든 작업을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b13-114">The Reliable State Manager logs every operation before it is replicated.</span></span>
<span data-ttu-id="f0b13-115">로깅하면 신뢰할 수 있는 컬렉션이 해당 작업만 메모리에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b13-115">Logging allows the Reliable Collections to apply the operation only in memory.</span></span>
<span data-ttu-id="f0b13-116">로그가 유지되므로 복제본이 실패하고 다시 시작해야 하는 경우에도 신뢰할 수 있는 상태 관리자에게 복제본이 손실한 모든 작업을 재생할 충분한 정보가 로그에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b13-116">Since logs are persisted, even when the replica fails and needs to be restarted, the Reliable State Manager has enough information in its log to replay all the operations the replica has lost.</span></span>
<span data-ttu-id="f0b13-117">디스크가 무한이므로 로그 레코드를 제거할 필요가 없고 신뢰할 수 있는 컬렉션만 메모리 내 상태를 관리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b13-117">As the disk is infinite, log records never need to be removed and the Reliable Collection needs to manage only the in-memory state.</span></span>

<span data-ttu-id="f0b13-118">이제 한정된 디스크 시나리오를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b13-118">Now let’s look at the finite disk scenario.</span></span>
<span data-ttu-id="f0b13-119">로그 레코드가 누적되면 신뢰할 수 있는 상태 관리자에게 디스크 공간이 부족한 경우가 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="f0b13-119">As log records accumulate, the Reliable State Manager will run out of disk space.</span></span>
<span data-ttu-id="f0b13-120">이런 일이 발생하기 전에 신뢰할 수 있는 상태 관리자가 로그를 잘라서 최신 레코드를 위한 공간을 확보해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b13-120">Before that happens, the Reliable State Manager needs to truncate its log to make room for the newer records.</span></span>
<span data-ttu-id="f0b13-121">신뢰할 수 있는 상태 관리자는 디스크에 대해 신뢰할 수 있는 컬렉션에 메모리 내 상태의 검사점을 설정하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b13-121">Reliable State Manager requests the Reliable Collections to checkpoint their in-memory state to disk.</span></span>
<span data-ttu-id="f0b13-122">이 시점에서 신뢰할 수 있는 컬렉션은 메모리 내 상태를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b13-122">At this point, the Reliable Collections' would persist its in-memory state.</span></span>
<span data-ttu-id="f0b13-123">신뢰할 수 있는 컬렉션이 검사점을 완료하면 신뢰할 수 있는 상태 관리자가 로그를 잘라서 디스크 공간을 확보할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b13-123">Once the Reliable Collections complete their checkpoints, the Reliable State Manager can truncate the log to free up disk space.</span></span>
<span data-ttu-id="f0b13-124">복제본을 다시 시작해야 하는 경우 신뢰할 수 있는 컬렉션이 검사점이 설정된 상태를 복구하고, 신뢰할 수 있는 상태 관리자가 마지막 검사점 이후 발생한 모든 상태 변경 내용을 다시 재생합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b13-124">When the replica needs to be restarted, Reliable Collections recover their checkpointed state, and the Reliable State Manager recovers and plays back all the state changes that occurred since the last checkpoint.</span></span>

<span data-ttu-id="f0b13-125">검사점에 다른 값이 추가되면 일반적인 시나리오에서 복구 시간이 개선됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b13-125">Another value add of checkpointing is that it improves recovery times in common scenarios.</span></span> <span data-ttu-id="f0b13-126">로그에는 마지막 검사점 이후 발생한 모든 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b13-126">Log contains all operations that have happened since the last checkpoint.</span></span>
<span data-ttu-id="f0b13-127">따라서 신뢰할 수 있는 사전에서 지정된 행에 대한 여러 값과 같이 항목의 여러 버전이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b13-127">So it may include multiple versions of an item like multiple values for a given row in Reliable Dictionary.</span></span>
<span data-ttu-id="f0b13-128">반대로, 신뢰할 수 있는 컬렉션 검사점은 키에 대한 각 값의 최신 버전에만 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b13-128">In contrast, a Reliable Collection checkpoints only the latest version of each value for a key.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0b13-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f0b13-129">Next steps</span></span>
* [<span data-ttu-id="f0b13-130">트랜잭션 및 잠금</span><span class="sxs-lookup"><span data-stu-id="f0b13-130">Transactions and Locks</span></span>](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

