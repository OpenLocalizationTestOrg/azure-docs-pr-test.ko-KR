---
title: "Azure Cosmos DB 디자인 패턴: 소셜 미디어 앱 | Microsoft Docs"
description: "Azure Cosmos DB 및 다른 Azure 서비스의 hello 저장소 유연성을 활용 하 여 소셜 네트워크에 대 한 디자인 패턴에 대 한 알아봅니다."
keywords: "소셜 미디어 앱"
services: cosmos-db
author: ealsur
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 2dbf83a7-512a-4993-bf1b-ea7d72e095d9
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2017
ms.author: mimig
ms.openlocfilehash: 47a22f2c5762d62b176921c8052e7bd75d8cf6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="going-social-with-azure-cosmos-db"></a><span data-ttu-id="ce162-104">Azure Cosmos DB를 사용하여 소셜 네트워크 디자인</span><span class="sxs-lookup"><span data-stu-id="ce162-104">Going social with Azure Cosmos DB</span></span>
<span data-ttu-id="ce162-105">광범위하게 상호 연결된 사회에서 살고 있다는 것은 삶의 어느 시점에서 **소셜 네트워크**의 일부가 된다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-105">Living in a massively-interconnected society means that, at some point in life, you become part of a **social network**.</span></span> <span data-ttu-id="ce162-106">사용 친구, 동료, 패밀리 또는 경우에 따라 tooshare 연락을 소셜 네트워크 tookeep 우리의 열 정의 공통 관심사를 가진 사용자와 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-106">We use social networks tookeep in touch with friends, colleagues, family, or sometimes tooshare our passion with people with common interests.</span></span>

<span data-ttu-id="ce162-107">엔지니어 또는 개발자로 어떻게 이러한 네트워크를 저장 하 고 데이터를 상호 연결 궁금 있을 수 있습니다 또는 수 있을 되었습니다 보강이 toocreate 또는 특정 드러나는 일에 대 한 새 소셜 네트워크 설계자 시장 자기 자신입니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-107">As engineers or developers, we might have wondered how do these networks store and interconnect our data, or might have even been tasked toocreate or architect a new social network for a specific niche market yourselves.</span></span> <span data-ttu-id="ce162-108">이 경우에 발생 하는 hello 중요 한 질문:이 모든 데이터 저장 방법?</span><span class="sxs-lookup"><span data-stu-id="ce162-108">That’s when hello big question arises: How is all this data stored?</span></span>

<span data-ttu-id="ce162-109">사용자가 사진, 동영상 또는 음악과 같은 관련 미디어와 함께 문서를 게시할 수 있는 새롭고 참신한 소셜 네트워크를 만든다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-109">Let’s suppose that we are creating a new and shiny social network, where our users can post articles with related media like, pictures, videos, or even music.</span></span> <span data-ttu-id="ce162-110">사용자는 게시물에 의견을 달고 평점을 매길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-110">Users can comment on posts and give points for ratings.</span></span> <span data-ttu-id="ce162-111">사용자와 수 toointeract hello 기본 웹 사이트 방문 페이지 수를 참조 하는 게시물의 피드가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-111">There will be a feed of posts that users will see and be able toointeract with on hello main website landing page.</span></span> <span data-ttu-id="ce162-112">이 실제로 복잡 한 사운드 하지 않습니다 (처음)에서는 편의 hello 위해서 보겠습니다 여기서 중지 하지만 (관계에 의해 영향을 받는 사용자 지정 피드 살펴 보겠습니다 수 있지만이 문서의 hello 목표 초과).</span><span class="sxs-lookup"><span data-stu-id="ce162-112">This doesn’t sound really complex (at first), but for hello sake of simplicity, let’s stop there (we could delve into custom user feeds affected by relationships, but it exceeds hello goal of this article).</span></span>

<span data-ttu-id="ce162-113">그렇다면 데이터는 어디에 어떻게 저장될까요?</span><span class="sxs-lookup"><span data-stu-id="ce162-113">So, how do we store this and where?</span></span>

