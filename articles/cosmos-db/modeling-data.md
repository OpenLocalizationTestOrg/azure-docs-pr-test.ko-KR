---
title: "NoSQL 데이터베이스의 문서 데이터 모델링 | Microsoft Docs"
description: "NoSQL 데이터베이스의 데이터 모델링에 대해 알아봅니다."
keywords: "데이터 모델링"
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig1
documentationcenter: 
ms.assetid: 69521eb9-590b-403c-9b36-98253a4c88b5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2016
ms.author: arramac
ms.openlocfilehash: 16c387fe574243544cf54cf283c7713ddcaa1942
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="modeling-document-data-for-nosql-databases"></a><span data-ttu-id="446e8-104">NoSQL 데이터베이스의 문서 데이터 모델링</span><span class="sxs-lookup"><span data-stu-id="446e8-104">Modeling document data for NoSQL databases</span></span>
<span data-ttu-id="446e8-105">Azure Cosmos DB와 같은 스키마가 없는 데이터베이스에서는 데이터 모델을 매우 쉽게 변경할 수 있지만, 데이터를 고려할 어느 정도의 시간이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-105">While schema-free databases, like Azure Cosmos DB, make it super easy to embrace changes to your data model you should still spend some time thinking about your data.</span></span> 

<span data-ttu-id="446e8-106">데이터를 어떻게 저장할 것인가?</span><span class="sxs-lookup"><span data-stu-id="446e8-106">How is data going to be stored?</span></span> <span data-ttu-id="446e8-107">응용 프로그램에서 데이터를 검색 및 쿼리하는 방법은 무엇인가?</span><span class="sxs-lookup"><span data-stu-id="446e8-107">How is your application going to retrieve and query data?</span></span> <span data-ttu-id="446e8-108">응용 프로그램 부하가 읽기 또는 쓰기 중 어디에 집중되어 있는가?</span><span class="sxs-lookup"><span data-stu-id="446e8-108">Is your application read heavy, or write heavy?</span></span> 

<span data-ttu-id="446e8-109">이 문서를 읽은 다음에는 다음과 같은 질문에 답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-109">After reading this article, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="446e8-110">문서 데이터베이스에서 문서는 무엇인가?</span><span class="sxs-lookup"><span data-stu-id="446e8-110">How should I think about a document in a document database?</span></span>
* <span data-ttu-id="446e8-111">데이터 모델링은 무엇이고 어떻게 사용해야 하는가?</span><span class="sxs-lookup"><span data-stu-id="446e8-111">What is data modeling and why should I care?</span></span> 
* <span data-ttu-id="446e8-112">관계형 데이터베이스와 다른 문서 데이터베이스에서 데이터는 어떻게 모델링되는가?</span><span class="sxs-lookup"><span data-stu-id="446e8-112">How is modeling data in a document database different to a relational database?</span></span>
* <span data-ttu-id="446e8-113">비관계형 데이터베이스에서 데이터 관계는 어떻게 표현하는가?</span><span class="sxs-lookup"><span data-stu-id="446e8-113">How do I express data relationships in a non-relational database?</span></span>
* <span data-ttu-id="446e8-114">데이터를 포함해야 하는 경우 및 데이터에 링크하는 경우는 언제인가?</span><span class="sxs-lookup"><span data-stu-id="446e8-114">When do I embed data and when do I link to data?</span></span>

## <a name="embedding-data"></a><span data-ttu-id="446e8-115">데이터 포함</span><span class="sxs-lookup"><span data-stu-id="446e8-115">Embedding data</span></span>
<span data-ttu-id="446e8-116">Azure Cosmos DB와 같은 문서 저장소에서 데이터 모델링을 시작하는 경우 엔터티를 JSON으로 표현된 **자체 포함 문서**로 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-116">When you start modeling data in a document store, such as Azure Cosmos DB, try to treat your entities as **self-contained documents** represented in JSON.</span></span>

<span data-ttu-id="446e8-117">자세한 설명을 시작하기 전에 먼저 이전 단계로 돌아가서 관계형 데이터베이스에서 모델링을 수행하는 방법에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-117">Before we dive in too much further, let us take a few steps back and have a look at how we might model something in a relational database, a subject many of us are already familiar with.</span></span> <span data-ttu-id="446e8-118">다음 예제에서는 관계형 데이터베이스에서 사용자가 저장되는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-118">The following example shows how a person might be stored in a relational database.</span></span> 

![관계형 데이터베이스 모델](./media/documentdb-modeling-data/relational-data-model.png)

<span data-ttu-id="446e8-120">관계형 데이터베이스를 사용할 때 우리는 정규화가 중요하다고 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-120">When working with relational databases, we've been taught for years to normalize, normalize, normalize.</span></span>

