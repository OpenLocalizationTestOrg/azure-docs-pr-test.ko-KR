---
title: "Apache Kafka를 통한 고가용성 - Azure HDInsight | Microsoft Docs"
description: "Azure HDInsight의 Apache Kafka를 사용하여 고가용성을 보장하는 방법을 알아봅니다. HDInsight가 포함된 Azure 지역 내의 여러 장애 도메인에 있도록 Kafka에서 파티션 복제본의 균형을 다시 조정하는 방법을 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: f8164d1c3483b28e5f2abcc8035da78880daec1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="541d2-104">HDInsight의 Apache Kafka(미리 보기)를 통한 데이터 고가용성</span><span class="sxs-lookup"><span data-stu-id="541d2-104">High availability of your data with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="541d2-105">기본 하드웨어 랙 구성을 활용하기 위해 Kafka 토픽에 대한 파티션 복제본을 구성하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="541d2-105">Learn how to configure partition replicas for Kafka topics to take advantage of underlying hardware rack configuration.</span></span> <span data-ttu-id="541d2-106">이 구성은 HDInsight의 Apache Kafka에 저장된 데이터의 가용성을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="541d2-106">This configuration ensures the availability of data stored in Apache Kafka on HDInsight.</span></span>

## <a name="fault-and-update-domains-with-kafka"></a><span data-ttu-id="541d2-107">Kafka를 사용하는 장애 및 업데이트 도메인</span><span class="sxs-lookup"><span data-stu-id="541d2-107">Fault and update domains with Kafka</span></span>

<span data-ttu-id="541d2-108">장애 도메인은 Azure 데이터 센터에 있는 기본 하드웨어의 논리적 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="541d2-108">A fault domain is a logical grouping of underlying hardware in an Azure data center.</span></span> <span data-ttu-id="541d2-109">장애 도메인마다 공통 전원과 네트워크 스위치를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="541d2-109">Each fault domain shares a common power source and network switch.</span></span> <span data-ttu-id="541d2-110">HDInsight 클러스터 내의 노드를 구현하는 가상 컴퓨터와 관리 디스크는 이러한 장애 도메인에 분산되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="541d2-110">The virtual machines and managed disks that implement the nodes within an HDInsight cluster are distributed across these fault domains.</span></span> <span data-ttu-id="541d2-111">이 아키텍처에서는 실제 하드웨어 오류의 잠재적 영향을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="541d2-111">This architecture limits the potential impact of physical hardware failures.</span></span>

<span data-ttu-id="541d2-112">Azure 지역마다 특정 수의 장애 도메인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="541d2-112">Each Azure region has a specific number of fault domains.</span></span> <span data-ttu-id="541d2-113">도메인 목록과 해당 도메인에 포함된 장애 도메인의 수에 대한 내용은 [가용성 집합](../virtual-machines/linux/regions-and-availability.md#availability-sets) 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="541d2-113">For a list of domains and the number of fault domains they contain, see the [Availability sets](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="541d2-114">Kafka는 장애 도메인을 인식하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="541d2-114">Kafka is not aware of fault domains.</span></span> <span data-ttu-id="541d2-115">Kafka에서 토픽을 만들 때 모든 파티션 복제본을 동일한 장애 도메인에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="541d2-115">When you create a topic in Kafka, it may store all partition replicas in the same fault domain.</span></span> <span data-ttu-id="541d2-116">이 문제를 해결하기 위해 [Kafka 파티션 리밸런스 도구](https://github.com/hdinsight/hdinsight-kafka-tools)(영문)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="541d2-116">To solve this problem, we provide the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span></span>

## <a name="when-to-rebalance-partition-replicas"></a><span data-ttu-id="541d2-117">파티션 복제본의 부하를 다시 조정해야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="541d2-117">When to rebalance partition replicas</span></span>

<span data-ttu-id="541d2-118">가장 높은 Kafka 데이터 가용성을 보장하려면 다음과 같은 경우에 토픽에 대한 파티션 복제본의 부하를 다시 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="541d2-118">To ensure the highest availability of your Kafka data, you should rebalance the partition replicas for your topic at the following times:</span></span>

* <span data-ttu-id="541d2-119">새 토픽 또는 파티션을 만들 때</span><span class="sxs-lookup"><span data-stu-id="541d2-119">When a new topic or partition is created</span></span>

* <span data-ttu-id="541d2-120">클러스터를 확장할 때</span><span class="sxs-lookup"><span data-stu-id="541d2-120">When you scale up a cluster</span></span>

## <a name="replication-factor"></a><span data-ttu-id="541d2-121">복제 계수</span><span class="sxs-lookup"><span data-stu-id="541d2-121">Replication factor</span></span>

> [!IMPORTANT]
> <span data-ttu-id="541d2-122">3개의 장애 도메인을 포함하는 Azure 지역을 사용하고 복제 계수로 3을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="541d2-122">We recommend using an Azure region that contains three fault domains, and using a replication factor of 3.</span></span>

<span data-ttu-id="541d2-123">2개의 장애 도메인만 포함하는 지역을 사용해야 하는 경우 복제 계수로 4를 사용하여 두 장애 도메인에 복제본을 동일하게 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="541d2-123">If you must use a region that contains only two fault domains, use a replication factor of 4 to spread the replicas evenly across the two fault domains.</span></span>

<span data-ttu-id="541d2-124">토픽을 만들고 복제 계수를 설정하는 예제는 [HDInsight의 Kafka 시작](hdinsight-apache-kafka-get-started.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="541d2-124">For an example of creating topics and setting the replication factor, see the [Start with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span>

## <a name="how-to-rebalance-partition-replicas"></a><span data-ttu-id="541d2-125">파티션 복제본의 부하를 다시 조정하는 방법</span><span class="sxs-lookup"><span data-stu-id="541d2-125">How to rebalance partition replicas</span></span>

<span data-ttu-id="541d2-126">[Kafka 파티션 리밸런스 도구](https://github.com/hdinsight/hdinsight-kafka-tools)를 사용하여 선택한 토픽의 부하를 다시 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="541d2-126">Use the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools) to rebalance selected topics.</span></span> <span data-ttu-id="541d2-127">이 도구는 SSH 세션에서 Kafka 클러스터의 헤드 노드로 실행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="541d2-127">This tool must be ran from an SSH session to the head node of your Kafka cluster.</span></span>

<span data-ttu-id="541d2-128">SSH를 사용하여 HDInsight에 연결하는 방법에 대한 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="541d2-128">For more information on connecting to HDInsight using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="541d2-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="541d2-129">Next steps</span></span>

* [<span data-ttu-id="541d2-130">HDInsight의 Kafka 확장성</span><span class="sxs-lookup"><span data-stu-id="541d2-130">Scalability of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* [<span data-ttu-id="541d2-131">HDInsight의 Kafka 미러링</span><span class="sxs-lookup"><span data-stu-id="541d2-131">Mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)