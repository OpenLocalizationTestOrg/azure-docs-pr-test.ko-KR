---
title: "TTL(Time To Live)을 사용하여 Azure Cosmos DB의 데이터 만료 | Microsoft Docs"
description: "TTL을 사용하여 Microsoft Azure Cosmos DB는 일정 기간 후에 시스템에서 문서를 자동으로 삭제하는 기능을 제공합니다."
services: cosmos-db
documentationcenter: 
keywords: TTL(Time to live)
author: arramac
manager: jhubbard
editor: 
ms.assetid: 25fcbbda-71f7-414a-bf57-d8671358ca3f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 6f1c43ca0113dc7579b0fc3743d3314c16ce78a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-to-live"></a><span data-ttu-id="b4e34-104">TTL(Time To Live)을 사용하여 자동으로 Azure Cosmos DB 컬렉션의 데이터 만료</span><span class="sxs-lookup"><span data-stu-id="b4e34-104">Expire data in Azure Cosmos DB collections automatically with time to live</span></span>
<span data-ttu-id="b4e34-105">응용 프로그램은 방대한 양의 데이터을 생성하고 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-105">Applications can produce and store vast amounts of data.</span></span> <span data-ttu-id="b4e34-106">컴퓨터에서 생성한 이벤트 데이터, 로그 및 사용자 세션 정보와 같은 이 데이터 중 일부는 한정된 기간에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-106">Some of this data, like machine generated event data, logs, and user session information is only useful for a finite period of time.</span></span> <span data-ttu-id="b4e34-107">데이터가 응용 프로그램의 요구를 넘게 되면 이 데이터를 삭제하고 응용 프로그램의 저장소 요구를 줄이는 것이 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-107">Once the data becomes surplus to the needs of the application it is safe to purge this data and reduce the storage needs of an application.</span></span>

<span data-ttu-id="b4e34-108">"time to live" 또는 TTL을 사용하여 Microsoft Azure Cosmos DB는 일정 기간 후에 데이터베이스에서 문서를 자동으로 삭제하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-108">With "time to live" or TTL, Microsoft Azure Cosmos DB provides the ability to have documents automatically purged from the database after a period of time.</span></span> <span data-ttu-id="b4e34-109">기본 TTL(Time to live)을 컬렉션 수준에서 설정할 수 있고 문서별로 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-109">The default time to live can be set at the collection level, and overridden on a per-document basis.</span></span> <span data-ttu-id="b4e34-110">TTL을 컬렉션 기본값으로 설정하거나 문서 수준에서 설정하면 Cosmos DB는 마지막으로 수정된 이후 해당 기간(초) 후에 존재하는 문서를 자동으로 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-110">Once TTL is set, either as a collection default or at a document level, Cosmos DB will automatically remove documents that exist after that period of time, in seconds, since they were last modified.</span></span>

<span data-ttu-id="b4e34-111">Cosmos DB의 TTL(Time To Live)은 문서가 마지막으로 수정된 시간을 기준으로 오프셋을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-111">Time to live in Cosmos DB uses an offset against when the document was last modified.</span></span> <span data-ttu-id="b4e34-112">이렇게 하려면 모든 문서에 있는 `_ts` 필드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-112">To do this it uses the `_ts` field which exists on every document.</span></span> <span data-ttu-id="b4e34-113">_ts 필드는 날짜 및 시간을 나타내는 Unix 스타일 Epoch 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-113">The _ts field is a unix-style epoch timestamp representing the date and time.</span></span> <span data-ttu-id="b4e34-114">`_ts` 필드는 문서가 수정될 때마다 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-114">The `_ts` field is updated every time a document is modified.</span></span> 

## <a name="ttl-behavior"></a><span data-ttu-id="b4e34-115">TTL 동작</span><span class="sxs-lookup"><span data-stu-id="b4e34-115">TTL behavior</span></span>
<span data-ttu-id="b4e34-116">TTL 기능은 컬렉션 수준 및 문서 수준 등 두 가지 수준으로 TTL 속성에 의해 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-116">The TTL feature is controlled by TTL properties at two levels - the collection level and the document level.</span></span> <span data-ttu-id="b4e34-117">값은 초 단위로 설정되고 문서가 마지막으로 수정되는 `_ts` 필드에서 델타로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-117">The values are set in seconds and are treated as a delta from the `_ts` that the document was last modified at.</span></span>