<span data-ttu-id="446e8-121">데이터 정규화를 위해서는 일반적으로 사용자와 같은 엔터티를 만들고 이를 개별적인 데이터 조각으로 세분화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-121">Normalizing your data typically involves taking an entity, such as a person, and breaking it down in to discrete pieces of data.</span></span> <span data-ttu-id="446e8-122">위 예제에서 사용자는 여러 주소 레코드뿐만 아니라 여러 개의 연락처 세부 레코드를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-122">In the example above, a person can have multiple contact detail records as well as multiple address records.</span></span> <span data-ttu-id="446e8-123">여기에서는 한 단계 더 나가서 유형과 같은 공통 필드를 추출하여 연락처 세부 정보를 보다 세분화합니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-123">We even go one step further and break down contact details by further extracting common fields like a type.</span></span> <span data-ttu-id="446e8-124">주소와 마찬가지로 각 레코드에는 *홈* 또는 *비즈니스*와 같은 유형에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-124">Same for address, each record here has a type like *Home* or *Business*</span></span> 

<span data-ttu-id="446e8-125">데이터를 정규화할 때의 원칙은 각 레코드에서 **중복된 데이터 저장을 피하고** 데이터를 참조하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-125">The guiding premise when normalizing data is to **avoid storing redundant data** on each record and rather refer to data.</span></span> <span data-ttu-id="446e8-126">이 예제에서 모든 연락처 세부 정보 및 주소를 사용해서 사용자를 읽으려면 JOINS를 사용해서 데이터를 런타임에 효율적으로 집계해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-126">In this example, to read a person, with all their contact details and addresses, you need to use JOINS to effectively aggregate your data at run time.</span></span>

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

<span data-ttu-id="446e8-127">연락처 세부 정보 및 주소를 사용해서 단일 사용자를 업데이트하려면 여러 개별 테이블 간의 쓰기 작업이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-127">Updating a single person with their contact details and addresses requires write operations across many individual tables.</span></span> 

<span data-ttu-id="446e8-128">이제는 문서 데이터베이스에서 자체 포함된 엔터티와 동일한 데이터를 모델링하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-128">Now let's take a look at how we would model the same data as a self-contained entity in a document database.</span></span>

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "addresses": [
            {            
                "line1": "100 Some Street",
                "line2": "Unit 1",
                "city": "Seattle",
                "state": "WA",
                "zip": 98012
            }
        ],
        "contactDetails": [
            {"email: "thomas@andersen.com"},
            {"phone": "+1 555 555-5555", "extension": 5555}
        ] 
    }

<span data-ttu-id="446e8-129">위 방법을 사용해서 우리는 연락처 세부 정보 및 주소와 같은 이 사용자와 관련된 모든 정보를 단일 JSON 문서에 **포함시킨** 사용자 레코드를 **비정규화**했습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-129">Using the approach above we have now **denormalized** the person record where we **embedded** all the information relating to this person, such as their contact details and addresses, in to a single JSON document.</span></span>
<span data-ttu-id="446e8-130">또한 고정된 스키마로 제한되지 않기 때문에 다른 도형의 연락처 세부 정보를 완전히 포함하는 것과 같은 유연성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-130">In addition, because we're not confined to a fixed schema we have the flexibility to do things like having contact details of different shapes entirely.</span></span> 

<span data-ttu-id="446e8-131">데이터베이스에서 전체 사용자 레코드를 검색하는 작업은 이제는 단일 컬렉션에 대해 그리고 단일 문서에 대해 단일 읽기 작업을 수행하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-131">Retrieving a complete person record from the database is now a single read operation against a single collection and for a single document.</span></span> <span data-ttu-id="446e8-132">연락처 세부 정보 및 주소로 사용자 레코드를 업데이트하는 작업도 단일 문서에 대해 단일 쓰기 작업을 수행하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-132">Updating a person record, with their contact details and addresses, is also a single write operation against a single document.</span></span>

<span data-ttu-id="446e8-133">데이터를 비정규화하면 응용 프로그램이 일반 작업 수행을 위해 실행해야 하는 쿼리 및 업데이트 수가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-133">By denormalizing data, your application may need to issue fewer queries and updates to complete common operations.</span></span> 

### <a name="when-to-embed"></a><span data-ttu-id="446e8-134">포함해야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="446e8-134">When to embed</span></span>
<span data-ttu-id="446e8-135">일반적으로 다음과 같은 경우에 포함된 데이터 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-135">In general, use embedded data models when:</span></span>

