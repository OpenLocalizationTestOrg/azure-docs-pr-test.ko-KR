---
title: "aaaAvailability Azure 이벤트 허브의 | Microsoft Docs"
description: "어떻게 tooprovide hello 최대한의 가용성 및 사용 하 여 Azure 이벤트 허브와의 일관성을 분할 합니다."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 8f3637a1-bbd7-481e-be49-b3adf9510ba1
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a8ededaae1589830da21cb8910ca694d2d628bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a><span data-ttu-id="f93d6-103">Event Hubs의 가용성 및 일관성</span><span class="sxs-lookup"><span data-stu-id="f93d6-103">Availability and consistency in Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="f93d6-104">개요</span><span class="sxs-lookup"><span data-stu-id="f93d6-104">Overview</span></span>
<span data-ttu-id="f93d6-105">Azure 이벤트 허브를 사용 하 여 한 [모델 분할](event-hubs-features.md#partitions) tooimprove 가용성 및 단일 이벤트 허브 내 평행 화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-105">Azure Event Hubs uses a [partitioning model](event-hubs-features.md#partitions) tooimprove availability and parallelization within a single event hub.</span></span> <span data-ttu-id="f93d6-106">예를 들어 이벤트 허브는 4 개의 파티션이 경우 부하 분산 작업에서에서 tooanother 하나의 서버에서에서 이동의 해당 파티션 중 하나 있습니다 여전히 보내고 받을 수에서 다른 3 개의 파티션과 합니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-106">For example, if an event hub has four partitions, and one of those partitions is moved from one server tooanother in a load balancing operation, you can still send and receive from three other partitions.</span></span> <span data-ttu-id="f93d6-107">더욱이, 파티션을 더 필요 하면 toohave 집계 된 처리량을 향상 더 많은 동시 판독기 데이터를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-107">Additionally, having more partitions enables you toohave more concurrent readers processing your data, improving your aggregate throughput.</span></span> <span data-ttu-id="f93d6-108">분할 및 순서는 분산된 시스템에서의 hello 의미를 이해 하는 것은 솔루션 디자인의 중요 한 측면입니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-108">Understanding hello implications of partitioning and ordering in a distributed system is a critical aspect of solution design.</span></span>

<span data-ttu-id="f93d6-109">toohelp 순서 지정 및 가용성 사이의 절충 값 hello 설명, hello 참조 [CAP 정리](https://en.wikipedia.org/wiki/CAP_theorem)가나다의 정리 라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-109">toohelp explain hello trade-off between ordering and availability, see hello [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem), also known as Brewer's theorem.</span></span> <span data-ttu-id="f93d6-110">이 정리, 일관성, 가용성 및 파티션 허용 오차 사이 hello 선택을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-110">This theorem discusses hello choice between consistency, availability, and partition tolerance.</span></span>

<span data-ttu-id="f93d6-111">Brewer의 정리는 일관성 및 가용성을 다음과 같이 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-111">Brewer's theorem defines consistency and availability as follows:</span></span>
* <span data-ttu-id="f93d6-112">허용 오차를 파티션: hello 파티션 오류가 발생 하는 경우에 데이터를 처리 하는 데이터 처리 시스템 toocontinue의 능력입니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-112">Partition tolerance: hello ability of a data processing system toocontinue processing data even if a partition failure occurs.</span></span>
* <span data-ttu-id="f93d6-113">가용성: 실패하지 않은 노드가 오류 또는 시간 제한 없이 적절한 시간 내에 적절한 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-113">Availability: a non-failing node returns a reasonable response within a reasonable amount of time (with no errors or timeouts).</span></span>
* <span data-ttu-id="f93d6-114">일관성: 읽기 tooreturn hello 지정된 된 클라이언트에 대 한 가장 최근의 쓰기가 보장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-114">Consistency: a read is guaranteed tooreturn hello most recent write for a given client.</span></span>

## <a name="partition-tolerance"></a><span data-ttu-id="f93d6-115">파티션 허용 오차</span><span class="sxs-lookup"><span data-stu-id="f93d6-115">Partition tolerance</span></span>
<span data-ttu-id="f93d6-116">Event Hubs는 분할된 데이터 모델을 기반으로 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-116">Event Hubs is built on top of a partitioned data model.</span></span> <span data-ttu-id="f93d6-117">설치 하는 동안 이벤트 허브에 hello 파티션 수를 구성할 수 있지만 나중에이 값을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-117">You can configure hello number of partitions in your event hub during setup, but you cannot change this value later.</span></span> <span data-ttu-id="f93d6-118">파티션은 이벤트 허브를 사용 해야 하므로 해야 toomake 가용성과 일관성을 유지 하는 방법에 대 한 의사 결정 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-118">Since you must use partitions with Event Hubs, you have toomake a decision about availability and consistency for your application.</span></span>

## <a name="availability"></a><span data-ttu-id="f93d6-119">Availability</span><span class="sxs-lookup"><span data-stu-id="f93d6-119">Availability</span></span>
<span data-ttu-id="f93d6-120">hello 가장 간단한 방법은 tooget 시작 이벤트 허브는 toouse hello 기본 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-120">hello simplest way tooget started with Event Hubs is toouse hello default behavior.</span></span> <span data-ttu-id="f93d6-121">새 만들면 `EventHubClient` 개체 및 hello를 사용 하 여 `Send` 메서드를 이벤트에서 이벤트 허브 파티션 간에 자동으로 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-121">If you create a new `EventHubClient` object and use hello `Send` method, your events are automatically distributed between partitions in your event hub.</span></span> <span data-ttu-id="f93d6-122">이 동작은 hello 최대한의 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-122">This behavior allows for hello greatest amount of up time.</span></span>

<span data-ttu-id="f93d6-123">이 모델은 hello 최대 시간을 필요로 하는 사용 사례에 대 한 기본 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-123">For use cases that require hello maximum up time, this model is preferred.</span></span>

## <a name="consistency"></a><span data-ttu-id="f93d6-124">일관성</span><span class="sxs-lookup"><span data-stu-id="f93d6-124">Consistency</span></span>
<span data-ttu-id="f93d6-125">일부 시나리오에서는 이벤트의 순서 지정 hello 중요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-125">In some scenarios, hello ordering of events can be important.</span></span> <span data-ttu-id="f93d6-126">예를 들어 프로그램 백 엔드 시스템 tooprocess delete 명령 전에 update 명령을 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-126">For example, you may want your back-end system tooprocess an update command before a delete command.</span></span> <span data-ttu-id="f93d6-127">이 경우에는 이벤트에 hello 파티션 키를 설정 하거나 사용 하 여 한 `PartitionSender` 개체 tooonly 보낼 이벤트 tooa 특정 파티션 합니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-127">In this instance, you can either set hello partition key on an event, or use a `PartitionSender` object tooonly send events tooa certain partition.</span></span> <span data-ttu-id="f93d6-128">이렇게 하면 이러한 이벤트는 hello 파티션에서 읽으면 순서로 읽어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-128">Doing so ensures that when these events are read from hello partition, they are read in order.</span></span>

<span data-ttu-id="f93d6-129">이 구성을 사용 하 여 보내는 hello 특정 파티션의 toowhich 사용할 수 없는 경우 오류 응답이 수신 됩니다 염두에서에 둬야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-129">With this configuration, keep in mind that if hello particular partition toowhich you are sending is unavailable, you will receive an error response.</span></span> <span data-ttu-id="f93d6-130">이벤트 허브 서비스 hello 선호도 tooa 단일 파티션에 없는 비교의 점으로 사용자 이벤트 toohello 사용 가능한 다음 파티션을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-130">As a point of comparison, if you do not have an affinity tooa single partition, hello Event Hubs service sends your event toohello next available partition.</span></span>

<span data-ttu-id="f93d6-131">순서 지정도 작동 시간을 극대화 하는 동안 한 가능한 해결 방법 tooensure 이벤트 처리 응용 프로그램의 일부로 tooaggregate 이벤트 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-131">One possible solution tooensure ordering, while also maximizing up time, would be tooaggregate events as part of your event processing application.</span></span> <span data-ttu-id="f93d6-132">이 가장 쉬운 방법은 tooaccomplish hello toostamp 사용자 정의 시퀀스 번호 속성을 갖는 사용자 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-132">hello easiest way tooaccomplish this is toostamp your event with a custom sequence number property.</span></span> <span data-ttu-id="f93d6-133">hello 코드 다음 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-133">hello following code shows an example:</span></span>

```csharp
// Get hello latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

<span data-ttu-id="f93d6-134">이 예제에서는 이벤트 허브에서 사용자 이벤트 tooone hello 사용 가능한 파티션 보내고 응용 프로그램에서 시퀀스 번호를 해당 하는 hello를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-134">This example sends your event tooone of hello available partitions in your event hub, and sets hello corresponding sequence number from your application.</span></span> <span data-ttu-id="f93d6-135">이 솔루션 상태 toobe 처리 응용 프로그램에 의해 유지 하는데 프로그램 보낸 사람을 사용할 수 있는 가능성이 toobe 되는 끝점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-135">This solution requires state toobe kept by your processing application, but gives your senders an endpoint that is more likely toobe available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f93d6-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f93d6-136">Next steps</span></span>
<span data-ttu-id="f93d6-137">Hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f93d6-137">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="f93d6-138">Event Hubs 서비스 개요</span><span class="sxs-lookup"><span data-stu-id="f93d6-138">Event Hubs service overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="f93d6-139">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="f93d6-139">Create an event hub</span></span>](event-hubs-create.md)