1. <span data-ttu-id="b4e34-118">컬렉션에 대한 DefaultTTL</span><span class="sxs-lookup"><span data-stu-id="b4e34-118">DefaultTTL for the collection</span></span>
   
   * <span data-ttu-id="b4e34-119">누락(또는 null로 설정)된 경우 문서는 자동으로 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-119">If missing (or set to null), documents are not deleted automatically.</span></span>
   * <span data-ttu-id="b4e34-120">표시되고 현재 값이 "-1" = 무한인 경우 문서는 기본적으로 만료되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-120">If present and the value is "-1" = infinite – documents don’t expire by default</span></span>
   * <span data-ttu-id="b4e34-121">표시되고 현재 값이 숫자("n")인 경우 문서는 마지막으로 수정되고 "n"초 후에 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-121">If present and the value is some number ("n") – documents expire "n” seconds after last modification</span></span>
2. <span data-ttu-id="b4e34-122">문서에 대한 TTL:</span><span class="sxs-lookup"><span data-stu-id="b4e34-122">TTL for the documents:</span></span> 
   
   * <span data-ttu-id="b4e34-123">속성은 DefaultTTL이 상위 컬렉션에 있는 경우에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-123">Property is applicable only if DefaultTTL is present for the parent collection.</span></span>
   * <span data-ttu-id="b4e34-124">상위 컬렉션에 대한 DefaultTTL 값을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-124">Overrides the DefaultTTL value for the parent collection.</span></span>

<span data-ttu-id="b4e34-125">문서가 만료되는 즉시(`ttl` + `_ts` >= 현재 서버 시간) 문서는 "만료"된 것으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-125">As soon as the document has expired (`ttl` + `_ts` >= current server time), the document is marked as "expired”.</span></span> <span data-ttu-id="b4e34-126">이 시간 이후에 어떤 작업도 이러한 문서에 허용되지 않으며 수행되는 쿼리 결과에서 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-126">No operation will be allowed on these documents after this time and they will be excluded from the results of any queries performed.</span></span> <span data-ttu-id="b4e34-127">문서는 시스템에서 물리적으로 삭제되고 나중에 선택적으로 백그라운드에서 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-127">The documents are physically deleted in the system, and are deleted in the background opportunistically at a later time.</span></span> <span data-ttu-id="b4e34-128">이는 컬렉션 예산에서 [RU(요청 단위)](request-units.md) 를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-128">This does not consume any [Request Units (RUs)](request-units.md) from the collection budget.</span></span>

<span data-ttu-id="b4e34-129">위의 논리는 다음 행렬에 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-129">The above logic can be shown in the following matrix:</span></span>

