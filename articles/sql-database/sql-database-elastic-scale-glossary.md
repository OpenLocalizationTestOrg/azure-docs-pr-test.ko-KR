---
title: "데이터베이스 도구 용어집 aaaElastic | Microsoft Docs"
description: "탄력적 데이터베이스 도구에 쓰이는 용어 설명."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: a23a4e81-6706-452d-afc1-a550e5e47af9
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: d6573aad9a097e07135b0a64d1dafec19bb8cc7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-glossary"></a><span data-ttu-id="1365c-103">탄력적 데이터베이스 도구 용어집</span><span class="sxs-lookup"><span data-stu-id="1365c-103">Elastic Database tools glossary</span></span>
<span data-ttu-id="1365c-104">hello 다음 용어에 대해 정의 된 hello [탄력적 데이터베이스 도구](sql-database-elastic-scale-introduction.md), Azure SQL 데이터베이스의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-104">hello following terms are defined for hello [Elastic Database tools](sql-database-elastic-scale-introduction.md), a feature of Azure SQL Database.</span></span> <span data-ttu-id="1365c-105">hello 도구를 사용 하는 toomanage [분할 맵](sql-database-elastic-scale-shard-map-management.md), hello 등과 [클라이언트 라이브러리](sql-database-elastic-database-client-library.md), hello [분할 / 병합 도구](sql-database-elastic-scale-overview-split-and-merge.md), [탄력적 풀](sql-database-elastic-pool.md), 및 [쿼리](sql-database-elastic-query-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-105">hello tools are used toomanage [shard maps](sql-database-elastic-scale-shard-map-management.md), and include hello [client library](sql-database-elastic-database-client-library.md), hello [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md), [elastic pools](sql-database-elastic-pool.md), and [queries](sql-database-elastic-query-overview.md).</span></span> 

