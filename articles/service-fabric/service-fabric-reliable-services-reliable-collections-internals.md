---
title: "서비스 패브릭 신뢰할 수 있는 상태 관리자 및 신뢰할 수 있는 컬렉션 내부 aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 651bfb52785a2475e4840cd471e87220d1936391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a><span data-ttu-id="42b82-103">Azure Service Fabric 신뢰할 수 있는 상태 관리자 및 신뢰할 수 있는 컬렉션 내부</span><span class="sxs-lookup"><span data-stu-id="42b82-103">Azure Service Fabric Reliable State Manager and Reliable Collection internals</span></span>
<span data-ttu-id="42b82-104">이 문서는 hello 백그라운드 핵심 구성 요소가 작동 하는 방법을 신뢰할 수 있는 상태 관리자 및 신뢰할 수 있는 컬렉션 toosee 내를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b82-104">This document delves inside Reliable State Manager and Reliable Collections toosee how core components work behind hello scenes.</span></span>

> [!NOTE]
> <span data-ttu-id="42b82-105">이 문서는 진행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="42b82-105">This document is work in-progress.</span></span> <span data-ttu-id="42b82-106">주석 toothis 문서 tootell us 추가 주제 선택에 대 한 자세한 toolearn 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b82-106">Add comments toothis article tootell us what topic you would like toolearn more about.</span></span>
>

##  <a name="local-persistence-model-log-and-checkpoint"></a><span data-ttu-id="42b82-107">로컬 지속성 모델: 로그 및 검사점</span><span class="sxs-lookup"><span data-stu-id="42b82-107">Local persistence model: log and checkpoint</span></span>
<span data-ttu-id="42b82-108">신뢰할 수 있는 상태 관리자 hello 및 신뢰할 수 있는 컬렉션 로그 및 검사점 라고 하는 지 속성 모델을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="42b82-108">hello Reliable State Manager and Reliable Collections follow a persistence model that is called Log and Checkpoint.</span></span>
<span data-ttu-id="42b82-109">이 모델에서 각 상태 변경은 먼저 디스크에 기록된 후 메모리에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="42b82-109">In this model, each state change is logged on disk first and then applied in memory.</span></span>
<span data-ttu-id="42b82-110">hello 완료 상태 자체 (규칙 하위 유지 가끔씩만</span><span class="sxs-lookup"><span data-stu-id="42b82-110">hello complete state itself is persisted only occasionally (a.k.a.</span></span> <span data-ttu-id="42b82-111">검사점).</span><span class="sxs-lookup"><span data-stu-id="42b82-111">Checkpoint).</span></span>
<span data-ttu-id="42b82-112">hello 이점은 델타 순차적 추가 전용 디스크에 대 한 쓰기 성능 향상된으로 설정 되어입니다.</span><span class="sxs-lookup"><span data-stu-id="42b82-112">hello benefit is that deltas are turned into sequential append-only writes on disk for improved performance.</span></span>

<span data-ttu-id="42b82-113">toobetter는 hello 로그 및 검사점 모델을 먼저 살펴보겠습니다 hello 무한 디스크 시나리오.</span><span class="sxs-lookup"><span data-stu-id="42b82-113">toobetter understand hello Log and Checkpoint model, let’s first look at hello infinite disk scenario.</span></span>
<span data-ttu-id="42b82-114">신뢰할 수 있는 상태 관리자 hello 복제 되기 전에 모든 작업을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b82-114">hello Reliable State Manager logs every operation before it is replicated.</span></span>
<span data-ttu-id="42b82-115">로깅에는 메모리에만 hello 신뢰할 수 있는 컬렉션 tooapply hello 작업을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42b82-115">Logging allows hello Reliable Collections tooapply hello operation only in memory.</span></span>
<span data-ttu-id="42b82-116">로그는 유지 않으므로 hello 복제 실패 하 고 다시 시작 되 면 toobe 필요한 경우에 hello 신뢰할 수 있는 상태 관리자는 작업이 충분 한 정보에서 해당 로그 tooreplay 모든 hello hello 복제본 끊어졌습니다입니다.</span><span class="sxs-lookup"><span data-stu-id="42b82-116">Since logs are persisted, even when hello replica fails and needs toobe restarted, hello Reliable State Manager has enough information in its log tooreplay all hello operations hello replica has lost.</span></span>
<span data-ttu-id="42b82-117">Hello 디스크 유한 아니므로 로그 레코드가 제거 toobe 필요 하며 hello 신뢰할 수 있는 컬렉션 toomanage 유일한 hello 메모리 상태 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b82-117">As hello disk is infinite, log records never need toobe removed and hello Reliable Collection needs toomanage only hello in-memory state.</span></span>

