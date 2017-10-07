---
title: "HDInsight의 Apache Storm aaaTwitter 추세 주제 | Microsoft Docs"
description: "어떻게 toouse Trident toocreate Twitter에 대 한 추세 항목을 결정 하는 Apache Storm 토폴로지를 기반으로 해시에 알아봅니다."
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
ms.openlocfilehash: 0281b495d10833c63868b36856c96369b139c553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a><span data-ttu-id="8b62a-103">HDInsight에서 Apache Storm을 사용하여 Twitter 추세 항목 확인</span><span class="sxs-lookup"><span data-stu-id="8b62a-103">Determine Twitter trending topics with Apache Storm on HDInsight</span></span>

<span data-ttu-id="8b62a-104">Toouse Trident toocreate 스톰 토폴로지를 결정 하는 방법 추세에 대해 알아봅니다 Twitter에 대 한 항목 (해시 태그).</span><span class="sxs-lookup"><span data-stu-id="8b62a-104">Learn how toouse Trident toocreate a Storm topology that determines trending topics (hash tags) on Twitter.</span></span>

<span data-ttu-id="8b62a-105">Trident는 조인, 집계, 그룹화, 함수 및 필터와 같은 도구를 제공하는 높은 수준의 추상화입니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-105">Trident is a high-level abstraction that provides tools such as joins, aggregations, grouping, functions, and filters.</span></span> <span data-ttu-id="8b62a-106">또한 Trident는 상태 저장, 증분 처리를 수행하기 위한 기본 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-106">Additionally, Trident adds primitives for doing stateful, incremental processing.</span></span> <span data-ttu-id="8b62a-107">이 문서에 사용 되는 hello 예제는 사용자 지정 배출구 및 함수와 Trident 토폴로지입니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-107">hello example used in this document is a Trident topology with a custom spout and function.</span></span> <span data-ttu-id="8b62a-108">또한 Trident에서 제공한 몇 가지 기본 함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-108">It also uses several built-in functions provided by Trident.</span></span>

## <a name="requirements"></a><span data-ttu-id="8b62a-109">요구 사항</span><span class="sxs-lookup"><span data-stu-id="8b62a-109">Requirements</span></span>

* <span data-ttu-id="8b62a-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java 및 hello JDK 1.8</a></span><span class="sxs-lookup"><span data-stu-id="8b62a-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java and hello JDK 1.8</a></span></span>

* <span data-ttu-id="8b62a-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span><span class="sxs-lookup"><span data-stu-id="8b62a-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span></span>

* <span data-ttu-id="8b62a-112"><a href="http://git-scm.com/" target="_blank">Git</a></span><span class="sxs-lookup"><span data-stu-id="8b62a-112"><a href="http://git-scm.com/" target="_blank">Git</a></span></span>

* <span data-ttu-id="8b62a-113">Twitter 개발자 계정</span><span class="sxs-lookup"><span data-stu-id="8b62a-113">A Twitter developer account</span></span>

## <a name="download-hello-project"></a><span data-ttu-id="8b62a-114">Hello 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="8b62a-114">Download hello project</span></span>

<span data-ttu-id="8b62a-115">다음 코드 tooclone hello 프로젝트 로컬로 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-115">Use hello following code tooclone hello project locally.</span></span>

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-hello-topology"></a><span data-ttu-id="8b62a-116">Hello 토폴로지 이해</span><span class="sxs-lookup"><span data-stu-id="8b62a-116">Understanding hello topology</span></span>

<span data-ttu-id="8b62a-117">hello 다음 다이어그램의이 토폴로지를 통해 데이터 흐름 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-117">hello following diagram shows of how data flows through this topology:</span></span>

