---
title: "Azure Cosmos DB를 사용하는 다중 마스터 데이터베이스 아키텍처 | Microsoft Docs"
description: "Azure Cosmos DB로 여러 지리적 지역에서 로컬 읽기 및 쓰기가 가능한 응용 프로그램 아키텍처를 디자인하는 방법을 알아봅니다."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 706ced74-ea67-45dd-a7de-666c3c893687
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf1482ae7b1070023703f5dbe861d151f5d64fd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a><span data-ttu-id="53f49-103">Azure Cosmos DB를 사용하는 다중 마스터 전역 복제 데이터베이스 아키텍처</span><span class="sxs-lookup"><span data-stu-id="53f49-103">Multi-master globally replicated database architectures with Azure Cosmos DB</span></span>
<span data-ttu-id="53f49-104">Azure Cosmos DB는 턴키 [전역 복제](distribute-data-globally.md)를 지원하므로 워크로드 어디서나 여러 지역에 데이터를 분산할 수 있으며 액세스 대기 시간이 짧습니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-104">Azure Cosmos DB supports turnkey [global replication](distribute-data-globally.md), which allows you to distribute data to multiple regions with low latency access anywhere in the workload.</span></span> <span data-ttu-id="53f49-105">이 모델은 한 지역에 기록기가 있고 다른 (읽기) 지역에 지리적으로 분산된 판독기가 있는 게시자/소비자 워크로드에 주로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-105">This model is commonly used for publisher/consumer workloads where there is a writer in a single geographic region and globally distributed readers in other (read) regions.</span></span> 

<span data-ttu-id="53f49-106">Azure Cosmos DB의 글로벌 복제 지원을 사용하여 기록기 및 판독기가 전역에 분산되는 응용 프로그램을 빌드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-106">You can also use Azure Cosmos DB's global replication support to build applications in which writers and readers are globally distributed.</span></span> <span data-ttu-id="53f49-107">이 문서에서는 Azure Cosmos DB를 사용하여 분산된 작성기에 대한 로컬 쓰기 및 로컬 읽기 액세스를 가능하게 하는 패턴을 개략적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-107">This document outlines a pattern that enables achieving local write and local read access for distributed writers using Azure Cosmos DB.</span></span>

## <span data-ttu-id="53f49-108"><a id="ExampleScenario"></a>콘텐츠 게시 - 예제 시나리오</span><span class="sxs-lookup"><span data-stu-id="53f49-108"><a id="ExampleScenario"></a>Content Publishing - an example scenario</span></span>
<span data-ttu-id="53f49-109">Azure Cosmos DB로 전역에 분산된 다중 지역/다중 마스터 읽기 쓰기 패턴을 사용하는 방법을 설명하는 실제 시나리오를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-109">Let's look at a real world scenario to describe how you can use globally distributed multi-region/multi-master read write patterns with Azure Cosmos DB.</span></span> <span data-ttu-id="53f49-110">Azure Cosmos DB를 기반으로 하는 콘텐츠 게시 플랫폼이 있다고 가정합시다.</span><span class="sxs-lookup"><span data-stu-id="53f49-110">Consider a content publishing platform built on Azure Cosmos DB.</span></span> <span data-ttu-id="53f49-111">이 플랫폼이 게시자와 소비자 모두에게 훌륭한 사용자 환경을 제공하기 위해 충족해야 하는 몇 가지 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-111">Here are some requirements that this platform must meet for a great user experience for both publishers and consumers.</span></span>