|  | <span data-ttu-id="b4e34-130">컬렉션에서 DefaultTTL 누락/설정되지 않음</span><span class="sxs-lookup"><span data-stu-id="b4e34-130">DefaultTTL missing/not set on the collection</span></span> | <span data-ttu-id="b4e34-131">컬렉션에서 DefaultTTL = -1</span><span class="sxs-lookup"><span data-stu-id="b4e34-131">DefaultTTL = -1 on collection</span></span> | <span data-ttu-id="b4e34-132">컬렉션에서 DefaultTTL = "n"</span><span class="sxs-lookup"><span data-stu-id="b4e34-132">DefaultTTL = "n" on collection</span></span> |
| --- |:--- |:--- |:--- |
| <span data-ttu-id="b4e34-133">문서에서 TTL 누락</span><span class="sxs-lookup"><span data-stu-id="b4e34-133">TTL Missing on document</span></span> |<span data-ttu-id="b4e34-134">문서와 컬렉션에 TTL의 개념이 없으므로 문서 수준에서 아무 것도 재정의할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-134">Nothing to override at document level since both the document and collection have no concept of TTL.</span></span> |<span data-ttu-id="b4e34-135">이 컬렉션에서 만료되는 문서가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-135">No documents in this collection will expire.</span></span> |<span data-ttu-id="b4e34-136">간격 n이 경과하면 이 컬렉션에서 문서가 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-136">The documents in this collection will expire when interval n elapses.</span></span> |
| <span data-ttu-id="b4e34-137">문서에서 TTL = -1</span><span class="sxs-lookup"><span data-stu-id="b4e34-137">TTL = -1 on document</span></span> |<span data-ttu-id="b4e34-138">문서가 재정의할 수 있는 DefaultTTL 속성을 수집이 정의하지 않으므로 문서 수준에서 아무 것도 재정의되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-138">Nothing to override at the document level since the collection doesn’t define the DefaultTTL property that a document can override.</span></span> <span data-ttu-id="b4e34-139">문서에서 TTL은 시스템에 의해 해석되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-139">TTL on a document is un-interpreted by the system.</span></span> |<span data-ttu-id="b4e34-140">이 컬렉션에서 만료되는 문서가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-140">No documents in this collection will expire.</span></span> |<span data-ttu-id="b4e34-141">이 컬렉션에서 TTL = -1인 문서는 만료되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-141">The document with TTL=-1 in this collection will never expire.</span></span> <span data-ttu-id="b4e34-142">다른 모든 문서는 "n" 간격 후에 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-142">All other documents will expire after "n" interval.</span></span> |
| <span data-ttu-id="b4e34-143">문서에서 TTL = n</span><span class="sxs-lookup"><span data-stu-id="b4e34-143">TTL = n on document</span></span> |<span data-ttu-id="b4e34-144">문서 수준에서 아무 것도 재정의하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-144">Nothing to override at the document level.</span></span> <span data-ttu-id="b4e34-145">문서에서 TTL은 시스템에 의해 해석되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-145">TTL on a document in un-interpreted by the system.</span></span> |<span data-ttu-id="b4e34-146">TTL = n인 문서는 간격 n(초) 후에 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-146">The document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="b4e34-147">다른 문서는 간격 -1을 상속하며 만료되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-147">Other documents will inherit interval of -1 and never expire.</span></span> |<span data-ttu-id="b4e34-148">TTL = n인 문서는 간격 n(초) 후에 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-148">The document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="b4e34-149">다른 문서는 컬렉션에서 "n" 간격을 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-149">Other documents will inherit "n" interval from the collection.</span></span> |

## <a name="configuring-ttl"></a><span data-ttu-id="b4e34-150">TTL 구성</span><span class="sxs-lookup"><span data-stu-id="b4e34-150">Configuring TTL</span></span>
<span data-ttu-id="b4e34-151">기본적으로 TTL(Time To Live)은 모든 Cosmos DB 컬렉션 및 문서에서 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-151">By default, time to live is disabled by default in all Cosmos DB collections and on all documents.</span></span>

## <a name="enabling-ttl"></a><span data-ttu-id="b4e34-152">TTL 사용</span><span class="sxs-lookup"><span data-stu-id="b4e34-152">Enabling TTL</span></span>
<span data-ttu-id="b4e34-153">컬렉션 또는 컬렉션 내 문서에서 TTL을 사용하려면 컬렉션의 DefaultTTL 속성을 -1 또는 0이 아닌 양수로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-153">To enable TTL on a collection, or the documents within a collection, you need to set the DefaultTTL property of a collection to either -1 or a non-zero positive number.</span></span> <span data-ttu-id="b4e34-154">DefaultTTL을 -1로 설정하면 기본적으로 컬렉션에 있는 모든 문서가 계속 존재하지만 Cosmos DB 서비스는 이 기본값을 재정의한 문서에 대해 이 컬렉션을 모니터링해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-154">Setting the DefaultTTL to -1 means that by default all documents in the collection will live forever but the Cosmos DB service should monitor this collection for documents that have overridden this default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a><span data-ttu-id="b4e34-155">컬렉션에서 기본 TTL 구성</span><span class="sxs-lookup"><span data-stu-id="b4e34-155">Configuring default TTL on a collection</span></span>
<span data-ttu-id="b4e34-156">기본 수명을 컬렉션 수준에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-156">You are able to configure a default time to live at a collection level.</span></span> <span data-ttu-id="b4e34-157">컬렉션에서 TTL을 설정하려면 문서(`_ts`)의 타임스탬프를 마지막으로 수정한 이후 컬렉션에 있는 모든 문서를 만료할 기간(초)을 나타내는 0이 아닌 양수 값을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-157">To set the TTL on a collection, you need to provide a non-zero positive number that indicates the period, in seconds, to expire all documents in the collection after the last modified timestamp of the document (`_ts`).</span></span> <span data-ttu-id="b4e34-158">또는 기본값을 -1로 설정할 수 있습니다. 즉, 컬렉션에 삽입된 모든 문서가 기본적으로 영원히 지속됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-158">Or, you can set the default to -1, which implies that all documents inserted in to the collection will live indefinitely by default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a><span data-ttu-id="b4e34-159">문서에서 TTL 설정</span><span class="sxs-lookup"><span data-stu-id="b4e34-159">Setting TTL on a document</span></span>
<span data-ttu-id="b4e34-160">컬렉션에서 기본 TTL을 설정하는 것 외에도 특정 문서 수준에서 TTL을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-160">In addition to setting a default TTL on a collection you can set specific TTL at a document level.</span></span> <span data-ttu-id="b4e34-161">이렇게 하면 컬렉션의 기본값을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-161">Doing this will override the default of the collection.</span></span>

