---
title: "Apache Kafka-Azure HDInsight와 aaaHigh 가용성 | Microsoft Docs"
description: "자세한 내용은 어떻게 Azure HDInsight의 Apache Kafka 있는 고가용성 tooensure 합니다. HDInsight를 포함 하는 Azure 지역 hello 내에서 여러 오류 도메인에 있는 있도록 toorebalance Kafka의 복제본을 분할 하는 방법을 알아봅니다."
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
ms.openlocfilehash: 337468f36b531f83c2999e87907de89cf3d19dd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="4624f-104">HDInsight의 Apache Kafka(미리 보기)를 통한 데이터 고가용성</span><span class="sxs-lookup"><span data-stu-id="4624f-104">High availability of your data with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="4624f-105">기본 하드웨어 Kafka 항목 tootake 사용에 대 한 파티션 복제본 tooconfigure 구성 랙 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4624f-105">Learn how tooconfigure partition replicas for Kafka topics tootake advantage of underlying hardware rack configuration.</span></span> <span data-ttu-id="4624f-106">이 구성을 통해 hello 가용성 HDInsight의 Apache Kafka에 저장 된 데이터.</span><span class="sxs-lookup"><span data-stu-id="4624f-106">This configuration ensures hello availability of data stored in Apache Kafka on HDInsight.</span></span>

## <a name="fault-and-update-domains-with-kafka"></a><span data-ttu-id="4624f-107">Kafka를 사용하는 장애 및 업데이트 도메인</span><span class="sxs-lookup"><span data-stu-id="4624f-107">Fault and update domains with Kafka</span></span>

<span data-ttu-id="4624f-108">장애 도메인은 Azure 데이터 센터에 있는 기본 하드웨어의 논리적 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="4624f-108">A fault domain is a logical grouping of underlying hardware in an Azure data center.</span></span> <span data-ttu-id="4624f-109">장애 도메인마다 공통 전원과 네트워크 스위치를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="4624f-109">Each fault domain shares a common power source and network switch.</span></span> <span data-ttu-id="4624f-110">hello 가상 컴퓨터 및 hello 노드 HDInsight 클러스터 내에서 구현 하는 관리 되는 디스크는 이러한 오류 도메인에 걸쳐 분산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4624f-110">hello virtual machines and managed disks that implement hello nodes within an HDInsight cluster are distributed across these fault domains.</span></span> <span data-ttu-id="4624f-111">이 아키텍처는 hello 물리적 하드웨어 오류의 잠재적 영향을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="4624f-111">This architecture limits hello potential impact of physical hardware failures.</span></span>

<span data-ttu-id="4624f-112">Azure 지역마다 특정 수의 장애 도메인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4624f-112">Each Azure region has a specific number of fault domains.</span></span> <span data-ttu-id="4624f-113">도메인 및 hello 포함 하는 장애 도메인 수의 목록이 참조 hello [가용성 집합](../virtual-machines/linux/regions-and-availability.md#availability-sets) 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="4624f-113">For a list of domains and hello number of fault domains they contain, see hello [Availability sets](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4624f-114">Kafka는 장애 도메인을 인식하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4624f-114">Kafka is not aware of fault domains.</span></span> <span data-ttu-id="4624f-115">Hello에서 모든 파티션 복제본을 저장할 수 있습니다 Kafka에 항목을 만들 때 동일한 장애 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="4624f-115">When you create a topic in Kafka, it may store all partition replicas in hello same fault domain.</span></span> <span data-ttu-id="4624f-116">toosolve hello 제공이 문제를 [Kafka 파티션을 리 밸런스 도구](https://github.com/hdinsight/hdinsight-kafka-tools)합니다.</span><span class="sxs-lookup"><span data-stu-id="4624f-116">toosolve this problem, we provide hello [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span></span>

## <a name="when-toorebalance-partition-replicas"></a><span data-ttu-id="4624f-117">Toorebalance 복제본을 분할 하는 경우</span><span class="sxs-lookup"><span data-stu-id="4624f-117">When toorebalance partition replicas</span></span>

<span data-ttu-id="4624f-118">tooensure Kafka 데이터의 가장 높은 가용성을 hello를 있습니다 해야 균형을 다시 조정할 hello 파티션 복제본 hello 다음 번에 항목:</span><span class="sxs-lookup"><span data-stu-id="4624f-118">tooensure hello highest availability of your Kafka data, you should rebalance hello partition replicas for your topic at hello following times:</span></span>

* <span data-ttu-id="4624f-119">새 토픽 또는 파티션을 만들 때</span><span class="sxs-lookup"><span data-stu-id="4624f-119">When a new topic or partition is created</span></span>

* <span data-ttu-id="4624f-120">클러스터를 확장할 때</span><span class="sxs-lookup"><span data-stu-id="4624f-120">When you scale up a cluster</span></span>

## <a name="replication-factor"></a><span data-ttu-id="4624f-121">복제 계수</span><span class="sxs-lookup"><span data-stu-id="4624f-121">Replication factor</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4624f-122">3개의 장애 도메인을 포함하는 Azure 지역을 사용하고 복제 계수로 3을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4624f-122">We recommend using an Azure region that contains three fault domains, and using a replication factor of 3.</span></span>

<span data-ttu-id="4624f-123">두 개의 오류 도메인을 포함 하는 영역의 사용 해야 할 경우 사용 하 여 4 toospread hello 복제본의 복제 요소 균등 하 게 hello 두 개의 오류 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="4624f-123">If you must use a region that contains only two fault domains, use a replication factor of 4 toospread hello replicas evenly across hello two fault domains.</span></span>

<span data-ttu-id="4624f-124">항목 및 설정 hello 복제 요소를 만드는 예를 들어 참조 hello [HDInsight의 Kafka로 시작](hdinsight-apache-kafka-get-started.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="4624f-124">For an example of creating topics and setting hello replication factor, see hello [Start with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span>

## <a name="how-toorebalance-partition-replicas"></a><span data-ttu-id="4624f-125">Toorebalance 복제본을 분할 하는 방법</span><span class="sxs-lookup"><span data-stu-id="4624f-125">How toorebalance partition replicas</span></span>

<span data-ttu-id="4624f-126">사용 하 여 hello [Kafka 파티션을 리 밸런스 도구](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance 항목을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4624f-126">Use hello [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance selected topics.</span></span> <span data-ttu-id="4624f-127">SSH 세션 toohello의 헤드 노드 Kafka 클러스터에서에서이 도구를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4624f-127">This tool must be ran from an SSH session toohello head node of your Kafka cluster.</span></span>

<span data-ttu-id="4624f-128">SSH를 사용 하 여 tooHDInsight 연결 방법에 대 한 자세한 내용은 참조는 [SSH HDInsight를 사용](hdinsight-hadoop-linux-use-ssh-unix.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="4624f-128">For more information on connecting tooHDInsight using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4624f-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4624f-129">Next steps</span></span>

* [<span data-ttu-id="4624f-130">HDInsight의 Kafka 확장성</span><span class="sxs-lookup"><span data-stu-id="4624f-130">Scalability of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* [<span data-ttu-id="4624f-131">HDInsight의 Kafka 미러링</span><span class="sxs-lookup"><span data-stu-id="4624f-131">Mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)