* <span data-ttu-id="53f49-112">작성자와 구독자 모두 전 세계에 분산되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-112">Both authors and subscribers are spread over the world</span></span> 
* <span data-ttu-id="53f49-113">작성자는 로컬(가장 가까운) 지역에 문서를 게시(쓰기)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-113">Authors must publish (write) articles to their local (closest) region</span></span>
* <span data-ttu-id="53f49-114">작성자의 문서 독자/구독자가 전 세계에 분산되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-114">Authors have readers/subscribers of their articles who are distributed across the globe.</span></span> 
* <span data-ttu-id="53f49-115">새 문서가 게시되면 구독자가 알림을 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-115">Subscribers should get a notification when new articles are published.</span></span>
* <span data-ttu-id="53f49-116">구독자는 로컬 지역에서 문서를 읽을 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-116">Subscribers must be able to read articles from their local region.</span></span> <span data-ttu-id="53f49-117">또한 이러한 문서에 리뷰를 추가할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-117">They should also be able to add reviews to these articles.</span></span> 
* <span data-ttu-id="53f49-118">문서 작성자를 포함한 모든 사람은 문서에 연결된 모든 리뷰를 로컬 지역에서 볼 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-118">Anyone including the author of the articles should be able view all the reviews attached to articles from a local region.</span></span> 

<span data-ttu-id="53f49-119">수백만 명의 소비자 및 게시자와 수십억 개의 문서가 있다고 가정한다면, 조만간 지역 액세스 보장과 함께 확장 문제에 직면하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-119">Assuming millions of consumers and publishers with billions of articles, soon we have to confront the problems of scale along with guaranteeing locality of access.</span></span> <span data-ttu-id="53f49-120">대부분의 확장 문제와 마찬가지로, 해결책은 좋은 분할 전략에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-120">As with most scalability problems, the solution lies in a good partitioning strategy.</span></span> <span data-ttu-id="53f49-121">다음으로 문서, 리뷰 및 알림을 문서로 모델링하고, Azure Cosmos DB 계정을 구성하고, 데이터 액세스 계층을 구현하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-121">Next, let's look at how to model articles, review, and notifications as documents, configure Azure Cosmos DB accounts, and implement a data access layer.</span></span> 

