---
title: "Azure 마이크로 서비스에서 상태 정의 및 관리| Microsoft Docs"
description: "서비스 패브릭에서 서비스 상태를 정의하고 관리하는 방법"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f5e618a5-3ea3-4404-94af-122278f91652
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 2f7835fab175bdb7ef7ce3894cab9e09a39457f3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="service-state"></a><span data-ttu-id="a5a50-103">서비스 상태</span><span class="sxs-lookup"><span data-stu-id="a5a50-103">Service state</span></span>
<span data-ttu-id="a5a50-104">**서비스 상태**는 서비스가 작동하기 위해 필요한 메모리 내 또는 디스크의 데이터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a5a50-104">**Service state** refers to the in-memory or on disk data that a service requires to function.</span></span> <span data-ttu-id="a5a50-105">예를 들어 서비스가 작업을 수행하기 위해 읽고 쓰는 데이터 구조 및 멤버 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a50-105">It includes, for example, the data structures and member variables that the service reads and writes to do work.</span></span> <span data-ttu-id="a5a50-106">서비스의 구성 방식에 따라 디스크에 저장되어 있는 파일이나 기타 리소스도 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a50-106">Depending on how the service is architected, it could also include files or other resources that are stored on disk.</span></span> <span data-ttu-id="a5a50-107">예를 들어 데이터베이스가 데이터 및 트랜잭션 로그를 저장하는 데 사용하는 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a50-107">For example, the files a database would use to store data and transaction logs.</span></span>

<span data-ttu-id="a5a50-108">예제 서비스로 계산기를 생각해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a50-108">As an example service, let's consider a calculator.</span></span> <span data-ttu-id="a5a50-109">기본 계산기 서비스는 두 개의 숫자를 받아 그 합계를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a50-109">A basic calculator service takes two numbers and returns their sum.</span></span> <span data-ttu-id="a5a50-110">이러한 계산 수행에는 멤버 변수나 기타 정보가 관련되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a50-110">Performing this calculation involves no member variables or other information.</span></span>

<span data-ttu-id="a5a50-111">이제 계산한 마지막 합계를 저장하고 반환하는 추가 메서드를 포함하는 동일한 계산기가 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a50-111">Now consider the same calculator, but with an additional method for storing and returning the last sum it has computed.</span></span> <span data-ttu-id="a5a50-112">이 서비스는 이제 상태를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a50-112">This service is now stateful.</span></span> <span data-ttu-id="a5a50-113">상태 저장은 새 합계를 계산할 때 쓰고, 마지막으로 계산한 합계를 반환하라는 요청을 받을 때 읽는 상태를 포함함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a50-113">Stateful means it contains some state that it writes to when it computes a new sum and reads from when you ask it to return the last computed sum.</span></span>

<span data-ttu-id="a5a50-114">Azure 서비스 패브릭에서 첫 번째 서비스는 상태 비저장 서비스라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a50-114">In Azure Service Fabric, the first service is called a stateless service.</span></span> <span data-ttu-id="a5a50-115">두 번째 서비스는 상태 저장 서비스라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a50-115">The second service is called a stateful service.</span></span>

## <a name="storing-service-state"></a><span data-ttu-id="a5a50-116">서비스 상태 저장</span><span class="sxs-lookup"><span data-stu-id="a5a50-116">Storing service state</span></span>
<span data-ttu-id="a5a50-117">상태는 외장화될 수도 있고 상태를 조작하는 코드와 함께 위치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a50-117">State can be either externalized or co-located with the code that is manipulating the state.</span></span> <span data-ttu-id="a5a50-118">상태의 외장화는 네트워크를 통해 여러 다른 컴퓨터에서 또는 같은 컴퓨터에서 out of process로 실행되는 기타 데이터 저장소 또는 외부 데이터베이스를 사용하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5a50-118">Externalization of state is typically done by using an external database or other data store that runs on different machines over the network or out of process on the same machine.</span></span> <span data-ttu-id="a5a50-119">계산기 예제에서는 SQL Database 또는 Azure Table Store의 인스턴스가 데이터 저장소일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a50-119">In our calculator example, the data store could be a SQL database or instance of Azure Table Store.</span></span> <span data-ttu-id="a5a50-120">모든 합계 계산 요청은 이 데이터에 대해 업데이트를 수행하고, 서비스에 대한 값 반환 요청은 저장소에서 현재 값을 가져오게 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a50-120">Every request to compute the sum performs an update on this data, and requests to the service to return the value result in the current value being fetched from the store.</span></span> 

<span data-ttu-id="a5a50-121">상태는 해당 상태를 조작하는 코드와 함께 위치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a50-121">State can also be co-located with the code that manipulates the state.</span></span> <span data-ttu-id="a5a50-122">Service Fabric의 상태 저장 서비스는 일반적으로 이 모델을 사용하여 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5a50-122">Stateful services in Service Fabric are typically built using this model.</span></span> <span data-ttu-id="a5a50-123">Service Fabric은 이 상태를 항상 사용 가능하게 하고, 일관되고 지속 가능하게 하고 이러한 방식으로 구축된 서비스를 쉽게 확장할 수 있도록 하는 인프라를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a50-123">Service Fabric provides the infrastructure to ensure that this state is highly available, consistent, and durable, and that the services built this way can easily scale.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5a50-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a5a50-124">Next steps</span></span>
<span data-ttu-id="a5a50-125">Service Fabric 개념에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5a50-125">For more information on Service Fabric concepts, see the following articles:</span></span>

* [<span data-ttu-id="a5a50-126">서비스 패브릭 서비스의 가용성</span><span class="sxs-lookup"><span data-stu-id="a5a50-126">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="a5a50-127">서비스 패브릭 서비스의 확장성</span><span class="sxs-lookup"><span data-stu-id="a5a50-127">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="a5a50-128">서비스 패브릭 서비스 분할</span><span class="sxs-lookup"><span data-stu-id="a5a50-128">Partitioning Service Fabric services</span></span>](service-fabric-concepts-partitioning.md)
* [<span data-ttu-id="a5a50-129">Service Fabric Reliable Services</span><span class="sxs-lookup"><span data-stu-id="a5a50-129">Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-introduction.md)
