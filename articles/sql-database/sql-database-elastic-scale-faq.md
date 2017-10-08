---
title: "SQL 탄력적인 크기 조정 FAQ aaaAzure | Microsoft Docs"
description: "Azure SQL 데이터베이스의 탄력적인 확장에 대한 질문과 대답을 제공합니다."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: e60dde9c-bb7b-4f2f-b52c-bdb506d49fcb
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 8c77902e8ce9cbbc5e081cd9d2c911d4c8dc9e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-faq"></a><span data-ttu-id="7dfb0-103">탄력적 데이터베이스 도구 FAQ</span><span class="sxs-lookup"><span data-stu-id="7dfb0-103">Elastic database tools FAQ</span></span>
#### <a name="if-i-have-a-single-tenant-per-shard-and-no-sharding-key-how-do-i-populate-hello-sharding-key-for-hello-schema-info"></a><span data-ttu-id="7dfb0-104">단일 테 넌 트 당 분할 된 데이터베이스 및 분할 키를 있으면 hello 스키마 정보에 대 한 분할 키 hello 어떻게 채울 합니까?</span><span class="sxs-lookup"><span data-stu-id="7dfb0-104">If I have a single-tenant per shard and no sharding key, how do I populate hello sharding key for hello schema info?</span></span>
<span data-ttu-id="7dfb0-105">hello 스키마 정보 개체에만 사용 되는 toosplit 병합 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="7dfb0-105">hello schema info object is only used toosplit merge scenarios.</span></span> <span data-ttu-id="7dfb0-106">기본적으로 단일-테 넌 트 응용 프로그램을 사용 하는 경우 hello 분할 병합 도구 하지 않아도 하 고 없기 때문에 필요 toopopulate hello 스키마 정보 개체가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7dfb0-106">If an application is inherently single-tenant, then it does not require hello Split Merge tool and thus there is no need toopopulate hello schema info object.</span></span>

#### <a name="ive-provisioned-a-database-and-i-already-have-a-shard-map-manager-how-do-i-register-this-new-database-as-a-shard"></a><span data-ttu-id="7dfb0-107">데이터베이스를 프로비전했으며 분할된 데이터베이스 맵 관리자가 이미 있습니다. 이 새로운 데이터베이스를 분할로 등록하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="7dfb0-107">I’ve provisioned a database and I already have a Shard Map Manager, how do I register this new database as a shard?</span></span>
<span data-ttu-id="7dfb0-108">참조 하십시오  **[hello 탄력적 데이터베이스 클라이언트 라이브러리를 사용 하 여 분할 tooan 응용 프로그램을 추가](sql-database-elastic-scale-add-a-shard.md)**합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfb0-108">Please see **[Adding a shard tooan application using hello elastic database client library](sql-database-elastic-scale-add-a-shard.md)**.</span></span> 

#### <a name="how-much-do-elastic-database-tools-cost"></a><span data-ttu-id="7dfb0-109">탄력적 데이터베이스 도구의 비용은 얼마인가요?</span><span class="sxs-lookup"><span data-stu-id="7dfb0-109">How much do elastic database tools cost?</span></span>
<span data-ttu-id="7dfb0-110">Hello 탄력적 데이터베이스 클라이언트 라이브러리를 사용 하 여 모든 비용 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7dfb0-110">Using hello elastic database client library does not incur any costs.</span></span> <span data-ttu-id="7dfb0-111">비용은은 hello 분할 병합 도구에 대 한 프로 비전 hello 웹/작업자 역할 뿐만 아니라 분할 영역 및 Shard Map Manager hello에 대 한 사용 하는 hello Azure SQL 데이터베이스에 대해서만 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7dfb0-111">Costs accrue only for hello Azure SQL databases that you use for shards and hello Shard Map Manager, as well as hello web/worker roles you provision for hello Split Merge tool.</span></span>

#### <a name="why-are-my-credentials-not-working-when-i-add-a-shard-from-a-different-server"></a><span data-ttu-id="7dfb0-112">다른 서버에서 분할을 추가할 경우 내 자격 증명이 작동하지 않는 것은 무엇 때문인가요?</span><span class="sxs-lookup"><span data-stu-id="7dfb0-112">Why are my credentials not working when I add a shard from a different server?</span></span>
<span data-ttu-id="7dfb0-113">Hello 형태의 자격 증명을 사용 하지 않는 "사용자 ID =username@servername"를 대신 사용 하 여 "사용자 ID 사용자 이름 =".</span><span class="sxs-lookup"><span data-stu-id="7dfb0-113">Do not use credentials in hello form of “User ID=username@servername”, instead simply use “User ID = username”.</span></span>  <span data-ttu-id="7dfb0-114">또한 해당 hello "username" 로그인에 대 한 권한이 hello 분할 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfb0-114">Also, be sure that hello “username” login has permissions on hello shard.</span></span>