<span data-ttu-id="1365c-106">이러한 용어에 사용 되는 [탄력적 데이터베이스 도구를 사용 하 여 분할 영역이 추가](sql-database-elastic-scale-add-a-shard.md) 및 [hello RecoveryManager 클래스 toofix 분할 맵 문제를 사용 하 여](sql-database-elastic-database-recovery-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-106">These terms are used in [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Using hello RecoveryManager class toofix shard map problems](sql-database-elastic-database-recovery-manager.md).</span></span>

![탄력적인 확장 용어][1]

<span data-ttu-id="1365c-108">**데이터베이스**: Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="1365c-108">**Database**: An Azure SQL database.</span></span> 

<span data-ttu-id="1365c-109">**데이터 종속 라우팅**: hello를 특정 분할 키를 제공 하는 응용 프로그램 tooconnect tooa 분할을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-109">**Data dependent routing**: hello functionality that enables an application tooconnect tooa shard given a specific sharding key.</span></span> <span data-ttu-id="1365c-110">[데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1365c-110">See [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> <span data-ttu-id="1365c-111">너무 비교**[다중 분할 된 데이터베이스 쿼리](sql-database-elastic-scale-multishard-querying.md)**합니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-111">Compare too**[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**.</span></span>

<span data-ttu-id="1365c-112">**전역 분할 맵은**: hello 맵에 분할 키와 내에서 각 해당 분할 영역 간에 **분할 집합**합니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-112">**Global shard map**: hello map between sharding keys and their respective shards within a **shard set**.</span></span> <span data-ttu-id="1365c-113">hello 글로벌 분할 맵은 hello에 저장 된 **shard map manager**합니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-113">hello global shard map is stored in hello **shard map manager**.</span></span> <span data-ttu-id="1365c-114">너무 비교**로컬 분할 맵은**합니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-114">Compare too**local shard map**.</span></span>

<span data-ttu-id="1365c-115">**목록 분할된 데이터베이스 맵**: 분할 키가 개별적으로 매핑되는 분할된 데이터베이스 맵입니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-115">**List shard map**: A shard map in which sharding keys are mapped individually.</span></span> <span data-ttu-id="1365c-116">너무 비교**범위 분할 맵은**합니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-116">Compare too**Range Shard Map**.</span></span>   

<span data-ttu-id="1365c-117">**로컬 분할 맵은**: hello 분할 된 데이터베이스에 상주 하는 hello shardlet에 대 한 매핑이 포함 되어 hello 로컬 분할 맵은 분할 영역에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-117">**Local shard map**: Stored on a shard, hello local shard map contains mappings for hello shardlets that reside on hello shard.</span></span>

<span data-ttu-id="1365c-118">**여러 분할 영역 쿼리**: hello 기능 tooissue 여러 분할 영역에 대 한 쿼리, UNION ALL 의미 체계 (또한 "팬 아웃 쿼리")를 사용 하 여 결과 집합이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-118">**Multi-shard query**: hello ability tooissue a query against multiple shards; results sets are returned using UNION ALL semantics (also known as “fan-out query”).</span></span> <span data-ttu-id="1365c-119">너무 비교**데이터 종속 라우팅**합니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-119">Compare too**data dependent routing**.</span></span>

<span data-ttu-id="1365c-120">**다중 테넌트** 및 **단일 테넌트**: 단일 테넌트 데이터베이스 및 다중 테넌트 데이터베이스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-120">**Multi-tenant** and **Single-tenant**: This shows a single-tenant database and a multi-tenant database:</span></span>

![단일 및 다중 테넌트 데이터베이스](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

<span data-ttu-id="1365c-122">여기에 대표적인 **분할된** 단일 및 다중 테넌트 데이터베이스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-122">Here is a representation of **sharded** single and multi-tenant databases.</span></span> 

![단일 및 다중 테넌트 데이터베이스](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

<span data-ttu-id="1365c-124">**범위 분할 맵은**:는 hello에 분할 된 데이터베이스 배포 전략은 기반 연속 값의 범위가 여러 분할 맵을 합니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-124">**Range shard map**: A shard map in which hello shard distribution strategy is based on multiple ranges of contiguous values.</span></span> 

<span data-ttu-id="1365c-125">**참조 테이블**: 분할되지 않았지만 여러 분할된 데이터베이스에 걸쳐 복제되는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-125">**Reference tables**: Tables that are not sharded but are replicated across shards.</span></span> <span data-ttu-id="1365c-126">예를 들어, 우편번호는 참조 테이블에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-126">For example, zip codes can be stored in a reference table.</span></span> 

<span data-ttu-id="1365c-127">**분할된 데이터베이스**: 분할된 데이터 집합의 데이터를 저장하는 Azure SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-127">**Shard**: An Azure SQL database that stores data from a sharded data set.</span></span> 

<span data-ttu-id="1365c-128">**분할 된 데이터베이스 탄력성**: 기능 tooperform hello **수평적 확장** 및 **세로 배율**합니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-128">**Shard elasticity**: hello ability tooperform both **horizontal scaling** and **vertical scaling**.</span></span>

<span data-ttu-id="1365c-129">**분할된 데이터베이스 테이블**: 분할되는 테이블, 즉 해당 데이터가 분할 키 값을 기준으로 여러 분할된 데이터베이스 간에 분산되는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-129">**Sharded tables**: Tables that are sharded, i.e., whose data is distributed across shards based on their sharding key values.</span></span> 

<span data-ttu-id="1365c-130">**분할된 데이터베이스 키**: 분할된 데이터베이스 간에 데이터를 배포하는 방법을 결정하는 열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-130">**Sharding key**: A column value that determines how data is distributed across shards.</span></span> <span data-ttu-id="1365c-131">hello 값 형식 중 하나일 수 있습니다 hello 다음: **int**, **bigint**, **varbinary**, 또는 **uniqueidentifier**합니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-131">hello value type can be one of hello following: **int**, **bigint**, **varbinary**, or **uniqueidentifier**.</span></span> 

<span data-ttu-id="1365c-132">**분할 집합**: 특성 사용된 toohello 있는 분할 된 데이터베이스의 컬렉션을 hello hello shard map manager에서 동일한 분할 맵을 합니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-132">**Shard set**: hello collection of shards that are attributed toohello same shard map in hello shard map manager.</span></span>  

<span data-ttu-id="1365c-133">**Shardlet**: hello 연결 된 모든 데이터가 단일 분할 영역에 분할 키 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-133">**Shardlet**: All of hello data associated with a single value of a sharding key on a shard.</span></span> <span data-ttu-id="1365c-134">Shardlet은 데이터 이동 가능한 가장 작은 단위 hello 때 분할 된 테이블을 재배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-134">A shardlet is hello smallest unit of data movement possible when redistributing sharded tables.</span></span> 

<span data-ttu-id="1365c-135">**분할 맵은**: hello 분할 키와 해당 각 분할 영역 간의 매핑 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-135">**Shard map**: hello set of mappings between sharding keys and their respective shards.</span></span>

<span data-ttu-id="1365c-136">**Shard map manager**: hello 분할 맵과, 분할 영역 위치 및 하나 이상의 분할 집합에 대 한 매핑을 포함 하는 관리 개체 및 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-136">**Shard map manager**: A management object and data store that contains hello shard map(s), shard locations, and mappings for one or more shard sets.</span></span>

![매핑][2]

## <a name="verbs"></a><span data-ttu-id="1365c-138">동사</span><span class="sxs-lookup"><span data-stu-id="1365c-138">Verbs</span></span>
<span data-ttu-id="1365c-139">**수평적 확장**: hello act 아웃 (또는) 확장을 추가 하거나 아래와 같이 분할 영역 tooa 분할 맵을 제거 하 여 분할 된 데이터베이스의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-139">**Horizontal scaling**: hello act of scaling out (or in) a collection of shards by adding or removing shards tooa shard map, as shown below.</span></span>

![수평 및 수직적 크기 조정][3]

<span data-ttu-id="1365c-141">**병합**: hello act tooone 분할 두 개의 분할 된 데이터베이스에서에서 shardlet을 이동 하 고 hello 분할 맵은 적절 하 게 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-141">**Merge**: hello act of moving shardlets from two shards tooone shard and updating hello shard map accordingly.</span></span>

<span data-ttu-id="1365c-142">**Shardlet 이동**: hello act 단일 shardlet tooa 다른 분할 영역을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-142">**Shardlet move**: hello act of moving a single shardlet tooa different shard.</span></span> 

<span data-ttu-id="1365c-143">**분할**: 분할 키에 따라 여러 데이터베이스 간에 구조화 된 데이터를 가로로 동일 하 게 분할의 hello 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-143">**Shard**: hello act of horizontally partitioning identically structured data across multiple databases based on a sharding key.</span></span>

<span data-ttu-id="1365c-144">**분할**: hello act 하나의 분할 tooanother (일반적으로 새) 분할 영역에서 여러 shardlet을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-144">**Split**: hello act of moving several shardlets from one shard tooanother (typically new) shard.</span></span> <span data-ttu-id="1365c-145">분할 키 hello 분할 지점으로 hello 사용자가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-145">A sharding key is provided by hello user as hello split point.</span></span>

<span data-ttu-id="1365c-146">**세로 배율**: hello 작업 확장 (또는 축소)는 개별 분할 된 데이터베이스의 성능 수준을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-146">**Vertical Scaling**: hello act of scaling up (or down) hello performance level of an individual shard.</span></span> <span data-ttu-id="1365c-147">예를 들어 표준 tooPremium (결과적 더욱 많은 컴퓨팅 리소스)에서 분할 영역을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="1365c-147">For example, changing a shard from Standard tooPremium (which results in more computing resources).</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