<span data-ttu-id="53f49-122">분할 및 파티션 키에 대한 자세한 내용은 [Azure Cosmos DB의 분할 및 크기 조정](partition-data.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53f49-122">If you would like to learn more about partitioning and partition keys, see [Partitioning and Scaling in Azure Cosmos DB](partition-data.md).</span></span>

## <span data-ttu-id="53f49-123"><a id="ModelingNotifications"></a>알림 모델링</span><span class="sxs-lookup"><span data-stu-id="53f49-123"><a id="ModelingNotifications"></a>Modeling notifications</span></span>
<span data-ttu-id="53f49-124">알림은 사용자에게 한정된 데이터 피드입니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-124">Notifications are data feeds specific to a user.</span></span> <span data-ttu-id="53f49-125">따라서 알림 문서의 액세스 패턴은 항상 단일 사용자의 컨텍스트와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-125">Therefore, the access patterns for notifications documents are always in the context of single user.</span></span> <span data-ttu-id="53f49-126">예를 들어 "사용자에게 알림을 게시"하거나 "지정된 사용자에 대한 모든 알림을 가져올" 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-126">For example, you would "post a notification to a user" or "fetch all notifications for a given user".</span></span> <span data-ttu-id="53f49-127">따라서 이 유형에 선택할 수 있는 최적의 분할 키는 `UserId`입니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-127">So, the optimal choice of partitioning key for this type would be `UserId`.</span></span>

    class Notification 
    { 
        // Unique ID for Notification. 
        public string Id { get; set; }

        // The user Id for which notification is addressed to. 
        public string UserId { get; set; }

        // The partition Key for the resource. 
        public string PartitionKey 
        { 
            get 
            { 
                return this.UserId; 
            }
        }

        // Subscription for which this notification is raised. 
        public string SubscriptionFilter { get; set; }

        // Subject of the notification. 
        public string ArticleId { get; set; } 
    }

## <span data-ttu-id="53f49-128"><a id="ModelingSubscriptions"></a>구독 모델링</span><span class="sxs-lookup"><span data-stu-id="53f49-128"><a id="ModelingSubscriptions"></a>Modeling subscriptions</span></span>
<span data-ttu-id="53f49-129">관심 있는 문서의 특정 범주나 특정 게시자처럼 다양한 조건에 대한 구독을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-129">Subscriptions can be created for various criteria like a specific category of articles of interest, or a specific publisher.</span></span> <span data-ttu-id="53f49-130">따라서 파티션 키에 좋은 선택은 `SubscriptionFilter`입니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-130">Hence the `SubscriptionFilter` is a good choice for partition key.</span></span>

    class Subscriptions 
    { 
        // Unique ID for Subscription 
        public string Id { get; set; }

        // Subscription source. Could be Author | Category etc. 
        public string SubscriptionFilter { get; set; }

        // subscribing User. 
        public string UserId { get; set; }

        public string PartitionKey 
        { 
            get 
            { 
                return this.SubscriptionFilter; 
            } 
        } 
    }

## <span data-ttu-id="53f49-131"><a id="ModelingArticles"></a>문서 모델링</span><span class="sxs-lookup"><span data-stu-id="53f49-131"><a id="ModelingArticles"></a>Modeling articles</span></span>
<span data-ttu-id="53f49-132">알림을 통해 문서가 식별되면 후속 쿼리는 일반적으로 `Article.Id`를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-132">Once an article is identified through notifications, subsequent queries are typically based on the `Article.Id`.</span></span> <span data-ttu-id="53f49-133">따라서 파티션 키로 `Article.Id`를 선택하면 Azure Cosmos DB 컬렉션 내에 문서를 저장하기에 가장 적합하게 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-133">Choosing `Article.Id` as partition the key thus provides the best distribution for storing articles inside an Azure Cosmos DB collection.</span></span> 

    class Article 
    { 
        // Unique ID for Article 
        public string Id { get; set; }
        
        public string PartitionKey 
        { 
            get 
            { 
                return this.Id; 
            } 
        }
        
        // Author of the article
        public string Author { get; set; }

        // Category/genre of the article
        public string Category { get; set; }

        // Tags associated with the article
        public string[] Tags { get; set; }

        // Title of the article
        public string Title { get; set; }
        
        //... 
    }

## <span data-ttu-id="53f49-134"><a id="ModelingReviews"></a>리뷰 모델링</span><span class="sxs-lookup"><span data-stu-id="53f49-134"><a id="ModelingReviews"></a>Modeling reviews</span></span>
<span data-ttu-id="53f49-135">리뷰 역시 문서와 마찬가지로 주로 문서의 컨텍스트에서 쓰고 읽힙니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-135">Like articles, reviews are mostly written and read in the context of article.</span></span> <span data-ttu-id="53f49-136">파티션 키로 `ArticleId`를 선택하면 가장 적절하게 분산될 뿐 아니라 문서와 연결된 리뷰를 효율적으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-136">Choosing `ArticleId` as a partition key provides best distribution and efficient access of reviews associated with article.</span></span> 

    class Review 
    { 
        // Unique ID for Review 
        public string Id { get; set; }

        // Article Id of the review 
        public string ArticleId { get; set; }

        public string PartitionKey 
        { 
            get 
            { 
                return this.ArticleId; 
            } 
        }
        
        //Reviewer Id 
        public string UserId { get; set; }
        public string ReviewText { get; set; }
        
        public int Rating { get; set; } }
    }

## <span data-ttu-id="53f49-137"><a id="DataAccessMethods"></a>데이터 액세스 계층 메서드</span><span class="sxs-lookup"><span data-stu-id="53f49-137"><a id="DataAccessMethods"></a>Data access layer methods</span></span>
<span data-ttu-id="53f49-138">이번에는 우리가 구현해야 하는 기본 데이터 액세스 메서드를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-138">Now let's look at the main data access methods we need to implement.</span></span> <span data-ttu-id="53f49-139">다음은 `ContentPublishDatabase`에 필요한 메서드 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-139">Here's the list of methods that the `ContentPublishDatabase` needs:</span></span>

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <span data-ttu-id="53f49-140"><a id="Architecture"></a>Azure Cosmos DB 계정 구성</span><span class="sxs-lookup"><span data-stu-id="53f49-140"><a id="Architecture"></a>Azure Cosmos DB account configuration</span></span>
<span data-ttu-id="53f49-141">로컬 읽기 및 쓰기를 보장하려면 파티션 키뿐 아니라 지리적 액세스 패턴을 기반으로 데이터를 여러 지역으로 분할해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-141">To guarantee local reads and writes, we must partition data not just on partition key, but also based on the geographical access pattern into regions.</span></span> <span data-ttu-id="53f49-142">이 모델은 각 지역에 지리적으로 복제된 Azure Cosmos DB 데이터베이스 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-142">The model relies on having a geo-replicated Azure Cosmos DB database account for each region.</span></span> <span data-ttu-id="53f49-143">예를 들어 지역이 두 개라면 다중 지역 쓰기에 대한 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-143">For example, with two regions, here's a setup for multi-region writes:</span></span>