* <span data-ttu-id="b4e34-162">문서에서 TTL을 설정하려면 문서(`_ts`)의 타임스탬프를 마지막으로 수정한 이후 문서를 만료할 기간(초)을 나타내는 0이 아닌 양수 값을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-162">To set the TTL on a document, you need to provide a non-zero positive number which indicates the period, in seconds, to expire the document after the last modified timestamp of the document (`_ts`).</span></span>
* <span data-ttu-id="b4e34-163">문서에 TTL 필드가 없는 경우 컬렉션의 기본값이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-163">If a document has no TTL field, then the default of the collection will apply.</span></span>
* <span data-ttu-id="b4e34-164">컬렉션 수준에서 TTL을 사용하지 않으면 문서에서 TTL 필드는 컬렉션에 다시 TTL을 사용할 때까지 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-164">If TTL is disabled at the collection level, the TTL field on the document will be ignored until TTL is enabled again on the collection.</span></span>

<span data-ttu-id="b4e34-165">문서에서 TTL 만료를 설정하는 방법을 보여 주는 코드 조각은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-165">Here's a snippet showing how to set the TTL expiration on a document:</span></span>

    // Include a property that serializes to "ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used to set expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set the value to the expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a><span data-ttu-id="b4e34-166">기존 문서에서 TTL 확장</span><span class="sxs-lookup"><span data-stu-id="b4e34-166">Extending TTL on an existing document</span></span>
<span data-ttu-id="b4e34-167">문서에 쓰기 작업을 수행하여 TTL을 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-167">You can reset the TTL on a document by doing any write operation on the document.</span></span> <span data-ttu-id="b4e34-168">이렇게 하여 `_ts`를 현재 시간으로 설정하면 문서에 대한 만료 카운트다운이 `ttl`에서 설정한 대로 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-168">Doing this will set the `_ts` to the current time, and the countdown to the document expiry, as set by the `ttl`, will begin again.</span></span> <span data-ttu-id="b4e34-169">문서의 `ttl`을 변경하려는 경우 설정할 수 있는 다른 필드에서처럼 필드를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-169">If you wish to change the `ttl` of a document, you can update the field as you can do with any other settable field.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time to live
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a><span data-ttu-id="b4e34-170">문서에서 TTL 제거</span><span class="sxs-lookup"><span data-stu-id="b4e34-170">Removing TTL from a document</span></span>
<span data-ttu-id="b4e34-171">문서에서 TTL을 설정했지만 해당 문서가 더 이상 만료되지 않게 하려면 문서를 검색하고 TTL 필드를 제거하여 서버에 있는 문서를 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-171">If a TTL has been set on a document and you no longer want that document to expire, then you can retrieve the document, remove the TTL field and replace the document on the server.</span></span> <span data-ttu-id="b4e34-172">문서에서 TTL 필드를 제거하면 컬렉션의 기본값이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-172">When the TTL field is removed from the document, the default of the collection will be applied.</span></span> <span data-ttu-id="b4e34-173">문서가 만료되지 않도록 중지하고 컬렉션에서 상속하지 않으려면 TTL 값을 -1로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-173">To stop a document from expiring and not inherit from the collection then you need to set the TTL value to -1.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit the default TTL of the collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a><span data-ttu-id="b4e34-174">TTL 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="b4e34-174">Disabling TTL</span></span>
<span data-ttu-id="b4e34-175">컬렉션에서 TTL을 사용하지 않고 만료된 문서를 찾는 백그라운드 프로세스를 중지하려면 컬렉션에서 DefaultTTL 속성을 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-175">To disable TTL entirely on a collection and stop the background process from looking for expired documents the DefaultTTL property on the collection should be deleted.</span></span> <span data-ttu-id="b4e34-176">이 속성을 삭제하는 것은 -1로 설정하는 것과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-176">Deleting this property is different from setting it to -1.</span></span> <span data-ttu-id="b4e34-177">-1로 설정하면 컬렉션에 추가된 새 문서는 계속 존재하게 되지만 컬렉션에 있는 특정 문서에서 이를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-177">Setting to -1 means new documents added to the collection will live forever but you can override this on specific documents in the collection.</span></span> <span data-ttu-id="b4e34-178">컬렉션에서 이 속성을 완전히 제거하면 이전의 기본값을 명시적으로 재정의한 문서가 있더라도 문서가 만료되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-178">Removing this property entirely from the collection means that no documents will expire, even if there are documents that have explicitly overridden a previous default.</span></span>

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a><span data-ttu-id="b4e34-179">FAQ</span><span class="sxs-lookup"><span data-stu-id="b4e34-179">FAQ</span></span>
<span data-ttu-id="b4e34-180">**TTL의 비용은 얼마인가요?**</span><span class="sxs-lookup"><span data-stu-id="b4e34-180">**What will TTL cost me?**</span></span>