* <span data-ttu-id="446e8-136">엔터티 간에 **포함** 관계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-136">There are **contains** relationships between entities.</span></span>
* <span data-ttu-id="446e8-137">엔터티 사이에 **일 대 몇(one-to-few)** 의 관계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-137">There are **one-to-few** relationships between entities.</span></span>
* <span data-ttu-id="446e8-138">포함된 데이터가 **자주 변경**되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-138">There is embedded data that **changes infrequently**.</span></span>
* <span data-ttu-id="446e8-139">포함된 데이터가 **바인딩 없이**증가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-139">There is embedded data won't grow **without bound**.</span></span>
* <span data-ttu-id="446e8-140">포함된 데이터가 문서의 데이터에 대한 **필수** 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-140">There is embedded data that is **integral** to data in a document.</span></span>

> [!NOTE]
> <span data-ttu-id="446e8-141">일반적으로 비정규화된 데이터 모델은 **읽기** 성능이 더 뛰어납니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-141">Typically denormalized data models provide better **read** performance.</span></span>
> 
> 

### <a name="when-not-to-embed"></a><span data-ttu-id="446e8-142">포함하지 않는 경우</span><span class="sxs-lookup"><span data-stu-id="446e8-142">When not to embed</span></span>
<span data-ttu-id="446e8-143">문서 데이터베이스에서 가장 좋은 원칙은 모든 것을 비정규화하고 모든 데이터를 단일 문서에 포함시키는 것이지만, 이 경우 방지해야 하는 몇 가지 상황이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-143">While the rule of thumb in a document database is to denormalize everything and embed all data in to a single document, this can lead to some situations that should be avoided.</span></span>

<span data-ttu-id="446e8-144">다음 JSON 코드 조각을 예로 들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-144">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "name": "What's new in the coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from the interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

<span data-ttu-id="446e8-145">이 코드 조각은 일반적인 블로그 또는 CMS 시스템을 모델링할 때 나타날 수 있는 포함된 주석이 있는 포스트 엔터티를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-145">This might be what a post entity with embedded comments would look like if we were modeling a typical blog, or CMS, system.</span></span> <span data-ttu-id="446e8-146">이 예제에서의 문제는 주석 배열이 **바인딩되지 않음**으로써, 단일 포스트가 가질 수 있는 주석 수에 대한 제한(실질적인)이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-146">The problem with this example is that the comments array is **unbounded**, meaning that there is no (practical) limit to the number of comments any single post can have.</span></span> <span data-ttu-id="446e8-147">이러한 상황은 문서 크기가 상당히 크게 증가할 수 있기 때문에 문제가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-147">This will become a problem as the size of the document could grow significantly.</span></span>

<span data-ttu-id="446e8-148">문서 크기가 증가함에 따라 확장 시 유선 상의 데이터 전송 기능과 문서 읽기 및 업데이트 기능이 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-148">As the size of the document grows the ability to transmit the data over the wire as well as reading and updating the document, at scale, will be impacted.</span></span>

<span data-ttu-id="446e8-149">이 경우에는 다음과 같은 모델을 고려하는 것이 더 좋을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-149">In this case it would be better to consider the following model.</span></span>

    Post document:
    {
        "id": "1",
        "name": "What's new in the coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from the interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from the field"},
            ...
            {"id": 99, "author": "angry", "comment": "blah angry blah angry"}
        ]
    },
    {
        "postId": "1"
        "comments": [
            {"id": 100, "author": "anon", "comment": "yet more"},
            ...
            {"id": 199, "author": "bored", "comment": "will this ever end?"}
        ]
    }

<span data-ttu-id="446e8-150">이 모델은 포스트 자체에 포함된 최근 3개 주석이 있으며, 이러한 포스트는 바인딩이 고정된 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-150">This model has the three most recent comments embedded on the post itself, which is an array with a fixed bound this time.</span></span> <span data-ttu-id="446e8-151">다른 주석은 100개 주석의 일괄 처리로 그룹화되고 개별 문서에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-151">The other comments are grouped in to batches of 100 comments and stored in separate documents.</span></span> <span data-ttu-id="446e8-152">일괄 처리의 크기를 100으로 선택한 이유는 이 예제의 가상 응용 프로그램에서 사용자가 한 번에 로드할 수 있는 주석의 수가 100개로 제한되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-152">The size of the batch was chosen as 100 because our fictitious application allows the user to load 100 comments at a time.</span></span>  

<span data-ttu-id="446e8-153">데이터 포함이 이상적인 대안이 될 수 없는 또 다른 경우는 포함된 데이터가 문서 간에 자주 사용되고 자주 변경되는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-153">Another case where embedding data is not a good idea is when the embedded data is used often across documents and will change frequently.</span></span> 