| <span data-ttu-id="53f49-144">계정 이름</span><span class="sxs-lookup"><span data-stu-id="53f49-144">Account Name</span></span> | <span data-ttu-id="53f49-145">쓰기 지역</span><span class="sxs-lookup"><span data-stu-id="53f49-145">Write Region</span></span> | <span data-ttu-id="53f49-146">읽기 지역</span><span class="sxs-lookup"><span data-stu-id="53f49-146">Read Region</span></span> |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

<span data-ttu-id="53f49-147">다음 다이어그램은 이 설정을 사용하는 일반 응용 프로그램에서 읽기 및 쓰기가 수행되는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-147">The following diagram shows how reads and writes are performed in a typical application with this setup:</span></span>

![Azure Cosmos DB 다중 마스터 아키텍처](./media/multi-region-writers/multi-master.png)

<span data-ttu-id="53f49-149">다음은 `West US` 지역에서 실행되는 DAL에서 클라이언트를 초기화하는 방법을 보여주는 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-149">Here is a code snippet showing how to initialize the clients in a DAL running in the `West US` region.</span></span>
    
    ConnectionPolicy writeClientPolicy = new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp };
    writeClientPolicy.PreferredLocations.Add(LocationNames.WestUS);
    writeClientPolicy.PreferredLocations.Add(LocationNames.NorthEurope);

    DocumentClient writeClient = new DocumentClient(
        new Uri("https://contentpubdatabase-usa.documents.azure.com"), 
        writeRegionAuthKey,
        writeClientPolicy);

    ConnectionPolicy readClientPolicy = new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp };
    readClientPolicy.PreferredLocations.Add(LocationNames.NorthEurope);
    readClientPolicy.PreferredLocations.Add(LocationNames.WestUS);

    DocumentClient readClient = new DocumentClient(
        new Uri("https://contentpubdatabase-europe.documents.azure.com"),
        readRegionAuthKey,
        readClientPolicy);

<span data-ttu-id="53f49-150">이전 설정을 사용하면 데이터 액세스 계층은 배포된 위치에 따라 모든 쓰기를 로컬 계정에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-150">With the preceding setup, the data access layer can forward all writes to the local account based on where it is deployed.</span></span> <span data-ttu-id="53f49-151">두 계정 모두에서 데이터를 읽어 읽기를 수행하여 데이터의 전역 보기를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-151">Reads are performed by reading from both accounts to get the global view of data.</span></span> <span data-ttu-id="53f49-152">이 방법은 필요한 만큼 여러 지역으로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-152">This approach can be extended to as many regions as required.</span></span> <span data-ttu-id="53f49-153">예를 들어 다음은 세 개 지역에 대한 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-153">For example, here's a setup with three geographic regions:</span></span>

| <span data-ttu-id="53f49-154">계정 이름</span><span class="sxs-lookup"><span data-stu-id="53f49-154">Account Name</span></span> | <span data-ttu-id="53f49-155">쓰기 지역</span><span class="sxs-lookup"><span data-stu-id="53f49-155">Write Region</span></span> | <span data-ttu-id="53f49-156">읽기 지역 1</span><span class="sxs-lookup"><span data-stu-id="53f49-156">Read Region 1</span></span> | <span data-ttu-id="53f49-157">읽기 지역 2</span><span class="sxs-lookup"><span data-stu-id="53f49-157">Read Region 2</span></span> |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <span data-ttu-id="53f49-158"><a id="DataAccessImplementation"></a>데이터 액세스 계층 구현</span><span class="sxs-lookup"><span data-stu-id="53f49-158"><a id="DataAccessImplementation"></a>Data access layer implementation</span></span>
<span data-ttu-id="53f49-159">이번에는 쓰기 가능한 지역이 두 개인 응용 프로그램의 DAL(데이터 액세스 계층) 구현을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-159">Now let's look at the implementation of the data access layer (DAL) for an application with two writable regions.</span></span> <span data-ttu-id="53f49-160">DAL은 다음 단계를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-160">The DAL must implement the following steps:</span></span>

