---
title: "Azure Cosmos DB와 함께 aaaMulti master 데이터베이스 아키텍처 | Microsoft Docs"
description: "로컬 응용 프로그램 아키텍처 toodesign 읽고 Azure Cosmos DB와 함께 여러 지리적 지역에 걸쳐 기록에 대해 알아봅니다."
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
ms.openlocfilehash: 3269c8405afe16f75db69b42e576fe76e00a8e16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a>Azure Cosmos DB를 사용하는 다중 마스터 전역 복제 데이터베이스 아키텍처
Azure Cosmos DB 지원 턴키 [전역 복제](distribute-data-globally.md), hello 작업의 대기 시간이 짧은 액세스할 수 있는 toodistribute 데이터 toomultiple 영역 수 있는 합니다. 이 모델은 한 지역에 기록기가 있고 다른 (읽기) 지역에 지리적으로 분산된 판독기가 있는 게시자/소비자 워크로드에 주로 사용됩니다. 

또한 Azure Cosmos DB 전역 복제 지원 toobuild는 writers 및 readers는 전역적으로 배포 된 응용 프로그램을 사용할 수 있습니다. 이 문서에서는 Azure Cosmos DB를 사용하여 분산된 작성기에 대한 로컬 쓰기 및 로컬 읽기 액세스를 가능하게 하는 패턴을 개략적으로 설명합니다.

## <a id="ExampleScenario"></a>콘텐츠 게시 - 예제 시나리오
에 대해 살펴보겠습니다 실제 시나리오 toodescribe 어떻게 Azure Cosmos DB와 함께 전 세계적으로 분산된 region 다중/마스터 다중 읽기/쓰기 패턴을 사용할 수 있습니다. Azure Cosmos DB를 기반으로 하는 콘텐츠 게시 플랫폼이 있다고 가정합시다. 이 플랫폼이 게시자와 소비자 모두에게 훌륭한 사용자 환경을 제공하기 위해 충족해야 하는 몇 가지 요구 사항이 있습니다.

* 작성자와 구독자는 hello world 퍼져 
* 작성자 (쓰기) 문서 tootheir 로컬 (가장 가까운) 영역을 게시 해야 합니다.
* 작성자 포함 판독기/구독자가 문서를 hello 전 세계에 분산 되어 있습니다. 
* 새 문서가 게시되면 구독자가 알림을 받아야 합니다.
* 구독자는 자신의 로컬 영역에서 수 tooread 문서 여야 합니다. 또한 수 tooadd 검토 toothese 문서 수 있어야 합니다. 
* Hello 아티클의 hello 작성자를 포함 한 모든 사용자 수 보기 로컬 영역에서 연결 된 tooarticles 검토 hello 모두 있어야 합니다. 

소비자와 수십억 개의 문서를 가진 게시자의 수백만 가정 액세스의 위치 정확성을 보장 하기 함께 범위의 tooconfront hello 문제 했으므로 곧 합니다. 대부분의 확장성 문제와 마찬가지로 hello 솔루션은 적절 한 분할 전략에 있습니다. 다음으로, 보겠습니다 toomodel 기사, 검토 및 문서로 알림을 Azure Cosmos DB 계정 구성 방법 확인 하 고 데이터 액세스 계층을 구현 합니다. 

분할 및 파티션 키에 대 한 자세한 toolearn, 원하는 경우 참조 [분할 및 Azure Cosmos DB에 크기 조정](partition-data.md)합니다.

## <a id="ModelingNotifications"></a>알림 모델링
알림은 데이터 피드 특정 tooa 사용자입니다. 따라서 알림 문서에 대 한 액세스 패턴 hello는 항상 단일 사용자의 hello 컨텍스트에서입니다. 예를 들어 "알림 tooa 사용자 post" 또는 "지정된 된 사용자에 대 한 모든 알림을 가져올" 것 있습니다. 따라서이 형식은 대 한 분할 키의 효율적인 옵션 hello `UserId`합니다.

    class Notification 
    { 
        // Unique ID for Notification. 
        public string Id { get; set; }

        // hello user Id for which notification is addressed to. 
        public string UserId { get; set; }

        // hello partition Key for hello resource. 
        public string PartitionKey 
        { 
            get 
            { 
                return this.UserId; 
            }
        }

        // Subscription for which this notification is raised. 
        public string SubscriptionFilter { get; set; }

        // Subject of hello notification. 
        public string ArticleId { get; set; } 
    }

## <a id="ModelingSubscriptions"></a>구독 모델링
관심 있는 문서의 특정 범주나 특정 게시자처럼 다양한 조건에 대한 구독을 만들 수 있습니다. 따라서 hello `SubscriptionFilter` 파티션 키에 대 한 것이 좋습니다.

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

## <a id="ModelingArticles"></a>문서 모델링
아티클의 알림을 통해 식별 되 면 후속 쿼리는 일반적으로 기반 hello `Article.Id`합니다. 선택 `Article.Id` 파티션으로 hello 키 하므로 제공 hello Azure Cosmos DB 컬렉션 내의 문서를 저장 하기 위한 최선의 배포 합니다. 

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
        
        // Author of hello article
        public string Author { get; set; }

        // Category/genre of hello article
        public string Category { get; set; }

        // Tags associated with hello article
        public string[] Tags { get; set; }

        // Title of hello article
        public string Title { get; set; }
        
        //... 
    }