<span data-ttu-id="b4e34-181">문서에 TTL을 설정하는 추가 비용은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-181">There is no additional cost to setting a TTL on a document.</span></span>

<span data-ttu-id="b4e34-182">**TTL이 실행되면 문서를 삭제하는 데 얼마나 걸리나요?**</span><span class="sxs-lookup"><span data-stu-id="b4e34-182">**How long will it take to delete my document once the TTL is up?**</span></span>

<span data-ttu-id="b4e34-183">문서는 TTL이 실행되면 즉시 만료되고 CRUD 또는 쿼리 API를 통해 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-183">The documents are expired immediately once the TTL is up, and will not be accessible via CRUD or query APIs.</span></span> 

<span data-ttu-id="b4e34-184">**문서에서 TTL은 RU 요금에 영향을 주나요?**</span><span class="sxs-lookup"><span data-stu-id="b4e34-184">**Will TTL on a document have any impact on RU charges?**</span></span>

<span data-ttu-id="b4e34-185">아니요, Cosmos DB에서 TTL을 통해 만료된 문서를 삭제할 경우 RU 요금에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-185">No, there will be no impact on RU charges for deletions of expired documents via TTL in Cosmos DB.</span></span>

<span data-ttu-id="b4e34-186">**TTL 기능이 전체 문서에 적용되나요, 또는 개별 문서 속성 값을 만료할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="b4e34-186">**Does the TTL feature only apply to entire documents, or can I expire individual document property values?**</span></span>

<span data-ttu-id="b4e34-187">TTL은 문서 전체에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-187">TTL applies to the entire document.</span></span> <span data-ttu-id="b4e34-188">문서의 일부만 만료하고 싶다면 "링크된" 별도 문서의 기본 문서에서 부분을 추출한 다음 추출된 문서에서 TTL을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-188">If you would like to expire just a portion of a document, then it is recommended that you extract the portion from the main document in to a separate "linked” document and then use TTL on that extracted document.</span></span>

<span data-ttu-id="b4e34-189">**TTL 기능에는 특정 인덱싱 요구 사항이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="b4e34-189">**Does the TTL feature have any specific indexing requirements?**</span></span>

<span data-ttu-id="b4e34-190">예.</span><span class="sxs-lookup"><span data-stu-id="b4e34-190">Yes.</span></span> <span data-ttu-id="b4e34-191">컬렉션에는 일관성 또는 지연 중 하나에 대한 [인덱싱 정책 집합](indexing-policies.md) 이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-191">The collection must have [indexing policy set](indexing-policies.md) to either Consistent or Lazy.</span></span> <span data-ttu-id="b4e34-192">인덱싱 설정을 사용하여 컬렉션에서 DefaultTTL을 없음으로 설정하면 DefaultTTL이 이미 설정되어 있는 컬렉션에서 인덱싱을 해제하는 것과 같은 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b4e34-192">Trying to set DefaultTTL on a collection with indexing set to None will result in an error, as will trying to turn off indexing on a collection that has a DefaultTTL already set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4e34-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4e34-193">Next steps</span></span>
<span data-ttu-id="b4e34-194">Azure Cosmos DB에 대한 자세한 내용은 서비스 [*설명서*](https://azure.microsoft.com/documentation/services/cosmos-db/) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4e34-194">To learn more about Azure Cosmos DB, refer to the service [*documentation*](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span>