* <span data-ttu-id="53f49-161">각 계정에 대해 여러 `DocumentClient` 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-161">Create multiple instances of `DocumentClient` for each account.</span></span> <span data-ttu-id="53f49-162">지역이 두 개이므로 각 DAL 인스턴스는 `writeClient` 하나와 `readClient` 하나를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-162">With two regions, each DAL instance has one `writeClient` and one `readClient`.</span></span> 
* <span data-ttu-id="53f49-163">배포된 응용 프로그램 지역에 따라 `writeclient` 및 `readClient`의 끝점을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-163">Based on the deployed region of the application, configure the endpoints for `writeclient` and `readClient`.</span></span> <span data-ttu-id="53f49-164">예를 들어 `West US`에 배포된 DAL은 쓰기 수행에 `contentpubdatabase-usa.documents.azure.com`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-164">For example, the DAL deployed in `West US` uses `contentpubdatabase-usa.documents.azure.com` for performing writes.</span></span> <span data-ttu-id="53f49-165">`NorthEurope`에 배포된 DAL은 쓰기에 `contentpubdatabase-europ.documents.azure.com`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-165">The DAL deployed in `NorthEurope` uses `contentpubdatabase-europ.documents.azure.com` for writes.</span></span>

<span data-ttu-id="53f49-166">이전 설정을 사용하면 데이터 액세스 메서드를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-166">With the preceding setup, the data access methods can be implemented.</span></span> <span data-ttu-id="53f49-167">쓰기 작업은 쓰기를 해당 `writeClient`에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-167">Write operations forward the write to the corresponding `writeClient`.</span></span>

    public async Task CreateSubscriptionAsync(string userId, string category)
    {
        await this.writeClient.CreateDocumentAsync(this.contentCollection, new Subscriptions
        {
            UserId = userId,
            SubscriptionFilter = category
        });
    }

    public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating)
    {
        await this.writeClient.CreateDocumentAsync(this.contentCollection, new Review
        {
            UserId = userId,
            ArticleId = articleId,
            ReviewText = reviewText,
            Rating = rating
        });
    }

