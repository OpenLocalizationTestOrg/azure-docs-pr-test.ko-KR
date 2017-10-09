---
title: "Azure SQL 데이터베이스를 분할 하는 aaaQuery | Microsoft Docs"
description: "Hello 탄력적 데이터베이스 클라이언트 라이브러리를 사용 하 여 분할 된 데이터베이스에서 쿼리를 실행 합니다."
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
ms.openlocfilehash: a1f0763935a6807b74aa9dec477714e8d117417d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="multi-shard-querying"></a><span data-ttu-id="f2e94-103">다중 분할된 데이터베이스 쿼리</span><span class="sxs-lookup"><span data-stu-id="f2e94-103">Multi-shard querying</span></span>
## <a name="overview"></a><span data-ttu-id="f2e94-104">개요</span><span class="sxs-lookup"><span data-stu-id="f2e94-104">Overview</span></span>
<span data-ttu-id="f2e94-105">Hello로 [탄력적 데이터베이스 도구](sql-database-elastic-scale-introduction.md), 분할 된 데이터베이스 솔루션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-105">With hello [Elastic Database tools](sql-database-elastic-scale-introduction.md), you can create sharded database solutions.</span></span> <span data-ttu-id="f2e94-106">**다중 분할된 데이터베이스 쿼리** 는 여러 분할된 데이터베이스 간에 걸친 쿼리를 실행해야 하는 데이터 컬렉션/보고와 같은 작업에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-106">**Multi-shard querying** is used for tasks such as data collection/reporting that require running a query that stretches across several shards.</span></span> <span data-ttu-id="f2e94-107">(너무 이와[데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md), 단일 분할 영역에 모든 작업을 수행 하는.)</span><span class="sxs-lookup"><span data-stu-id="f2e94-107">(Contrast this too[data-dependent routing](sql-database-elastic-scale-data-dependent-routing.md), which performs all work on a single shard.)</span></span> 

