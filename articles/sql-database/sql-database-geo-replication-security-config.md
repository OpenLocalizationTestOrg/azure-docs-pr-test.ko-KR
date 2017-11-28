---
title: "재해 복구에 대 한 Azure SQL 데이터베이스 보안 aaaConfigure | Microsoft Docs"
description: "이 항목에서는 구성 및 데이터베이스 복원 또는 장애 조치 tooa 보조 서버에서 데이터 센터 중단 이나 다른 재해의 hello 이벤트 후 보안 관리에 대 한 보안 고려 사항 설명"
services: sql-database
documentationcenter: na
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: c7c898c9-69d4-4e16-8b7e-720bbb3353dd
ms.service: sql-database
ms.custom: business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 10/13/2016
ms.author: sashan
ms.openlocfilehash: c3172568e1b8ad2a53958200aa6cf19b4a9434ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a><span data-ttu-id="05049-103">지역 복원 또는 장애 조치를 위해 Azure SQL Database 보안 구성 및 관리</span><span class="sxs-lookup"><span data-stu-id="05049-103">Configure and manage Azure SQL Database security for geo-restore or failover</span></span> 

> [!NOTE]
> <span data-ttu-id="05049-104">[활성 지역 복제](sql-database-geo-replication-overview.md)는 현재 모든 서비스 계층의 모든 데이터베이스에 대해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="05049-104">[Active geo-replication](sql-database-geo-replication-overview.md) is now available for all databases in all service tiers.</span></span>
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a><span data-ttu-id="05049-105">재해 복구에 대한 인증 요구 사항 개요</span><span class="sxs-lookup"><span data-stu-id="05049-105">Overview of authentication requirements for disaster recovery</span></span>
<span data-ttu-id="05049-106">인증 요구 사항 tooconfigure hello 및 제어에 설명 [활성 지리적 복제](sql-database-geo-replication-overview.md) 한 hello 필요한 tooset 사용자 액세스 toohello 보조 데이터베이스를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="05049-106">This topic describes hello authentication requirements tooconfigure and control [active geo-replication](sql-database-geo-replication-overview.md) and hello steps required tooset up user access toohello secondary database.</span></span> <span data-ttu-id="05049-107">에 대해서도 설명 하려면 어떻게 해야 액세스 toohello 복구 된 데이터베이스를 사용한 후 [지역에서 복원은](sql-database-recovery-using-backups.md#geo-restore)합니다.</span><span class="sxs-lookup"><span data-stu-id="05049-107">It also describes how enable access toohello recovered database after using [geo-restore](sql-database-recovery-using-backups.md#geo-restore).</span></span> <span data-ttu-id="05049-108">복구 옵션에 대한 자세한 내용은 [비즈니스 연속성 개요](sql-database-business-continuity.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05049-108">For more information on recovery options, see [Business Continuity Overview](sql-database-business-continuity.md).</span></span>

## <a name="disaster-recovery-with-contained-users"></a><span data-ttu-id="05049-109">포함된 사용자를 사용한 재해 복구</span><span class="sxs-lookup"><span data-stu-id="05049-109">Disaster recovery with contained users</span></span>
<span data-ttu-id="05049-110">기존 사용자와 달리 toologins hello master 데이터베이스에 매핑된 이어야, hello 데이터베이스 자체가 포함된 된 사용자를 완전히 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="05049-110">Unlike traditional users, which must be mapped toologins in hello master database, a contained user is managed completely by hello database itself.</span></span> <span data-ttu-id="05049-111">두 가지 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05049-111">This has two benefits.</span></span> <span data-ttu-id="05049-112">Hello 재해 복구 시나리오에서 hello 사용자 tooconnect toohello 새로운 주 데이터베이스 또는 모든 추가 구성 없이 지역 복원을 사용 하 여 hello 데이터베이스 hello 사용자를 관리 하기 때문에 복구 하는 hello 데이터베이스 계속 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05049-112">In hello disaster recovery scenario, hello users can continue tooconnect toohello new primary database or hello database recovered using geo-restore without any additional configuration, because hello database manages hello users.</span></span> <span data-ttu-id="05049-113">로그인 관점에서 이 구성에는 잠재적인 확장성 및 성능 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05049-113">There are also potential scalability and performance benefits from this configuration from a login perspective.</span></span> <span data-ttu-id="05049-114">자세한 내용은 [포함된 데이터베이스 사용자 - 데이터베이스를 이식 가능하게 만들기](https://msdn.microsoft.com/library/ff929188.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05049-114">For more information, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span> 

<span data-ttu-id="05049-115">hello 주 절충 배율로 hello 재해 복구 프로세스를 관리 합니다. 가장 까다로운 된다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="05049-115">hello main trade-off is that managing hello disaster recovery process at scale is more challenging.</span></span> <span data-ttu-id="05049-116">데이터베이스가 여러 개 포함 된 동일한 로그인을 사용 하 여 hello 자격 증명을 유지 관리를 사용 하 여 hello 있을 때 여러 데이터베이스에 사용자가 포함 된 사용자의 hello 이점을 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05049-116">When you have multiple databases that use hello same login, maintaining hello credentials using contained users in multiple databases may negate hello benefits of contained users.</span></span> <span data-ttu-id="05049-117">예를 들어 hello 암호 회전 정책 변경 내용 수 있어야 일관 되 게 여러 아니라 데이터베이스에 hello 로그인에 대 한 hello 암호를 변경할 한 번 hello master 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05049-117">For example, hello password rotation policy requires that changes be made consistently in multiple databases rather than changing hello password for hello login once in hello master database.</span></span> <span data-ttu-id="05049-118">이러한 이유로, 여러 데이터베이스를 사용 하 여 hello 있는 경우 동일한 사용자 이름 및 암호 포함 된 사용자를 사용 하 여 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05049-118">For this reason, if you have multiple databases that use hello same user name and password, using contained users is not recommended.</span></span> 

## <a name="how-tooconfigure-logins-and-users"></a><span data-ttu-id="05049-119">어떻게 tooconfigure 로그인 및 사용자</span><span class="sxs-lookup"><span data-stu-id="05049-119">How tooconfigure logins and users</span></span>
<span data-ttu-id="05049-120">로그인 및 사용자를 사용 하는 경우 (포함 된 사용자의 경우) 하는 대신 취해야 추가 단계 tooinsure 동일한 로그인이 있는 해당 hello hello master 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05049-120">If you are using logins and users (rather than contained users), you must take extra steps tooinsure that hello same logins exist in hello master database.</span></span> <span data-ttu-id="05049-121">hello 다음 섹션에는 정리 hello 단계 추가 관련 된 고려 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="05049-121">hello following sections outline hello steps involved and additional considerations.</span></span>

### <a name="set-up-user-access-tooa-secondary-or-recovered-database"></a><span data-ttu-id="05049-122">사용자 액세스 tooa 보조 또는 복구 된 데이터베이스 설정</span><span class="sxs-lookup"><span data-stu-id="05049-122">Set up user access tooa secondary or recovered database</span></span>
<span data-ttu-id="05049-123">사용 가능한 hello 보조 데이터베이스 toobe에 대 한 읽기 전용 보조 데이터베이스와 tooensure 적절 한 액세스 toohello 새로운 주 데이터베이스 또는 hello 데이터베이스 지역에서 복원을 사용 하 여 복구할 hello 마스터으로 hello 대상 서버의 데이터베이스 있어야 hello hello 복구 하기 전에 적절 한 보안 구성이입니다.</span><span class="sxs-lookup"><span data-stu-id="05049-123">In order for hello secondary database toobe usable as a read-only secondary database, and tooensure proper access toohello new primary database or hello database recovered using geo-restore, hello master database of hello target server must have hello appropriate security configuration in place before hello recovery.</span></span>

<span data-ttu-id="05049-124">각 단계에 대 한 특정 권한은 hello이이 항목의 뒷부분에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05049-124">hello specific permissions for each step are described later in this topic.</span></span>

<span data-ttu-id="05049-125">사용자 액세스 tooa 준비 지리적 복제 보조를 지리적 복제를 구성 하는 일환으로 수행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05049-125">Preparing user access tooa geo-replication secondary should be performed as part configuring geo-replication.</span></span> <span data-ttu-id="05049-126">Toohello 지리적 복원 된 데이터베이스 사용자 액세스 준비 언제 든 지 원래 서버 hello 온라인임 수행 합니다 (예: 일부로 hello DR 드릴의).</span><span class="sxs-lookup"><span data-stu-id="05049-126">Preparing user access toohello geo-restored databases should be performed at any time when hello original server is online (e.g. as part of hello DR drill).</span></span>

> [!NOTE]
> <span data-ttu-id="05049-127">실패 하면 올바르게 구성 된 로그인 하지 않은 또는 병렬 지역에서 복원은 tooa 서버 액세스 tooit 제한 toohello 서버 관리자 계정이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05049-127">If you fail over or geo-restore tooa server that does not have properly configured logins, access tooit will be limited toohello server admin account.</span></span>
> 
> 

<span data-ttu-id="05049-128">Hello 대상 서버의 로그인을 설정 하는 작업 아래에 설명 된 3 단계:</span><span class="sxs-lookup"><span data-stu-id="05049-128">Setting up logins on hello target server involves three steps outlined below:</span></span>

#### <a name="1-determine-logins-with-access-toohello-primary-database"></a><span data-ttu-id="05049-129">1. Access toohello 주 데이터베이스를 사용 하 여 로그인을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="05049-129">1. Determine logins with access toohello primary database:</span></span>
<span data-ttu-id="05049-130">hello hello 프로세스의 첫 번째 단계는 toodetermine hello 대상 서버에 있는 로그인을 복제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05049-130">hello first step of hello process is toodetermine which logins must be duplicated on hello target server.</span></span> <span data-ttu-id="05049-131">이 옵션은 SELECT 문과 hello hello 원본 서버의 논리적 master 데이터베이스에서 자체 hello 주 데이터베이스에서 쌍으로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05049-131">This is accomplished with a pair of SELECT statements, one in hello logical master database on hello source server and one in hello primary database itself.</span></span>

<span data-ttu-id="05049-132">서버 관리자 또는 hello의 구성원만 hello **LoginManager** 서버 역할 SELECT 문 다음 hello로 hello 원본 서버에서 hello 로그인을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05049-132">Only hello server admin or a member of hello **LoginManager** server role can determine hello logins on hello source server with hello following SELECT statement.</span></span> 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

<span data-ttu-id="05049-133">Hello db_owner 데이터베이스 역할, hello dbo 사용자 또는 서버 관리자의 구성원만 모든 주 데이터베이스 hello hello 데이터베이스 사용자 계정을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05049-133">Only a member of hello db_owner database role, hello dbo user, or server admin, can determine all of hello database user principals in hello primary database.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-hello-sid-for-hello-logins-identified-in-step-1"></a><span data-ttu-id="05049-134">2. 1 단계에서 식별 하는 hello 로그인에 대 한 hello를 SID를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="05049-134">2. Find hello SID for hello logins identified in step 1:</span></span>
<span data-ttu-id="05049-135">Hello 쿼리의 출력을 hello hello 이전 섹션에서 일치 하는 hello Sid 비교 하 여 hello 서버 로그인 toodatabase 사용자를 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05049-135">By comparing hello output of hello queries from hello previous section and matching hello SIDs, you can map hello server login toodatabase user.</span></span> <span data-ttu-id="05049-136">사용자 액세스 toothat 데이터베이스와 해당 데이터베이스 사용자 계정이 있어야 하는 일치 하는 SID 가진 데이터베이스 사용자가 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="05049-136">Logins that have a database user with a matching SID have user access toothat database as that database user principal.</span></span> 

<span data-ttu-id="05049-137">hello 다음 쿼리 수 toosee 사용 되는 모든 hello 사용자 계정 및 데이터베이스에서 해당 Sid입니다.</span><span class="sxs-lookup"><span data-stu-id="05049-137">hello following query can be used toosee all of hello user principals and their SIDs in a database.</span></span> <span data-ttu-id="05049-138">Hello db_owner 데이터베이스 역할 또는 서버 관리자의 구성원만이 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05049-138">Only a member of hello db_owner database role or server admin can run this query.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> <span data-ttu-id="05049-139">hello **INFORMATION_SCHEMA** 및 **sys** 사용자에 게 *NULL* Sid 및 hello **게스트** SID는 **0x00**합니다.</span><span class="sxs-lookup"><span data-stu-id="05049-139">hello **INFORMATION_SCHEMA** and **sys** users have *NULL* SIDs, and hello **guest** SID is **0x00**.</span></span> <span data-ttu-id="05049-140">hello **dbo** SID로 시작할 수 *0x01060000000001648000000000048454*hello 데이터베이스 작성자가 구성원이 아닌 서버 admin 님 안녕하세요, **DbManager**합니다.</span><span class="sxs-lookup"><span data-stu-id="05049-140">hello **dbo** SID may start with *0x01060000000001648000000000048454*, if hello database creator was hello server admin instead of a member of **DbManager**.</span></span>
> 
> 

#### <a name="3-create-hello-logins-on-hello-target-server"></a><span data-ttu-id="05049-141">3. 대상 서버 hello에 hello 로그인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05049-141">3. Create hello logins on hello target server:</span></span>
<span data-ttu-id="05049-142">hello 마지막 단계는 toogo toohello 대상 서버 또는 서버 이며 생성 hello 사용 하 여 hello 로그인 Sid 적절 합니다.</span><span class="sxs-lookup"><span data-stu-id="05049-142">hello last step is toogo toohello target server, or servers, and generate hello logins with hello appropriate SIDs.</span></span> <span data-ttu-id="05049-143">hello 기본 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="05049-143">hello basic syntax is as follows.</span></span>

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> <span data-ttu-id="05049-144">원할 경우 toogrant 사용자 액세스 toohello 보조 하지만 하지 toohello 주 하는 구문 다음 hello를 사용 하 여 hello 주 서버의 hello 사용자 로그인을 변경 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05049-144">If you want toogrant user access toohello secondary, but not toohello primary, you can do that by altering hello user login on hello primary server by using hello following syntax.</span></span>
> 
> <span data-ttu-id="05049-145">ALTER LOGIN <login name> DISABLE</span><span class="sxs-lookup"><span data-stu-id="05049-145">ALTER LOGIN <login name> DISABLE</span></span>
> 
> <span data-ttu-id="05049-146">필요한 경우 항상 사용할 수 있도록 사용 안 함 hello 암호를 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05049-146">DISABLE doesn’t change hello password, so you can always enable it if needed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="05049-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="05049-147">Next steps</span></span>
* <span data-ttu-id="05049-148">데이터베이스 액세스 및 로그인 관리에 대한 자세한 내용은 [SQL 데이터베이스 보안: 데이터베이스 액세스 및 로그인 보안 관리](sql-database-manage-logins.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05049-148">For more information on managing database access and logins, see [SQL Database security: Manage database access and login security](sql-database-manage-logins.md).</span></span>
* <span data-ttu-id="05049-149">포함된 데이터베이스 사용자에 대한 자세한 내용은 [포함된 데이터베이스 사용자 - 데이터베이스를 이식 가능하게 만들기](https://msdn.microsoft.com/library/ff929188.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05049-149">For more information on contained database users, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span>
* <span data-ttu-id="05049-150">활성 지역 복제를 사용 및 구성하는 방법에 대한 자세한 내용은 [활성 지역 복제](sql-database-geo-replication-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05049-150">For information about using and configuring active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>
* <span data-ttu-id="05049-151">지역 복원을 사용하는 방법에 대한 내용은 [지역 복원](sql-database-recovery-using-backups.md#geo-restore)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05049-151">For information about using geo-restore, see [geo-restore](sql-database-recovery-using-backups.md#geo-restore)</span></span>