#### <a name="do-i-need-toocreate-a-shard-map-manager-and-populate-shards-every-time-i-start-my-applications"></a><span data-ttu-id="7dfb0-115">Shard Map Manager toocreate 필요 하 고 하는 내 응용 프로그램을 시작할 때마다 분할 영역을 채우는?</span><span class="sxs-lookup"><span data-stu-id="7dfb0-115">Do I need toocreate a Shard Map Manager and populate shards every time I start my applications?</span></span>
<span data-ttu-id="7dfb0-116">더-hello Shard Map Manager 만들 hello (예를 들어  **[ShardMapManagerFactory.CreateSqlShardMapManager](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)**) 작업은 일회성 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="7dfb0-116">No—hello creation of hello Shard Map Manager (for example, **[ShardMapManagerFactory.CreateSqlShardMapManager](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)**) is a one-time operation.</span></span>  <span data-ttu-id="7dfb0-117">응용 프로그램 hello 호출을 사용 해야  **[ShardMapManagerFactory.TryGetSqlShardMapManager()](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)**  응용 프로그램 시작 시.</span><span class="sxs-lookup"><span data-stu-id="7dfb0-117">Your application should use hello call **[ShardMapManagerFactory.TryGetSqlShardMapManager()](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)** at application start-up time.</span></span>  <span data-ttu-id="7dfb0-118">이러한 호출은 응용 프로그램 도메인당 하나만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfb0-118">There should only one such call per application domain.</span></span>

#### <a name="i-have-questions-about-using-elastic-database-tools-how-do-i-get-them-answered"></a><span data-ttu-id="7dfb0-119">탄력적 데이터베이스 도구 사용과 관련된 질문이 있는 경우 답변을 받으려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="7dfb0-119">I have questions about using elastic database tools, how do I get them answered?</span></span>
<span data-ttu-id="7dfb0-120">에 게 연락 하세요 hello에 toous [Azure SQL 데이터베이스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfb0-120">Please reach out toous on hello [Azure SQL Database forum](https://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted).</span></span>

#### <a name="when-i-get-a-database-connection-using-a-sharding-key-i-can-still-query-data-for-other-sharding-keys-on-hello-same-shard--is-this-by-design"></a><span data-ttu-id="7dfb0-121">분할 키를 사용 하 여 데이터베이스 연결을 받으면 볼 수 있습니다. 여전히 데이터를 쿼리 hello에 다른 분할 키 동일 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfb0-121">When I get a database connection using a sharding key, I can still query data for other sharding keys on hello same shard.</span></span>  <span data-ttu-id="7dfb0-122">의도한 동작인가요?</span><span class="sxs-lookup"><span data-stu-id="7dfb0-122">Is this by design?</span></span>
<span data-ttu-id="7dfb0-123">hello 탄력적인 확장 Api 분할 키에 대 한 연결 toohello 올바른 데이터베이스를 제공 하지만 분할 키 필터링을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7dfb0-123">hello Elastic Scale APIs give you a connection toohello correct database for your sharding key, but do not provide sharding key filtering.</span></span>  <span data-ttu-id="7dfb0-124">추가 **여기서** 필요한 경우 절 tooyour 쿼리 toorestrict hello 범위 toohello 분할 키를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfb0-124">Add **WHERE** clauses tooyour query toorestrict hello scope toohello provided sharding key, if necessary.</span></span>

#### <a name="can-i-use-a-different-azure-database-edition-for-each-shard-in-my-shard-set"></a><span data-ttu-id="7dfb0-125">내 분할 집합의 각 분할에 대해 다른 Azure 데이터베이스 버전을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7dfb0-125">Can I use a different Azure Database edition for each shard in my shard set?</span></span>
<span data-ttu-id="7dfb0-126">예, 분할은 개별 데이터베이스이므로 한 분할은 Premium Edition이고 다른 버전은 Standard Edition일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7dfb0-126">Yes, a shard is an individual database, and thus one shard could be a Premium edition while another be a Standard edition.</span></span> <span data-ttu-id="7dfb0-127">또한 분할 영역이 hello 에디션의 hello 분할의 hello 수명 동안 여러 번 위나 아래로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7dfb0-127">Further, hello edition of a shard can scale up or down multiple times during hello lifetime of hello shard.</span></span>

#### <a name="does-hello-split-merge-tool-provision-or-delete-a-database-during-a-split-or-merge-operation"></a><span data-ttu-id="7dfb0-128">가 분할 병합 도구 프로 비전 hello (또는 삭제) 분할 또는 병합 작업 중에 데이터베이스?</span><span class="sxs-lookup"><span data-stu-id="7dfb0-128">Does hello Split Merge tool provision (or delete) a database during a split or merge operation?</span></span>
<span data-ttu-id="7dfb0-129">아니요.</span><span class="sxs-lookup"><span data-stu-id="7dfb0-129">No.</span></span> <span data-ttu-id="7dfb0-130">에 대 한 **분할** 작업 hello 대상 데이터베이스 hello 적절 한 스키마와 함께 존재 해야 하며 hello Shard Map Manager에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfb0-130">For **split** operations, hello target database must exist with hello appropriate schema and be registered with hello Shard Map Manager.</span></span>  <span data-ttu-id="7dfb0-131">에 대 한 **병합** 작업 hello shard map manager에서 hello 분할 된 데이터베이스를 삭제 한 다음 hello 데이터베이스를 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7dfb0-131">For **merge** operations, you must delete hello shard from hello shard map manager and then delete hello database.</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