1. <span data-ttu-id="f2e94-108">가져오기는 [ **RangeShardMap** ](https://msdn.microsoft.com/library/azure/dn807318.aspx) 또는 [ **ListShardMap** ](https://msdn.microsoft.com/library/azure/dn807370.aspx) hello를 사용 하 여 [ **TryGetRangeShardMap** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [ **TryGetListShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), 또는 hello [ **GetShardMap** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) 메서드.</span><span class="sxs-lookup"><span data-stu-id="f2e94-108">Get a [**RangeShardMap**](https://msdn.microsoft.com/library/azure/dn807318.aspx) or [**ListShardMap**](https://msdn.microsoft.com/library/azure/dn807370.aspx) using hello [**TryGetRangeShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [**TryGetListShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), or hello [**GetShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) method.</span></span> <span data-ttu-id="f2e94-109">[**ShardMapManager 생성**](sql-database-elastic-scale-shard-map-management.md#constructing-a-shardmapmanager) 및 [**RangeShardMap 또는 ListShardMap 가져오기**](sql-database-elastic-scale-shard-map-management.md#get-a-rangeshardmap-or-listshardmap)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2e94-109">See [**Constructing a ShardMapManager**](sql-database-elastic-scale-shard-map-management.md#constructing-a-shardmapmanager) and [**Get a RangeShardMap or ListShardMap**](sql-database-elastic-scale-shard-map-management.md#get-a-rangeshardmap-or-listshardmap).</span></span>
2. <span data-ttu-id="f2e94-110">**[MultiShardConnection](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardconnection.aspx)** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-110">Create a **[MultiShardConnection](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardconnection.aspx)** object.</span></span>
3. <span data-ttu-id="f2e94-111">**[MultiShardCommand](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.aspx)**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-111">Create a **[MultiShardCommand](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.aspx)**.</span></span> 
4. <span data-ttu-id="f2e94-112">집합 hello  **[CommandText 속성이](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.commandtext.aspx#P:Microsoft.Azure.SqlDatabase.ElasticScale.Query.MultiShardCommand.CommandText)**  tooa T-SQL 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-112">Set hello **[CommandText property](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.commandtext.aspx#P:Microsoft.Azure.SqlDatabase.ElasticScale.Query.MultiShardCommand.CommandText)** tooa T-SQL command.</span></span>
5. <span data-ttu-id="f2e94-113">Hello를 호출 하 여 hello 명령을 실행  **[ExecuteReader 메서드](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.executereader.aspx)**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-113">Execute hello command by calling hello **[ExecuteReader method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.executereader.aspx)**.</span></span>
6. <span data-ttu-id="f2e94-114">Hello를 사용 하 여 hello 결과 보려면  **[MultiShardDataReader 클래스](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multisharddatareader.aspx)**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-114">View hello results using hello **[MultiShardDataReader class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multisharddatareader.aspx)**.</span></span> 

## <a name="example"></a><span data-ttu-id="f2e94-115">예제</span><span class="sxs-lookup"><span data-stu-id="f2e94-115">Example</span></span>
<span data-ttu-id="f2e94-116">hello 다음 코드에서는 쿼리를 사용 하 여 다중 분할 된 데이터베이스의 hello 사용은 주어진 **ShardMap** 라는 *myShardMap*합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-116">hello following code illustrates hello usage of multi-shard querying using a given **ShardMap** named *myShardMap*.</span></span> 

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


<span data-ttu-id="f2e94-117">주요 차이점은 다중 분할 된 데이터베이스 연결의 hello 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-117">A key difference is hello construction of multi-shard connections.</span></span> <span data-ttu-id="f2e94-118">여기서 **SqlConnection** 에서 작동 하는 단일 데이터베이스 hello **MultiShardConnection** 사용는 ***분할 영역 컬렉션*** 입력으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-118">Where **SqlConnection** operates on a single database, hello **MultiShardConnection** takes a ***collection of shards*** as its input.</span></span> <span data-ttu-id="f2e94-119">분할 된 데이터베이스에서 분할 맵은 hello 컬렉션을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-119">Populate hello collection of shards from a shard map.</span></span> <span data-ttu-id="f2e94-120">hello 쿼리를 사용 하 여 분할 된 데이터베이스의 hello 컬렉션에서 실행할 **UNION ALL** 의미 체계 tooassemble는 하나의 전체 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-120">hello query is then executed on hello collection of shards using **UNION ALL** semantics tooassemble a single overall result.</span></span> <span data-ttu-id="f2e94-121">필요에 따라 hello 이름은 hello 행에서 시작 되는 위치 hello 분할의 추가 될 수 hello를 사용 하 여 출력 toohello **ExecutionOptions** 명령에는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-121">Optionally, hello name of hello shard where hello row originates from can be added toohello output using hello **ExecutionOptions** property on command.</span></span> 

<span data-ttu-id="f2e94-122">Hello 호출 너무 참고**myShardMap.GetShards()**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-122">Note hello call too**myShardMap.GetShards()**.</span></span> <span data-ttu-id="f2e94-123">이 메서드는 분할 맵을 hello에서 모든 분할 영역을 검색 하 고 모든 관련 데이터베이스에서 쉽게 toorun 쿼리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-123">This method retrieves all shards from hello shard map and provides an easy way toorun a query across all relevant databases.</span></span> <span data-ttu-id="f2e94-124">hello 분할 영역 컬렉션 다중 분할 쿼리를 구체화할 수 있습니다에 대 한 추가 LINQ를 수행 하 여 쿼리 너무 hello 호출에서 반환 된 hello 컬렉션에 대해**myShardMap.GetShards()**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-124">hello collection of shards for a multi-shard query can be refined further by performing a LINQ query over hello collection returned from hello call too**myShardMap.GetShards()**.</span></span> <span data-ttu-id="f2e94-125">Hello 부분 결과 정책 함께 쿼리 하는 다중 분할 된 데이터베이스의 현재 기능 hello toohundreds 분할 영역을 수십에 대 한 잘 설계 된 toowork 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-125">In combination with hello partial results policy, hello current capability in multi-shard querying has been designed toowork well for tens up toohundreds of shards.</span></span>

<span data-ttu-id="f2e94-126">제한 사항으로 쿼리 하는 다중 분할 된 데이터베이스의 쿼리는 shardlet 및 분할 된 데이터베이스에 대 한 유효성 검사의 hello 부족 현재입니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-126">A limitation with multi-shard querying is currently hello lack of validation for shards and shardlets that are queried.</span></span> <span data-ttu-id="f2e94-127">데이터 종속 라우팅 지정 된 영역 쿼리 작업의 hello 시 hello 분할 맵은의 일부 인지를 확인 하는 동안 여러 분할 영역 쿼리는이 검사를 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-127">While data-dependent routing verifies that a given shard is part of hello shard map at hello time of querying, multi-shard queries do not perform this check.</span></span> <span data-ttu-id="f2e94-128">Hello 분할 맵을에서 제거 된 데이터베이스에서 실행 중인 toomulti shard 쿼리 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-128">This can lead toomulti-shard queries running on databases that have  been removed from hello shard map.</span></span>

## <a name="multi-shard-queries-and-split-merge-operations"></a><span data-ttu-id="f2e94-129">다중 분할된 데이터베이스 쿼리 및 분할/병합 작업</span><span class="sxs-lookup"><span data-stu-id="f2e94-129">Multi-shard queries and split-merge operations</span></span>
<span data-ttu-id="f2e94-130">여러 분할 영역 쿼리 hello 쿼리 된 데이터베이스에서 shardlet은 분할 / 병합 작업이 진행 중에 참여 하는지 여부를 확인 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-130">Multi-shard queries do not verify whether shardlets on hello queried database are participating in ongoing split-merge operations.</span></span> <span data-ttu-id="f2e94-131">(참조 [hello 탄력적 데이터베이스 분할 / 병합 도구를 사용 하 여 크기 조정](sql-database-elastic-scale-overview-split-and-merge.md).) 위치에서 행 hello hello에서 여러 데이터베이스에 대 한 동일한 shardlet 슬라이드쇼 tooinconsistencies 않을 수 있습니다 같은 다중 분할 된 데이터베이스를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-131">(See [Scaling using hello Elastic Database split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md).) This can lead tooinconsistencies where rows from hello same shardlet show for multiple databases in hello same multi-shard query.</span></span> <span data-ttu-id="f2e94-132">이러한 제한 사항을 고려해 야 하 고 지속적인 분할 / 병합 작업 및 변경 내용은 toohello 분할 맵을 다중 분할 쿼리를 수행 하는 동안 드레이닝을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-132">Be aware of these limitations and consider draining ongoing split-merge operations and changes toohello shard map while performing multi-shard queries.</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

## <a name="see-also"></a><span data-ttu-id="f2e94-133">참고 항목</span><span class="sxs-lookup"><span data-stu-id="f2e94-133">See also</span></span>
<span data-ttu-id="f2e94-134">**[System.Data.SqlClient](http://msdn.microsoft.com/library/System.Data.SqlClient.aspx)** 클래스 및 메서드.</span><span class="sxs-lookup"><span data-stu-id="f2e94-134">**[System.Data.SqlClient](http://msdn.microsoft.com/library/System.Data.SqlClient.aspx)** classes and methods.</span></span>

<span data-ttu-id="f2e94-135">Hello를 사용 하 여 분할 된 데이터베이스를 관리 [탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-database-client-library.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-135">Manage shards using hello [Elastic Database client library](sql-database-elastic-database-client-library.md).</span></span> <span data-ttu-id="f2e94-136">라는 네임 스페이스를 포함 [Microsoft.Azure.SqlDatabase.ElasticScale.Query](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.aspx) hello 기능 tooquery를 제공 하는 단일 쿼리 및 결과 사용 하 여 여러 분할 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-136">Includes a  namespace called [Microsoft.Azure.SqlDatabase.ElasticScale.Query](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.aspx) that provides hello ability tooquery multiple shards using a single query and result.</span></span> <span data-ttu-id="f2e94-137">분할된 데이터베이스의 컬렉션에 대해 쿼리 추상화를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e94-137">It provides a querying abstraction over a collection of shards.</span></span> <span data-ttu-id="f2e94-138">또한 제공 대체 실행 정책, 특히 부분 결과, toodeal 실패 하 여 많은 분할 영역을 통해 쿼리할 때.</span><span class="sxs-lookup"><span data-stu-id="f2e94-138">It also provides alternative execution policies, in particular partial results, toodeal with failures when querying over many shards.</span></span>  

