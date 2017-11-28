---
title: "분할된 Azure SQL Database 쿼리 | Microsoft Docs"
description: "분할된 데이터베이스간의 쿼리를 실행할 때는 탄력적 데이터베이스 클라이언트 라이브러리를 사용합니다."
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: a4379c15-f213-4026-ab6f-a450ee9d5758
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2016
ms.author: torsteng
ms.openlocfilehash: 67bcb3c7fe33341103f28bc70e8cc2acbb924cae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="multi-shard-querying"></a><span data-ttu-id="e2546-103">다중 분할된 데이터베이스 쿼리</span><span class="sxs-lookup"><span data-stu-id="e2546-103">Multi-shard querying</span></span>
## <a name="overview"></a><span data-ttu-id="e2546-104">개요</span><span class="sxs-lookup"><span data-stu-id="e2546-104">Overview</span></span>
<span data-ttu-id="e2546-105">[탄력적 데이터베이스 도구](sql-database-elastic-scale-introduction.md)를 사용하면 분할된 데이터베이스 솔루션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-105">With the [Elastic Database tools](sql-database-elastic-scale-introduction.md), you can create sharded database solutions.</span></span> <span data-ttu-id="e2546-106">**다중 분할된 데이터베이스 쿼리** 는 여러 분할된 데이터베이스 간에 걸친 쿼리를 실행해야 하는 데이터 컬렉션/보고와 같은 작업에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-106">**Multi-shard querying** is used for tasks such as data collection/reporting that require running a query that stretches across several shards.</span></span> <span data-ttu-id="e2546-107">(이 쿼리는 단일 분할된 데이터베이스에서 모든 작업을 수행하는 [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md)과 대조됩니다.)</span><span class="sxs-lookup"><span data-stu-id="e2546-107">(Contrast this to [data-dependent routing](sql-database-elastic-scale-data-dependent-routing.md), which performs all work on a single shard.)</span></span> 