![토폴로지](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> <span data-ttu-id="8b62a-119">이 다이어그램은 토폴로지 hello의 단순화 된 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-119">This diagram is a simplified view of hello topology.</span></span> <span data-ttu-id="8b62a-120">Hello 구성 요소의 여러 인스턴스 hello 클러스터 내의 hello 노드 간에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-120">Multiple instances of hello components are distributed across hello nodes in hello cluster.</span></span>


<span data-ttu-id="8b62a-121">hello hello 토폴로지를 구현 하는 Trident 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-121">hello Trident code that implements hello topology is as follows:</span></span>

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

<span data-ttu-id="8b62a-122">이 코드는 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-122">This code performs hello following actions:</span></span>

1. <span data-ttu-id="8b62a-123">Hello 배출구에서 스트림을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-123">Creates a stream from hello spout.</span></span> <span data-ttu-id="8b62a-124">hello 배출구 Twitter에서 트 윗을 검색 하 고 특정 키워드 (love, 음악 및이 예제의 커피)에 대 한이 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-124">hello spout retrieves tweets from Twitter, and filters them for specific keywords (love, music, and coffee in this example).</span></span>

2. <span data-ttu-id="8b62a-125">HashtagExtractor, 사용자 지정 함수는 각 윗에서 사용 되는 tooextract 해시 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-125">HashtagExtractor, a custom function, is used tooextract hash tags from each tweet.</span></span> <span data-ttu-id="8b62a-126">hello 해시 태그는 내보낸된 toohello 스트림입니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-126">hello hash tags are emitted toohello stream.</span></span>

3. <span data-ttu-id="8b62a-127">hello 스트림 해시 태그에 의해 그룹화 되 고 tooan aggregator에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-127">hello stream is grouped by hash tag, and passed tooan aggregator.</span></span> <span data-ttu-id="8b62a-128">이 집계는 각 해시 태그가 발생한 횟수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-128">This aggregator creates a count of how many times each hash tag has occurred.</span></span> <span data-ttu-id="8b62a-129">이 데이터는 메모리에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-129">This data is persisted in memory.</span></span> <span data-ttu-id="8b62a-130">마지막으로, hello 해시 태그 및 hello 수를 포함 하는 새 스트림을 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-130">Finally, a new stream is emitted that contains hello hash tag and hello count.</span></span>

4. <span data-ttu-id="8b62a-131">hello **FirstN** 어셈블리는 적용 된 tooreturn hello 상위 10 개의 값만을 hello 수 필드를 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-131">hello **FirstN** assembly is applied tooreturn only hello top 10 values, based on hello count field.</span></span>

> [!NOTE]
> <span data-ttu-id="8b62a-132">Trident 사용한 작업에 대 한 자세한 내용은 참조 hello [Trident API 개요](http://storm.apache.org/releases/current/Trident-API-Overview.html) 문서.</span><span class="sxs-lookup"><span data-stu-id="8b62a-132">For more information on working with Trident, see hello [Trident API overview](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span></span>

### <a name="hello-spout"></a><span data-ttu-id="8b62a-133">hello 배출구</span><span class="sxs-lookup"><span data-stu-id="8b62a-133">hello spout</span></span>

<span data-ttu-id="8b62a-134">hello 배출구 **TwitterSpout**를 사용 하 여 [Twitter4j](http://twitter4j.org/en/) Twitter에서 tooretrieve 트 윗 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-134">hello spout, **TwitterSpout**, uses [Twitter4j](http://twitter4j.org/en/) tooretrieve tweets from Twitter.</span></span> <span data-ttu-id="8b62a-135">Hello 단어에 대 한 필터가 만들어집니다 __선호__, **음악**, 및 **커피**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-135">A filter is created for hello words __love__, **music**, and **coffee**.</span></span> <span data-ttu-id="8b62a-136">Hello 필터와 일치 하는 들어오는 윗 (상태) 연결 된 차단 큐에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-136">Incoming tweets (status) that match hello filter are stored in a linked blocking queue.</span></span> <span data-ttu-id="8b62a-137">마지막으로 항목을 hello 큐 해제 가져오고 toohello 토폴로지 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-137">Finally, items are pulled off hello queue and emitted toohello topology.</span></span>

### <a name="hello-hashtagextractor"></a><span data-ttu-id="8b62a-138">hello HashtagExtractor</span><span class="sxs-lookup"><span data-stu-id="8b62a-138">hello HashtagExtractor</span></span>

<span data-ttu-id="8b62a-139">tooextract 해시 태그 [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) hello 트 윗에 포함 된 모든 해시 태그 tooretrieve 사용된 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-139">tooextract hash tags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) is used tooretrieve all hash tags that are contained in hello tweet.</span></span> <span data-ttu-id="8b62a-140">이 다음 내보낸된 toohello 스트림 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-140">These are then emitted toohello stream.</span></span>

## <a name="configure-twitter"></a><span data-ttu-id="8b62a-141">Twitter 구성</span><span class="sxs-lookup"><span data-stu-id="8b62a-141">Configure Twitter</span></span>

<span data-ttu-id="8b62a-142">Twitter에서 hello 소비자 및 액세스 토큰 정보 필요한 tooread 가져올 및 hello 단계 tooregister 새 Twitter 응용 프로그램을 다음 사용:</span><span class="sxs-lookup"><span data-stu-id="8b62a-142">Use hello following steps tooregister a new Twitter application and obtain hello consumer and access token information needed tooread from Twitter:</span></span>

1. <span data-ttu-id="8b62a-143">너무 이동[Twitter 앱](https://apps.twitter.com) hello 클릭 **새 앱 만들기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-143">Go too[Twitter Apps](https://apps.twitter.com) and click hello **Create new app** button.</span></span> <span data-ttu-id="8b62a-144">Hello 형태로 데이터를 입력할 때 상태로 hello **콜백 URL** 필드를 빈 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-144">When filling in hello form, leave hello **Callback URL** field empty.</span></span>

2. <span data-ttu-id="8b62a-145">Hello 앱을 만든 경우 클릭 hello **키와 액세스 토큰이** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-145">When hello app is created, click hello **Keys and Access Tokens** tab.</span></span>

3. <span data-ttu-id="8b62a-146">복사 hello **소비자 키** 및 **소비자 암호** 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-146">Copy hello **Consumer Key** and **Consumer Secret** information.</span></span>

4. <span data-ttu-id="8b62a-147">Hello 페이지의 hello 맨 아래에 선택 **내 액세스 토큰 만들기** 토큰이 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-147">At hello bottom of hello page, select **Create my access token** if no tokens exist.</span></span> <span data-ttu-id="8b62a-148">Hello 토큰 생성 된 경우, 복사 hello **액세스 토큰** 및 **액세스 토큰 암호** 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-148">When hello tokens have been created, copy hello **Access Token** and **Access Token Secret** information.</span></span>

5. <span data-ttu-id="8b62a-149">Hello에 **TwitterSpoutTopology** 프로젝트 열기, 이전에 복제 된 hello **resources/twitter4j.properties** 파일 hello 이전 단계에서 수집한 hello 정보를 추가 하 고 다음 hello 파일 저장 .</span><span class="sxs-lookup"><span data-stu-id="8b62a-149">In hello **TwitterSpoutTopology** project you previously cloned, open hello **resources/twitter4j.properties** file, add hello information you gathered in hello previous steps, and then save hello file.</span></span>

## <a name="build-hello-topology"></a><span data-ttu-id="8b62a-150">Hello 토폴로지 빌드</span><span class="sxs-lookup"><span data-stu-id="8b62a-150">Build hello topology</span></span>

<span data-ttu-id="8b62a-151">다음 코드 toobuild hello 프로젝트 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-151">Use hello following code toobuild hello project:</span></span>

        cd [directoryname]
        mvn compile

## <a name="test-hello-topology"></a><span data-ttu-id="8b62a-152">테스트 hello 토폴로지</span><span class="sxs-lookup"><span data-stu-id="8b62a-152">Test hello topology</span></span>

<span data-ttu-id="8b62a-153">다음 명령을 로컬로 토폴로지 tootest hello hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-153">Use hello following command tootest hello topology locally:</span></span>

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

<span data-ttu-id="8b62a-154">Hello 토폴로지 시작 된 후 태그와 hello 토폴로지 별로 내보낸 수를 hello 해시를 포함 하는 디버그 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-154">After hello topology starts, you should see debug information that contains hello hash tags and counts emitted by hello topology.</span></span> <span data-ttu-id="8b62a-155">hello 출력 텍스트 다음 비슷한 toohello 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-155">hello output should appear similar toohello following text:</span></span>

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a><span data-ttu-id="8b62a-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8b62a-156">Next steps</span></span>

<span data-ttu-id="8b62a-157">Hello 토폴로지 로컬로 테스트할 했으므로 검색 방법을 toodeploy hello 토폴로지: [배포 HDInsight의 Apache Storm 토폴로지를 관리할 및](hdinsight-storm-deploy-monitor-topology.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-157">Now that you have tested hello topology locally, discover how toodeploy hello topology: [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span></span>

<span data-ttu-id="8b62a-158">다음 스톰 항목 hello 관심이 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b62a-158">You may also be interested in hello following Storm topics:</span></span>

* [<span data-ttu-id="8b62a-159">Maven을 사용하여 HDInsight의 Storm용 Java 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="8b62a-159">Develop Java topologies for Storm on HDInsight using Maven</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="8b62a-160">Visual Studio를 사용하여 HDInsight의 Storm용 C# 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="8b62a-160">Develop C# topologies for Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="8b62a-161">HDinsight에 대한 추가 Storm 예제:</span><span class="sxs-lookup"><span data-stu-id="8b62a-161">For more Storm examples for HDInsight:</span></span>

* [<span data-ttu-id="8b62a-162">HDInsight의 Storm에 대한 예제 토폴로지</span><span class="sxs-lookup"><span data-stu-id="8b62a-162">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