<span data-ttu-id="42b82-118">이제 hello 유한 디스크 시나리오를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="42b82-118">Now let’s look at hello finite disk scenario.</span></span>
<span data-ttu-id="42b82-119">로그 레코드가 누적 hello 신뢰할 수 있는 상태 관리자는 디스크 공간 부족 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42b82-119">As log records accumulate, hello Reliable State Manager will run out of disk space.</span></span>
<span data-ttu-id="42b82-120">먼저 발생 하는 hello 신뢰할 수 있는 상태 관리자 해야 tootruncate hello 최신 레코드를 위한 해당 로그 toomake 공간.</span><span class="sxs-lookup"><span data-stu-id="42b82-120">Before that happens, hello Reliable State Manager needs tootruncate its log toomake room for hello newer records.</span></span>
<span data-ttu-id="42b82-121">신뢰할 수 있는 컬렉션 toocheckpoint의 메모리 내 상태 toodisk을 hello 하는 안정성 상태 관리자 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b82-121">Reliable State Manager requests hello Reliable Collections toocheckpoint their in-memory state toodisk.</span></span>
<span data-ttu-id="42b82-122">이 시점에서 hello 신뢰할 수 있는 컬렉션의 메모리 상태를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b82-122">At this point, hello Reliable Collections' would persist its in-memory state.</span></span>
<span data-ttu-id="42b82-123">해당 검사점을 완료 하는 hello 신뢰할 수 있는 컬렉션 hello 신뢰할 수 있는 상태 관리자 hello 로그 toofree 디스크 공간을 자를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42b82-123">Once hello Reliable Collections complete their checkpoints, hello Reliable State Manager can truncate hello log toofree up disk space.</span></span>
<span data-ttu-id="42b82-124">Hello 복제본 toobe 다시 시작 하면 신뢰할 수 있는 컬렉션 검사점 상태를 복구한 hello 신뢰할 수 있는 상태 관리자 복구 하 고 hello 마지막 검사점 이후에 발생 한 모든 hello 상태 변화를 재생 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b82-124">When hello replica needs toobe restarted, Reliable Collections recover their checkpointed state, and hello Reliable State Manager recovers and plays back all hello state changes that occurred since hello last checkpoint.</span></span>

<span data-ttu-id="42b82-125">검사점에 다른 값이 추가되면 일반적인 시나리오에서 복구 시간이 개선됩니다.</span><span class="sxs-lookup"><span data-stu-id="42b82-125">Another value add of checkpointing is that it improves recovery times in common scenarios.</span></span> <span data-ttu-id="42b82-126">로그는 hello 마지막 검사점 이후 발생 한 모든 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b82-126">Log contains all operations that have happened since hello last checkpoint.</span></span>
<span data-ttu-id="42b82-127">따라서 신뢰할 수 있는 사전에서 지정된 행에 대한 여러 값과 같이 항목의 여러 버전이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42b82-127">So it may include multiple versions of an item like multiple values for a given row in Reliable Dictionary.</span></span>
<span data-ttu-id="42b82-128">반면에 신뢰할 수 있는 컬렉션 검사점 키에 대 한 각 값의 최신 버전을만 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b82-128">In contrast, a Reliable Collection checkpoints only hello latest version of each value for a key.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42b82-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="42b82-129">Next steps</span></span>
* [<span data-ttu-id="42b82-130">트랜잭션 및 잠금</span><span class="sxs-lookup"><span data-stu-id="42b82-130">Transactions and Locks</span></span>](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