<span data-ttu-id="446e8-154">다음 JSON 코드 조각을 예로 들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-154">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            {
                "numberHeld": 100,
                "stock": { "symbol": "zaza", "open": 1, "high": 2, "low": 0.5 }
            },
            {
                "numberHeld": 50,
                "stock": { "symbol": "xcxc", "open": 89, "high": 93.24, "low": 88.87 }
            }
        ]
    }

<span data-ttu-id="446e8-155">이 예제는 한 사용자의 주식 포트폴리오를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-155">This could represent a person's stock portfolio.</span></span> <span data-ttu-id="446e8-156">여기에서는 주식 정보를 각 포트폴리오 문서에 포함하도록 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-156">We have chosen to embed the stock information in to each portfolio document.</span></span> <span data-ttu-id="446e8-157">주식 거래 응용 프로그램과 같이 관련 데이터가 자주 변경되는 환경에서, 자주 변경되는 데이터를 포함시키면 주식이 거래될 때마다 포트폴리오 문서를 계속해서 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-157">In an environment where related data is changing frequently, like a stock trading application, embedding data that changes frequently is going to mean that you are constantly updating each portfolio document every time a stock is traded.</span></span>

<span data-ttu-id="446e8-158">*zaza* 주식은 하루에도 수백 번 거래될 수 있으며 수천 명의 사용자 포트폴리오에 *zaza* 주식이 포함되어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-158">Stock *zaza* may be traded many hundreds of times in a single day and thousands of users could have *zaza* on their portfolio.</span></span> <span data-ttu-id="446e8-159">위와 같은 데이터 모델에서는 매일 여러 번 수천 개의 포트폴리오 문서를 업데이트해야 하므로, 시스템의 확장성이 낮아질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-159">With a data model like the above we would have to update many thousands of portfolio documents many times every day leading to a system that won't scale very well.</span></span> 

## <span data-ttu-id="446e8-160"><a id="Refer"></a>데이터 참조</span><span class="sxs-lookup"><span data-stu-id="446e8-160"><a id="Refer"></a>Referencing data</span></span>
<span data-ttu-id="446e8-161">따라서 데이터 포함 방식이 많은 경우에 효과적일 수 있지만, 데이터 비정규화로 인해 얻는 이득보다 잃게 되는 손실이 큰 경우도 있다는 것을 잘 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-161">So, embedding data works nicely for many cases but it is clear that there are scenarios when denormalizing your data will cause more problems than it is worth.</span></span> <span data-ttu-id="446e8-162">그러면 이제 무엇을 해야 할까요?</span><span class="sxs-lookup"><span data-stu-id="446e8-162">So what do we do now?</span></span> 

<span data-ttu-id="446e8-163">관계형 데이터베이스는 엔터티 간의 관계를 생성할 수 있는 유일한 대안이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-163">Relational databases are not the only place where you can create relationships between entities.</span></span> <span data-ttu-id="446e8-164">문서 데이터베이스에서는 다른 문서에 있는 데이터와 연관되는 정보를 하나의 문서에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-164">In a document database you can have information in one document that actually relates to data in other documents.</span></span> <span data-ttu-id="446e8-165">여기서는 Azure Cosmos DB의 관계형 데이터베이스 또는 다른 문서 데이터베이스에 더 적합한 시스템을 빌드하는 것보다 단순한 관계로도 충분하고 매우 유용할 수 있다는 것을 보여드리고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-165">Now, I am not advocating for even one minute that we build systems that would be better suited to a relational database in Azure Cosmos DB, or any other document database, but simple relationships are fine and can be very useful.</span></span> 

<span data-ttu-id="446e8-166">아래의 JSON에서도 이전 단락의 주식 포트폴리오 예제를 사용하지만, 이번에는 포함시키는 대신 포트폴리오의 주식 항목에 대해 설명하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-166">In the JSON below we chose to use the example of a stock portfolio from earlier but this time we refer to the stock item on the portfolio instead of embedding it.</span></span> <span data-ttu-id="446e8-167">이렇게 하면 주식 항목이 하루 중 자주 변경되더라도 업데이트해야 하는 문서는 단일 주식 문서뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-167">This way, when the stock item changes frequently throughout the day the only document that needs to be updated is the single stock document.</span></span> 

    Person document:
    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            { "numberHeld":  100, "stockId": 1},
            { "numberHeld":  50, "stockId": 2}
        ]
    }

    Stock documents:
    {
        "id": "1",
        "symbol": "zaza",
        "open": 1,
        "high": 2,
        "low": 0.5,
        "vol": 11970000,
        "mkt-cap": 42000000,
        "pe": 5.89
    },
    {
        "id": "2",
        "symbol": "xcxc",
        "open": 89,
        "high": 93.24,
        "low": 88.87,
        "vol": 2970200,
        "mkt-cap": 1005000,
        "pe": 75.82
    }


