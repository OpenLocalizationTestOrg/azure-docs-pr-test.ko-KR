---
title: "Azure Cosmos DB 디자인 패턴: 소셜 미디어 앱 | Microsoft Docs"
description: "Azure Cosmos DB 및 기타 Azure 서비스의 저장소 유연성을 활용하여 소셜 네트워크에 대한 디자인 패턴을 알아봅니다."
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
ms.openlocfilehash: 43025adeaf954fedfbcee32e636fb30935f2126b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="going-social-with-azure-cosmos-db"></a><span data-ttu-id="ec825-104">Azure Cosmos DB를 사용하여 소셜 네트워크 디자인</span><span class="sxs-lookup"><span data-stu-id="ec825-104">Going social with Azure Cosmos DB</span></span>
<span data-ttu-id="ec825-105">광범위하게 상호 연결된 사회에서 살고 있다는 것은 삶의 어느 시점에서 **소셜 네트워크**의 일부가 된다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-105">Living in a massively-interconnected society means that, at some point in life, you become part of a **social network**.</span></span> <span data-ttu-id="ec825-106">우리는 소셜 네트워크를 사용하여 친구, 동료, 가족 등과 연락하거나, 때로는 공통의 관심사를 가진 사람들과 열정을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-106">We use social networks to keep in touch with friends, colleagues, family, or sometimes to share our passion with people with common interests.</span></span>

<span data-ttu-id="ec825-107">엔지니어 또는 개발자로서 우리는 이러한 네트워크가 데이터를 저장하고 상호 연결하는 방법 또는 특정 틈새 시장을 위한 새로운 소셜 네트워크를 만들거나 설계하는 데 활용되어 왔을 수 있는 방법이 궁금할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-107">As engineers or developers, we might have wondered how do these networks store and interconnect our data, or might have even been tasked to create or architect a new social network for a specific niche market yourselves.</span></span> <span data-ttu-id="ec825-108">특히 이 모든 데이터가 어떻게 저장되는지가 매우 궁금할 때 더욱 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-108">That’s when the big question arises: How is all this data stored?</span></span>

<span data-ttu-id="ec825-109">사용자가 사진, 동영상 또는 음악과 같은 관련 미디어와 함께 문서를 게시할 수 있는 새롭고 참신한 소셜 네트워크를 만든다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-109">Let’s suppose that we are creating a new and shiny social network, where our users can post articles with related media like, pictures, videos, or even music.</span></span> <span data-ttu-id="ec825-110">사용자는 게시물에 의견을 달고 평점을 매길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-110">Users can comment on posts and give points for ratings.</span></span> <span data-ttu-id="ec825-111">기본 웹 사이트 방문 페이지에는 사용자가 보고 상호 작용할 수 있는 게시물 피드가 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-111">There will be a feed of posts that users will see and be able to interact with on the main website landing page.</span></span> <span data-ttu-id="ec825-112">처음에는 실제로 복잡하게 들리지 않겠지만 간단한 설명을 위해 이에 대한 내용은 생략하겠습니다(관계별 영향을 받는 사용자 지정 사용자 피드를 자세히 살펴볼 수 있지만 이는 이 문서의 목표를 벗어남).</span><span class="sxs-lookup"><span data-stu-id="ec825-112">This doesn’t sound really complex (at first), but for the sake of simplicity, let’s stop there (we could delve into custom user feeds affected by relationships, but it exceeds the goal of this article).</span></span>

<span data-ttu-id="ec825-113">그렇다면 데이터는 어디에 어떻게 저장될까요?</span><span class="sxs-lookup"><span data-stu-id="ec825-113">So, how do we store this and where?</span></span>

