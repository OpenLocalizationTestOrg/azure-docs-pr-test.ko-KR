---
title: "탄력적 데이터베이스 도구를 사용하여 분할된 데이터베이스 추가하기 | Microsoft Docs"
description: "이 문서에서는 탄력적인 확장 API를 사용하여 새 분할된 데이터베이스를 분할된 데이터베이스 집합에 추가하는 방법을 설명합니다."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 62a349db-bebe-406f-a120-2f1986f2b286
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 6a91ea2251ea3b748faba5c97765bfded9c00234
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="adding-a-shard-using-elastic-database-tools"></a><span data-ttu-id="1a8fa-103">탄력적 데이터베이스 도구를 사용하여 분할된 데이터베이스 추가하기</span><span class="sxs-lookup"><span data-stu-id="1a8fa-103">Adding a shard using Elastic Database tools</span></span>
## <a name="to-add-a-shard-for-a-new-range-or-key"></a><span data-ttu-id="1a8fa-104">새 범위 또는 키에 대해 분할된 데이터베이스를 추가하기</span><span class="sxs-lookup"><span data-stu-id="1a8fa-104">To add a shard for a new range or key</span></span>
<span data-ttu-id="1a8fa-105">이미 존재하는 분할된 데이터베이스 맵의 경우 응용 프로그램은 대개 새 키 또는 키 범위에서 예상되는 데이터를 처리할 새로운 분할된 데이터베이스를 추가하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a8fa-105">Applications often need to simply add new shards to handle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="1a8fa-106">예를 들어 테넌트 ID를 기준으로 분할된 응용 프로그램이 새로운 테넌트에 대한 새로운 분할된 데이터베이스를 프로비전해야 할 수 있습니다. 또는 월별로 분할된 데이터의 경우 새로운 달이 시작되기 전에 새로운 분할된 데이터베이스를 프로비전해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8fa-106">For example, an application sharded by Tenant ID may need to provision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before the start of each new month.</span></span> 

<span data-ttu-id="1a8fa-107">키 값의 새로운 범위가 기존 매핑에 속하지 않는 경우에는 매우 간편하게 새 분할된 데이터베이스를 추가하고 새 키 또는 범위를 해당 분할된 데이터베이스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8fa-107">If the new range of key values is not already part of an existing mapping, it is very simple to add the new shard and associate the new key or range to that shard.</span></span> 

### <a name="example--adding-a-shard-and-its-range-to-an-existing-shard-map"></a><span data-ttu-id="1a8fa-108">예 : 기존 분할된 데이터베이스 맵에 분할된 데이터베이스 및 해당 범위 추가</span><span class="sxs-lookup"><span data-stu-id="1a8fa-108">Example:  adding a shard and its range to an existing shard map</span></span>
<span data-ttu-id="1a8fa-109">이 샘플에서는 [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx), [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) 메서드를 사용하며 [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) 클래스의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a8fa-109">This sample uses the [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) the [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) methods, and creates an instance of the [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) class.</span></span> <span data-ttu-id="1a8fa-110">아래 샘플에서는 [300, 400) 범위를 포함하도록 **sample_shard_2** 데이터베이스와 이 데이터베이스 내의 필요한 모든 스키마 개체를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8fa-110">In the sample below, a database named **sample_shard_2** and all necessary schema objects inside of it have been created to hold range [300, 400).</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard to hold the range being added. 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 
        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Create the mapping and associate it with the new shard 
    sm.CreateRangeMapping(new RangeMappingCreationInfo<long> 
                            (new Range<long>(300, 400), shard2, MappingStatus.Online)); 