<span data-ttu-id="446e8-168">하지만 이 방식에서 나타날 수 있는 분명한 단점은 응용 프로그램이 사용자 포트폴리오를 표시할 때 저장된 각 주식에 대한 정보를 표시해야 할 경우에 나타납니다. 이 경우에는 각 주식 문서에 대한 정보를 로드하기 위해 데이터베이스를 여러 번에 걸쳐서 경유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-168">An immediate downside to this approach though is if your application is required to show information about each stock that is held when displaying a person's portfolio; in this case you would need to make multiple trips to the database to load the information for each stock document.</span></span> <span data-ttu-id="446e8-169">여기에서는 하루 중 자주 발생하는 쓰기 작업의 효율을 향상시키지만, 그에 따라 이 특정 시스템의 성능에 대한 영향이 덜할 수 있는 읽기 작업 성능은 희생하기로 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-169">Here we've made a decision to improve the efficiency of write operations, which happen frequently throughout the day, but in turn compromised on the read operations that potentially have less impact on the performance of this particular system.</span></span>

> [!NOTE]
> <span data-ttu-id="446e8-170">정규화된 데이터 모델은 서버에 대해 **더 많은 라운드 트립이 요구될 수 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="446e8-170">Normalized data models **can require more round trips** to the server.</span></span>
> 
> 

### <a name="what-about-foreign-keys"></a><span data-ttu-id="446e8-171">외래 키의 경우는 어떻게 될까요?</span><span class="sxs-lookup"><span data-stu-id="446e8-171">What about foreign keys?</span></span>
<span data-ttu-id="446e8-172">현재는 제약 조건이라는 개념이 없으므로, 외래 키 등 문서에 포함될 수 있는 모든 문서 간 관계는 실질적으로 "약한 링크"이며 데이터베이스 자체에서 확인되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-172">Because there is currently no concept of a constraint, foreign-key or otherwise, any inter-document relationships that you have in documents are effectively "weak links" and will not be verified by the database itself.</span></span> <span data-ttu-id="446e8-173">문서가 참조하는 데이터가 실제로 존재하는지 확인하기 위해서는 응용 프로그램에서 또는 서버측 트리거 또는 Azure Cosmos DB의 저장 프로시저를 사용해서 이를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-173">If you want to ensure that the data a document is referring to actually exists, then you need to do this in your application, or through the use of server-side triggers or stored procedures on Azure Cosmos DB.</span></span>

### <a name="when-to-reference"></a><span data-ttu-id="446e8-174">참조하는 경우</span><span class="sxs-lookup"><span data-stu-id="446e8-174">When to reference</span></span>
<span data-ttu-id="446e8-175">일반적으로 정규화된 데이터 모델은 다음과 같은 경우에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-175">In general, use normalized data models when:</span></span>

* <span data-ttu-id="446e8-176">**일대다** 관계를 나타내는 경우</span><span class="sxs-lookup"><span data-stu-id="446e8-176">Representing **one-to-many** relationships.</span></span>
* <span data-ttu-id="446e8-177">**다대다** 관계를 나타내는 경우</span><span class="sxs-lookup"><span data-stu-id="446e8-177">Representing **many-to-many** relationships.</span></span>
* <span data-ttu-id="446e8-178">관련 데이터가 **자주 변경**되는 경우</span><span class="sxs-lookup"><span data-stu-id="446e8-178">Related data **changes frequently**.</span></span>
* <span data-ttu-id="446e8-179">참조 데이터가 **바인딩되지 않는**경우</span><span class="sxs-lookup"><span data-stu-id="446e8-179">Referenced data could be **unbounded**.</span></span>

> [!NOTE]
> <span data-ttu-id="446e8-180">일반적으로 정규화에서는 **쓰기** 성능이 더 뛰어납니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-180">Typically normalizing provides better **write** performance.</span></span>
> 
> 

### <a name="where-do-i-put-the-relationship"></a><span data-ttu-id="446e8-181">관계는 어디에 배치해야 할까요?</span><span class="sxs-lookup"><span data-stu-id="446e8-181">Where do I put the relationship?</span></span>
<span data-ttu-id="446e8-182">관계의 성장은 참조를 저장할 문서를 결정하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-182">The growth of the relationship will help determine in which document to store the reference.</span></span>

<span data-ttu-id="446e8-183">아래의 JSON에서는 발행자와 책을 모델링합니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-183">If we look at the JSON below that models publishers and books.</span></span>

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over the world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in to Azure Cosmos DB" }

