---
title: "데이터베이스 재해 복구 훈련 aaaSQL | Microsoft Docs"
description: "업무상 중요 한 비즈니스 응용 프로그램에 대 한 복원 력 있는 toofailures 및 중단 지침 및 Azure SQL 데이터베이스 tooperform 재해 복구 훈련 toohelp 유지를 사용 하기 위한 모범 사례에 알아봅니다."
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
ms.openlocfilehash: bf17857a19fdebddf0d4f55e4db3a1b33efb4e8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="performing-disaster-recovery-drill"></a><span data-ttu-id="9149c-103">재해 복구 훈련 수행</span><span class="sxs-lookup"><span data-stu-id="9149c-103">Performing Disaster Recovery Drill</span></span>
<span data-ttu-id="9149c-104">복구 워크플로에 대한 응용 프로그램 준비의 유효성 검사를 정기적으로 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9149c-104">It is recommended that validation of application readiness for recovery workflow is performed periodically.</span></span> <span data-ttu-id="9149c-105">장애 조치가 수행 되는 hello 응용 프로그램 동작을 확인 하 고 데이터 손실 및/또는 hello 중단의 영향이 엔지니어링 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9149c-105">Verifying hello application behavior and implications of data loss and/or hello disruption that failover involves is a good engineering practice.</span></span> <span data-ttu-id="9149c-106">또한 대부분의 업계 표준에서 비즈니스 연속성 인증의 일부로 요구하는 사항이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="9149c-106">It is also a requirement by most industry standards as part of business continuity certification.</span></span>

<span data-ttu-id="9149c-107">재해 복구 훈련의 수행은 다음으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9149c-107">Performing a disaster recovery drill consists of:</span></span>

* <span data-ttu-id="9149c-108">데이터 계층 중단 시뮬레이션</span><span class="sxs-lookup"><span data-stu-id="9149c-108">Simulating data tier outage</span></span>
* <span data-ttu-id="9149c-109">복구</span><span class="sxs-lookup"><span data-stu-id="9149c-109">Recovering</span></span>
* <span data-ttu-id="9149c-110">복구 후 응용 프로그램 무결성 검사</span><span class="sxs-lookup"><span data-stu-id="9149c-110">Validate application integrity post recovery</span></span>

<span data-ttu-id="9149c-111">방법에 따라 있습니다 [비즈니스 연속성을 위한 응용 프로그램을 디자인](sql-database-business-continuity.md), hello 워크플로 tooexecute hello 드릴 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9149c-111">Depending on how you [designed your application for business continuity](sql-database-business-continuity.md), hello workflow tooexecute hello drill can vary.</span></span> <span data-ttu-id="9149c-112">아래 hello 모범 사례를 수행 하는 Azure SQL 데이터베이스의 hello 컨텍스트에서 재해 복구 훈련과 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9149c-112">Below we describe hello best practices conducting a disaster recovery drill in hello context of Azure SQL Database.</span></span>

## <a name="geo-restore"></a><span data-ttu-id="9149c-113">지역 복원</span><span class="sxs-lookup"><span data-stu-id="9149c-113">Geo-restore</span></span>
<span data-ttu-id="9149c-114">tooprevent hello 가능한 데이터 손실 시 재해 복구 훈련과 권장 테스트 환경을 사용 하 여 hello 프로덕션 환경의 복사본을 만들고 사용 하 여 hello 드릴 수행 tooverify hello 응용 프로그램의 장애 조치 워크플로가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9149c-114">tooprevent hello potential data loss when conducting a disaster recovery drill, we recommend performing hello drill using a test environment by creating a copy of hello production environment and using it tooverify hello application’s failover workflow.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="9149c-115">중단 시뮬레이션</span><span class="sxs-lookup"><span data-stu-id="9149c-115">Outage simulation</span></span>
<span data-ttu-id="9149c-116">toosimulate hello 중단, 삭제 하거나 hello 원본 데이터베이스의 이름을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9149c-116">toosimulate hello outage, you can delete or rename hello source database.</span></span> <span data-ttu-id="9149c-117">그러면 응용 프로그램 연결이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="9149c-117">This causes application connectivity failures.</span></span>