<span data-ttu-id="53f49-168">알림 및 리뷰 읽기의 경우 다음 코드 조각에 나와 있는 것처럼 두 지역 모두에서 읽고 결과를 조합해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-168">For reading notifications and reviews, you must read from both regions and union the results as shown in the following snippet:</span></span>

    public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId)
    {
        IDocumentQuery<Notification> writeAccountNotification = (
            from notification in this.writeClient.CreateDocumentQuery<Notification>(this.contentCollection) 
            where notification.UserId == userId 
            select notification).AsDocumentQuery();
        
        IDocumentQuery<Notification> readAccountNotification = (
            from notification in this.readClient.CreateDocumentQuery<Notification>(this.contentCollection) 
            where notification.UserId == userId 
            select notification).AsDocumentQuery();

        List<Notification> notifications = new List<Notification>();

        while (writeAccountNotification.HasMoreResults || readAccountNotification.HasMoreResults)
        {
            IList<Task<FeedResponse<Notification>>> results = new List<Task<FeedResponse<Notification>>>();

            if (writeAccountNotification.HasMoreResults)
            {
                results.Add(writeAccountNotification.ExecuteNextAsync<Notification>());
            }

            if (readAccountNotification.HasMoreResults)
            {
                results.Add(readAccountNotification.ExecuteNextAsync<Notification>());
            }

            IList<FeedResponse<Notification>> notificationFeedResult = await Task.WhenAll(results);

            foreach (FeedResponse<Notification> feed in notificationFeedResult)
            {
                notifications.AddRange(feed);
            }
        }
        return notifications;
    }

    public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId)
    {
        IDocumentQuery<Review> writeAccountReviews = (
            from review in this.writeClient.CreateDocumentQuery<Review>(this.contentCollection) 
            where review.ArticleId == articleId 
            select review).AsDocumentQuery();
        
        IDocumentQuery<Review> readAccountReviews = (
            from review in this.readClient.CreateDocumentQuery<Review>(this.contentCollection) 
            where review.ArticleId == articleId 
            select review).AsDocumentQuery();

        List<Review> reviews = new List<Review>();
        
        while (writeAccountReviews.HasMoreResults || readAccountReviews.HasMoreResults)
        {
            IList<Task<FeedResponse<Review>>> results = new List<Task<FeedResponse<Review>>>();

            if (writeAccountReviews.HasMoreResults)
            {
                results.Add(writeAccountReviews.ExecuteNextAsync<Review>());
            }

            if (readAccountReviews.HasMoreResults)
            {
                results.Add(readAccountReviews.ExecuteNextAsync<Review>());
            }

            IList<FeedResponse<Review>> notificationFeedResult = await Task.WhenAll(results);

            foreach (FeedResponse<Review> feed in notificationFeedResult)
            {
                reviews.AddRange(feed);
            }
        }

        return reviews;
    }

<span data-ttu-id="53f49-169">따라서 적절한 분할 키와 정적 계정 기반 분할을 선택하면 Azure Cosmos DB를 사용하여 다중 지역 로컬 쓰기 및 읽기를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-169">Thus, by choosing a good partitioning key and static account-based partitioning, you can achieve multi-region local writes and reads using Azure Cosmos DB.</span></span>

## <span data-ttu-id="53f49-170"><a id="NextSteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="53f49-170"><a id="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="53f49-171">이 문서에서는 콘텐츠 게시를 샘플 시나리오로 사용하여 전 세계에 분산된 다중 지역 읽기 쓰기 패턴을 Azure Cosmos DB와 함께 사용하는 방법을 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="53f49-171">In this article, we described how you can use globally distributed multi-region read write patterns with Azure Cosmos DB using content publishing as a sample scenario.</span></span>

* <span data-ttu-id="53f49-172">Azure Cosmos DB에서 [전역 배포](distribute-data-globally.md)를 지원하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="53f49-172">Learn about how Azure Cosmos DB supports [global distribution](distribute-data-globally.md)</span></span>
* <span data-ttu-id="53f49-173">[Azure Cosmos DB의 자동 및 수동 장애 조치(failover)](regional-failover.md) 알아보기</span><span class="sxs-lookup"><span data-stu-id="53f49-173">Learn about [automatic and manual failovers in Azure Cosmos DB](regional-failover.md)</span></span>
* <span data-ttu-id="53f49-174">[Azure Cosmos DB를 통한 전역 일관성](consistency-levels.md) 알아보기</span><span class="sxs-lookup"><span data-stu-id="53f49-174">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span></span>
* <span data-ttu-id="53f49-175">[Azure Cosmos DB - DocumentDB API](tutorial-global-distribution-documentdb.md)를 사용하여 여러 지역으로 개발</span><span class="sxs-lookup"><span data-stu-id="53f49-175">Develop with multiple regions using the [Azure Cosmos DB - DocumentDB API](tutorial-global-distribution-documentdb.md)</span></span>
* <span data-ttu-id="53f49-176">[Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)를 사용하여 여러 지역으로 개발</span><span class="sxs-lookup"><span data-stu-id="53f49-176">Develop with multiple regions using the [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)</span></span>
* <span data-ttu-id="53f49-177">[Azure Cosmos DB - Table API](tutorial-global-distribution-table.md)를 사용하여 여러 지역으로 개발</span><span class="sxs-lookup"><span data-stu-id="53f49-177">Develop with multiple regions using the [Azure Cosmos DB - Table API](tutorial-global-distribution-table.md)</span></span>