<span data-ttu-id="446e8-184">발행자당 책 수가 작고 제한적으로 증가할 경우, 책 참조를 해당 발행자 문서에 저장해도 좋을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-184">If the number of the books per publisher is small with limited growth, then storing the book reference inside the publisher document may be useful.</span></span> <span data-ttu-id="446e8-185">하지만 발행자당 책 수가 제한적이지 않으면, 이 데이터 모델의 경우 위의 발행자 문서 예제와 같이 배열이 변하기 쉽고 계속 증가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-185">However, if the number of books per publisher is unbounded, then this data model would lead to mutable, growing arrays, as in the example publisher document above.</span></span> 

<span data-ttu-id="446e8-186">이를 조금만 변경하면 동일한 데이터를 제공하지만, 쉽게 변경되는 대규모 컬렉션을 피할 수 있는 모델을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-186">Switching things around a bit would result in a model that still represents the same data but now avoids these large mutable collections.</span></span>

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over the world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in to Azure Cosmos DB", "pub-id": "mspress"}

<span data-ttu-id="446e8-187">위 예제에서는 발행자 문서에 바인딩되지 않은 컬렉션을 배치했습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-187">In the above example, we have dropped the unbounded collection on the publisher document.</span></span> <span data-ttu-id="446e8-188">그리고 각 책 문서에서 발행자에 대한 참조만 두었습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-188">Instead we just have a a reference to the publisher on each book document.</span></span>

### <a name="how-do-i-model-manymany-relationships"></a><span data-ttu-id="446e8-189">다대다 관계는 어떻게 모델링할 수 있을까요?</span><span class="sxs-lookup"><span data-stu-id="446e8-189">How do I model many:many relationships?</span></span>
<span data-ttu-id="446e8-190">관계형 데이터베이스에서 *다대다* 관계는 다른 테이블의 레코드를 단순히 하나로 조인하는 조인 테이블을 사용해서 모델링되는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-190">In a relational database *many:many* relationships are often modeled with join tables, which just join records from other tables together.</span></span> 

![테이블 조인](./media/documentdb-modeling-data/join-table.png)

<span data-ttu-id="446e8-192">여기에서도 문서를 사용해서 동일한 방식을 따르고 다음과 비슷하게 보이는 데이터 모델을 만들고 싶을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-192">You might be tempted to replicate the same thing using documents and produce a data model that looks similar to the following.</span></span>

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over the world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in to Azure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

<span data-ttu-id="446e8-193">이러한 모델도 작동은 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-193">This would work.</span></span> <span data-ttu-id="446e8-194">하지만 특정 저자와 해당 저자의 책을 로드하거나 특정 책과 해당 책의 저자를 로드하려면 항상 데이터베이스에 대해 2개 이상의 추가 쿼리를 실행해야 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-194">However, loading either an author with their books, or loading a book with its author, would always require at least two additional queries against the database.</span></span> <span data-ttu-id="446e8-195">조인 문서에 대해 쿼리를 한 번 수행하고 조인되는 실제 문서를 인출하기 위해 또 다른 쿼리를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-195">One query to the joining document and then another query to fetch the actual document being joined.</span></span> 

<span data-ttu-id="446e8-196">이 조인 테이블이 수행하는 작업이 두 가지 데이터를 하나로 묶는 작업뿐이라면 이를 완전히 삭제할 수도 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-196">If all this join table is doing is gluing together two pieces of data, then why not drop it completely?</span></span>
<span data-ttu-id="446e8-197">다음을 고려해보세요.</span><span class="sxs-lookup"><span data-stu-id="446e8-197">Consider the following.</span></span>

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in to Azure Cosmos DB", "authors": ["a2"]}

<span data-ttu-id="446e8-198">특정 저자가 있으면, 그가 작성한 책이 무엇인지 즉시 알 수 있고, 반대로, 로드된 책 문서가 있으면, 해당 저자의 ID를 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-198">Now, if I had an author, I immediately know which books they have written, and conversely if I had a book document loaded I would know the ids of the author(s).</span></span> <span data-ttu-id="446e8-199">이렇게 하면 조인 테이블에 대한 중간 쿼리를 절약해서 응용 프로그램에서 수행해야 하는 서버 라운드 트립 수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-199">This saves that intermediary query against the join table reducing the number of server round trips your application has to make.</span></span> 

