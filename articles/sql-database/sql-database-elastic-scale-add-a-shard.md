---
title: "탄력적 데이터베이스 도구를 사용 하 여 분할 된 데이터베이스는 aaaAdding | Microsoft Docs"
description: "탄력적인 확장 Api tooadd 새 분할 영역이 tooa 분할 toouse 설정 하는 방법입니다."
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
ms.openlocfilehash: f44b59578376d1238b3012a3cb52339978079f0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-shard-using-elastic-database-tools"></a><span data-ttu-id="00f4b-103">탄력적 데이터베이스 도구를 사용하여 분할된 데이터베이스 추가하기</span><span class="sxs-lookup"><span data-stu-id="00f4b-103">Adding a shard using Elastic Database tools</span></span>
## <a name="tooadd-a-shard-for-a-new-range-or-key"></a><span data-ttu-id="00f4b-104">새 범위 또는 키에 대 한 분할 tooadd</span><span class="sxs-lookup"><span data-stu-id="00f4b-104">tooadd a shard for a new range or key</span></span>
<span data-ttu-id="00f4b-105">응용 프로그램 종종 필요한 toosimply 새로운 키 또는 키 범위에서 예상 되는 새 분할 영역이 toohandle 데이터 대 한 추가 분할 맵은 이미 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="00f4b-105">Applications often need toosimply add new shards toohandle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="00f4b-106">예를 들어 테 넌 트 ID에 따라 분할 응용 프로그램 tooprovision 새로운 분할 새 테 넌 트에 대 한 하거나 데이터 분할 매월 새로운 분할 hello 새로운 달이 시작 하기 전에 사용자를 프로 비전 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00f4b-106">For example, an application sharded by Tenant ID may need tooprovision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before hello start of each new month.</span></span> 

<span data-ttu-id="00f4b-107">Hello 새로운 키 값의 범위로 되어 있지 않은 경우 기존 매핑의 일부를 매우 간단한 tooadd hello 새 분할 영역 및 연결 hello 새 키 또는 범위 toothat 분할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00f4b-107">If hello new range of key values is not already part of an existing mapping, it is very simple tooadd hello new shard and associate hello new key or range toothat shard.</span></span> 