<span data-ttu-id="ce162-114">SQL 데이터베이스에 대 본 경험이 수도의 개념이 최소한 여러분 중 많은 [관계형 데이터의 모델링](https://en.wikipedia.org/wiki/Relational_model) 시도할된 toostart 그리기 다음과 같이 필요할 수:</span><span class="sxs-lookup"><span data-stu-id="ce162-114">Many of you might have experience on SQL databases or at least have notion of [relational modeling of data](https://en.wikipedia.org/wiki/Relational_model) and you might be tempted toostart drawing something like this:</span></span>

![상대 관계형 모델을 보여 주는 다이어그램](./media/social-media-apps/social-media-apps-sql.png) 

<span data-ttu-id="ce162-116">완전히 정규화되고 세련된 데이터 구조는...</span><span class="sxs-lookup"><span data-stu-id="ce162-116">A perfectly normalized and pretty data structure…</span></span> <span data-ttu-id="ce162-117">확장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-117">that doesn't scale.</span></span> 

<span data-ttu-id="ce162-118">저에 대해 오해하지 마세요. 저는 SQL 데이터베이스를 평생 사용해 왔으며, SQL 데이터베이스는 정말 대단하지만 모든 패턴, 방식 및 소프트웨어 플랫폼과 마찬가지로 모든 시나리오에 완벽한 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-118">Don’t get me wrong, I’ve worked with SQL databases all my life, they are great, but like every pattern, practice and software platform, it’s not perfect for every scenario.</span></span>

<span data-ttu-id="ce162-119">이 시나리오에서는 SQL hello 최선의 선택 되지 않는 이유는?</span><span class="sxs-lookup"><span data-stu-id="ce162-119">Why isn't SQL hello best choice in this scenario?</span></span> <span data-ttu-id="ce162-120">단일 post의 hello 구조에 살펴보겠습니다, 그리고 웹 사이트 또는 응용 프로그램에서 게시 하는 tooshow을 원할 경우 되어 toodo 사용 하 여 쿼리 중...</span><span class="sxs-lookup"><span data-stu-id="ce162-120">Let’s look at hello structure of a single post, if I wanted tooshow that post in a website or application, I’d have toodo a query with…</span></span> <span data-ttu-id="ce162-121">8 테이블 조인 (!) 정당한 tooshow 하나의 단일 post, 이제 그림 댓를 동적으로 로드 하 고 hello 화면에 표시 하는 게시물의 스트림을 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-121">8 table joins (!) just tooshow one single post, now, picture a stream of posts that dynamically load and appear on hello screen and you might see where I am going.</span></span>

<span data-ttu-id="ce162-122">म 수 물론, humongous SQL 인스턴스와 함께 사용할 충분 한 전력 toosolve 수천 쿼리의 이러한 많은 조인 tooserve와 콘텐츠를 하지만 진정한 이유는 경우 간단한 솔루션에서는 존재?</span><span class="sxs-lookup"><span data-stu-id="ce162-122">We could, of course, use a humongous SQL instance with enough power toosolve thousands of queries with these many joins tooserve our content, but truly, why would we when a simpler solution exists?</span></span>

## <a name="hello-nosql-road"></a><span data-ttu-id="ce162-123">hello NoSQL road</span><span class="sxs-lookup"><span data-stu-id="ce162-123">hello NoSQL road</span></span>
<span data-ttu-id="ce162-124">이 문서에서는 하면 Azure의 NoSQL 데이터베이스를 사용 하 여 소셜 플랫폼의 데이터 모델링에 안내 [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) hello와 같은 다른 Azure Cosmos DB 기능을 활용 하면서 비용 효율적인 방식으로 [Gremlin Graph API ](../cosmos-db/graph-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ce162-124">This article will guide you into modeling your social platform's data with Azure's NoSQL database [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) in a cost-effective way while leveraging other Azure Cosmos DB features like hello  [Gremlin Graph API](../cosmos-db/graph-introduction.md).</span></span> <span data-ttu-id="ce162-125">[NoSQL](https://en.wikipedia.org/wiki/NoSQL) 접근 방식을 사용하여 데이터를 JSON 형식으로 저장하고 [역정규화](https://en.wikipedia.org/wiki/Denormalization)를 적용하면 이전의 복잡한 게시물을 단일 [문서](https://en.wikipedia.org/wiki/Document-oriented_database)로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-125">Using a [NoSQL](https://en.wikipedia.org/wiki/NoSQL) approach, storing data in JSON format and applying [denormalization](https://en.wikipedia.org/wiki/Denormalization), our previously complicated post can be transformed into a single [Document](https://en.wikipedia.org/wiki/Document-oriented_database):</span></span>


    {
        "id":"ew12-res2-234e-544f",
        "title":"post title",
        "date":"2016-01-01",
        "body":"this is an awesome post stored on NoSQL",
        "createdBy":User,
        "images":["http://myfirstimage.png","http://mysecondimage.png"],
        "videos":[
            {"url":"http://myfirstvideo.mp4", "title":"hello first video"},
            {"url":"http://mysecondvideo.mp4", "title":"hello second video"}
        ],
        "audios":[
            {"url":"http://myfirstaudio.mp3", "title":"hello first audio"},
            {"url":"http://mysecondaudio.mp3", "title":"hello second audio"}
        ]
    }

<span data-ttu-id="ce162-126">또한 조인 없이 단일 쿼리로 이를 실현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-126">And it can be obtained with a single query, and with no joins.</span></span> <span data-ttu-id="ce162-127">이 훨씬 더 쉽고 간단 하 고 budget-wise, 더 적은 리소스 tooachieve 더 좋은 결과 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-127">This is much more simple and straightforward, and, budget-wise, it requires fewer resources tooachieve a better result.</span></span>

<span data-ttu-id="ce162-128">Azure Cosmos DB 있게 된 모든 hello 속성 인덱싱 되는지와 해당 자동 인덱싱이 될 수 있습니다 [사용자 지정 된](indexing-policies.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-128">Azure Cosmos DB makes sure that all hello properties are indexed with its automatic indexing, which can even be [customized](indexing-policies.md).</span></span> <span data-ttu-id="ce162-129">hello 접근 방식을 통해 서로 다른 문서를 저장 하 고 동적 구조, 어쩌면 내일 게시물 toohave 처리 하는 범주 또는 Cosmos DB 그와 관련 된 해시의 목록을 원하는 hello로 새 문서를 hello 스키마 없는 추가 사용 하 여 특성 추가 자체는 데 필요한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-129">hello schema-free approach lets us store Documents with different and dynamic structures, maybe tomorrow we want posts toohave a list of categories or hashtags associated with them, Cosmos DB will handle hello new Documents with hello added attributes with no extra work required by us.</span></span>

<span data-ttu-id="ce162-130">부모 속성을 사용하여 게시물에 대한 의견을 다른 게시물로 처리할 수 있습니다. 이는 개체 매핑을 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-130">Comments on a post can be treated as just other posts with a parent property (this simplifies our object mapping).</span></span> 

    {
        "id":"1234-asd3-54ts-199a",
        "title":"Awesome post!",
        "date":"2016-01-02",
        "createdBy":User2,
        "parent":"ew12-res2-234e-544f"
    }

    {
        "id":"asd2-fee4-23gc-jh67",
        "title":"Ditto!",
        "date":"2016-01-03",
        "createdBy":User3,
        "parent":"ew12-res2-234e-544f"
    }

<span data-ttu-id="ce162-131">또한 모든 소셜 상호 작용을 별도의 개체에 카운터로 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-131">And all social interactions can be stored on a separate object as counters:</span></span>

    {
        "id":"dfe3-thf5-232s-dse4",
        "post":"ew12-res2-234e-544f",
        "comments":2,
        "likes":10,
        "points":200
    }

<span data-ttu-id="ce162-132">피드를 만들려면 주어진 연관성 순으로 게시물 id 목록을 유지할 수 있는 문서를 만들기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-132">Creating feeds is just a matter of creating documents that can hold a list of post ids with a given relevance order:</span></span>

    [
        {"relevance":9, "post":"ew12-res2-234e-544f"},
        {"relevance":8, "post":"fer7-mnb6-fgh9-2344"},
        {"relevance":7, "post":"w34r-qeg6-ref6-8565"}
    ]

<span data-ttu-id="ce162-133">"최신" 스트림을 만든 날짜별으로 정렬 된 포스트가, 지난 24 시간 동안 hello에 더 많은 like 있는 게시 설정과 "가장 많이 사용" 스트림도 구현 하 여 후속 작업이 관심사에 같은 논리에 따라 각 사용자에 대 한 사용자 지정 스트림 및 목록이 됩니다.  게시합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-133">We could have a “latest” stream with posts ordered by creation date, a “hottest” stream with those posts with more likes in hello last 24 hours, we could even implement a custom stream for each user based on logic like followers and interests, and it would still be a list of posts.</span></span> <span data-ttu-id="ce162-134">어떻게 toobuild 이러한으로 나열 하는 것 이지만 hello 읽기 성능 제약 없이 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-134">It’s a matter of how toobuild these lists, but hello reading performance remains unhindered.</span></span> <span data-ttu-id="ce162-135">이러한 목록 중 하나를 획득 म म 실행 하 여 단일 쿼리 tooCosmos DB hello를 사용 하 여 [연산자에서](documentdb-sql-query.md#WhereClause) 한 번에 대 한 게시의 tooobtain 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-135">Once we acquire one of these lists, we issue a single query tooCosmos DB using hello [IN operator](documentdb-sql-query.md#WhereClause) tooobtain pages of posts at a time.</span></span>

<span data-ttu-id="ce162-136">스트림 피드 hello를 사용 하 여 구축 될 수 [Azure 앱 서비스](https://azure.microsoft.com/services/app-service/) 백그라운드 프로세스: [Webjobs](../app-service-web/web-sites-create-web-jobs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-136">hello feed streams could be built using [Azure App Services’](https://azure.microsoft.com/services/app-service/) background processes: [Webjobs](../app-service-web/web-sites-create-web-jobs.md).</span></span> <span data-ttu-id="ce162-137">사용 하 여 백그라운드 처리를 트리거할 수 게시물 만들어지면 [Azure 저장소](https://azure.microsoft.com/services/storage/) [큐](../storage/queues/storage-dotnet-how-to-use-queues.md) Webjobs hello를 사용 하 여 발생 하 고 [Azure Webjobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md), 구현 hello 고유한 사용자 지정 논리에 따라 스트림 내 전파를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-137">Once a post is created, background processing can be triggered by using [Azure Storage](https://azure.microsoft.com/services/storage/) [Queues](../storage/queues/storage-dotnet-how-to-use-queues.md) and Webjobs triggered using hello [Azure Webjobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md), implementing hello post propagation inside streams based on our own custom logic.</span></span> 

<span data-ttu-id="ce162-138">지점 및 게시물을 통해 사용이 동일한 기술을 toocreate 결국 일관 된 환경을 사용 하 여 지연 된 방식으로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-138">Points and likes over a post can be processed in a deferred manner using this same technique toocreate an eventually consistent environment.</span></span>

<span data-ttu-id="ce162-139">팔로워는 더 복잡합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-139">Followers are trickier.</span></span> <span data-ttu-id="ce162-140">Cosmos DB에는 최대 문서 크기 제한 및 큰 문서에 대 한 읽기/쓰기 응용 프로그램의 hello 확장성에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-140">Cosmos DB has a maximum document size limit, and reading/writing large documents can impact hello scalability of your application.</span></span> <span data-ttu-id="ce162-141">다음 구조를 사용하여 팔로워를 저장하는 방법을 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-141">So you may think about storing followers as a document with this structure:</span></span>

    {
        "id":"234d-sd23-rrf2-552d",
        "followersOf": "dse4-qwe2-ert4-aad2",
        "followers":[
            "ewr5-232d-tyrg-iuo2",
            "qejh-2345-sdf1-ytg5",
            //...
            "uie0-4tyg-3456-rwjh"
        ]
    }

<span data-ttu-id="ce162-142">이 방식은 몇 천 있는 사용자에 대 한 작동 후속 작업이 있지만 경우 일부 유명인 우리의 순위 조인,이 방법은 tooa 큰 문서 크기를 일으킵니다 결국 적중된 hello 문서 크기를 닫을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-142">This might work for a user with a few thousands followers, but if some celebrity joins our ranks, this approach will lead tooa large document size, and might eventually hit hello document size cap.</span></span>

<span data-ttu-id="ce162-143">toosolve이 혼합된 접근 방식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-143">toosolve this, we can use a mixed approach.</span></span> <span data-ttu-id="ce162-144">Hello 사용자 통계 문서의 일부로 hello 수가 후속 작업이 저장할 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="ce162-144">As part of hello User Statistics document we can store hello number of followers:</span></span>

    {
        "id":"234d-sd23-rrf2-552d",
        "user": "dse4-qwe2-ert4-aad2",
        "followers":55230,
        "totalPosts":452,
        "totalPoints":11342
    }

<span data-ttu-id="ce162-145">후속 작업이의 실제 그래프 hello Azure Cosmos DB를 사용 하 여 저장 될 수 있습니다 [Gremlin Graph API](../cosmos-db/graph-introduction.md), toocreate [정점](http://mathworld.wolfram.com/GraphVertex.html) 각 사용자에 대해 및 [가장자리](http://mathworld.wolfram.com/GraphEdge.html) hello 유지 관리 하는 " A-다음과 같이-B "관계입니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-145">And hello actual graph of followers can be stored using Azure Cosmos DB [Gremlin Graph API](../cosmos-db/graph-introduction.md), toocreate [vertexes](http://mathworld.wolfram.com/GraphVertex.html) for each user and [edges](http://mathworld.wolfram.com/GraphEdge.html) that maintain hello "A-follows-B" relationships.</span></span> <span data-ttu-id="ce162-146">hello Graph API 보겠습니다 있습니다 가져올 특정 사용자의 hello 후속 작업이 뿐아니라 tooeven 공통 사용자를 제안 하는 보다 복잡 한 쿼리를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-146">hello Graph API let's you not only obtain hello followers of a certain user but create more complex queries tooeven suggest people in common.</span></span> <span data-ttu-id="ce162-147">Toohello 그래프 hello 추가 콘텐츠 범주 주는 같은 또는 즐길 수, 우리 수 시작 스마트 내용 검색을 포함 하는 환경을 구성 콘텐츠를 제안 하는 것 것 처럼, 따릅니다 또는 함께 수 있는 많은 공통 사람 찾기.</span><span class="sxs-lookup"><span data-stu-id="ce162-147">If we add toohello graph hello Content Categories that people like or enjoy, we can start weaving experiences that include smart content discovery, suggesting content that those we follow like, or finding people with whom we might have much in common.</span></span>

<span data-ttu-id="ce162-148">hello 사용자 통계 문서 hello UI 또는 빠른 프로필 미리 보기에서 사용 되는 toocreate 카드 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-148">hello User Statistics document can still be used toocreate cards in hello UI or quick profile previews.</span></span>

## <a name="hello-ladder-pattern-and-data-duplication"></a><span data-ttu-id="ce162-149">"사다리" 패턴 및 데이터 중복 hello</span><span class="sxs-lookup"><span data-stu-id="ce162-149">hello “Ladder” pattern and data duplication</span></span>
<span data-ttu-id="ce162-150">게시물을 참조 하는 hello JSON 문서에서 보았을 것, 사용자를 여러 번 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-150">As you might have noticed in hello JSON document that references a post, there are multiple occurrences of a user.</span></span> <span data-ttu-id="ce162-151">고가 있는 개이면 오른쪽이 비 정규화 지정 된 사용자를 나타내는 hello 정보는 둘 이상의 위치에 있는 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-151">And you’d have guessed right, this means that hello information that represents a user, given this denormalization, might be present in more than one place.</span></span>

<span data-ttu-id="ce162-152">더 빠른 쿼리에 대 한 순서 tooallow에서 우리에 데이터 중복을 발생 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-152">In order tooallow for faster queries, we incur data duplication.</span></span> <span data-ttu-id="ce162-153">이 인해 hello 문제는 일부 작업을 사용자의 데이터 변경 내용을 통해 toofind 해야 하는 경우 모든 hello 활동 그 되지 않았습니다 및 업데이트는 모두입니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-153">hello problem with this side-effect is that if by some action, a user’s data changes, we need toofind all hello activities he ever did and update them all.</span></span> <span data-ttu-id="ce162-154">그다지 실용적으로 들리지 않죠, 그렇죠?</span><span class="sxs-lookup"><span data-stu-id="ce162-154">Doesn’t sound very practical, right?</span></span>

<span data-ttu-id="ce162-155">진행 중인 toosolve 각 활동에 대 한 응용 프로그램에서 표시 하는 사용자의 키 속성을 식별 하 여 hello 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-155">We are going toosolve it by identifying hello Key attributes of a user that we show in our application for each activity.</span></span> <span data-ttu-id="ce162-156">시각적으로 응용 프로그램의 게시물을 표시 하 고 방금 hello 작성자의 이름 및 표시 사진, 경우 이유 저장 hello 사용자의 데이터를 모두 createdBy"hello" 특성에 합니까?</span><span class="sxs-lookup"><span data-stu-id="ce162-156">If we visually show a post in our application and show just hello creator’s name and picture, why store all of hello user’s data in hello “createdBy” attribute?</span></span> <span data-ttu-id="ce162-157">각 추가 대 한 방금 알아보겠습니다 hello 사용자의 사진, 경우 hello 나머지 자신의 정보 실제로 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-157">If for each comment we just show hello user’s picture, we don’t really need hello rest of his information.</span></span> <span data-ttu-id="ce162-158">플레이 놓임 "사다리 패턴" hello를 호출 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-158">That’s where something I call hello “Ladder pattern” comes into play.</span></span>

<span data-ttu-id="ce162-159">다음 사용자 정보를 예로 들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-159">Let’s take user information as an example:</span></span>

    {
        "id":"dse4-qwe2-ert4-aad2",
        "name":"John",
        "surname":"Doe",
        "address":"742 Evergreen Terrace",
        "birthday":"1983-05-07",
        "email":"john@doe.com",
        "twitterHandle":"@john",
        "username":"johndoe",
        "password":"some_encrypted_phrase",
        "totalPoints":100,
        "totalPosts":24
    }

<span data-ttu-id="ce162-160">이 정보를 보면 중요한 정보와 중요하지 않은 정보를 신속하게 감지할 수 있으므로 다음과 같은 “사다리”가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-160">By looking at this information, we can quickly detect which is critical information and which isn’t, thus creating a “Ladder”:</span></span>

![사다리 패턴의 다이어그램](./media/social-media-apps/social-media-apps-ladder.png)

<span data-ttu-id="ce162-162">hello 가장 작은 단계 UserChunk, hello 최소 부분의 사용자를 식별 하는 정보 라고 하 고 데이터 중복 제거에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-162">hello smallest step is called a UserChunk, hello minimal piece of information that identifies a user and it’s used for data duplication.</span></span> <span data-ttu-id="ce162-163">중복 hello 데이터 tooonly hello 정보 "보겠지만" hello 크기를 줄여 대규모 업데이트 hello 가능성을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-163">By reducing hello size of hello duplicated data tooonly hello information we will “show”, we reduce hello possibility of massive updates.</span></span>

<span data-ttu-id="ce162-164">hello 중간 단계 hello 사용자 라고, 것이 가장 액세스 되 고 중요 한 Cosmos DB에서 대부분의 성능 종속 쿼리에 사용 될 hello 전체 데이터 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-164">hello middle step is called hello user, it’s hello full data that will be used on most performance-dependent queries on Cosmos DB, hello most accessed and critical.</span></span> <span data-ttu-id="ce162-165">UserChunk 표현 hello 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-165">It includes hello information represented by a UserChunk.</span></span>

<span data-ttu-id="ce162-166">가장 큰 hello는 hello 확장 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-166">hello largest is hello Extended User.</span></span> <span data-ttu-id="ce162-167">모든 hello 중요 사용자 정보를 포함 하지 않는 정말 신속 하 게 toobe 읽기를 필요한 다른 데이터 또는 사용이 최종 (예: hello 로그인 프로세스).</span><span class="sxs-lookup"><span data-stu-id="ce162-167">It includes all hello critical user information plus other data that doesn’t really require toobe read quickly or it’s usage is eventual (like hello login process).</span></span> <span data-ttu-id="ce162-168">이 데이터를 Cosmos DB 외부, Azure SQL Database 또는 Azure Storage 테이블에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-168">This data can be stored outside of Cosmos DB, in Azure SQL Database or Azure Storage Tables.</span></span>

<span data-ttu-id="ce162-169">이유는 म hello 사용자 나누고도 서로 다른 위치에서이 정보를 저장할?</span><span class="sxs-lookup"><span data-stu-id="ce162-169">Why would we split hello user and even store this information in different places?</span></span> <span data-ttu-id="ce162-170">성능 관점에서 hello 큰 hello 문서 hello costlier hello 쿼리 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-170">Because from a performance point of view, hello bigger hello documents, hello costlier hello queries.</span></span> <span data-ttu-id="ce162-171">문서 보관 hello로 slim 오른쪽 정보 toodo 모든 사용자 성능 종속 소셜 네트워크를 쿼리하고 저장소 hello 같은 최종 시나리오, 전체 프로필을 편집, 로그인에 대 한 기타 추가 정보, 사용 현황 분석 및 큰에 대 한 데이터 마이닝에도 데이터 이니셔티브입니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-171">Keep documents slim, with hello right information toodo all your performance-dependent queries for your social network, and store hello other extra information for eventual scenarios like, full profile edits, logins, even data mining for usage analytics and Big Data initiatives.</span></span> <span data-ttu-id="ce162-172">에서는 실제로 중요 하지 않으면 Azure SQL 데이터베이스에서 실행 되 고 있어서 hello 데이터 수집을 데이터 마이닝에 대 한 느린 경우, 우리 않습니다가 관련 하지만 사용자가 신속 하 고 slim 경험 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-172">We really don’t care if hello data gathering for data mining is slower because it’s running on Azure SQL Database, we do have concern though that our users have a fast and slim experience.</span></span> <span data-ttu-id="ce162-173">Cosmos DB에 저장된 사용자는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-173">A user, stored on Cosmos DB, would look like this:</span></span>

    {
        "id":"dse4-qwe2-ert4-aad2",
        "name":"John",
        "surname":"Doe",
        "username":"johndoe"
        "email":"john@doe.com",
        "twitterHandle":"@john"
    }

<span data-ttu-id="ce162-174">그리고 게시물은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-174">And a Post would look like:</span></span>

    {
        "id":"1234-asd3-54ts-199a",
        "title":"Awesome post!",
        "date":"2016-01-02",
        "createdBy":{
            "id":"dse4-qwe2-ert4-aad2",
            "username":"johndoe"
        }
    }

<span data-ttu-id="ce162-175">이므로 여기서 hello 청크의 hello 특성 중 하나는 영향을 편집 하는 발생 하는 경우 쉽게 toofind 영향을 받는 hello 문서 toohello 인덱싱된 특성을 가리키는 쿼리를 사용 하 여 (선택 * FROM 게시 p WHERE p.createdBy.id "edited_user_id" = =) 제거한 다음 업데이트 hello 청크 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-175">And when an edit arises where one of hello attributes of hello chunk is affected, it’s easy toofind hello affected documents by using queries that point toohello indexed attributes (SELECT * FROM posts p WHERE p.createdBy.id == “edited_user_id”) and then updating hello chunks.</span></span>

## <a name="hello-search-box"></a><span data-ttu-id="ce162-176">hello 검색 상자</span><span class="sxs-lookup"><span data-stu-id="ce162-176">hello search box</span></span>
<span data-ttu-id="ce162-177">다행히 사용자는 많은 콘텐츠를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-177">Users will generate, luckily, a lot of content.</span></span> <span data-ttu-id="ce162-178">수 tooprovide hello 기능 toosearch 수와 수 없는 자신의 콘텐츠 스트림을에서 직접 미정 hello 작성자를 준수 하지 않는 것 때문에 콘텐츠를 찾을 해야 하거나 미정 노력 하 고 방금 toofind 6 개월 전에 수행한 해당 이전 게시물.</span><span class="sxs-lookup"><span data-stu-id="ce162-178">And we should be able tooprovide hello ability toosearch and find content that might not be directly in their content streams, maybe because we don’t follow hello creators, or maybe we are just trying toofind that old post we did 6 months ago.</span></span>

<span data-ttu-id="ce162-179">다행히 Azure Cosmos DB를 사용 하 고 있으므로 서 구현할 수 있는 쉽게 사용 하 여 검색 엔진 및 [Azure 검색](https://azure.microsoft.com/services/search/) 는 몇 시간 (분) 및 코드 한 줄을 입력 하지 않고도 (물론 hello 이외의 검색 프로세스와 UI).</span><span class="sxs-lookup"><span data-stu-id="ce162-179">Thankfully, and because we are using Azure Cosmos DB, we can easily implement a search engine using [Azure Search](https://azure.microsoft.com/services/search/) in a couple of minutes and without typing a single line of code (other than obviously, hello search process and UI).</span></span>

<span data-ttu-id="ce162-180">이 작업이 이렇게 쉬운 이유는 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="ce162-180">Why is this so easy?</span></span>

<span data-ttu-id="ce162-181">Azure 검색을 호출 하기 구현 [인덱서](https://msdn.microsoft.com/library/azure/dn946891.aspx), 백그라운드 처리 후크 하는 데이터 저장소에서 및 자동으로 추가, 업데이트 또는 hello 인덱스에 개체를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-181">Azure Search implements what they call [Indexers](https://msdn.microsoft.com/library/azure/dn946891.aspx), background processes that hook in your data repositories and automagically add, update or remove your objects in hello indexes.</span></span> <span data-ttu-id="ce162-182">Azure Search는 [Azure SQL Database 인덱서](https://blogs.msdn.microsoft.com/kaevans/2015/03/06/indexing-azure-sql-database-with-azure-search/), [Azure Blob 인덱서](../search/search-howto-indexing-azure-blob-storage.md) 그리고 다행히도 [Azure Cosmos DB 인덱서](../search/search-howto-index-documentdb.md)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-182">They support an [Azure SQL Database indexers](https://blogs.msdn.microsoft.com/kaevans/2015/03/06/indexing-azure-sql-database-with-azure-search/), [Azure Blobs indexers](../search/search-howto-indexing-azure-blob-storage.md) and thankfully, [Azure Cosmos DB indexers](../search/search-howto-index-documentdb.md).</span></span> <span data-ttu-id="ce162-183">hello Cosmos DB tooAzure 검색에서에서 정보의 변환은 두 저장소 정보를 JSON 형식으로 간단 하 게, त ु म च 너무[우리의 인덱스를 만들](../search/search-create-index-portal.md) 문서 특성 인덱싱된 원하는 및 설정 작업이 완료를 하 고 매핑할 몇 분 내에 (데이터의 hello 크기에 따라 다름)이 모든 콘텐츠는 클라우드 인프라에서 hello 최상의 검색-as a Service 솔루션에 의해 검색 되는 특성을 사용할 수 있는 toobe 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-183">hello transition of information from Cosmos DB tooAzure Search is straightforward, as both store information in JSON format, we just need too[create our Index](../search/search-create-index-portal.md) and map which attributes from our Documents we want indexed and that’s it, in a matter of minutes (depends on hello size of our data), all our content will be available toobe searched upon, by hello best Search-as-a-Service solution in cloud infrastructure.</span></span> 

<span data-ttu-id="ce162-184">Azure 검색에 대 한 자세한 내용은 hello를 방문할 수 있는 [Hitchhiker's Guide tooSearch](https://blogs.msdn.microsoft.com/mvpawardprogram/2016/02/02/a-hitchhikers-guide-to-search/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-184">For more information about Azure Search, you can visit hello [Hitchhiker’s Guide tooSearch](https://blogs.msdn.microsoft.com/mvpawardprogram/2016/02/02/a-hitchhikers-guide-to-search/).</span></span>

## <a name="hello-underlying-knowledge"></a><span data-ttu-id="ce162-185">hello 기본 기술</span><span class="sxs-lookup"><span data-stu-id="ce162-185">hello underlying knowledge</span></span>
<span data-ttu-id="ce162-186">매일 증가하는 이 모든 콘텐츠를 저장한 후에는 이 모든 사용자 정보 스트림으로 수행할 수 있는 작업이 무엇인지 궁금할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-186">After storing all this content that grows and grows every day, we might find ourselves thinking: What can I do with all this stream of information from my users?</span></span>

<span data-ttu-id="ce162-187">hello 응답은 간단: toowork 배치 고 알아두는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-187">hello answer is straightforward: Put it toowork and learn from it.</span></span>

<span data-ttu-id="ce162-188">그렇다면 무엇을 배울 수 있을까요?</span><span class="sxs-lookup"><span data-stu-id="ce162-188">But, what can we learn?</span></span> <span data-ttu-id="ce162-189">몇 가지 쉽게 예로 [감성 분석](https://en.wikipedia.org/wiki/Sentiment_analysis), 사용자의 기본 설정에 따라 권장 사항을 또는 심지어는 자동화 된 콘텐츠 중재자 소셜 네트워크에서 게시 한 콘텐츠를 hello 모두 보장 하는 hello에 대 한 안전 콘텐츠 패밀리입니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-189">A few easy examples include [sentiment analysis](https://en.wikipedia.org/wiki/Sentiment_analysis), content recommendations based on a user’s preferences or even an automated content moderator that ensures that all hello content published by our social network is safe for hello family.</span></span>

<span data-ttu-id="ce162-190">연결 하면 수신 됨, 했으므로 이러한 패턴 및 단순 데이터베이스 및 파일을 정보 수학 과학 tooextract에서 일부 조차 필요 하지만 잘못 된 것 아마도 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-190">Now that I got you hooked, you’ll probably think you need some PhD in math science tooextract these patterns and information out of simple databases and files, but you’d be wrong.</span></span>

<span data-ttu-id="ce162-191">[Azure 기계 학습](https://azure.microsoft.com/services/machine-learning/)hello의 일부인 [Cortana 인텔리전스 Suite](https://www.microsoft.com/en/server-cloud/cortana-analytics-suite/overview.aspx)는 hello 간단한 끌어서 놓기 인터페이스에서 알고리즘을 사용 하 여 워크플로 만들고, 사용자 고유의 알고리즘 코드 있습니다 수 있게 해 주는 완전히 관리 되는 클라우드 서비스 [R](https://en.wikipedia.org/wiki/R_\(programming_language\)) hello 이미 작성의 일부를 사용 하 고 사용할 수 있는 상태 toouse Api와 같은: [텍스트 분석](https://gallery.cortanaanalytics.com/MachineLearningAPI/Text-Analytics-2), [콘텐츠 중재자](https://www.microsoft.com/moderator) 또는 [권장사항](https://gallery.cortanaanalytics.com/MachineLearningAPI/Recommendations-2).</span><span class="sxs-lookup"><span data-stu-id="ce162-191">[Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/), part of hello [Cortana Intelligence Suite](https://www.microsoft.com/en/server-cloud/cortana-analytics-suite/overview.aspx), is hello a fully managed cloud service that lets you create workflows using algorithms in a simple drag-and-drop interface, code your own algorithms in [R](https://en.wikipedia.org/wiki/R_\(programming_language\)) or use some of hello already-built and ready toouse APIs such as: [Text Analytics](https://gallery.cortanaanalytics.com/MachineLearningAPI/Text-Analytics-2),  [Content Moderator](https://www.microsoft.com/moderator) or [Recommendations](https://gallery.cortanaanalytics.com/MachineLearningAPI/Recommendations-2).</span></span>

<span data-ttu-id="ce162-192">tooachieve 모든 이러한 기계 학습 시나리오를 사용할 수 [Azure 데이터 레이크](https://azure.microsoft.com/services/data-lake-store/) tooingest hello 다양 한 원본에서 정보 및 사용 하 여 [U-SQL](https://azure.microsoft.com/documentation/videos/data-lake-u-sql-query-execution/) tooprocess hello 정보 및 출력을 생성 합니다. Azure 기계 학습에서 처리 될 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-192">tooachieve any of these Machine Learning scenarios, we can use [Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/) tooingest hello information from different sources, and use [U-SQL](https://azure.microsoft.com/documentation/videos/data-lake-u-sql-query-execution/) tooprocess hello information and generate an output that can be processed by Azure Machine Learning.</span></span>

<span data-ttu-id="ce162-193">또 다른 사용 가능한 옵션은 toouse [Microsoft Cognitive 서비스](https://www.microsoft.com/cognitive-services) tooanalyze 콘텐츠; 뿐만 아니라 이해 수에서는 사용자에 게 더욱 효율적인 (으로 작성할 어떤 분석을 통해 [텍스트 분석 API](https://www.microsoft.com/cognitive-services/en-us/text-analytics-api)), 하지만 또한 원하지 않거나 성숙한 내용을 검색 하 고 적절 하 게 작동할 수와 [컴퓨터 비전 API](https://www.microsoft.com/cognitive-services/en-us/computer-vision-api)합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-193">Another available option is toouse [Microsoft Cognitive Services](https://www.microsoft.com/cognitive-services) tooanalyze our users content; not only can we understand them better (through analyzing what they write with [Text Analytics API](https://www.microsoft.com/cognitive-services/en-us/text-analytics-api)) , but we could also detect unwanted or mature content and act accordingly with [Computer Vision API](https://www.microsoft.com/cognitive-services/en-us/computer-vision-api).</span></span> <span data-ttu-id="ce162-194">Cognitive 서비스의 기본 솔루션에 어떤 유형의 기계 학습 기술 toouse 요구 하지 않는 많이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-194">Cognitive Services include a lot of out-of-the-box solutions that don't require any kind of Machine Learning knowledge toouse.</span></span>

## <a name="a-planet-scale-social-experience"></a><span data-ttu-id="ce162-195">전 세계적인 규모의 소셜 환경</span><span class="sxs-lookup"><span data-stu-id="ce162-195">A planet-scale social experience</span></span>
<span data-ttu-id="ce162-196">마지막으로 해결해야 하는 중요한 사항은 **확장성**입니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-196">There is a last, but not least, important topic I must address: **scalability**.</span></span> <span data-ttu-id="ce162-197">각 구성 요소 크기를 조정할 수는 자체적으로 하거나 tooprocess 더 많은 데이터가 필요 하기 때문에 중요 한 아키텍처를 설계할 때 또는 큰 지리적 검사 (또는 둘 다!) toohave 확인 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-197">When designing an architecture it's crucial that each component can scale on its own, either because we need tooprocess more data or because we want toohave a bigger geographical coverage (or both!).</span></span> <span data-ttu-id="ce162-198">다행스럽게도 Cosmos DB를 사용하여 **턴키 환경**에서 이러한 복잡한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-198">Thankfully, achieving such a complex task is a **turnkey experience** with Cosmos DB.</span></span>

<span data-ttu-id="ce162-199">Cosmos DB 지원 [동적 분할](https://azure.microsoft.com/blog/10-things-to-know-about-documentdb-partitioned-collections/) -의-즉시 자동으로 만들어을 기반으로 파티션은 주어진 **파티션 키** (문서에 hello 특성 중 하나로 정의 됨).</span><span class="sxs-lookup"><span data-stu-id="ce162-199">Cosmos DB supports [dynamic partitioning](https://azure.microsoft.com/blog/10-things-to-know-about-documentdb-partitioned-collections/) out-of-the-box by automatically creating partitions based on a given **partition key** (defined as one of hello attributes in your documents).</span></span> <span data-ttu-id="ce162-200">디자인 타임에 파티션 키를 수행 해야 올바른 hello를 정의 하 고 주의 hello에 유지 [모범 사례](../cosmos-db/partition-data.md#designing-for-partitioning) 사용할 수 있습니다;은 소셜 환경의 hello 경우 분할 전략에 정렬 되어야 합니다 (읽기를 쿼리 하는 hello 방식으로 hello에 동일한 파티션에 바람직한) 및 쓰기 ("핫 스폿을" 여러 파티션에 쓰기를 분산 함으로써 방지).</span><span class="sxs-lookup"><span data-stu-id="ce162-200">Defining hello correct partition key must be done at design time and keeping in mind hello [best practices](../cosmos-db/partition-data.md#designing-for-partitioning) available; in hello case of a social experience, your partitioning strategy must be aligned with hello way you query (reads within hello same partition are desirable) and write (avoid "hot spots" by spreading writes on multiple partitions).</span></span> <span data-ttu-id="ce162-201">일부 옵션은:; 사용자가 지리적 지역에 따라 콘텐츠 범주별으로 보여 줍니다 (일/월/주) 임시 키에 따라 파티션 실제로 이것은 모두는 hello 데이터를 쿼리 하는 방법을 소셜 환경을에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-201">Some options are: partitions based on a temporal key (day/month/week), by content category, by geographical region, by user; it all really depends on how you will query hello data and show it in your social experience.</span></span> 

<span data-ttu-id="ce162-202">중요 한 한 흥미로운 점을 주의 해야 Cosmos DB가 쿼리를 실행 합니다 (포함 하 여 [집계](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/)) 모든 파티션을 통해 투명 하 게, 필요 하지 않습니다 tooadd는 논리 데이터 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-202">One interesting point worth mentioning is that Cosmos DB will run your queries (including [aggregates](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/)) across all your partitions transparently, you don't need tooadd any logic as your data grows.</span></span>

<span data-ttu-id="ce162-203">시간이 지나면 결국 트래픽이 증가하고 리소스 사용([RU](request-units.md) 또는 요청 단위)도 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-203">With time, you will eventually grow in traffic and your resource consumption (measured in [RUs](request-units.md), or Request Units) will increase.</span></span> <span data-ttu-id="ce162-204">읽기 및 쓰기 작업을 더 자주 프로그램 userbase 증가 하 고 만들고 더 많은 콘텐츠; 읽기 시작 합니다 됩니다. 능력을 hello **처리량 배율** 이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-204">You will read and write more frequently as your userbase grows and they will start creating and reading more content; hello ability of **scaling your throughput** is vital.</span></span> <span data-ttu-id="ce162-205">우리의 RUs 증가 하는 것은 매우 쉽게, 또는 hello Azure 포털에서 몇 번의 클릭 하겠습니다 [hello API 통해 명령을 발급](https://docs.microsoft.com/rest/api/documentdb/replace-an-offer)합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-205">Increasing our RUs is very easy, we can do it with a few clicks on hello Azure Portal or by [issuing commands through hello API](https://docs.microsoft.com/rest/api/documentdb/replace-an-offer).</span></span>

![파티션 키 확장 및 정의](./media/social-media-apps/social-media-apps-scaling.png)

<span data-ttu-id="ce162-207">기능이 점점 확장되고 다른 지역, 국가 또는 대륙의 사용자가 당신의 플랫폼을 알고 사용하기 시작한다면 놀라운 일이 벌어집니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-207">What happens if things keep getting better and users from another region, country or continent, notice your platform and start using it, what a great surprise!</span></span>

<span data-ttu-id="ce162-208">잠깐... 경험 플랫폼에 최적이 아닌; 곧 실현 지금까지 operational 해당 지역에서 멀리는 hello 대기 시간은 테러, 분명 할 tooquit 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-208">But wait... you soon realize their experience with your platform is not optimal; they are so far away from your operational region that hello latency is terrible, and you obviously don't want them tooquit.</span></span> <span data-ttu-id="ce162-209">**글로벌 도달률을 확장**하는 쉬운 방법이 있다면 얼마나 좋을까요. 방법이 있습니다!</span><span class="sxs-lookup"><span data-stu-id="ce162-209">If only there was an easy way of **extending your global reach**... but there is!</span></span>

<span data-ttu-id="ce162-210">Cosmos DB을 사용 하면 [데이터를 전역적으로 복제](../cosmos-db/tutorial-global-distribution-documentdb.md) 투명 하 게의 클릭 하 고 자동으로 두 hello에서 사용 가능한 영역 사이에서 선택할 사용자 [클라이언트 코드](../cosmos-db/tutorial-global-distribution-documentdb.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-210">Cosmos DB lets you [replicate your data globally](../cosmos-db/tutorial-global-distribution-documentdb.md) and transparently with a couple of clicks and automatically select among hello available regions from your [client code](../cosmos-db/tutorial-global-distribution-documentdb.md).</span></span> <span data-ttu-id="ce162-211">즉, [여러 장애 조치 지역](regional-failover.md)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-211">This also means that you can have [multiple failover regions](regional-failover.md).</span></span> 

<span data-ttu-id="ce162-212">데이터를 전역적으로 복제 하 여 클라이언트를 사용할 수 있습니다는 있는지 toomake가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-212">When you replicate your data globally, you need toomake sure that your clients can take advantage of it.</span></span> <span data-ttu-id="ce162-213">웹 프런트 엔드 또는 모바일 클라이언트 로부터의 액세스 Api 사용 하는 경우 배포할 수 있습니다 [Azure 트래픽 관리자](https://azure.microsoft.com/services/traffic-manager/) 및 Azure 앱 서비스에서 모든 필요한 hello 지역을 사용 하 여 복제를 [성능 구성](../app-service-web/web-sites-traffic-manager.md)toosupport 확장된 광범위 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-213">If you are using a web frontend or accesing APIs from mobile clients, you can deploy [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) and clone your Azure App Service on all hello desired regions, using a [Performance configuration](../app-service-web/web-sites-traffic-manager.md) toosupport your extended global coverage.</span></span> <span data-ttu-id="ce162-214">라우트된 toohello 됩니다 클라이언트 프런트 엔드 또는 Api에 액세스 하는 경우 가장 가까운 응용 프로그램 서비스를 차례로 toohello 로컬 Cosmos DB 복제본 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-214">When your clients access your frontend or APIs, they will be routed toohello closest App Service, which in turn, will connect toohello local Cosmos DB replica.</span></span>

![범위 tooyour 소셜 플랫폼 추가](./media/social-media-apps/social-media-apps-global-replicate.png)

## <a name="conclusion"></a><span data-ttu-id="ce162-216">결론</span><span class="sxs-lookup"><span data-stu-id="ce162-216">Conclusion</span></span>
<span data-ttu-id="ce162-217">이 문서는 tooshed 저렴 한 비용 서비스와 Azure에서 완전히 소셜 네트워크를 만드는 및 "사다리" 라는 저장소 다중 계층된 솔루션 및 데이터 배포 하도록 권유 hello 사용 하 여 만족 스러운 결과 제공 하는 hello 대안에 연한 일부를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-217">This article tries tooshed some light into hello alternatives of creating social networks completely on Azure with low-cost services and providing great results by encouraging hello use of a multi-layered storage solution and data distribution called “Ladder”.</span></span>

![소셜 네트워킹에 대한 Azure 서비스 간 상호 작용의 다이어그램](./media/social-media-apps/social-media-apps-azure-solution.png)

<span data-ttu-id="ce162-219">이러한 종류의 시나리오에 대 한 은색 글머리 기호 없음에 hello 사실입니다 hello toobuild 훌륭한 환경을 수 있는 훌륭한 서비스의 hello 조합 하 여 만든 시너지 효과: 속도 Azure Cosmos DB tooprovide 훌륭한 소셜 응용 프로그램의 자유 hello Azure 앱 서비스 toohost의 hello 유연성 강력한 백그라운드 프로세스를 제외한 언어를 알 수 없는 응용 프로그램에도 없고 Azure 저장소 및 Azure SQL 데이터베이스에 대 한 확장 가능한 hello, hello intelligence 첫 번째 클래스 검색 솔루션 뒤에 Azure 검색 등과 같은 대량의 toocreate Azure 기계 학습의 데이터 및 hello 분석 전원 저장 지식과 tooour 프로세스 피드백을 제공 하 고 도움을 수 있는 intelligence hello 오른쪽 콘텐츠 toohello 오른쪽 사용자에 게 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-219">hello truth is that there is no silver bullet for this kind of scenarios, it’s hello synergy created by hello combination of great services that allow us toobuild great experiences: hello speed and freedom of Azure Cosmos DB tooprovide a great social application, hello intelligence behind a first-class search solution like Azure Search, hello flexibility of Azure App Services toohost not even language-agnostic applications but powerful background processes and hello expandable Azure Storage and Azure SQL Database for storing massive amounts of data and hello analytic power of Azure Machine Learning toocreate knowledge and intelligence that can provide feedback tooour processes and help us deliver hello right content toohello right users.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce162-220">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ce162-220">Next steps</span></span>
<span data-ttu-id="ce162-221">Cosmos DB에 대 한 사용 사례에 대해 자세히 toolearn 참조 [Cosmos DB 일반적인 사용 사례](use-cases.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ce162-221">toolearn more about use cases for Cosmos DB, see [Common Cosmos DB use cases](use-cases.md).</span></span>