## <span data-ttu-id="446e8-200"><a id="WrapUp"></a>하이브리드 데이터 모델</span><span class="sxs-lookup"><span data-stu-id="446e8-200"><a id="WrapUp"></a>Hybrid data models</span></span>
<span data-ttu-id="446e8-201">지금까지 데이터 포함(또는 비정규화)과 참조(또는 정규화)에 대해 살펴봤습니다. 이러한 데이터 포함과 참조는 위에서 살펴본 것처럼 각각 장점과 단점을 갖고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-201">We've now looked embedding (or denormalizing) and referencing (or normalizing) data, each have their upsides and each have compromises as we have seen.</span></span> 

<span data-ttu-id="446e8-202">하지만 어느 쪽이든 장단점이 있으므로 두 방식을 혼합해서 사용해도 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-202">It doesn't always have to be either or, don't be scared to mix things up a little.</span></span> 

<span data-ttu-id="446e8-203">응용 프로그램의 특정 사용 패턴 및 워크로드에 따라 포함 및 참조 데이터를 혼합하는 것이 적합할 수 있으며, 응용 프로그램 논리를 단순화하면서 서버 라운드 트립도 줄이고, 적절한 수준으로 성능을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-203">Based on your application's specific usage patterns and workloads there may be cases where mixing embedded and referenced data makes sense and could lead to simpler application logic with fewer server round trips while still maintaining a good level of performance.</span></span>

<span data-ttu-id="446e8-204">다음과 같은 JSON을 고려해보세요.</span><span class="sxs-lookup"><span data-stu-id="446e8-204">Consider the following JSON.</span></span> 

    Author documents: 
    {
        "id": "a1",
        "firstName": "Thomas",
        "lastName": "Andersen",        
        "countOfBooks": 3,
         "books": ["b1", "b2", "b3"],
        "images": [
            {"thumbnail": "http://....png"}
            {"profile": "http://....png"}
            {"large": "http://....png"}
        ]
    },
    {
        "id": "a2",
        "firstName": "William",
        "lastName": "Wakefield",
        "countOfBooks": 1,
        "books": ["b1"],
        "images": [
            {"thumbnail": "http://....png"}
        ]
    }

    Book documents:
    {
        "id": "b1",
        "name": "Azure Cosmos DB 101",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
            {"id": "a2", "name": "William Wakefield", "thumbnailUrl": "http://....png"}
        ]
    },
    {
        "id": "b2",
        "name": "Azure Cosmos DB for RDBMS Users",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
        ]
    }

<span data-ttu-id="446e8-205">여기에서는 주로 포함된 모델을 따랐으며, 다른 엔터티의 데이터가 최상위 문서에 포함되지만 다른 데이터는 참조됩니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-205">Here we've (mostly) followed the embedded model, where data from other entities are embedded in the top-level document, but other data is referenced.</span></span> 

<span data-ttu-id="446e8-206">책 문서를 보면 저자 배열을 볼 때 몇 가지 흥미로운 필드를 발견할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-206">If you look at the book document, we can see a few interesting fields when we look at the array of authors.</span></span> <span data-ttu-id="446e8-207">여기에는 정규화된 모델의 표준 방법인 저자 문서를 다시 참조하기 위해 사용하는 필드인 *id* 필드가 있지만, *이름* 및 *thumbnailUrl*도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-207">There is an *id* field which is the field we use to refer back to an author document, standard practice in a normalized model, but then we also have *name* and *thumbnailUrl*.</span></span> <span data-ttu-id="446e8-208">*id* 만 사용하고 응용 프로그램이 필요한 추가 정보를 "link"를 사용해서 해당 저자 문서에서 가져오도록 할 수도 있지만, 이 응용 프로그램에서는 표시된 모든 책과 함께 저자 이름과 썸네일 사진을 표시하므로, 저자에서 **일부** 데이터를 비정규화해서 목록에 있는 책당 서버에 대한 라운드 트립을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-208">We could've just stuck with *id* and left the application to get any additional information it needed from the respective author document using the "link", but because our application displays the author's name and a thumbnail picture with every book displayed we can save a round trip to the server per book in a list by denormalizing **some** data from the author.</span></span>

<span data-ttu-id="446e8-209">물론, 저자 이름이 변경되거나 사진을 업데이트하기를 원할 경우, 저자가 출판한 모든 책에 대해 업데이트를 수행해야 하지만, 저자가 자신의 이름을 자주 변경하지 않는다는 가정에 따라 이 응용 프로그램에서 이러한 정도는 설계상으로 수락할 수 있는 정도입니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-209">Sure, if the author's name changed or they wanted to update their photo we'd have to go an update every book they ever published but for our application, based on the assumption that authors don't change their names very often, this is an acceptable design decision.</span></span>  