<span data-ttu-id="1a8fa-111">대신 Powershell을 사용하여 새 분할된 데이터베이스 맵 관리자를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8fa-111">As an alternative, you can use Powershell to create a new Shard Map Manager.</span></span> <span data-ttu-id="1a8fa-112">[여기](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)에 예제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8fa-112">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="to-add-a-shard-for-an-empty-part-of-an-existing-range"></a><span data-ttu-id="1a8fa-113">기존 범위의 빈 부분에 대해 분할된 데이터베이스를 추가하기</span><span class="sxs-lookup"><span data-stu-id="1a8fa-113">To add a shard for an empty part of an existing range</span></span>
<span data-ttu-id="1a8fa-114">특정 범위를 분할된 데이터베이스에 이미 매핑했으며 데이터를 일부분 추가했는데 그 이후에 들어오는 데이터는 다른 분할된 데이터베이스로 이동하려는 경우가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8fa-114">In some circumstances, you may have already mapped a range to a shard and partially filled it with data, but you now want upcoming data to be directed to a different shard.</span></span> <span data-ttu-id="1a8fa-115">일 범위로 데이터베이스를 분할했으며 분할된 데이터베이스에 이미 50일을 할당했는데 24일째부터는 추가 데이터를 다른 분할된 데이터베이스에 저장하려는 경우를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8fa-115">For example, you shard by day range and have already allocated 50 days to a shard, but on day 24, you want future data to land in a different shard.</span></span> <span data-ttu-id="1a8fa-116">탄력적 데이터베이스의 [분할-합병 도구](sql-database-elastic-scale-overview-split-and-merge.md) 는 이 작업을 수행할 수는 있지만 25, 50 범위의 데이터, 즉 25일째부터 50일째까지의 데이터가 없는 경우와 같이 데이터를 이동할 필요가 없는 경우에는 분할된 데이터베이스 맵 관리 API를 직접 사용하여 이 작업 전체를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8fa-116">The elastic database [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) can perform this operation, but if data movement is not necessary (for example, data for the range of days [25, 50), i.e., day 25 inclusive to 50 exclusive, does not yet exist) you can perform this entirely using the Shard Map Management APIs directly.</span></span>

### <a name="example-splitting-a-range-and-assigning-the-empty-portion-to-a-newly-added-shard"></a><span data-ttu-id="1a8fa-117">예: 범위를 분할하고 새로 추가한 분할된 데이터베이스에 빈 부분 할당</span><span class="sxs-lookup"><span data-stu-id="1a8fa-117">Example: splitting a range and assigning the empty portion to a newly-added shard</span></span>
<span data-ttu-id="1a8fa-118">이 예제에서는 "sample_shard_2" 데이터베이스와 해당 데이터베이스 내의 필요한 모든 스키마 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a8fa-118">A database named “sample_shard_2” and all necessary schema objects inside of it have been created.</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard to hold the range we will move 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 

        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Split the Range holding Key 25 

    sm.SplitMapping(sm.GetMappingForKey(25), 25); 

    // Map new range holding [25-50) to different shard: 
    // first take existing mapping offline 
    sm.MarkMappingOffline(sm.GetMappingForKey(25)); 
    // now map while offline to a different shard and take online 
    RangeMappingUpdate upd = new RangeMappingUpdate(); 
    upd.Shard = shard2; 
    sm.MarkMappingOnline(sm.UpdateMapping(sm.GetMappingForKey(25), upd)); 

<span data-ttu-id="1a8fa-119">**중요**: 업데이트되는 매핑의 범위가 비어 있는 것이 확실한 경우에만 이 기술을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="1a8fa-119">**Important**:  Use this technique only if you are certain that the range for the updated mapping is empty.</span></span>  <span data-ttu-id="1a8fa-120">위의 방법에서는 이동하는 범위에서 데이터를 확인하지 않으므로 코드에 검사를 포함하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1a8fa-120">The methods above do not check data for the range being moved, so it is best to include checks in your code.</span></span>  <span data-ttu-id="1a8fa-121">이동하는 범위에 행이 있으면 실제 데이터 분포가 업데이트된 분할된 데이터베이스 맵과 일치하지 않게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a8fa-121">If rows exist in the range being moved, the actual data distribution will not match the updated shard map.</span></span> <span data-ttu-id="1a8fa-122">이 경우 대신 [분할-합병 도구](sql-database-elastic-scale-overview-split-and-merge.md) 를 사용하여 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1a8fa-122">Use the [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) to perform the operation instead in these cases.</span></span>  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

