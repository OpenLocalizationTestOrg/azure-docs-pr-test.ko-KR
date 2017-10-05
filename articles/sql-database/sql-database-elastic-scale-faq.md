---
title: "Azure SQL 탄력적인 확장 FAQ | Microsoft Docs"
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
ms.openlocfilehash: f0a7b5ce61feaead608d457465f64813737fa112
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="elastic-database-tools-faq"></a><span data-ttu-id="10f2c-103">탄력적 데이터베이스 도구 FAQ</span><span class="sxs-lookup"><span data-stu-id="10f2c-103">Elastic database tools FAQ</span></span>
#### <a name="if-i-have-a-single-tenant-per-shard-and-no-sharding-key-how-do-i-populate-the-sharding-key-for-the-schema-info"></a><span data-ttu-id="10f2c-104">분할 및 분할 안 함 키당 단일 테넌트가 있는 경우 스키마 정보에 대한 분할 키를 채우려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="10f2c-104">If I have a single-tenant per shard and no sharding key, how do I populate the sharding key for the schema info?</span></span>
<span data-ttu-id="10f2c-105">스키마 정보 개체는 시나리오를 분할 병합하는 데만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="10f2c-105">The schema info object is only used to split merge scenarios.</span></span> <span data-ttu-id="10f2c-106">응용 프로그램이 기본적으로 단일 테넌트인 경우에는 분할 병합 도구가 필요하지 않으므로 스키마 정보 개체를 채울 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10f2c-106">If an application is inherently single-tenant, then it does not require the Split Merge tool and thus there is no need to populate the schema info object.</span></span>

#### <a name="ive-provisioned-a-database-and-i-already-have-a-shard-map-manager-how-do-i-register-this-new-database-as-a-shard"></a><span data-ttu-id="10f2c-107">데이터베이스를 프로비전했으며 분할된 데이터베이스 맵 관리자가 이미 있습니다. 이 새로운 데이터베이스를 분할로 등록하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="10f2c-107">I’ve provisioned a database and I already have a Shard Map Manager, how do I register this new database as a shard?</span></span>
<span data-ttu-id="10f2c-108">**[탄력적 데이터베이스 클라이언트 라이브러리를 사용하여 응용 프로그램에 분할된 데이터베이스 추가](sql-database-elastic-scale-add-a-shard.md)**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="10f2c-108">Please see **[Adding a shard to an application using the elastic database client library](sql-database-elastic-scale-add-a-shard.md)**.</span></span> 

#### <a name="how-much-do-elastic-database-tools-cost"></a><span data-ttu-id="10f2c-109">탄력적 데이터베이스 도구의 비용은 얼마인가요?</span><span class="sxs-lookup"><span data-stu-id="10f2c-109">How much do elastic database tools cost?</span></span>
<span data-ttu-id="10f2c-110">탄력적 데이터베이스 클라이언트 라이브러리 사용에는 비용이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="10f2c-110">Using the elastic database client library does not incur any costs.</span></span> <span data-ttu-id="10f2c-111">분할된 데이터베이스 및 분할된 데이터베이스 맵 관리자에 사용하는 Azure SQL 데이터베이스와 분할 병합 도구에 대해 프로비전된 웹/작업자 역할과 관련된 비용만 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="10f2c-111">Costs accrue only for the Azure SQL databases that you use for shards and the Shard Map Manager, as well as the web/worker roles you provision for the Split Merge tool.</span></span>

#### <a name="why-are-my-credentials-not-working-when-i-add-a-shard-from-a-different-server"></a><span data-ttu-id="10f2c-112">다른 서버에서 분할을 추가할 경우 내 자격 증명이 작동하지 않는 것은 무엇 때문인가요?</span><span class="sxs-lookup"><span data-stu-id="10f2c-112">Why are my credentials not working when I add a shard from a different server?</span></span>
<span data-ttu-id="10f2c-113">형식의 자격 증명을 사용 하지 않는 "사용자 ID =username@servername", 대신 사용 하 여 "사용자 ID 사용자 이름 =".</span><span class="sxs-lookup"><span data-stu-id="10f2c-113">Do not use credentials in the form of “User ID=username@servername”, instead simply use “User ID = username”.</span></span>  <span data-ttu-id="10f2c-114">또한 "사용자 이름" 로그인에 분할에 대한 권한이 있는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="10f2c-114">Also, be sure that the “username” login has permissions on the shard.</span></span>