### <a name="example--adding-a-shard-and-its-range-tooan-existing-shard-map"></a><span data-ttu-id="00f4b-108">예제: 분할 영역 및 해당 범위 tooan 기존 분할 맵 추가</span><span class="sxs-lookup"><span data-stu-id="00f4b-108">Example:  adding a shard and its range tooan existing shard map</span></span>
<span data-ttu-id="00f4b-109">이 샘플에서는 hello [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) 메서드 hello의 인스턴스를 만듭니다 [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="00f4b-109">This sample uses hello [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) methods, and creates an instance of hello [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) class.</span></span> <span data-ttu-id="00f4b-110">데이터베이스 이름은 아래 hello 샘플에서 **sample_shard_2** 및 내부에서 모든 필요한 스키마 개체가 만들어진 toohold 범위 [300, 400).</span><span class="sxs-lookup"><span data-stu-id="00f4b-110">In hello sample below, a database named **sample_shard_2** and all necessary schema objects inside of it have been created toohold range [300, 400).</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range being added. 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 
        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Create hello mapping and associate it with hello new shard 
    sm.CreateRangeMapping(new RangeMappingCreationInfo<long> 
                            (new Range<long>(300, 400), shard2, MappingStatus.Online)); 


<span data-ttu-id="00f4b-111">대신 Powershell toocreate 새 Shard Map Manager를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00f4b-111">As an alternative, you can use Powershell toocreate a new Shard Map Manager.</span></span> <span data-ttu-id="00f4b-112">[여기](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)에 예제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00f4b-112">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="tooadd-a-shard-for-an-empty-part-of-an-existing-range"></a><span data-ttu-id="00f4b-113">기존 범위의 빈 부분에 대 한 분할 tooadd</span><span class="sxs-lookup"><span data-stu-id="00f4b-113">tooadd a shard for an empty part of an existing range</span></span>
<span data-ttu-id="00f4b-114">일부 환경에서는 이미 범위 tooa 분할 영역을 매핑 고 데이터를 부분적으로 채워진 있을 수 있지만 예정 된 데이터 toobe 방향이 지정 된 tooa 다른 분할 하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="00f4b-114">In some circumstances, you may have already mapped a range tooa shard and partially filled it with data, but you now want upcoming data toobe directed tooa different shard.</span></span> <span data-ttu-id="00f4b-115">예를 들어 하면 분할 일별 범위 및 50 일 tooa 분할 할당 이미 있지만 다른 분할 영역에 대 한 예측 데이터 tooland 24 일에 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="00f4b-115">For example, you shard by day range and have already allocated 50 days tooa shard, but on day 24, you want future data tooland in a different shard.</span></span> <span data-ttu-id="00f4b-116">탄력적 데이터베이스 hello [분할 / 병합 도구](sql-database-elastic-scale-overview-split-and-merge.md) 이 작업을 수행할 수 있지만 25 일 (포함) too50 단독 아직 존재 하지 않는 데이터 이동 필요가 없는 경우 (예: [25, 50 일의 hello 범위에 대 한 데이터), 즉,)를 수행할 수 있습니다 분할 맵 관리 Api를 직접 hello 전적으로 사용 하 여이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00f4b-116">hello elastic database [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) can perform this operation, but if data movement is not necessary (for example, data for hello range of days [25, 50), i.e., day 25 inclusive too50 exclusive, does not yet exist) you can perform this entirely using hello Shard Map Management APIs directly.</span></span>

### <a name="example-splitting-a-range-and-assigning-hello-empty-portion-tooa-newly-added-shard"></a><span data-ttu-id="00f4b-117">예: hello 할당과 범위 분 빈 부분 tooa 새로 추가 된 분할</span><span class="sxs-lookup"><span data-stu-id="00f4b-117">Example: splitting a range and assigning hello empty portion tooa newly-added shard</span></span>
<span data-ttu-id="00f4b-118">이 예제에서는 "sample_shard_2" 데이터베이스와 해당 데이터베이스 내의 필요한 모든 스키마 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00f4b-118">A database named “sample_shard_2” and all necessary schema objects inside of it have been created.</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range we will move 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 

        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Split hello Range holding Key 25 

    sm.SplitMapping(sm.GetMappingForKey(25), 25); 

    // Map new range holding [25-50) toodifferent shard: 
    // first take existing mapping offline 
    sm.MarkMappingOffline(sm.GetMappingForKey(25)); 
    // now map while offline tooa different shard and take online 
    RangeMappingUpdate upd = new RangeMappingUpdate(); 
    upd.Shard = shard2; 
    sm.MarkMappingOnline(sm.UpdateMapping(sm.GetMappingForKey(25), upd)); 

<span data-ttu-id="00f4b-119">**중요 한**: hello에 대 한 범위 하는 경우 업데이트 hello 매핑 빈에이 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="00f4b-119">**Important**:  Use this technique only if you are certain that hello range for hello updated mapping is empty.</span></span>  <span data-ttu-id="00f4b-120">위의 hello 방법 이동 hello 범위에 대 한 데이터를 검사 하지 않습니다, 그리고 코드에서 tooinclude 확인 되므로 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="00f4b-120">hello methods above do not check data for hello range being moved, so it is best tooinclude checks in your code.</span></span>  <span data-ttu-id="00f4b-121">행이 이동 hello 범위에 있는 경우 hello 실제 데이터 분산 hello 업데이트 된 분할 맵을 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00f4b-121">If rows exist in hello range being moved, hello actual data distribution will not match hello updated shard map.</span></span> <span data-ttu-id="00f4b-122">사용 하 여 hello [분할 / 병합 도구](sql-database-elastic-scale-overview-split-and-merge.md) tooperform hello 작업 대신 이러한 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="00f4b-122">Use hello [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) tooperform hello operation instead in these cases.</span></span>  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