1. <span data-ttu-id="e2546-108">[**TryGetRangeShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), [**TryGetListShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx) 또는 [**GetShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) 메서드를 사용하여 [**RangeShardMap**](https://msdn.microsoft.com/library/azure/dn807318.aspx) 또는 [**ListShardMap**](https://msdn.microsoft.com/library/azure/dn807370.aspx)을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-108">Get a [**RangeShardMap**](https://msdn.microsoft.com/library/azure/dn807318.aspx) or [**ListShardMap**](https://msdn.microsoft.com/library/azure/dn807370.aspx) using the [**TryGetRangeShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), the [**TryGetListShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), or the [**GetShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) method.</span></span> <span data-ttu-id="e2546-109">[**ShardMapManager 생성**](sql-database-elastic-scale-shard-map-management.md#constructing-a-shardmapmanager) 및 [**RangeShardMap 또는 ListShardMap 가져오기**](sql-database-elastic-scale-shard-map-management.md#get-a-rangeshardmap-or-listshardmap)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e2546-109">See [**Constructing a ShardMapManager**](sql-database-elastic-scale-shard-map-management.md#constructing-a-shardmapmanager) and [**Get a RangeShardMap or ListShardMap**](sql-database-elastic-scale-shard-map-management.md#get-a-rangeshardmap-or-listshardmap).</span></span>
2. <span data-ttu-id="e2546-110">**[MultiShardConnection](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardconnection.aspx)** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-110">Create a **[MultiShardConnection](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardconnection.aspx)** object.</span></span>
3. <span data-ttu-id="e2546-111">**[MultiShardCommand](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.aspx)**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-111">Create a **[MultiShardCommand](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.aspx)**.</span></span> 
4. <span data-ttu-id="e2546-112">**[CommandText 속성](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.commandtext.aspx#P:Microsoft.Azure.SqlDatabase.ElasticScale.Query.MultiShardCommand.CommandText)**을 T-SQL 명령으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-112">Set the **[CommandText property](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.commandtext.aspx#P:Microsoft.Azure.SqlDatabase.ElasticScale.Query.MultiShardCommand.CommandText)** to a T-SQL command.</span></span>
5. <span data-ttu-id="e2546-113">**[ExecuteReader 메서드](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.executereader.aspx)**를 호출하여 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-113">Execute the command by calling the **[ExecuteReader method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.executereader.aspx)**.</span></span>
6. <span data-ttu-id="e2546-114">**[MultiShardDataReader 클래스](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multisharddatareader.aspx)**를 사용하여 결과를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-114">View the results using the **[MultiShardDataReader class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multisharddatareader.aspx)**.</span></span> 

## <a name="example"></a><span data-ttu-id="e2546-115">예제</span><span class="sxs-lookup"><span data-stu-id="e2546-115">Example</span></span>
<span data-ttu-id="e2546-116">다음 코드는 **myShardMap** 이라는 *ShardMap*을 사용하는 다중 분할된 데이터베이스 쿼리를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-116">The following code illustrates the usage of multi-shard querying using a given **ShardMap** named *myShardMap*.</span></span> 

    using (MultiShardConnection conn = new MultiShardConnection( 
                                        myShardMap.GetShards(), 
                                        myShardConnectionString) 
          ) 
    { 
    using (MultiShardCommand cmd = conn.CreateCommand())
           { 
            cmd.CommandText = "SELECT c1, c2, c3 FROM ShardedTable"; 
            cmd.CommandType = CommandType.Text; 
            cmd.ExecutionOptions = MultiShardExecutionOptions.IncludeShardNameColumn; 
            cmd.ExecutionPolicy = MultiShardExecutionPolicy.PartialResults; 

            using (MultiShardDataReader sdr = cmd.ExecuteReader()) 
                { 
                    while (sdr.Read())
                        { 
                            var c1Field = sdr.GetString(0); 
                            var c2Field = sdr.GetFieldValue<int>(1); 
                            var c3Field = sdr.GetFieldValue<Int64>(2);
                        } 
                 } 
           } 
    } 


<span data-ttu-id="e2546-117">주요 차이점은 다중 분할된 데이터베이스 연결을 생성한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-117">A key difference is the construction of multi-shard connections.</span></span> <span data-ttu-id="e2546-118">여기서 **SqlConnection**은 단일 데이터베이스에서 작동하고, **MultiShardConnection**은 ***분할된 데이터베이스 컬렉션***을 입력으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-118">Where **SqlConnection** operates on a single database, the **MultiShardConnection** takes a ***collection of shards*** as its input.</span></span> <span data-ttu-id="e2546-119">분할된 데이터베이스 맵에서 분할된 데이터베이스의 컬렉션을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-119">Populate the collection of shards from a shard map.</span></span> <span data-ttu-id="e2546-120">그런 다음 쿼리는 **UNION ALL** 의미 체계를 사용하여 분할된 데이터베이스 컬렉션에서 실행되어 전반적인 단일 결과를 조합합니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-120">The query is then executed on the collection of shards using **UNION ALL** semantics to assemble a single overall result.</span></span> <span data-ttu-id="e2546-121">필요에 따라 행이 속한 분할된 데이터베이스의 이름을 명령에서 **ExecutionOptions** 속성을 사용하여 출력에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-121">Optionally, the name of the shard where the row originates from can be added to the output using the **ExecutionOptions** property on command.</span></span> 

<span data-ttu-id="e2546-122">**myShardMap.GetShards()**호출을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="e2546-122">Note the call to **myShardMap.GetShards()**.</span></span> <span data-ttu-id="e2546-123">이 메서드는 분할된 데이터베이스 맵에서 모든 분할된 데이터베이스를 검색하고 모든 관련된 데이터베이스간에 쿼리를 실행하는 간편한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-123">This method retrieves all shards from the shard map and provides an easy way to run a query across all relevant databases.</span></span> <span data-ttu-id="e2546-124">다중 분할된 데이터베이스 쿼리에 대한 분할된 데이터베이스의 컬렉션은 **myShardMap.GetShards()**호출에서 반환된 컬렉션에 대해 LINQ 쿼리를 수행하여 구체화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-124">The collection of shards for a multi-shard query can be refined further by performing a LINQ query over the collection returned from the call to **myShardMap.GetShards()**.</span></span> <span data-ttu-id="e2546-125">부분 결과 정책과 함께, 다중 분할된 데이터베이스 쿼리의 현재 기능은 수십에서 수백 개의 분할된 데이터베이스에 대해 원활하게 작동하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-125">In combination with the partial results policy, the current capability in multi-shard querying has been designed to work well for tens up to hundreds of shards.</span></span>

<span data-ttu-id="e2546-126">다중 분할된 데이터베이스 쿼리의 제한 사항은 현재 쿼리가 실행되는 shardlet 및 분할된 데이터베이스에 대한 유효성 검사가 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-126">A limitation with multi-shard querying is currently the lack of validation for shards and shardlets that are queried.</span></span> <span data-ttu-id="e2546-127">데이터 종속 라우팅이 쿼리 시 지정된 분할된 데이터베이스가 분할된 데이터베이스 맵의 일부인지 확인하며, 다중 분할된 데이터베이스 쿼리가 이 검사를 수행하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-127">While data-dependent routing verifies that a given shard is part of the shard map at the time of querying, multi-shard queries do not perform this check.</span></span> <span data-ttu-id="e2546-128">따라서 분할된 데이터베이스 맵에서 제거된 데이터베이스에서 다중 분할된 데이터베이스 쿼리가 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-128">This can lead to multi-shard queries running on databases that have  been removed from the shard map.</span></span>

## <a name="multi-shard-queries-and-split-merge-operations"></a><span data-ttu-id="e2546-129">다중 분할된 데이터베이스 쿼리 및 분할/병합 작업</span><span class="sxs-lookup"><span data-stu-id="e2546-129">Multi-shard queries and split-merge operations</span></span>
<span data-ttu-id="e2546-130">다중 분할된 데이터베이스 쿼리는 쿼리되는 데이터베이스의 shardlet이 지속적인 분할/병합 작업에 참여하는지 여부를 확인하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-130">Multi-shard queries do not verify whether shardlets on the queried database are participating in ongoing split-merge operations.</span></span> <span data-ttu-id="e2546-131">[Elastic Database 분할/병합 도구를 사용하여 확장하기](sql-database-elastic-scale-overview-split-and-merge.md)를 참조하세요. 따라서 동일한 shardlet의 행이 동일한 다중 분할된 데이터베이스 쿼리의 여러 데이터베이스에 대해 표시하는 경우 불일치가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-131">(See [Scaling using the Elastic Database split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md).) This can lead to inconsistencies where rows from the same shardlet show for multiple databases in the same multi-shard query.</span></span> <span data-ttu-id="e2546-132">이러한 제한 사항에 유의하고 다중 분할된 데이터베이스 쿼리를 수행하는 동안 사용되는 지속적인 분할-병합 작업과 분할된 데이터베이스 맵 변경 사항을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-132">Be aware of these limitations and consider draining ongoing split-merge operations and changes to the shard map while performing multi-shard queries.</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

## <a name="see-also"></a><span data-ttu-id="e2546-133">참고 항목</span><span class="sxs-lookup"><span data-stu-id="e2546-133">See also</span></span>
<span data-ttu-id="e2546-134">**[System.Data.SqlClient](http://msdn.microsoft.com/library/System.Data.SqlClient.aspx)** 클래스 및 메서드.</span><span class="sxs-lookup"><span data-stu-id="e2546-134">**[System.Data.SqlClient](http://msdn.microsoft.com/library/System.Data.SqlClient.aspx)** classes and methods.</span></span>

<span data-ttu-id="e2546-135">[탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-database-client-library.md)를 사용하여 분할된 데이터베이스를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-135">Manage shards using the [Elastic Database client library](sql-database-elastic-database-client-library.md).</span></span> <span data-ttu-id="e2546-136">[Microsoft.Azure.SqlDatabase.ElasticScale.Query](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.aspx)라고 하는 네임스페이스가 포함되며, 이 네임스페이스는 단일 쿼리 및 결과를 사용하여 여러 분할된 데이터베이스를 쿼리하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-136">Includes a  namespace called [Microsoft.Azure.SqlDatabase.ElasticScale.Query](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.aspx) that provides the ability to query multiple shards using a single query and result.</span></span> <span data-ttu-id="e2546-137">분할된 데이터베이스의 컬렉션에 대해 쿼리 추상화를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-137">It provides a querying abstraction over a collection of shards.</span></span> <span data-ttu-id="e2546-138">또한 대체 실행 정책, 특히 부분 결과를 제공하여 많은 분할된 데이터베이스를 쿼리할 때 오류를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="e2546-138">It also provides alternative execution policies, in particular partial results, to deal with failures when querying over many shards.</span></span>  