#### <a name="do-i-need-to-create-a-shard-map-manager-and-populate-shards-every-time-i-start-my-applications"></a><span data-ttu-id="10f2c-115">내 응용 프로그램을 시작할 때마다 분할된 데이터베이스 맵 관리자를 만들고 분할을 채워야 하나요?</span><span class="sxs-lookup"><span data-stu-id="10f2c-115">Do I need to create a Shard Map Manager and populate shards every time I start my applications?</span></span>
<span data-ttu-id="10f2c-116">아니요, 분할된 데이터베이스 맵 관리자(예: **[ShardMapManagerFactory.CreateSqlShardMapManager](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)**)는 한 번만 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10f2c-116">No—the creation of the Shard Map Manager (for example, **[ShardMapManagerFactory.CreateSqlShardMapManager](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)**) is a one-time operation.</span></span>  <span data-ttu-id="10f2c-117">응용 프로그램 시작 시 응용 프로그램에서 **[ShardMapManagerFactory.TryGetSqlShardMapManager()](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)** 호출을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10f2c-117">Your application should use the call **[ShardMapManagerFactory.TryGetSqlShardMapManager()](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)** at application start-up time.</span></span>  <span data-ttu-id="10f2c-118">이러한 호출은 응용 프로그램 도메인당 하나만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10f2c-118">There should only one such call per application domain.</span></span>

#### <a name="i-have-questions-about-using-elastic-database-tools-how-do-i-get-them-answered"></a><span data-ttu-id="10f2c-119">탄력적 데이터베이스 도구 사용과 관련된 질문이 있는 경우 답변을 받으려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="10f2c-119">I have questions about using elastic database tools, how do I get them answered?</span></span>
<span data-ttu-id="10f2c-120">[Azure SQL 데이터베이스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)에서 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="10f2c-120">Please reach out to us on the [Azure SQL Database forum](https://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted).</span></span>

#### <a name="when-i-get-a-database-connection-using-a-sharding-key-i-can-still-query-data-for-other-sharding-keys-on-the-same-shard--is-this-by-design"></a><span data-ttu-id="10f2c-121">분할 키를 사용하여 데이터베이스에 연결하는 경우 동일한 분할의 다른 분할 키에 대한 데이터도 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10f2c-121">When I get a database connection using a sharding key, I can still query data for other sharding keys on the same shard.</span></span>  <span data-ttu-id="10f2c-122">의도한 동작인가요?</span><span class="sxs-lookup"><span data-stu-id="10f2c-122">Is this by design?</span></span>
<span data-ttu-id="10f2c-123">탄력적인 확장 API는 분할 키에 맞는 데이터베이스 연결을 제공하지만 분할 키 필터링 기능을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="10f2c-123">The Elastic Scale APIs give you a connection to the correct database for your sharding key, but do not provide sharding key filtering.</span></span>  <span data-ttu-id="10f2c-124">필요한 경우 쿼리에 **WHERE** 절을 추가하여 범위를 제공된 분할 키로 제한하세요.</span><span class="sxs-lookup"><span data-stu-id="10f2c-124">Add **WHERE** clauses to your query to restrict the scope to the provided sharding key, if necessary.</span></span>

#### <a name="can-i-use-a-different-azure-database-edition-for-each-shard-in-my-shard-set"></a><span data-ttu-id="10f2c-125">내 분할 집합의 각 분할에 대해 다른 Azure 데이터베이스 버전을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="10f2c-125">Can I use a different Azure Database edition for each shard in my shard set?</span></span>
<span data-ttu-id="10f2c-126">예, 분할은 개별 데이터베이스이므로 한 분할은 Premium Edition이고 다른 버전은 Standard Edition일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10f2c-126">Yes, a shard is an individual database, and thus one shard could be a Premium edition while another be a Standard edition.</span></span> <span data-ttu-id="10f2c-127">또한 분할 수명 동안 여러 번 분할 버전의 규모가 확장되거나 축소될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10f2c-127">Further, the edition of a shard can scale up or down multiple times during the lifetime of the shard.</span></span>

#### <a name="does-the-split-merge-tool-provision-or-delete-a-database-during-a-split-or-merge-operation"></a><span data-ttu-id="10f2c-128">분할 또는 병합 작업 중 분할 병합 도구에서 데이터베이스를 프로비전(또는 삭제)하나요?</span><span class="sxs-lookup"><span data-stu-id="10f2c-128">Does the Split Merge tool provision (or delete) a database during a split or merge operation?</span></span>
<span data-ttu-id="10f2c-129">아니요.</span><span class="sxs-lookup"><span data-stu-id="10f2c-129">No.</span></span> <span data-ttu-id="10f2c-130">**분할** 작업의 경우 적절한 스키마를 가진 대상 데이터베이스가 있고 분할된 데이터베이스 맵 관리자에 등록되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10f2c-130">For **split** operations, the target database must exist with the appropriate schema and be registered with the Shard Map Manager.</span></span>  <span data-ttu-id="10f2c-131">**병합** 작업의 경우 분할된 데이터베이스 맵 관리자에서 분할된 데이터베이스를 삭제한 후 데이터베이스를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10f2c-131">For **merge** operations, you must delete the shard from the shard map manager and then delete the database.</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

