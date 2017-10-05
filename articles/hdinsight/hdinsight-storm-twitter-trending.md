---
title: "HDInsight에서 Apache Storm을 사용하는 Twitter 추세 항목| Microsoft Docs"
description: "Trident를 사용하여 해시 태그에 기반하는 Twitter에서 추세 항목을 확인하는 Apache Storm 토폴로지를 만드는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 63b280ea-5c07-4dc8-a35f-dccf5a96ba93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/14/2017
ms.author: larryfr
ms.openlocfilehash: d588221586f151319436525c5098b0bb2694e5f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a><span data-ttu-id="3d065-103">HDInsight에서 Apache Storm을 사용하여 Twitter 추세 항목 확인</span><span class="sxs-lookup"><span data-stu-id="3d065-103">Determine Twitter trending topics with Apache Storm on HDInsight</span></span>

<span data-ttu-id="3d065-104">Trident를 사용하여 Twitter에서 추세 항목(해시 태그)을 확인하는 Storm 토폴로지를 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-104">Learn how to use Trident to create a Storm topology that determines trending topics (hash tags) on Twitter.</span></span>

<span data-ttu-id="3d065-105">Trident는 조인, 집계, 그룹화, 함수 및 필터와 같은 도구를 제공하는 높은 수준의 추상화입니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-105">Trident is a high-level abstraction that provides tools such as joins, aggregations, grouping, functions, and filters.</span></span> <span data-ttu-id="3d065-106">또한 Trident는 상태 저장, 증분 처리를 수행하기 위한 기본 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-106">Additionally, Trident adds primitives for doing stateful, incremental processing.</span></span> <span data-ttu-id="3d065-107">이 문서에 사용된 예제는 사용자 지정 Spout와 함수가 포함된 Trident 토폴로지입니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-107">The example used in this document is a Trident topology with a custom spout and function.</span></span> <span data-ttu-id="3d065-108">또한 Trident에서 제공한 몇 가지 기본 함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-108">It also uses several built-in functions provided by Trident.</span></span>

## <a name="requirements"></a><span data-ttu-id="3d065-109">요구 사항</span><span class="sxs-lookup"><span data-stu-id="3d065-109">Requirements</span></span>

* <span data-ttu-id="3d065-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java 및 JDK 1.8</a></span><span class="sxs-lookup"><span data-stu-id="3d065-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java and the JDK 1.8</a></span></span>

* <span data-ttu-id="3d065-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span><span class="sxs-lookup"><span data-stu-id="3d065-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span></span>

* <span data-ttu-id="3d065-112"><a href="http://git-scm.com/" target="_blank">Git</a></span><span class="sxs-lookup"><span data-stu-id="3d065-112"><a href="http://git-scm.com/" target="_blank">Git</a></span></span>

* <span data-ttu-id="3d065-113">Twitter 개발자 계정</span><span class="sxs-lookup"><span data-stu-id="3d065-113">A Twitter developer account</span></span>

## <a name="download-the-project"></a><span data-ttu-id="3d065-114">프로젝트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-114">Download the project</span></span>

<span data-ttu-id="3d065-115">다음 코드를 사용하여 프로젝트를 로컬로 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-115">Use the following code to clone the project locally.</span></span>

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-the-topology"></a><span data-ttu-id="3d065-116">토폴로지 이해</span><span class="sxs-lookup"><span data-stu-id="3d065-116">Understanding the topology</span></span>

<span data-ttu-id="3d065-117">다음 다이어그램은 데이터가 이 토폴로지를 통해 이동하는 방식을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-117">The following diagram shows of how data flows through this topology:</span></span>