<span data-ttu-id="ec825-114">여러분 대다수는 SQL 데이터베이스에 대한 경험이 있거나 적어도 [데이터의 관계형 모델링](https://en.wikipedia.org/wiki/Relational_model) 에 대한 개념을 알고 있을 것이므로 다음과 같은 다이어그램을 그리기 시작할 수 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-114">Many of you might have experience on SQL databases or at least have notion of [relational modeling of data](https://en.wikipedia.org/wiki/Relational_model) and you might be tempted to start drawing something like this:</span></span>

![상대 관계형 모델을 보여 주는 다이어그램](./media/social-media-apps/social-media-apps-sql.png) 

<span data-ttu-id="ec825-116">완전히 정규화되고 세련된 데이터 구조는...</span><span class="sxs-lookup"><span data-stu-id="ec825-116">A perfectly normalized and pretty data structure…</span></span> <span data-ttu-id="ec825-117">확장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-117">that doesn't scale.</span></span> 

<span data-ttu-id="ec825-118">저에 대해 오해하지 마세요. 저는 SQL 데이터베이스를 평생 사용해 왔으며, SQL 데이터베이스는 정말 대단하지만 모든 패턴, 방식 및 소프트웨어 플랫폼과 마찬가지로 모든 시나리오에 완벽한 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-118">Don’t get me wrong, I’ve worked with SQL databases all my life, they are great, but like every pattern, practice and software platform, it’s not perfect for every scenario.</span></span>

<span data-ttu-id="ec825-119">이 시나리오에서 SQL이 최선의 선택이 아닌 이유는 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="ec825-119">Why isn't SQL the best choice in this scenario?</span></span> <span data-ttu-id="ec825-120">단일 게시물의 구조를 살펴봅시다. 웹사이트나 응용 프로그램에 이 게시물을 나타내려면 테이블 조인</span><span class="sxs-lookup"><span data-stu-id="ec825-120">Let’s look at the structure of a single post, if I wanted to show that post in a website or application, I’d have to do a query with…</span></span> <span data-ttu-id="ec825-121">8개(!)로 쿼리를 수행해야 합니다. 단지 게시물 하나를 나타내기 위해서 말입니다. 이제 동적으로 로드되어 화면에 나타나는 게시물 스트림을 그려보면 어디를 향하고 있는지 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-121">8 table joins (!) just to show one single post, now, picture a stream of posts that dynamically load and appear on the screen and you might see where I am going.</span></span>

<span data-ttu-id="ec825-122">물론 이 많은 조인으로 수천 개의 쿼리를 해결할 정도의 방대한 SQL 인스턴스를 사용하여 콘텐츠를 제공할 수 있지만 보다 간단한 솔루션이 있는 데 그래야 하는 이유가 있을까요?</span><span class="sxs-lookup"><span data-stu-id="ec825-122">We could, of course, use a humongous SQL instance with enough power to solve thousands of queries with these many joins to serve our content, but truly, why would we when a simpler solution exists?</span></span>

## <a name="the-nosql-road"></a><span data-ttu-id="ec825-123">NoSQL</span><span class="sxs-lookup"><span data-stu-id="ec825-123">The NoSQL road</span></span>
<span data-ttu-id="ec825-124">이 문서에서는 Azure의 NoSQL 데이터베이스 [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)를 사용하여 비용 효율적인 방법으로 소셜 플랫폼의 데이터를 모델링하고 [Gremlin Graph API](../cosmos-db/graph-introduction.md) 같은 다른 Azure Cosmos DB 기능을 활용하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-124">This article will guide you into modeling your social platform's data with Azure's NoSQL database [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) in a cost-effective way while leveraging other Azure Cosmos DB features like the  [Gremlin Graph API](../cosmos-db/graph-introduction.md).</span></span> <span data-ttu-id="ec825-125">[NoSQL](https://en.wikipedia.org/wiki/NoSQL) 접근 방식을 사용하여 데이터를 JSON 형식으로 저장하고 [역정규화](https://en.wikipedia.org/wiki/Denormalization)를 적용하면 이전의 복잡한 게시물을 단일 [문서](https://en.wikipedia.org/wiki/Document-oriented_database)로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-125">Using a [NoSQL](https://en.wikipedia.org/wiki/NoSQL) approach, storing data in JSON format and applying [denormalization](https://en.wikipedia.org/wiki/Denormalization), our previously complicated post can be transformed into a single [Document](https://en.wikipedia.org/wiki/Document-oriented_database):</span></span>


    {
        "id":"ew12-res2-234e-544f",
        "title":"post title",
        "date":"2016-01-01",
        "body":"this is an awesome post stored on NoSQL",
        "createdBy":User,
        "images":["http://myfirstimage.png","http://mysecondimage.png"],
        "videos":[
            {"url":"http://myfirstvideo.mp4", "title":"The first video"},
            {"url":"http://mysecondvideo.mp4", "title":"The second video"}
        ],
        "audios":[
            {"url":"http://myfirstaudio.mp3", "title":"The first audio"},
            {"url":"http://mysecondaudio.mp3", "title":"The second audio"}
        ]
    }

<span data-ttu-id="ec825-126">또한 조인 없이 단일 쿼리로 이를 실현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-126">And it can be obtained with a single query, and with no joins.</span></span> <span data-ttu-id="ec825-127">이는 훨씬 간단하고 저렴하며, 보다 적은 리소스로 더 나은 결과를 얻을 수 있는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-127">This is much more simple and straightforward, and, budget-wise, it requires fewer resources to achieve a better result.</span></span>

<span data-ttu-id="ec825-128">Azure Cosmos DB는 모든 속성이 자체 자동 인덱싱을 통해 인덱싱되도록 하며, 이를 [사용자 지정](indexing-policies.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-128">Azure Cosmos DB makes sure that all the properties are indexed with its automatic indexing, which can even be [customized](indexing-policies.md).</span></span> <span data-ttu-id="ec825-129">스키마 없는 접근 방식을 통해 다양한 동적 구조로 문서를 저장할 수 있으며, 향후에는 게시물과 관련된 해시 태그 또는 범주 목록을 함께 유지할 수 있을 것입니다. Cosmos DB는 추가 작업 없이 새 문서를 추가된 특성과 함께 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-129">The schema-free approach lets us store Documents with different and dynamic structures, maybe tomorrow we want posts to have a list of categories or hashtags associated with them, Cosmos DB will handle the new Documents with the added attributes with no extra work required by us.</span></span>

<span data-ttu-id="ec825-130">부모 속성을 사용하여 게시물에 대한 의견을 다른 게시물로 처리할 수 있습니다. 이는 개체 매핑을 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-130">Comments on a post can be treated as just other posts with a parent property (this simplifies our object mapping).</span></span> 

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

<span data-ttu-id="ec825-131">또한 모든 소셜 상호 작용을 별도의 개체에 카운터로 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-131">And all social interactions can be stored on a separate object as counters:</span></span>

    {
        "id":"dfe3-thf5-232s-dse4",
        "post":"ew12-res2-234e-544f",
        "comments":2,
        "likes":10,
        "points":200
    }

<span data-ttu-id="ec825-132">피드를 만들려면 주어진 연관성 순으로 게시물 id 목록을 유지할 수 있는 문서를 만들기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-132">Creating feeds is just a matter of creating documents that can hold a list of post ids with a given relevance order:</span></span>

    [
        {"relevance":9, "post":"ew12-res2-234e-544f"},
        {"relevance":8, "post":"fer7-mnb6-fgh9-2344"},
        {"relevance":7, "post":"w34r-qeg6-ref6-8565"}
    ]

<span data-ttu-id="ec825-133">만든 날짜 순으로 게시물이 정렬된 “최신” 스트림을 유지하거나, 지난 24시간 이내에 좋아요가 많이 추가된 순으로 게시물이 정렬된 “인기” 스트림을 유지할 수 있습니다. 또한 팔로워와 관심사 같은 논리에 따라 각 사용자에 대한 사용자 지정 스트림을 구현할 수도 있으며, 이는 여전히 게시물 목록으로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-133">We could have a “latest” stream with posts ordered by creation date, a “hottest” stream with those posts with more likes in the last 24 hours, we could even implement a custom stream for each user based on logic like followers and interests, and it would still be a list of posts.</span></span> <span data-ttu-id="ec825-134">이러한 목록을 빌드하는 방법이 중요하지만 읽기 성능이 그대로 유지되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-134">It’s a matter of how to build these lists, but the reading performance remains unhindered.</span></span> <span data-ttu-id="ec825-135">이러한 목록 중 하나를 가져온 후에는 여러 페이지의 게시물을 한 번에 가져오기 위해 [IN 연산자](documentdb-sql-query.md#WhereClause)를 사용하여 Cosmos DB에 대한 단일 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-135">Once we acquire one of these lists, we issue a single query to Cosmos DB using the [IN operator](documentdb-sql-query.md#WhereClause) to obtain pages of posts at a time.</span></span>

<span data-ttu-id="ec825-136">피드 스트림은 [Azure App Service](https://azure.microsoft.com/services/app-service/)의 백그라운드 프로세스인 [Webjobs](../app-service-web/web-sites-create-web-jobs.md)를 사용하여 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-136">The feed streams could be built using [Azure App Services’](https://azure.microsoft.com/services/app-service/) background processes: [Webjobs](../app-service-web/web-sites-create-web-jobs.md).</span></span> <span data-ttu-id="ec825-137">게시물을 만든 후 [Azure Webjobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md)를 통해 트리거되고 고유한 사용자 지정 논리를 기반으로 스트림 내에 게시물 전파를 구현하는 [Azure Storage](https://azure.microsoft.com/services/storage/), [큐](../storage/queues/storage-dotnet-how-to-use-queues.md) 및 Webjobs를 사용하여 백그라운드 처리를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-137">Once a post is created, background processing can be triggered by using [Azure Storage](https://azure.microsoft.com/services/storage/) [Queues](../storage/queues/storage-dotnet-how-to-use-queues.md) and Webjobs triggered using the [Azure Webjobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md), implementing the post propagation inside streams based on our own custom logic.</span></span> 

<span data-ttu-id="ec825-138">이 동일한 기술을 사용하여 궁극적으로 일관된 환경을 만들어 게시물에 대한 평점 및 좋아요를 지연된 방식으로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-138">Points and likes over a post can be processed in a deferred manner using this same technique to create an eventually consistent environment.</span></span>

<span data-ttu-id="ec825-139">팔로워는 더 복잡합니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-139">Followers are trickier.</span></span> <span data-ttu-id="ec825-140">Cosmos DB에는 최대 문서 크기 제한이 있으며 크기가 큰 문서의 읽기/쓰기는 응용 프로그램의 확장성에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-140">Cosmos DB has a maximum document size limit, and reading/writing large documents can impact the scalability of your application.</span></span> <span data-ttu-id="ec825-141">다음 구조를 사용하여 팔로워를 저장하는 방법을 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-141">So you may think about storing followers as a document with this structure:</span></span>

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

<span data-ttu-id="ec825-142">이 방식은 수천 명의 팔로워를 지닌 사용자에게 적합하지만 일부 유명인이 랭크에 조인하면 결국 이 접근 방식은 큰 문서에 도달해 문서 크기 용량이 부족하게 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-142">This might work for a user with a few thousands followers, but if some celebrity joins our ranks, this approach will lead to a large document size, and might eventually hit the document size cap.</span></span>

<span data-ttu-id="ec825-143">이 문제를 해결하기 위해 혼합된 접근 방식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-143">To solve this, we can use a mixed approach.</span></span> <span data-ttu-id="ec825-144">사용자 통계 문서의 일부로 팔로워의 수를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-144">As part of the User Statistics document we can store the number of followers:</span></span>

    {
        "id":"234d-sd23-rrf2-552d",
        "user": "dse4-qwe2-ert4-aad2",
        "followers":55230,
        "totalPosts":452,
        "totalPoints":11342
    }

<span data-ttu-id="ec825-145">Azure Cosmos DB [Gremlin Graph API](../cosmos-db/graph-introduction.md)를 사용하여 팔로워의 실제 그래프를 저장하고, 각 사용자에 대한 [꼭짓점](http://mathworld.wolfram.com/GraphVertex.html)을 만들고, "A가 B를 팔로우" 관계를 유지하는 [가장자리](http://mathworld.wolfram.com/GraphEdge.html)를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-145">And the actual graph of followers can be stored using Azure Cosmos DB [Gremlin Graph API](../cosmos-db/graph-introduction.md), to create [vertexes](http://mathworld.wolfram.com/GraphVertex.html) for each user and [edges](http://mathworld.wolfram.com/GraphEdge.html) that maintain the "A-follows-B" relationships.</span></span> <span data-ttu-id="ec825-146">Graph API를 사용하여 특정 사용자의 팔로워를 가져올 수 있을 뿐 아니라 공통점이 있는 사람들을 제안하는 좀 더 복잡한 쿼리도 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-146">The Graph API let's you not only obtain the followers of a certain user but create more complex queries to even suggest people in common.</span></span> <span data-ttu-id="ec825-147">그래프에 사람들이 좋아하는 콘텐츠 범주를 추가하면 스마트 콘텐츠 검색이 포함된 환경을 만들어서 우리가 팔로우 또는 좋아하는 콘텐츠를 제안하거나 공통점이 많을 것 같은 사람을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-147">If we add to the graph the Content Categories that people like or enjoy, we can start weaving experiences that include smart content discovery, suggesting content that those we follow like, or finding people with whom we might have much in common.</span></span>

<span data-ttu-id="ec825-148">사용자 통계 문서는 여전히 UI 또는 빠른 프로필 미리 보기에서 카드를 만드는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-148">The User Statistics document can still be used to create cards in the UI or quick profile previews.</span></span>

## <a name="the-ladder-pattern-and-data-duplication"></a><span data-ttu-id="ec825-149">"사다리" 패턴 및 데이터 중복</span><span class="sxs-lookup"><span data-stu-id="ec825-149">The “Ladder” pattern and data duplication</span></span>
<span data-ttu-id="ec825-150">게시물을 참조하는 JSON 문서에서 볼 수 있듯이 하나의 사용자가 여러 번 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-150">As you might have noticed in the JSON document that references a post, there are multiple occurrences of a user.</span></span> <span data-ttu-id="ec825-151">이는 이러한 역정규화가 주어진 경우 사용자를 나태는 정보가 여러 곳에 표시될 수 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-151">And you’d have guessed right, this means that the information that represents a user, given this denormalization, might be present in more than one place.</span></span>

<span data-ttu-id="ec825-152">데이터 중복이 발생하도록 둔 것은 더 빠른 쿼리를 허용하기 위해서입니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-152">In order to allow for faster queries, we incur data duplication.</span></span> <span data-ttu-id="ec825-153">그 부작용으로 인한 문제는 일부 작업으로 인해 사용자의 데이터가 변경된 경우 해당 사용자가 지금까지 수행한 모든 활동을 찾아서 모두 업데이트해야 한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-153">The problem with this side-effect is that if by some action, a user’s data changes, we need to find all the activities he ever did and update them all.</span></span> <span data-ttu-id="ec825-154">그다지 실용적으로 들리지 않죠, 그렇죠?</span><span class="sxs-lookup"><span data-stu-id="ec825-154">Doesn’t sound very practical, right?</span></span>

<span data-ttu-id="ec825-155">각 활동에 대해 응용 프로그램에 표시하는 사용자의 주요 특성을 식별하여 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-155">We are going to solve it by identifying the Key attributes of a user that we show in our application for each activity.</span></span> <span data-ttu-id="ec825-156">게시물을 응용 프로그램에 시각적으로 표시하고 만든 사람의 이름과 사진만 표시했을 뿐인데 "createdBy" 특성에 해당 사용자의 모든 데이터가 저장되는 이유는 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="ec825-156">If we visually show a post in our application and show just the creator’s name and picture, why store all of the user’s data in the “createdBy” attribute?</span></span> <span data-ttu-id="ec825-157">각 의견에 대해 사용자의 사진만 표시하면 나머지 정보는 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-157">If for each comment we just show the user’s picture, we don’t really need the rest of his information.</span></span> <span data-ttu-id="ec825-158">바로 여기에 "사다리 패턴"이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-158">That’s where something I call the “Ladder pattern” comes into play.</span></span>

<span data-ttu-id="ec825-159">다음 사용자 정보를 예로 들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-159">Let’s take user information as an example:</span></span>

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

<span data-ttu-id="ec825-160">이 정보를 보면 중요한 정보와 중요하지 않은 정보를 신속하게 감지할 수 있으므로 다음과 같은 “사다리”가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-160">By looking at this information, we can quickly detect which is critical information and which isn’t, thus creating a “Ladder”:</span></span>

![사다리 패턴의 다이어그램](./media/social-media-apps/social-media-apps-ladder.png)

<span data-ttu-id="ec825-162">가장 작은 단계는 사용자를 식별하는 정보의 최소 조각인 UserChunk로서, 데이터 중복에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-162">The smallest step is called a UserChunk, the minimal piece of information that identifies a user and it’s used for data duplication.</span></span> <span data-ttu-id="ec825-163">중복된 데이터의 크기를 “표시”할 정보로만 줄이면 대량 업데이트의 가능성이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-163">By reducing the size of the duplicated data to only the information we will “show”, we reduce the possibility of massive updates.</span></span>

<span data-ttu-id="ec825-164">중간 단계는 사용자라고 합니다. 이는 Cosmos DB에 대한 대부분의 성능 종속 쿼리에 사용되고 가장 자주 액세스되며 중요한 전체 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-164">The middle step is called the user, it’s the full data that will be used on most performance-dependent queries on Cosmos DB, the most accessed and critical.</span></span> <span data-ttu-id="ec825-165">여기에는 UserChunk가 나타내는 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-165">It includes the information represented by a UserChunk.</span></span>

<span data-ttu-id="ec825-166">가장 큰 단계는 Extended User입니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-166">The largest is the Extended User.</span></span> <span data-ttu-id="ec825-167">여기에는 중요한 모든 사용자 정보와 실제로 빠르게 읽을 필요가 없으며 마지막에 사용되는(예: 로그인 프로세스) 기타 데이터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-167">It includes all the critical user information plus other data that doesn’t really require to be read quickly or it’s usage is eventual (like the login process).</span></span> <span data-ttu-id="ec825-168">이 데이터를 Cosmos DB 외부, Azure SQL Database 또는 Azure Storage 테이블에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-168">This data can be stored outside of Cosmos DB, in Azure SQL Database or Azure Storage Tables.</span></span>

<span data-ttu-id="ec825-169">사용자를 분할하고 심지어 이 정보를 여러 곳에 저장하는 이유는 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="ec825-169">Why would we split the user and even store this information in different places?</span></span> <span data-ttu-id="ec825-170">성능 면에서 문서가 클수록 쿼리 비용이 많이 들기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-170">Because from a performance point of view, the bigger the documents, the costlier the queries.</span></span> <span data-ttu-id="ec825-171">소셜 네트워크에 대한 모든 성능 종속 쿼리를 수행하는 데 적합한 정보로 문서를 간소하게 유지하고 전체 프로필 편집, 로그인, 사용량 분석 및 빅 데이터 이니셔티브를 위한 데이터 마이닝 등 최종적인 시나리오에 대한 기타 추가 정보를 저장하세요.</span><span class="sxs-lookup"><span data-stu-id="ec825-171">Keep documents slim, with the right information to do all your performance-dependent queries for your social network, and store the other extra information for eventual scenarios like, full profile edits, logins, even data mining for usage analytics and Big Data initiatives.</span></span> <span data-ttu-id="ec825-172">사용자 환경이 빠르고 간소하게 유지된다면 데이터 마이닝을 위한 데이터 수집이 Azure SQL 데이터베이스에서 실행되기 때문에 느려지는 것은 중요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-172">We really don’t care if the data gathering for data mining is slower because it’s running on Azure SQL Database, we do have concern though that our users have a fast and slim experience.</span></span> <span data-ttu-id="ec825-173">Cosmos DB에 저장된 사용자는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-173">A user, stored on Cosmos DB, would look like this:</span></span>

    {
        "id":"dse4-qwe2-ert4-aad2",
        "name":"John",
        "surname":"Doe",
        "username":"johndoe"
        "email":"john@doe.com",
        "twitterHandle":"@john"
    }

<span data-ttu-id="ec825-174">그리고 게시물은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-174">And a Post would look like:</span></span>

    {
        "id":"1234-asd3-54ts-199a",
        "title":"Awesome post!",
        "date":"2016-01-02",
        "createdBy":{
            "id":"dse4-qwe2-ert4-aad2",
            "username":"johndoe"
        }
    }

<span data-ttu-id="ec825-175">청크의 특성 중 하나가 영향을 받는 곳에서 편집 작업이 수행된 경우 인덱싱된 특성(SELECT * FROM posts p WHERE p.createdBy.id == “edited_user_id”)을 가리키는 쿼리를 사용한 후 청크를 업데이트하여 영향을 받는 문서를 쉽게 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-175">And when an edit arises where one of the attributes of the chunk is affected, it’s easy to find the affected documents by using queries that point to the indexed attributes (SELECT * FROM posts p WHERE p.createdBy.id == “edited_user_id”) and then updating the chunks.</span></span>

## <a name="the-search-box"></a><span data-ttu-id="ec825-176">검색 상자</span><span class="sxs-lookup"><span data-stu-id="ec825-176">The search box</span></span>
<span data-ttu-id="ec825-177">다행히 사용자는 많은 콘텐츠를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-177">Users will generate, luckily, a lot of content.</span></span> <span data-ttu-id="ec825-178">우리는 콘텐츠 스트림에 없을 수 있는 콘텐츠를 검색하고 찾을 수 있는 기능을 제공할 수 있어야 합니다. 만든 사람을 추적하지 않거나 6개월 전에 게시한 오래된 게시물을 찾으려고 할 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-178">And we should be able to provide the ability to search and find content that might not be directly in their content streams, maybe because we don’t follow the creators, or maybe we are just trying to find that old post we did 6 months ago.</span></span>

<span data-ttu-id="ec825-179">다행히 Azure Cosmos DB를 사용하기 때문에 단일 코드 줄을 입력하지 않고도 [Azure Search](https://azure.microsoft.com/services/search/)를 통해 몇 분 이내에 검색 엔진을 쉽게 구현할 수 있습니다(검색 프로세스 및 UI가 아님).</span><span class="sxs-lookup"><span data-stu-id="ec825-179">Thankfully, and because we are using Azure Cosmos DB, we can easily implement a search engine using [Azure Search](https://azure.microsoft.com/services/search/) in a couple of minutes and without typing a single line of code (other than obviously, the search process and UI).</span></span>

<span data-ttu-id="ec825-180">이 작업이 이렇게 쉬운 이유는 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="ec825-180">Why is this so easy?</span></span>

<span data-ttu-id="ec825-181">Azure Search는 데이터 리포지토리에 후크되는 백그라운드 프로세스인 [인덱서](https://msdn.microsoft.com/library/azure/dn946891.aspx)를 호출하여 인덱스에서 개체를 자동으로 추가, 업데이트 또는 제거하는 기능을 구현하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-181">Azure Search implements what they call [Indexers](https://msdn.microsoft.com/library/azure/dn946891.aspx), background processes that hook in your data repositories and automagically add, update or remove your objects in the indexes.</span></span> <span data-ttu-id="ec825-182">Azure Search는 [Azure SQL Database 인덱서](https://blogs.msdn.microsoft.com/kaevans/2015/03/06/indexing-azure-sql-database-with-azure-search/), [Azure Blob 인덱서](../search/search-howto-indexing-azure-blob-storage.md) 그리고 다행히도 [Azure Cosmos DB 인덱서](../search/search-howto-index-documentdb.md)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-182">They support an [Azure SQL Database indexers](https://blogs.msdn.microsoft.com/kaevans/2015/03/06/indexing-azure-sql-database-with-azure-search/), [Azure Blobs indexers](../search/search-howto-indexing-azure-blob-storage.md) and thankfully, [Azure Cosmos DB indexers](../search/search-howto-index-documentdb.md).</span></span> <span data-ttu-id="ec825-183">Cosmos DB에서 Azure Search로 정보를 전환하는 것은 간단합니다. 둘 다 정보를 JSON 형식으로 저장하기 때문에 [인덱스를 만들고](../search/search-create-index-portal.md) 문서에서 인덱싱할 특성을 매핑하기만 하면 됩니다. 그러면 몇 분(데이터 크기에 따라 다름) 이내에 클라우드 인프라에서 제공되는 최고의 SaaS(Search-as-a-Service) 솔루션을 통해 모든 콘텐츠를 검색할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-183">The transition of information from Cosmos DB to Azure Search is straightforward, as both store information in JSON format, we just need to [create our Index](../search/search-create-index-portal.md) and map which attributes from our Documents we want indexed and that’s it, in a matter of minutes (depends on the size of our data), all our content will be available to be searched upon, by the best Search-as-a-Service solution in cloud infrastructure.</span></span> 

<span data-ttu-id="ec825-184">Azure 검색에 대한 자세한 내용은 [Hitchhiker의 검색 가이드](https://blogs.msdn.microsoft.com/mvpawardprogram/2016/02/02/a-hitchhikers-guide-to-search/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec825-184">For more information about Azure Search, you can visit the [Hitchhiker’s Guide to Search](https://blogs.msdn.microsoft.com/mvpawardprogram/2016/02/02/a-hitchhikers-guide-to-search/).</span></span>

## <a name="the-underlying-knowledge"></a><span data-ttu-id="ec825-185">기본 지식</span><span class="sxs-lookup"><span data-stu-id="ec825-185">The underlying knowledge</span></span>
<span data-ttu-id="ec825-186">매일 증가하는 이 모든 콘텐츠를 저장한 후에는 이 모든 사용자 정보 스트림으로 수행할 수 있는 작업이 무엇인지 궁금할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-186">After storing all this content that grows and grows every day, we might find ourselves thinking: What can I do with all this stream of information from my users?</span></span>

<span data-ttu-id="ec825-187">대답은 간단합니다. 사용할 수 있도록 구성한 후 학습하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-187">The answer is straightforward: Put it to work and learn from it.</span></span>

<span data-ttu-id="ec825-188">그렇다면 무엇을 배울 수 있을까요?</span><span class="sxs-lookup"><span data-stu-id="ec825-188">But, what can we learn?</span></span> <span data-ttu-id="ec825-189">몇 가지 쉬운 예를 들면 [정서 분석](https://en.wikipedia.org/wiki/Sentiment_analysis), 사용자의 선호도에 따른 콘텐츠 추천 또는 소셜 네트워크에서 게시된 모든 콘텐츠가 가족에게 안전하도록 보장하는 자동화된 콘텐츠 중재자 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-189">A few easy examples include [sentiment analysis](https://en.wikipedia.org/wiki/Sentiment_analysis), content recommendations based on a user’s preferences or even an automated content moderator that ensures that all the content published by our social network is safe for the family.</span></span>

<span data-ttu-id="ec825-190">이제 간단한 데이터베이스 및 파일에서 이러한 패턴과 정보를 추출하려면 수학 박사가 필요하다고 생각하겠지만 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-190">Now that I got you hooked, you’ll probably think you need some PhD in math science to extract these patterns and information out of simple databases and files, but you’d be wrong.</span></span>

<span data-ttu-id="ec825-191">[Cortana Intelligence 제품군](https://www.microsoft.com/en/server-cloud/cortana-analytics-suite/overview.aspx)의 일부인 [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/)은 완전히 관리되는 클라우드 서비스로서, 간단한 끌어서 놓기 인터페이스에서 알고리즘을 사용하여 워크플로를 만들거나, [R](https://en.wikipedia.org/wiki/R_\(programming_language\))에서 사용자 고유의 알고리즘을 코딩하거나, 이미 빌드되고 즉시 사용 가능한 API(예: [텍스트 분석](https://gallery.cortanaanalytics.com/MachineLearningAPI/Text-Analytics-2), [Content Moderator](https://www.microsoft.com/moderator) 또는 [추천](https://gallery.cortanaanalytics.com/MachineLearningAPI/Recommendations-2))를 사용할 수 있도록 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-191">[Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/), part of the [Cortana Intelligence Suite](https://www.microsoft.com/en/server-cloud/cortana-analytics-suite/overview.aspx), is the a fully managed cloud service that lets you create workflows using algorithms in a simple drag-and-drop interface, code your own algorithms in [R](https://en.wikipedia.org/wiki/R_\(programming_language\)) or use some of the already-built and ready to use APIs such as: [Text Analytics](https://gallery.cortanaanalytics.com/MachineLearningAPI/Text-Analytics-2),  [Content Moderator](https://www.microsoft.com/moderator) or [Recommendations](https://gallery.cortanaanalytics.com/MachineLearningAPI/Recommendations-2).</span></span>

<span data-ttu-id="ec825-192">이러한 Machine Learning 시나리오를 달성하려면 [Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/)를 사용하여 다양 한 원본에서 정보를 수집하고 [U-SQL](https://azure.microsoft.com/documentation/videos/data-lake-u-sql-query-execution/)을 사용하여 정보를 처리하고 Azure Machine Learning에서 처리할 수 있는 출력을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-192">To achieve any of these Machine Learning scenarios, we can use [Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/) to ingest the information from different sources, and use [U-SQL](https://azure.microsoft.com/documentation/videos/data-lake-u-sql-query-execution/) to process the information and generate an output that can be processed by Azure Machine Learning.</span></span>

<span data-ttu-id="ec825-193">또 다른 사용 가능한 옵션은 [Microsoft Cognitive Services](https://www.microsoft.com/cognitive-services)를 사용하여 사용자의 콘텐츠를 분석하는 것입니다. 이를 통해 보다 잘 이해할 수 있을 뿐만 아니라([Text Analytics API](https://www.microsoft.com/cognitive-services/en-us/text-analytics-api)로 작성한 것을 분석하여) 원치 않거나 성숙한 콘텐츠를 검색하고 [Computer Vision API](https://www.microsoft.com/cognitive-services/en-us/computer-vision-api)를 사용하여 그에 따라 동작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-193">Another available option is to use [Microsoft Cognitive Services](https://www.microsoft.com/cognitive-services) to analyze our users content; not only can we understand them better (through analyzing what they write with [Text Analytics API](https://www.microsoft.com/cognitive-services/en-us/text-analytics-api)) , but we could also detect unwanted or mature content and act accordingly with [Computer Vision API](https://www.microsoft.com/cognitive-services/en-us/computer-vision-api).</span></span> <span data-ttu-id="ec825-194">Cognitive Services는 사용하기 위해 Machine Learning의 지식이 필요하지 않은 많은 기본 제공 솔루션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-194">Cognitive Services include a lot of out-of-the-box solutions that don't require any kind of Machine Learning knowledge to use.</span></span>

## <a name="a-planet-scale-social-experience"></a><span data-ttu-id="ec825-195">전 세계적인 규모의 소셜 환경</span><span class="sxs-lookup"><span data-stu-id="ec825-195">A planet-scale social experience</span></span>
<span data-ttu-id="ec825-196">마지막으로 해결해야 하는 중요한 사항은 **확장성**입니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-196">There is a last, but not least, important topic I must address: **scalability**.</span></span> <span data-ttu-id="ec825-197">아키텍처를 디자인하는 경우 더 많은 데이터를 처리해야 하거나 더 큰 지역 적용 범위가 필요하기 때문에(또는 두 가지 이유 모두로 인해) 각 구성 요소를 자체적으로 확장할 수 하는지가 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-197">When designing an architecture it's crucial that each component can scale on its own, either because we need to process more data or because we want to have a bigger geographical coverage (or both!).</span></span> <span data-ttu-id="ec825-198">다행스럽게도 Cosmos DB를 사용하여 **턴키 환경**에서 이러한 복잡한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-198">Thankfully, achieving such a complex task is a **turnkey experience** with Cosmos DB.</span></span>

<span data-ttu-id="ec825-199">Cosmos DB는 지정된 **파티션 키**(문서의 특성 중 하나로 정의됨)를 기반으로 해서 파티션을 자동으로 만들어 기본적으로 [동적 분할](https://azure.microsoft.com/blog/10-things-to-know-about-documentdb-partitioned-collections/)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-199">Cosmos DB supports [dynamic partitioning](https://azure.microsoft.com/blog/10-things-to-know-about-documentdb-partitioned-collections/) out-of-the-box by automatically creating partitions based on a given **partition key** (defined as one of the attributes in your documents).</span></span> <span data-ttu-id="ec825-200">디자인 과정에서 올바른 파티션 키를 정의해야 합니다. 또한 [모범 사례](../cosmos-db/partition-data.md#designing-for-partitioning) 사용할 수 있다는 점을 기억하세요. 소셜 환경의 경우에 쿼리(동일한 파티션 내의 읽기는 바람직함) 및 작성(여러 파티션에 쓰기를 분산하여 "핫 스폿" 방지)하는 방법으로 분할 전략을 정렬해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-200">Defining the correct partition key must be done at design time and keeping in mind the [best practices](../cosmos-db/partition-data.md#designing-for-partitioning) available; in the case of a social experience, your partitioning strategy must be aligned with the way you query (reads within the same partition are desirable) and write (avoid "hot spots" by spreading writes on multiple partitions).</span></span> <span data-ttu-id="ec825-201">일부 옵션은 다음과 같습니다. 콘텐츠 범주별, 지리적 지역별, 사용자별 임시 키(일/월/주)에 기반한 파티션은 데이터를 쿼리하는 방법에 따라 다르고 소셜 환경에서 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-201">Some options are: partitions based on a temporal key (day/month/week), by content category, by geographical region, by user; it all really depends on how you will query the data and show it in your social experience.</span></span> 

<span data-ttu-id="ec825-202">한 가지 흥미로운 점은 Cosmos DB가 모든 파티션에 투명하게 쿼리([집계](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/) 포함)를 실행한다는 것입니다. 데이터의 증가에 따라 논리를 추가할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-202">One interesting point worth mentioning is that Cosmos DB will run your queries (including [aggregates](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/)) across all your partitions transparently, you don't need to add any logic as your data grows.</span></span>

<span data-ttu-id="ec825-203">시간이 지나면 결국 트래픽이 증가하고 리소스 사용([RU](request-units.md) 또는 요청 단위)도 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-203">With time, you will eventually grow in traffic and your resource consumption (measured in [RUs](request-units.md), or Request Units) will increase.</span></span> <span data-ttu-id="ec825-204">userbase가 증가하면 더 자주 읽고 쓰게 되고 더 많은 콘텐츠를 만들고 읽기 시작합니다. **처리량 크기 조정** 기능이 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-204">You will read and write more frequently as your userbase grows and they will start creating and reading more content; the ability of **scaling your throughput** is vital.</span></span> <span data-ttu-id="ec825-205">RU를 증가시키는 것은 매우 쉽습니다. Azure Portal에서 몇 번 클릭하거나 [API를 통해 명령을 실행](https://docs.microsoft.com/rest/api/documentdb/replace-an-offer)하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-205">Increasing our RUs is very easy, we can do it with a few clicks on the Azure Portal or by [issuing commands through the API](https://docs.microsoft.com/rest/api/documentdb/replace-an-offer).</span></span>

![파티션 키 확장 및 정의](./media/social-media-apps/social-media-apps-scaling.png)

<span data-ttu-id="ec825-207">기능이 점점 확장되고 다른 지역, 국가 또는 대륙의 사용자가 당신의 플랫폼을 알고 사용하기 시작한다면 놀라운 일이 벌어집니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-207">What happens if things keep getting better and users from another region, country or continent, notice your platform and start using it, what a great surprise!</span></span>

<span data-ttu-id="ec825-208">하지만 플랫폼에서 해당 환경이 최적화되지 않음을 알게 됩니다. 당신의 운영 지역에서 멀리 떨어져 있으므로 대기 시간이 엄청나지만 포기할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-208">But wait... you soon realize their experience with your platform is not optimal; they are so far away from your operational region that the latency is terrible, and you obviously don't want them to quit.</span></span> <span data-ttu-id="ec825-209">**글로벌 도달률을 확장**하는 쉬운 방법이 있다면 얼마나 좋을까요. 방법이 있습니다!</span><span class="sxs-lookup"><span data-stu-id="ec825-209">If only there was an easy way of **extending your global reach**... but there is!</span></span>

<span data-ttu-id="ec825-210">Cosmos DB를 사용하면 몇 번의 클릭으로 투명하게 [데이터를 전역으로 복제](../cosmos-db/tutorial-global-distribution-documentdb.md)하고 [클라이언트 코드](../cosmos-db/tutorial-global-distribution-documentdb.md)에서 사용 가능한 지역 중 하나를 자동으로 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-210">Cosmos DB lets you [replicate your data globally](../cosmos-db/tutorial-global-distribution-documentdb.md) and transparently with a couple of clicks and automatically select among the available regions from your [client code](../cosmos-db/tutorial-global-distribution-documentdb.md).</span></span> <span data-ttu-id="ec825-211">즉, [여러 장애 조치 지역](regional-failover.md)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-211">This also means that you can have [multiple failover regions](regional-failover.md).</span></span> 

<span data-ttu-id="ec825-212">전역적으로 데이터를 복제하는 경우 클라이언트에서 활용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-212">When you replicate your data globally, you need to make sure that your clients can take advantage of it.</span></span> <span data-ttu-id="ec825-213">웹 프런트 엔드를 사용하거나 모바일 클라이언트의 API에 액세스하는 경우 확장된 글로벌 범위를 지원하는 [성능 구성](../app-service-web/web-sites-traffic-manager.md)을 사용하여 [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/)를 배포하고 원하는 모든 지역에서 Azure App Service를 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-213">If you are using a web frontend or accesing APIs from mobile clients, you can deploy [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) and clone your Azure App Service on all the desired regions, using a [Performance configuration](../app-service-web/web-sites-traffic-manager.md) to support your extended global coverage.</span></span> <span data-ttu-id="ec825-214">클라이언트가 프런트 엔드 또는 API에 액세스하는 경우 가장 가까운 App Service에 라우팅되고 따라서 로컬 Cosmos DB 복제본에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-214">When your clients access your frontend or APIs, they will be routed to the closest App Service, which in turn, will connect to the local Cosmos DB replica.</span></span>

![소셜 플랫폼에 전역적 적용 범위 추가](./media/social-media-apps/social-media-apps-global-replicate.png)

## <a name="conclusion"></a><span data-ttu-id="ec825-216">결론</span><span class="sxs-lookup"><span data-stu-id="ec825-216">Conclusion</span></span>
<span data-ttu-id="ec825-217">이 문서에서는 완전히 Azure에서 저렴한 서비스를 사용하여 소셜 네트워크를 만들고, 다중 계층 저장소 솔루션 및 “사다리”라는 데이터 분산을 사용하도록 권장하여 뛰어난 결과를 제공하는 대안에 대해 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-217">This article tries to shed some light into the alternatives of creating social networks completely on Azure with low-cost services and providing great results by encouraging the use of a multi-layered storage solution and data distribution called “Ladder”.</span></span>

![소셜 네트워킹에 대한 Azure 서비스 간 상호 작용의 다이어그램](./media/social-media-apps/social-media-apps-azure-solution.png)

<span data-ttu-id="ec825-219">이러한 종류의 시나리오에 대한 묘책은 없습니다. 이는 뛰어난 환경을 빌드할 수 있도록 해주는 유용한 서비스의 조합으로 생성되는 시너지입니다. 예를 들어 뛰어난 소셜 응용 프로그램을 제공하는 Azure Cosmos DB의 속도와 자유로움, Azure Search와 같은 최고 수준의 검색 솔루션에 숨은 인텔리전스, 언어에 관계없는 응용 프로그램뿐 아니라 강력한 백그라운드 프로세스를 호스트하는 Azure App Services의 유연성, 방대한 양의 데이터를 저장하기 위한 확장 가능한 Azure Storage 및 Azure SQL Database, 프로세스에 대한 피드백을 제공할 수 있는 지식과 인텔리전스를 만들고 올바른 사용자에게 올바른 콘텐츠를 제공하도록 도와주는 Azure Machine Learning의 분석 기능 등이 조합된 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="ec825-219">The truth is that there is no silver bullet for this kind of scenarios, it’s the synergy created by the combination of great services that allow us to build great experiences: the speed and freedom of Azure Cosmos DB to provide a great social application, the intelligence behind a first-class search solution like Azure Search, the flexibility of Azure App Services to host not even language-agnostic applications but powerful background processes and the expandable Azure Storage and Azure SQL Database for storing massive amounts of data and the analytic power of Azure Machine Learning to create knowledge and intelligence that can provide feedback to our processes and help us deliver the right content to the right users.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec825-220">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ec825-220">Next steps</span></span>
<span data-ttu-id="ec825-221">Cosmos DB의 사용 사례에 대한 자세한 내용은 [일반적인 Cosmos DB 사용 사례](use-cases.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec825-221">To learn more about use cases for Cosmos DB, see [Common Cosmos DB use cases](use-cases.md).</span></span>