#### <a name="recovery"></a><span data-ttu-id="9149c-118">복구</span><span class="sxs-lookup"><span data-stu-id="9149c-118">Recovery</span></span>
* <span data-ttu-id="9149c-119">설명 된 대로 hello 데이터베이스의 지역에서 복원은 hello를 다른 서버로 수행 [여기](sql-database-disaster-recovery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9149c-119">Perform hello geo-restore of hello database into a different server as described [here](sql-database-disaster-recovery.md).</span></span>
* <span data-ttu-id="9149c-120">변경 hello 응용 프로그램 구성 tooconnect toohello 복구 된 데이터베이스와 다음 hello [복구 후 데이터베이스 구성](sql-database-disaster-recovery.md) toocomplete hello 복구를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="9149c-120">Change hello application configuration tooconnect toohello recovered database and follow hello [Configure a database after recovery](sql-database-disaster-recovery.md) guide toocomplete hello recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="9149c-121">유효성 검사</span><span class="sxs-lookup"><span data-stu-id="9149c-121">Validation</span></span>
* <span data-ttu-id="9149c-122">Hello 응용 프로그램 무결성 post 복구 (연결 문자열, 로그인, 기본 기능 테스트 또는 사인 프로시저 표준 응용 프로그램의 다른 유효성 검사 부분 포함)를 확인 하 여 전체 hello 드릴 합니다.</span><span class="sxs-lookup"><span data-stu-id="9149c-122">Complete hello drill by verifying hello application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="geo-replication"></a><span data-ttu-id="9149c-123">지역에서 복제</span><span class="sxs-lookup"><span data-stu-id="9149c-123">Geo-replication</span></span>
<span data-ttu-id="9149c-124">Hello 드릴 지리적 복제를 사용 하 여 보호 되는 데이터베이스에 대 한 연습에서는 계획 된 장애 조치 toohello 보조 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="9149c-124">For a database that is protected using geo-replication hello drill exercise involves planned failover toohello secondary database.</span></span> <span data-ttu-id="9149c-125">hello 계획 된 장애 조치 하면 hello 기본 및 보조 데이터베이스 hello 남아 있는지 동기화 hello 역할이 전환 된 경우.</span><span class="sxs-lookup"><span data-stu-id="9149c-125">hello planned failover ensures that hello primary and hello secondary databases remain in sync when hello roles are switched.</span></span> <span data-ttu-id="9149c-126">와 달리 hello 계획 되지 않은 장애 조치,이 작업 hello 프로덕션 환경에서 수행할 수 없습니다 hello 드릴 데이터가 손실 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9149c-126">Unlike hello unplanned failover, this operation does not result in data loss, so hello drill can be performed in hello production environment.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="9149c-127">중단 시뮬레이션</span><span class="sxs-lookup"><span data-stu-id="9149c-127">Outage simulation</span></span>
<span data-ttu-id="9149c-128">toosimulate hello 중단 hello 웹 응용 프로그램 또는 연결 된 가상 컴퓨터 toohello 데이터베이스를 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9149c-128">toosimulate hello outage, you can disable hello web application or virtual machine connected toohello database.</span></span> <span data-ttu-id="9149c-129">그러면 웹 클라이언트 hello에 대 한 hello 연결 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="9149c-129">This results in hello connectivity failures for hello web clients.</span></span>

#### <a name="recovery"></a><span data-ttu-id="9149c-130">복구</span><span class="sxs-lookup"><span data-stu-id="9149c-130">Recovery</span></span>
* <span data-ttu-id="9149c-131">DR hello 영역 요소 toohello 전자 보조 hello 됨에서 hello 응용 프로그램 구성 되어 있는지 확인 완벽 하 게 액세스할 수 있는 새로운 주입니다.</span><span class="sxs-lookup"><span data-stu-id="9149c-131">Make sure hello application configuration in hello DR region points toohello former secondary which becomes hello fully accessible new primary.</span></span>
* <span data-ttu-id="9149c-132">수행 [계획 된 장애 조치](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) toomake hello 보조 데이터베이스는 새로운 주 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="9149c-132">Perform [planned failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) toomake hello secondary database a new primary</span></span>
* <span data-ttu-id="9149c-133">Hello에 따라 [복구 후 데이터베이스 구성](sql-database-disaster-recovery.md) toocomplete hello 복구를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="9149c-133">Follow hello [Configure a database after recovery](sql-database-disaster-recovery.md) guide toocomplete hello recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="9149c-134">유효성 검사</span><span class="sxs-lookup"><span data-stu-id="9149c-134">Validation</span></span>
* <span data-ttu-id="9149c-135">Hello 응용 프로그램 무결성 post 복구 (연결 문자열, 로그인, 기본 기능 테스트 또는 사인 프로시저 표준 응용 프로그램의 다른 유효성 검사 부분 포함)를 확인 하 여 전체 hello 드릴 합니다.</span><span class="sxs-lookup"><span data-stu-id="9149c-135">Complete hello drill by verifying hello application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9149c-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9149c-136">Next steps</span></span>
* <span data-ttu-id="9149c-137">비즈니스 연속성 시나리오에 대 한 toolearn 참조 [연속성 시나리오](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="9149c-137">toolearn about business continuity scenarios, see [Continuity scenarios](sql-database-business-continuity.md)</span></span>
* <span data-ttu-id="9149c-138">Azure SQL 데이터베이스 자동화 된 백업에 대 한 toolearn 참조 [자동화 된 백업을 SQL 데이터베이스](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="9149c-138">toolearn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span></span>
* <span data-ttu-id="9149c-139">복구를 위한 자동화 된 백업을 사용 하는 방법에 대 한 toolearn 참조 [hello 서비스 개시 백업에서 데이터베이스를 복원 합니다.](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="9149c-139">toolearn about using automated backups for recovery, see [restore a database from hello service-initiated backups](sql-database-recovery-using-backups.md)</span></span>
* <span data-ttu-id="9149c-140">빠른 복구 옵션에 대 한 toolearn 참조 [활성 지리적 복제](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="9149c-140">toolearn about faster recovery options, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>  