![토폴로지](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> <span data-ttu-id="3d065-119">이 다이어그램은 토폴로지를 단순화한 그림입니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-119">This diagram is a simplified view of the topology.</span></span> <span data-ttu-id="3d065-120">구성 요소의 여러 인스턴스가 클러스터 내 노드 사이에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-120">Multiple instances of the components are distributed across the nodes in the cluster.</span></span>


<span data-ttu-id="3d065-121">토폴로지를 구현하는 Trident 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-121">The Trident code that implements the topology is as follows:</span></span>

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

<span data-ttu-id="3d065-122">이 코드는 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-122">This code performs the following actions:</span></span>

1. <span data-ttu-id="3d065-123">Spout에서 스트림을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-123">Creates a stream from the spout.</span></span> <span data-ttu-id="3d065-124">Spout는 Twitter에서 트윗을 검색하여 특정 키워드(이 예제의 경우 love, music 및 coffee)로 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-124">The spout retrieves tweets from Twitter, and filters them for specific keywords (love, music, and coffee in this example).</span></span>

2. <span data-ttu-id="3d065-125">사용자 지정 함수인 HashtagExtractor는 각 트윗에서 해시 태그를 추출하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-125">HashtagExtractor, a custom function, is used to extract hash tags from each tweet.</span></span> <span data-ttu-id="3d065-126">해시 태그는 스트림으로 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-126">The hash tags are emitted to the stream.</span></span>

3. <span data-ttu-id="3d065-127">스트림은 해시 태그로 그룹화되어 집계로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-127">The stream is grouped by hash tag, and passed to an aggregator.</span></span> <span data-ttu-id="3d065-128">이 집계는 각 해시 태그가 발생한 횟수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-128">This aggregator creates a count of how many times each hash tag has occurred.</span></span> <span data-ttu-id="3d065-129">이 데이터는 메모리에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-129">This data is persisted in memory.</span></span> <span data-ttu-id="3d065-130">마지막으로 해시 태그 및 개수가 포함된 새 스트림을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-130">Finally, a new stream is emitted that contains the hash tag and the count.</span></span>

4. <span data-ttu-id="3d065-131">**FirstN** 어셈블리는 count 필드를 기준으로 상위 10개 값만 반환하도록 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-131">The **FirstN** assembly is applied to return only the top 10 values, based on the count field.</span></span>

> [!NOTE]
> <span data-ttu-id="3d065-132">Trident 사용에 대한 자세한 내용은 [Trident API 개요](http://storm.apache.org/releases/current/Trident-API-Overview.html) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d065-132">For more information on working with Trident, see the [Trident API overview](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span></span>

### <a name="the-spout"></a><span data-ttu-id="3d065-133">spout</span><span class="sxs-lookup"><span data-stu-id="3d065-133">The spout</span></span>

<span data-ttu-id="3d065-134">**TwitterSpout** Spout는 [Twitter4j](http://twitter4j.org/en/)를 사용하여 Twitter에서 트윗을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-134">The spout, **TwitterSpout**, uses [Twitter4j](http://twitter4j.org/en/) to retrieve tweets from Twitter.</span></span> <span data-ttu-id="3d065-135">__love__, **music**, **coffee** 단어에 대한 필터가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-135">A filter is created for the words __love__, **music**, and **coffee**.</span></span> <span data-ttu-id="3d065-136">수신된 트윗(상태) 중 필터와 일치하는 필터는 연결된 차단 큐에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-136">Incoming tweets (status) that match the filter are stored in a linked blocking queue.</span></span> <span data-ttu-id="3d065-137">마지막으로 항목을 큐에서 가져와 토폴로지로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-137">Finally, items are pulled off the queue and emitted to the topology.</span></span>

### <a name="the-hashtagextractor"></a><span data-ttu-id="3d065-138">HashtagExtractor</span><span class="sxs-lookup"><span data-stu-id="3d065-138">The HashtagExtractor</span></span>

<span data-ttu-id="3d065-139">해시태그를 추출하기 위해 [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--)를 사용하여 트윗에 포함된 모든 해시 태그를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-139">To extract hash tags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) is used to retrieve all hash tags that are contained in the tweet.</span></span> <span data-ttu-id="3d065-140">그런 다음 스트림으로 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-140">These are then emitted to the stream.</span></span>

## <a name="configure-twitter"></a><span data-ttu-id="3d065-141">Twitter 구성</span><span class="sxs-lookup"><span data-stu-id="3d065-141">Configure Twitter</span></span>

<span data-ttu-id="3d065-142">새 Twitter 응용 프로그램을 등록하고를 Twitter에서 읽는 데 필요한 소비자 및 액세스 토큰 정보를 받으려면 다음 단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d065-142">Use the following steps to register a new Twitter application and obtain the consumer and access token information needed to read from Twitter:</span></span>

1. <span data-ttu-id="3d065-143">[Twitter Apps](https://apps.twitter.com)로 이동하여 **Create new app** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-143">Go to [Twitter Apps](https://apps.twitter.com) and click the **Create new app** button.</span></span> <span data-ttu-id="3d065-144">양식을 작성할 때 **Callback URL** 필드는 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-144">When filling in the form, leave the **Callback URL** field empty.</span></span>

2. <span data-ttu-id="3d065-145">앱이 만들어지면 **Keys and Access Tokens** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-145">When the app is created, click the **Keys and Access Tokens** tab.</span></span>

3. <span data-ttu-id="3d065-146">**Consumer Key** 및 **Consumer Secret** 정보를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-146">Copy the **Consumer Key** and **Consumer Secret** information.</span></span>

4. <span data-ttu-id="3d065-147">토큰이 없는 경우 페이지 아래쪽에서 **Create my access token** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-147">At the bottom of the page, select **Create my access token** if no tokens exist.</span></span> <span data-ttu-id="3d065-148">토큰을 만들었으면 **Access Token** 및 **Access Token Secret** 정보를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-148">When the tokens have been created, copy the **Access Token** and **Access Token Secret** information.</span></span>

5. <span data-ttu-id="3d065-149">앞에서 복사한 **TwitterSpoutTopology** 프로젝트에서 **resources/twitter4j.properties** 파일을 열고 이전 단계에서 수집한 정보를 추가한 다음 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-149">In the **TwitterSpoutTopology** project you previously cloned, open the **resources/twitter4j.properties** file, add the information you gathered in the previous steps, and then save the file.</span></span>

## <a name="build-the-topology"></a><span data-ttu-id="3d065-150">토폴로지 작성</span><span class="sxs-lookup"><span data-stu-id="3d065-150">Build the topology</span></span>

<span data-ttu-id="3d065-151">다음 코드를 사용하여 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-151">Use the following code to build the project:</span></span>

        cd [directoryname]
        mvn compile

## <a name="test-the-topology"></a><span data-ttu-id="3d065-152">포톨로지 테스트</span><span class="sxs-lookup"><span data-stu-id="3d065-152">Test the topology</span></span>

<span data-ttu-id="3d065-153">다음 명령을 사용하여 토폴로지를 로컬로 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-153">Use the following command to test the topology locally:</span></span>

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

<span data-ttu-id="3d065-154">토폴로지가 시작된 후 해당 토폴로지에서 내보낸 해시 태그 및 개수가 포함된 디버그 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-154">After the topology starts, you should see debug information that contains the hash tags and counts emitted by the topology.</span></span> <span data-ttu-id="3d065-155">출력은 다음 텍스트와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-155">The output should appear similar to the following text:</span></span>

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a><span data-ttu-id="3d065-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3d065-156">Next steps</span></span>

<span data-ttu-id="3d065-157">토폴로지를 로컬로 테스트했으므로 이제 [HDInsight의 Apache Strom 토폴로지 배포 및 관리](hdinsight-storm-deploy-monitor-topology.md)에서 토폴로지를 배포하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-157">Now that you have tested the topology locally, discover how to deploy the topology: [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span></span>

<span data-ttu-id="3d065-158">다음과 같은 Storm 항목을 참조할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d065-158">You may also be interested in the following Storm topics:</span></span>

* [<span data-ttu-id="3d065-159">Maven을 사용하여 HDInsight의 Storm용 Java 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="3d065-159">Develop Java topologies for Storm on HDInsight using Maven</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="3d065-160">Visual Studio를 사용하여 HDInsight의 Storm용 C# 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="3d065-160">Develop C# topologies for Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="3d065-161">HDinsight에 대한 추가 Storm 예제:</span><span class="sxs-lookup"><span data-stu-id="3d065-161">For more Storm examples for HDInsight:</span></span>

* [<span data-ttu-id="3d065-162">HDInsight의 Storm에 대한 예제 토폴로지</span><span class="sxs-lookup"><span data-stu-id="3d065-162">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

