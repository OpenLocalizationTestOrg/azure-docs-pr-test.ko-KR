---
title: "SQL Database 재해 복구 훈련 | Microsoft Docs"
description: "Azure SQL Database를 사용하여 중요 업무용 비즈니스 응용 프로그램이 오류 및 중단에 대한 복원력을 유지하기 위해 재해 복구 훈련을 수행하는 과정에 대한 지침과 모범 사례에 대해 알아봅니다."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: b44a269c-fe2a-404f-b013-290030860bd1
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/31/2016
ms.author: sashan
ms.openlocfilehash: 1b1d65a41a794a566287dcffe3581ac58e2a965f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="performing-disaster-recovery-drill"></a><span data-ttu-id="1d91c-103">재해 복구 훈련 수행</span><span class="sxs-lookup"><span data-stu-id="1d91c-103">Performing Disaster Recovery Drill</span></span>
<span data-ttu-id="1d91c-104">복구 워크플로에 대한 응용 프로그램 준비의 유효성 검사를 정기적으로 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1d91c-104">It is recommended that validation of application readiness for recovery workflow is performed periodically.</span></span> <span data-ttu-id="1d91c-105">응용 프로그램 동작과 데이터 손실의 영향 및/또는 장애 조치(failover)와 관련된 중단을 검사하는 것은 적절한 엔지니어링 실무입니다.</span><span class="sxs-lookup"><span data-stu-id="1d91c-105">Verifying the application behavior and implications of data loss and/or the disruption that failover involves is a good engineering practice.</span></span> <span data-ttu-id="1d91c-106">또한 대부분의 업계 표준에서 비즈니스 연속성 인증의 일부로 요구하는 사항이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d91c-106">It is also a requirement by most industry standards as part of business continuity certification.</span></span>

<span data-ttu-id="1d91c-107">재해 복구 훈련의 수행은 다음으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d91c-107">Performing a disaster recovery drill consists of:</span></span>

* <span data-ttu-id="1d91c-108">데이터 계층 중단 시뮬레이션</span><span class="sxs-lookup"><span data-stu-id="1d91c-108">Simulating data tier outage</span></span>
* <span data-ttu-id="1d91c-109">복구</span><span class="sxs-lookup"><span data-stu-id="1d91c-109">Recovering</span></span>
* <span data-ttu-id="1d91c-110">복구 후 응용 프로그램 무결성 검사</span><span class="sxs-lookup"><span data-stu-id="1d91c-110">Validate application integrity post recovery</span></span>

<span data-ttu-id="1d91c-111">[비즈니스 연속성을 위한 응용 프로그램 설계](sql-database-business-continuity.md)방법에 따라 연습을 실행하는 워크플로가 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d91c-111">Depending on how you [designed your application for business continuity](sql-database-business-continuity.md), the workflow to execute the drill can vary.</span></span> <span data-ttu-id="1d91c-112">아래에 Azure SQL 데이터베이스와 관련하여 재해 복구 훈련을 수행하는 모범 사례가 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d91c-112">Below we describe the best practices conducting a disaster recovery drill in the context of Azure SQL Database.</span></span>

## <a name="geo-restore"></a><span data-ttu-id="1d91c-113">지역 복원</span><span class="sxs-lookup"><span data-stu-id="1d91c-113">Geo-restore</span></span>
<span data-ttu-id="1d91c-114">재해 복구 훈련을 수행할 때 잠재적인 데이터 손실을 방지하려면, 프로덕션 환경의 복사본을 만들고 이를 응용 프로그램의 장애 조치 워크플로를 검사하는 데 사용하는 방법으로 훈련을 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1d91c-114">To prevent the potential data loss when conducting a disaster recovery drill, we recommend performing the drill using a test environment by creating a copy of the production environment and using it to verify the application’s failover workflow.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="1d91c-115">중단 시뮬레이션</span><span class="sxs-lookup"><span data-stu-id="1d91c-115">Outage simulation</span></span>
<span data-ttu-id="1d91c-116">중단을 시뮬레이션하기 위해 원본 데이터베이스를 삭제하거나 이름을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d91c-116">To simulate the outage, you can delete or rename the source database.</span></span> <span data-ttu-id="1d91c-117">그러면 응용 프로그램 연결이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="1d91c-117">This causes application connectivity failures.</span></span>

