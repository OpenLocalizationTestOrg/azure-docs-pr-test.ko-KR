---
title: "HDInsight의 Apache Kafka 소개 - Azure | Microsoft Docs"
description: "HDInsight의 Apache Kafka에 대해 알아보세요. 이것이 무엇인지, 무엇을 하는지, 어디서 예제와 시작 정보를 찾는지에 대해 설명합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: f284b6e3-5f3b-4a50-b455-917e77588069
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: larryfr
ms.openlocfilehash: 1976c52bd7fa56bb07104e205ab3699b2dfa4c50
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a><span data-ttu-id="59004-103">HDInsight의 Apache Kafka 소개(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="59004-103">Introducing Apache Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="59004-104">[Apache Kafka](https://kafka.apache.org)는 실시간 스트리밍 데이터 파이프라인과 응용 프로그램을 만드는 데 사용할 수 있는 오픈 소스 분산형 스트리밍 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="59004-104">[Apache Kafka](https://kafka.apache.org) is an open-source distributed streaming platform that can be used to build real-time streaming data pipelines and applications.</span></span> <span data-ttu-id="59004-105">또한 Kafka는 명명된 데이터 스트림을 게시하고 구독할 수 있는 메시지 대기열과 비슷한 메시지 브로커 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="59004-105">Kafka also provides message broker functionality similar to a message queue, where you can publish and subscribe to named data streams.</span></span> <span data-ttu-id="59004-106">HDInsight의 Kafka는 Microsoft Azure 클라우드에서 관리되고 확장성이 뛰어난 고가용성 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="59004-106">Kafka on HDInsight provides you with a managed, highly scalable, and highly available service in the Microsoft Azure cloud.</span></span>

## <a name="why-use-kafka-on-hdinsight"></a><span data-ttu-id="59004-107">HDInsight에서 Kafka를 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="59004-107">Why use Kafka on HDInsight?</span></span>

<span data-ttu-id="59004-108">Kafka에서 제공하는 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="59004-108">Kafka provides the following features:</span></span>

* <span data-ttu-id="59004-109">게시-구독 메시징 패턴: Kafka는 Kafka 토픽에 레코드를 게시하기 위한 생산자 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="59004-109">Publish-subscribe messaging pattern: Kafka provides a Producer API for publishing records to a Kafka topic.</span></span> <span data-ttu-id="59004-110">소비자 API는 토픽을 구독할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="59004-110">The Consumer API is used when subscribing to a topic.</span></span>

* <span data-ttu-id="59004-111">스트림 처리: Kafka는 종종 실시간 스트리밍 처리를 위해 Apache Storm 또는 Apache Spark와 함께 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="59004-111">Stream processing: Kafka is often used with Apache Storm or Spark for real-time stream processing.</span></span> <span data-ttu-id="59004-112">Kafka 0.10.0.0(HDInsight 버전 3.5)은 Storm이나 Spark를 요구하지 않고 스트리밍 솔루션을 빌드할 수 있는 스트리밍 API를 도입했습니다.</span><span class="sxs-lookup"><span data-stu-id="59004-112">Kafka 0.10.0.0 (HDInsight version 3.5) introduced a streaming API that allows you to build streaming solutions without requiring Storm or Spark.</span></span>

* <span data-ttu-id="59004-113">수평 확장: Kafka는 HDInsight 클러스터의 노드에서 스트림을 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="59004-113">Horizontal scale: Kafka partitions streams across the nodes in the HDInsight cluster.</span></span> <span data-ttu-id="59004-114">소비자 프로세스는 개별 파티션에 연결하여 레코드를 소비할 때 부하 분산을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59004-114">Consumer processes can be associated with individual partitions to provide load balancing when consuming records.</span></span>

* <span data-ttu-id="59004-115">순차적 전달: 레코드는 각 파티션 내에서 수신된 순서대로 스트림에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="59004-115">In-order delivery: Within each partition, records are stored in the stream in the order that they were received.</span></span> <span data-ttu-id="59004-116">파티션마다 소비자 프로세스를 하나씩 연결하여 레코드가 순서대로 처리되도록 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59004-116">By associating one consumer process per partition, you can guarantee that records are processed in-order.</span></span>

* <span data-ttu-id="59004-117">내결함성: 노드 간에 결함을 허용하기 위해 파티션을 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59004-117">Fault-tolerant: Partitions can be replicated between nodes to provide fault tolerance.</span></span>

* <span data-ttu-id="59004-118">Azure Managed Disks와 통합: 관리 디스크는 HDInsight 클러스터에서 가상 컴퓨터에 사용된 디스크에 대해 더 높은 규모와 처리량을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="59004-118">Integration with Azure Managed Disks: Managed disks provides higher scale and throughput for the disks used by the virtual machines in the HDInsight cluster.</span></span>

    <span data-ttu-id="59004-119">기본적으로 관리 디스크는 HDInsight에서 Kafka에 대해 사용하도록 설정되며 HDInsight 생성 중에 노드당 사용된 디스크 수를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59004-119">Managed disks are enabled by default for Kafka on HDInsight, and the number of disks used per node can be configured during HDInsight creation.</span></span> <span data-ttu-id="59004-120">관리 디스크에 대한 자세한 내용은 [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59004-120">For more information on managed disks, see [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).</span></span>

    <span data-ttu-id="59004-121">HDInsight에서 Kafka로 관리 디스크 구성에 대한 자세한 내용은 [HDInsight에서 Kafka의 확장성 높이기](hdinsight-apache-kafka-scalability.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59004-121">For information on configuring managed disks with Kafka on HDInsight, see [Increase scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

## <a name="use-cases"></a><span data-ttu-id="59004-122">사용 사례</span><span class="sxs-lookup"><span data-stu-id="59004-122">Use cases</span></span>

* <span data-ttu-id="59004-123">**메시징**: Kafka는 게시-구독 메시지 패턴을 지원하므로 종종 메시지 브로커로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="59004-123">**Messaging**: Since it supports the publish-subscribe message pattern, Kafka is often used as a message broker.</span></span>

* <span data-ttu-id="59004-124">**활동 추적**: Kafka는 순서대로 레코드 로그를 기록하므로 활동을 추적하고 다시 만드는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59004-124">**Activity tracking**: Since Kafka provides in-order logging of records, it can be used to track and re-create activities.</span></span> <span data-ttu-id="59004-125">예를 들어 웹 사이트 또는 응용 프로그램에서의 사용자 작업이 여기에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="59004-125">For example, user actions on a web site or within an application.</span></span>

* <span data-ttu-id="59004-126">**집계**: 스트림 처리를 사용하여 결합할 서로 다른 스트림의 정보를 한데 모으고 중앙에서 이 정보를 운영 데이터로 집중적으로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59004-126">**Aggregation**: Using stream processing, you can aggregate information from different streams to combine and centralize the information into operational data.</span></span>

* <span data-ttu-id="59004-127">**변환**: 스트림 처리를 사용하여 여러 입력 토픽의 데이터를 하나 이상의 출력 토픽으로 결합하고 보강할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59004-127">**Transformation**: Using stream processing, you can combine and enrich data from multiple input topics into one or more output topics.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59004-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="59004-128">Next steps</span></span>

<span data-ttu-id="59004-129">다음 링크를 사용하여 HDInsight에서 Apache Kafka를 사용하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="59004-129">Use the following links to learn how to use Apache Kafka on HDInsight:</span></span>

* [<span data-ttu-id="59004-130">HDInsight에서 Apache Kafka 시작</span><span class="sxs-lookup"><span data-stu-id="59004-130">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)

* [<span data-ttu-id="59004-131">MirrorMaker를 사용하여 HDInsight에 Kafka 복제본 만들기</span><span class="sxs-lookup"><span data-stu-id="59004-131">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)

* [<span data-ttu-id="59004-132">HDInsight의 Kafka에서 Apache Storm 사용</span><span class="sxs-lookup"><span data-stu-id="59004-132">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

* [<span data-ttu-id="59004-133">HDInsight의 Kafka에서 Apache Spark 사용</span><span class="sxs-lookup"><span data-stu-id="59004-133">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)

* [<span data-ttu-id="59004-134">Azure Virtual Network를 통해 Kafka에 연결</span><span class="sxs-lookup"><span data-stu-id="59004-134">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)