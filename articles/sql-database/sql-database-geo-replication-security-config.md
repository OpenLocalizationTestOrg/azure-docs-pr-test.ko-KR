---
title: "재해 복구를 위해 Azure SQL Database 보안 구성 | Microsoft Docs"
description: "이 항목에서는 데이터 센터 가동 중단 또는 다른 재해 발생 시 데이터베이스를 복원하거나 보조 서버로 장애 조치 후 보안을 구성하고 관리하기 위한 보안 고려 사항을 설명합니다."
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
ms.openlocfilehash: de5e1732dab570b80692efcdd08e4ed2d8c98800
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a><span data-ttu-id="1fd6a-103">지역 복원 또는 장애 조치를 위해 Azure SQL Database 보안 구성 및 관리</span><span class="sxs-lookup"><span data-stu-id="1fd6a-103">Configure and manage Azure SQL Database security for geo-restore or failover</span></span> 

> [!NOTE]
> <span data-ttu-id="1fd6a-104">[활성 지역 복제](sql-database-geo-replication-overview.md)는 현재 모든 서비스 계층의 모든 데이터베이스에 대해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-104">[Active geo-replication](sql-database-geo-replication-overview.md) is now available for all databases in all service tiers.</span></span>
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a><span data-ttu-id="1fd6a-105">재해 복구에 대한 인증 요구 사항 개요</span><span class="sxs-lookup"><span data-stu-id="1fd6a-105">Overview of authentication requirements for disaster recovery</span></span>
<span data-ttu-id="1fd6a-106">이 항목은 [활성 지역 복제](sql-database-geo-replication-overview.md) 구성 및 제어에 대한 인증 요구 사항 및 보조 데이터베이스에 대한 사용자 액세스 설정이 필요한 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-106">This topic describes the authentication requirements to configure and control [active geo-replication](sql-database-geo-replication-overview.md) and the steps required to set up user access to the secondary database.</span></span> <span data-ttu-id="1fd6a-107">또한 [지역 복원](sql-database-recovery-using-backups.md#geo-restore)을 사용한 후에 복구된 데이터베이스에 대한 액세스를 활성화하는 방법도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-107">It also describes how enable access to the recovered database after using [geo-restore](sql-database-recovery-using-backups.md#geo-restore).</span></span> <span data-ttu-id="1fd6a-108">복구 옵션에 대한 자세한 내용은 [비즈니스 연속성 개요](sql-database-business-continuity.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-108">For more information on recovery options, see [Business Continuity Overview](sql-database-business-continuity.md).</span></span>

## <a name="disaster-recovery-with-contained-users"></a><span data-ttu-id="1fd6a-109">포함된 사용자를 사용한 재해 복구</span><span class="sxs-lookup"><span data-stu-id="1fd6a-109">Disaster recovery with contained users</span></span>
<span data-ttu-id="1fd6a-110">master 데이터베이스에서 로그인에 매핑되어야 하는 기존 사용자와 달리 포함된 사용자는 데이터베이스 자체에서 완전히 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-110">Unlike traditional users, which must be mapped to logins in the master database, a contained user is managed completely by the database itself.</span></span> <span data-ttu-id="1fd6a-111">두 가지 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-111">This has two benefits.</span></span> <span data-ttu-id="1fd6a-112">재해 복구 시나리오에서 데이터베이스는 사용자를 관리하므로 사용자는 추가 구성 없이 지역 복원을 사용하여 복구된 새로운 주 데이터베이스 또는 데이터베이스에 계속해서 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-112">In the disaster recovery scenario, the users can continue to connect to the new primary database or the database recovered using geo-restore without any additional configuration, because the database manages the users.</span></span> <span data-ttu-id="1fd6a-113">로그인 관점에서 이 구성에는 잠재적인 확장성 및 성능 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-113">There are also potential scalability and performance benefits from this configuration from a login perspective.</span></span> <span data-ttu-id="1fd6a-114">자세한 내용은 [포함된 데이터베이스 사용자 - 데이터베이스를 이식 가능하게 만들기](https://msdn.microsoft.com/library/ff929188.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-114">For more information, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span> 

<span data-ttu-id="1fd6a-115">기본 절충점은 대규모로 재해 복구 프로세스를 관리하는 것이 좀 더 어렵다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-115">The main trade-off is that managing the disaster recovery process at scale is more challenging.</span></span> <span data-ttu-id="1fd6a-116">동일한 로그인을 사용하는 여러 데이터베이스가 있는 경우 여러 데이터베이스에 포함된 사용자를 사용하여 자격 증명을 유지 관리하면 포함된 사용자의 이점이 없어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-116">When you have multiple databases that use the same login, maintaining the credentials using contained users in multiple databases may negate the benefits of contained users.</span></span> <span data-ttu-id="1fd6a-117">예를 들어 암호 회전 정책에 따라 마스터 데이터베이스에 한 번 로그인하기 위해 암호를 변경하는 대신 여러 데이터베이스에 변경 내용이 일관되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-117">For example, the password rotation policy requires that changes be made consistently in multiple databases rather than changing the password for the login once in the master database.</span></span> <span data-ttu-id="1fd6a-118">이러한 이유로 동일한 사용자 이름 및 암호를 사용하는 여러 데이터베이스가 있는 경우 포함된 사용자를 사용하는 것은 좋지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-118">For this reason, if you have multiple databases that use the same user name and password, using contained users is not recommended.</span></span> 

## <a name="how-to-configure-logins-and-users"></a><span data-ttu-id="1fd6a-119">로그인 및 사용자를 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="1fd6a-119">How to configure logins and users</span></span>
<span data-ttu-id="1fd6a-120">로그인 및 사용자를 사용하는 경우(포함된 사용자 대신) 마스터 데이터베이스에 동일한 로그인이 존재하는지 보장하는 추가 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-120">If you are using logins and users (rather than contained users), you must take extra steps to insure that the same logins exist in the master database.</span></span> <span data-ttu-id="1fd6a-121">다음 섹션에서는 관련된 단계 및 추가 고려 사항을 간략히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-121">The following sections outline the steps involved and additional considerations.</span></span>

### <a name="set-up-user-access-to-a-secondary-or-recovered-database"></a><span data-ttu-id="1fd6a-122">보조 또는 복구된 데이터베이스에 대한 사용자 액세스 설정</span><span class="sxs-lookup"><span data-stu-id="1fd6a-122">Set up user access to a secondary or recovered database</span></span>
<span data-ttu-id="1fd6a-123">보조 데이터베이스를 읽기 전용 보조 데이터베이스로 사용할 수 있고 새로운 주 데이터베이스 또는 지역 복원 기능을 사용하여 복구된 데이터베이스에 적절하게 액세스할 수 있기 위해 복구하기 전에 대상 서버의 마스터 데이터베이스에 적절한 보안 구성이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-123">In order for the secondary database to be usable as a read-only secondary database, and to ensure proper access to the new primary database or the database recovered using geo-restore, the master database of the target server must have the appropriate security configuration in place before the recovery.</span></span>

<span data-ttu-id="1fd6a-124">각 단계에 대한 특정 사용 권한은 이 항목의 뒷 부분에서 설명됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-124">The specific permissions for each step are described later in this topic.</span></span>

<span data-ttu-id="1fd6a-125">지역에서 복제 보조 데이터베이스에 대한 사용자 액세스를 준비하는 작업은 지역에서 복제를 구성하는 일환으로 수행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-125">Preparing user access to a geo-replication secondary should be performed as part configuring geo-replication.</span></span> <span data-ttu-id="1fd6a-126">지역 복원된 데이터베이스에 대한 사용자 액세스를 준비하는 작업은 원래 서버가 온라인인 경우 언제든지 수행되어야 합니다(예: DR 드릴의 일부).</span><span class="sxs-lookup"><span data-stu-id="1fd6a-126">Preparing user access to the geo-restored databases should be performed at any time when the original server is online (e.g. as part of the DR drill).</span></span>

> [!NOTE]
> <span data-ttu-id="1fd6a-127">적절히 구성된 로그인 액세스가 없는 서버에 장애 조치 또는 지역 복원을 수행하는 경우 서버 관리자 계정으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-127">If you fail over or geo-restore to a server that does not have properly configured logins, access to it will be limited to the server admin account.</span></span>
> 
> 

<span data-ttu-id="1fd6a-128">대상 서버에서 로그인을 설정하는 작업은 아래에서 설명할 세 가지 단계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-128">Setting up logins on the target server involves three steps outlined below:</span></span>

#### <a name="1-determine-logins-with-access-to-the-primary-database"></a><span data-ttu-id="1fd6a-129">1. 주 데이터베이스에 대한 액세스를 사용하여 로그인을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-129">1. Determine logins with access to the primary database:</span></span>
<span data-ttu-id="1fd6a-130">프로세스의 첫 번째 단계는 대상 서버에 중복되어야 하는 로그인을 결정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-130">The first step of the process is to determine which logins must be duplicated on the target server.</span></span> <span data-ttu-id="1fd6a-131">이는 원본 서버의 논리적 master 데이터베이스에 있는 하나와 주 데이터베이스 자체에 있는 하나로 이루어진 SELECT 문 쌍으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-131">This is accomplished with a pair of SELECT statements, one in the logical master database on the source server and one in the primary database itself.</span></span>

<span data-ttu-id="1fd6a-132">서버 관리자 또는 **LoginManager** 서버 역할의 멤버만 다음 SELECT 문을 사용하여 원본 서버에서 로그인을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-132">Only the server admin or a member of the **LoginManager** server role can determine the logins on the source server with the following SELECT statement.</span></span> 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

<span data-ttu-id="1fd6a-133">db_owner 데이터베이스 역할의 멤버, dbo 사용자 또는 서버 관리자만 주 데이터베이스에서 모든 데이터베이스 사용자 계정을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-133">Only a member of the db_owner database role, the dbo user, or server admin, can determine all of the database user principals in the primary database.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-the-sid-for-the-logins-identified-in-step-1"></a><span data-ttu-id="1fd6a-134">2. 1단계에서 확인된 로그인에 대한 SID를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-134">2. Find the SID for the logins identified in step 1:</span></span>
<span data-ttu-id="1fd6a-135">이전 섹션에서 쿼리의 출력을 비교하고 SID와 일치하여 서버 로그인을 데이터베이스 사용자에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-135">By comparing the output of the queries from the previous section and matching the SIDs, you can map the server login to database user.</span></span> <span data-ttu-id="1fd6a-136">일치하는 SID가 있는 데이터베이스 사용자를 가진 로그인은 해당 데이터베이스 사용자 계정으로 해당 데이터베이스에 대한 사용자 액세스를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-136">Logins that have a database user with a matching SID have user access to that database as that database user principal.</span></span> 

<span data-ttu-id="1fd6a-137">다음 쿼리를 사용하여 데이터베이스에서 모든 사용자 계정 및 해당 SID를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-137">The following query can be used to see all of the user principals and their SIDs in a database.</span></span> <span data-ttu-id="1fd6a-138">db_owner 데이터베이스 역할의 멤버 또는 서버 관리자만 이 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-138">Only a member of the db_owner database role or server admin can run this query.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> <span data-ttu-id="1fd6a-139">**INFORMATION_SCHEMA** 및 **sys** 사용자는 *NULL* SID가 있으며 **게스트** SID는 **0x00**입니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-139">The **INFORMATION_SCHEMA** and **sys** users have *NULL* SIDs, and the **guest** SID is **0x00**.</span></span> <span data-ttu-id="1fd6a-140">데이터베이스 작성자가 **DbManager**의 멤버가 아닌 서버 관리자인 경우 **dbo** SID는 *0x01060000000001648000000000048454*로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-140">The **dbo** SID may start with *0x01060000000001648000000000048454*, if the database creator was the server admin instead of a member of **DbManager**.</span></span>
> 
> 

#### <a name="3-create-the-logins-on-the-target-server"></a><span data-ttu-id="1fd6a-141">3. 대상 서버의 로그인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-141">3. Create the logins on the target server:</span></span>
<span data-ttu-id="1fd6a-142">마지막 단계는 대상 서버 또는 서버로 이동하고 적절한 SID를 사용하여 로그인을 생성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-142">The last step is to go to the target server, or servers, and generate the logins with the appropriate SIDs.</span></span> <span data-ttu-id="1fd6a-143">기본 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-143">The basic syntax is as follows.</span></span>

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> <span data-ttu-id="1fd6a-144">주 데이터베이스가 아닌 보조 데이터베이스에 사용자 액세스 권한을 부여하려는 경우 주 서버의 사용자 로그인을 변경하고 다음 구문을 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-144">If you want to grant user access to the secondary, but not to the primary, you can do that by altering the user login on the primary server by using the following syntax.</span></span>
> 
> <span data-ttu-id="1fd6a-145">ALTER LOGIN <login name> DISABLE</span><span class="sxs-lookup"><span data-stu-id="1fd6a-145">ALTER LOGIN <login name> DISABLE</span></span>
> 
> <span data-ttu-id="1fd6a-146">DISABLE은 암호를 변경하지 않으므로 필요한 경우 항상 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-146">DISABLE doesn’t change the password, so you can always enable it if needed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="1fd6a-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1fd6a-147">Next steps</span></span>
* <span data-ttu-id="1fd6a-148">데이터베이스 액세스 및 로그인 관리에 대한 자세한 내용은 [SQL 데이터베이스 보안: 데이터베이스 액세스 및 로그인 보안 관리](sql-database-manage-logins.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-148">For more information on managing database access and logins, see [SQL Database security: Manage database access and login security](sql-database-manage-logins.md).</span></span>
* <span data-ttu-id="1fd6a-149">포함된 데이터베이스 사용자에 대한 자세한 내용은 [포함된 데이터베이스 사용자 - 데이터베이스를 이식 가능하게 만들기](https://msdn.microsoft.com/library/ff929188.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-149">For more information on contained database users, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span>
* <span data-ttu-id="1fd6a-150">활성 지역 복제를 사용 및 구성하는 방법에 대한 자세한 내용은 [활성 지역 복제](sql-database-geo-replication-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-150">For information about using and configuring active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>
* <span data-ttu-id="1fd6a-151">지역 복원을 사용하는 방법에 대한 내용은 [지역 복원](sql-database-recovery-using-backups.md#geo-restore)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fd6a-151">For information about using geo-restore, see [geo-restore](sql-database-recovery-using-backups.md#geo-restore)</span></span>