#### <a name="recovery"></a><span data-ttu-id="1d91c-118">복구</span><span class="sxs-lookup"><span data-stu-id="1d91c-118">Recovery</span></span>
* <span data-ttu-id="1d91c-119">[여기](sql-database-disaster-recovery.md)에 설명된 대로 서로 다른 서버에 데이터베이스의 지역 복원을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1d91c-119">Perform the geo-restore of the database into a different server as described [here](sql-database-disaster-recovery.md).</span></span>
* <span data-ttu-id="1d91c-120">복구된 데이터베이스에 연결하도록 응용 프로그램 구성을 변경하고 [복구 후 데이터베이스 구성](sql-database-disaster-recovery.md) 가이드에 따라 복구를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1d91c-120">Change the application configuration to connect to the recovered database and follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="1d91c-121">유효성 검사</span><span class="sxs-lookup"><span data-stu-id="1d91c-121">Validation</span></span>
* <span data-ttu-id="1d91c-122">복구 후 응용 프로그램 무결성 검사(연결 문자열, 로그인, 기본 기능 테스트 또는 기타 표준 응용 프로그램 로그아웃 절차의 유효성 검사 부분 포함)로 훈련을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1d91c-122">Complete the drill by verifying the application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="geo-replication"></a><span data-ttu-id="1d91c-123">지역에서 복제</span><span class="sxs-lookup"><span data-stu-id="1d91c-123">Geo-replication</span></span>
<span data-ttu-id="1d91c-124">지역에서 복제를 사용하여 보호되는 데이터베이스의 경우에는 보조 데이터베이스로의 계획된 장애 조치가 연습에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d91c-124">For a database that is protected using geo-replication the drill exercise involves planned failover to the secondary database.</span></span> <span data-ttu-id="1d91c-125">계획된 장애 조치(failover)는 역할이 전환될 때 주 데이터베이스와 보조 데이터베이스가 동기화 상태로 유지되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d91c-125">The planned failover ensures that the primary and the secondary databases remain in sync when the roles are switched.</span></span> <span data-ttu-id="1d91c-126">계획되지 않은 장애 조치와 달리 이 작업에서는 데이터가 손실되지 않으므로 프로덕션 환경에서 연습을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d91c-126">Unlike the unplanned failover, this operation does not result in data loss, so the drill can be performed in the production environment.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="1d91c-127">중단 시뮬레이션</span><span class="sxs-lookup"><span data-stu-id="1d91c-127">Outage simulation</span></span>
<span data-ttu-id="1d91c-128">중단을 시뮬레이션하기 위해 데이터베이스에 연결된 웹 응용 프로그램 또는 가상 컴퓨터를 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d91c-128">To simulate the outage, you can disable the web application or virtual machine connected to the database.</span></span> <span data-ttu-id="1d91c-129">그러면 웹 클라이언트에 대한 연결이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="1d91c-129">This results in the connectivity failures for the web clients.</span></span>

#### <a name="recovery"></a><span data-ttu-id="1d91c-130">복구</span><span class="sxs-lookup"><span data-stu-id="1d91c-130">Recovery</span></span>
* <span data-ttu-id="1d91c-131">DR 지역의 응용 프로그램 구성이 완전히 액세스 가능한 새로운 주 데이터베이스가 될 이전의 보조 데이터베이스를 가리키는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1d91c-131">Make sure the application configuration in the DR region points to the former secondary which becomes the fully accessible new primary.</span></span>
* <span data-ttu-id="1d91c-132">[계획된 장애 조치(failover)](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) 를 수행하여 보조 데이터베이스를 새로운 주 데이터베이스로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1d91c-132">Perform [planned failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) to make the secondary database a new primary</span></span>
* <span data-ttu-id="1d91c-133">[복구 후 데이터베이스 구성](sql-database-disaster-recovery.md) 가이드에 따라 복구를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1d91c-133">Follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="1d91c-134">유효성 검사</span><span class="sxs-lookup"><span data-stu-id="1d91c-134">Validation</span></span>
* <span data-ttu-id="1d91c-135">복구 후 응용 프로그램 무결성 검사(연결 문자열, 로그인, 기본 기능 테스트 또는 기타 표준 응용 프로그램 로그아웃 절차의 유효성 검사 부분 포함)로 훈련을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1d91c-135">Complete the drill by verifying the application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d91c-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1d91c-136">Next steps</span></span>
* <span data-ttu-id="1d91c-137">비즈니스 연속성 시나리오에 대해 알아보려면 [연속성 시나리오](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="1d91c-137">To learn about business continuity scenarios, see [Continuity scenarios](sql-database-business-continuity.md)</span></span>
* <span data-ttu-id="1d91c-138">Azure SQL 데이터베이스 자동화 백업에 대한 자세한 내용은 [SQL 데이터베이스 자동화 백업](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="1d91c-138">To learn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span></span>
* <span data-ttu-id="1d91c-139">복구를 위해 자동화된 백업을 사용하는 방법을 알아보려면 [서비스에서 시작한 백업에서 데이터베이스 복원](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="1d91c-139">To learn about using automated backups for recovery, see [restore a database from the service-initiated backups](sql-database-recovery-using-backups.md)</span></span>
* <span data-ttu-id="1d91c-140">빠른 복구 옵션에 대해 알아보려면 [활성 지역 복제](sql-database-geo-replication-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d91c-140">To learn about faster recovery options, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>  