<span data-ttu-id="446e8-210">위 예제에서는 읽기 작업에 대한 고비용 처리 작업을 줄이기 위해 **사전 계산된 집계** 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-210">In the example there are **pre-calculated aggregates** values to save expensive processing on a read operation.</span></span> <span data-ttu-id="446e8-211">이 예제에서 저자의 문서에 포함된 일부 데이터는 런타임에 계산되는 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-211">In the example, some of the data embedded in the author document is data that is calculated at run-time.</span></span> <span data-ttu-id="446e8-212">새 책이 게시될 때마다, 책 문서가 생성됩니다. **그리고** countOfBooks 필드가 특정 저자에 대해 존재하는 책 문서 번호를 기준으로 계산된 값으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-212">Every time a new book is published, a book document is created **and** the countOfBooks field is set to a calculated value based on the number of book documents that exist for a particular author.</span></span> <span data-ttu-id="446e8-213">이러한 최적화는 읽기를 최적화하기 위해 읽기 계산을 수행할 수 있는 읽기에 집중된 시스템에서 효과적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-213">This optimization would be good in read heavy systems where we can afford to do computations on writes in order to optimize reads.</span></span>

<span data-ttu-id="446e8-214">모델에 사전 계산된 필드를 포함할 수 있는 기능은 Azure Cosmos DB에서 **다중 문서 트랜잭션**이 지원되기 때문에 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-214">The ability to have a model with pre-calculated fields is made possible because Azure Cosmos DB supports **multi-document transactions**.</span></span> <span data-ttu-id="446e8-215">많은 NoSQL 저장소에서는 문서 간 트랜잭션을 수행할 수 없기 때문에 이러한 제한으로 인해 "항상 모든 것으로 포함"하는 디자인을 선호합니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-215">Many NoSQL stores cannot do transactions across documents and therefore advocate design decisions, such as "always embed everything", due to this limitation.</span></span> <span data-ttu-id="446e8-216">Azure Cosmos DB에서는 서버 쪽 트리거 또는 저장 프로시저를 사용해서 ACID 트랜잭션 내에서 책을 삽입하고 저자를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-216">With Azure Cosmos DB, you can use server-side triggers, or stored procedures, that insert books and update authors all within an ACID transaction.</span></span> <span data-ttu-id="446e8-217">이제는 단지 데이터 일관성 유지를 위해 모든 것을 하나의 문서에 포함시켜야 할 **필요가** 없습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-217">Now you don't **have** to embed everything in to one document just to be sure that your data remains consistent.</span></span>

## <span data-ttu-id="446e8-218"><a name="NextSteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="446e8-218"><a name="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="446e8-219">이 문서에서 가장 중요한 사항은 스키마가 없는 환경에서의 데이터 모델링도 이전과 같이 중요하다는 것을 이해하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-219">The biggest takeaways from this article is to understand that data modeling in a schema-free world is just as important as ever.</span></span> 

<span data-ttu-id="446e8-220">화면에 데이터를 표시하는 방법이 하나만 있지 않은 것처럼 데이터를 모델링하는 방법도 하나만 있는 것이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-220">Just as there is no single way to represent a piece of data on a screen, there is no single way to model your data.</span></span> <span data-ttu-id="446e8-221">응용 프로그램을 이해하고 데이터를 생산, 소비 및 처리하는 방법을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-221">You need to understand your application and how it will produce, consume, and process the data.</span></span> <span data-ttu-id="446e8-222">그런 다음 여기에 제공된 일부 지침을 적용해서 응용 프로그램에 즉시 필요한 사항을 처리할 수 있는 모델을 제작 방법을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-222">Then, by applying some of the guidelines presented here you can set about creating a model that addresses the immediate needs of your application.</span></span> <span data-ttu-id="446e8-223">응용 프로그램에 변경이 필요한 경우에는 스키마가 없는 데이터베이스의 유연성을 활용해서 변경 사항을 포용하고 데이터 모델을 쉽게 발전시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="446e8-223">When your applications need to change, you can leverage the flexibility of a schema-free database to embrace that change and evolve your data model easily.</span></span> 

<span data-ttu-id="446e8-224">Azure Cosmos DB에 대한 자세한 내용은 서비스의 [설명서](https://azure.microsoft.com/documentation/services/cosmos-db/) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="446e8-224">To learn more about Azure Cosmos DB, refer to the service's [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span> 

<span data-ttu-id="446e8-225">여러 파티션에 데이터를 분할하는 방법에 대한 자세한 내용은 [Azure Cosmos DB에서 데이터 분할](documentdb-partition-data.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="446e8-225">To understand how to shard your data across multiple partitions, refer to [Partitioning Data in Azure Cosmos DB](documentdb-partition-data.md).</span></span> 