## <a id="ModelingReviews"></a>리뷰 모델링
문서와 같은 검토 대부분 작성 되 고 읽을 hello 문서의 합니다. 파티션 키로 `ArticleId`를 선택하면 가장 적절하게 분산될 뿐 아니라 문서와 연결된 리뷰를 효율적으로 액세스할 수 있습니다. 

    class Review 
    { 
        // Unique ID for Review 
        public string Id { get; set; }

        // Article Id of hello review 
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

## <a id="DataAccessMethods"></a>데이터 액세스 계층 메서드
이제 살펴보겠습니다 hello 기본 데이터 액세스 방법을 tooimplement이 필요 합니다. 다음은 hello 메서드의 hello 목록 `ContentPublishDatabase` 필요:

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <a id="Architecture"></a>Azure Cosmos DB 계정 구성
로컬 tooguarantee 읽기 및 쓰기, 파티션 키에 뿐 아니라 데이터를 분할 해야 하 म 하지만 또한 지역으로 hello 지리적 액세스 패턴에 기반 합니다. hello 모델은 각 지역에 대 한 지리적 복제 Azure Cosmos DB 데이터베이스 계정에 기반 합니다. 예를 들어 지역이 두 개라면 다중 지역 쓰기에 대한 설정은 다음과 같습니다.

| 계정 이름 | 쓰기 지역 | 읽기 지역 |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

hello 다음 다이어그램은이 설치 프로그램을 일반 응용 프로그램에서 읽기 및 쓰기를 수행 하는 방법을 보여 줍니다.

![Azure Cosmos DB 다중 마스터 아키텍처](./media/multi-region-writers/multi-master.png)

다음은 tooinitialize hello에서 실행 되는 DAL에서 클라이언트 hello 하는 방법을 보여 주는 코드 조각 `West US` 영역입니다.
    
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

Hello 설치 앞로 hello 데이터 액세스 계층에는 모든 쓰기 toohello 로컬 계정 배포 되는 위치에 따라 전달할 수 있습니다. 읽기는 두 계정 뷰에서 tooget hello 글로벌 데이터의 읽기에 의해 수행 됩니다. 이 방법은 tooas 필요에 따라 많은 영역을 확장 합니다. 예를 들어 다음은 세 개 지역에 대한 설정입니다.

| 계정 이름 | 쓰기 지역 | 읽기 지역 1 | 읽기 지역 2 |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <a id="DataAccessImplementation"></a>데이터 액세스 계층 구현
이제 두 개의 쓰기 가능한 영역으로 응용 프로그램에 대 한 hello 데이터 액세스 계층 (DAL)의 hello 구현에 살펴보겠습니다. hello DAL hello 다음 단계를 구현 해야 합니다.

* 각 계정에 대해 여러 `DocumentClient` 인스턴스를 만듭니다. 지역이 두 개이므로 각 DAL 인스턴스는 `writeClient` 하나와 `readClient` 하나를 갖습니다. 
* 에 대 한 hello 끝점 구성 hello 응용 프로그램의 배포 된 hello 지역에 따라, `writeclient` 및 `readClient`합니다. 예를 들어에 배포 된 hello DAL `West US` 사용 하 여 `contentpubdatabase-usa.documents.azure.com` 쓰기를 수행 하기 위한 합니다. 에 배포 된 hello DAL `NorthEurope` 사용 하 여 `contentpubdatabase-europ.documents.azure.com` 쓰기에 대 한 합니다.

설치 프로그램을 이전 hello로 hello 데이터 액세스 메서드를 구현할 수 있습니다. Operations 전달 hello 쓰기 toohello 해당 쓰기 `writeClient`합니다.

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

에 대 한 알림 및 검토 hello 다음 코드 조각에에서 나와 있는 것 처럼 영역과 union hello 결과에서 읽어 해야 있습니다.

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

따라서 적절한 분할 키와 정적 계정 기반 분할을 선택하면 Azure Cosmos DB를 사용하여 다중 지역 로컬 쓰기 및 읽기를 구현할 수 있습니다.

## <a id="NextSteps"></a>다음 단계
이 문서에서는 콘텐츠 게시를 샘플 시나리오로 사용하여 전 세계에 분산된 다중 지역 읽기 쓰기 패턴을 Azure Cosmos DB와 함께 사용하는 방법을 설명했습니다.

* Azure Cosmos DB에서 [전역 배포](distribute-data-globally.md)를 지원하는 방법 알아보기
* [Azure Cosmos DB의 자동 및 수동 장애 조치(failover)](regional-failover.md) 알아보기
* [Azure Cosmos DB를 통한 전역 일관성](consistency-levels.md)에 대한 자세한 정보
* Hello를 사용 하 여 여러 영역을 사용 하 여 개발 [Azure Cosmos DB-DocumentDB API](tutorial-global-distribution-documentdb.md)
* Hello를 사용 하 여 여러 영역을 사용 하 여 개발 [Azure Cosmos DB-MongoDB API](tutorial-global-distribution-MongoDB.md)
* Hello를 사용 하 여 여러 영역을 사용 하 여 개발 [Azure Cosmos DB-테이블 API](tutorial-global-distribution-table.md)
