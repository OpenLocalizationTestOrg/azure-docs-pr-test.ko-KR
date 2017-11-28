---
title: "Azure SQL 데이터베이스 aaaCopy | Microsoft Docs"
description: "Azure SQL 데이터베이스 사본 만들기"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5aaf6bcd-3839-49b5-8c77-cbdf786e359b
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 64a297d819d6da89600fda60abe8394ae405abfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-an-azure-sql-database"></a><span data-ttu-id="88b7d-103">Azure SQL 데이터베이스 복사</span><span class="sxs-lookup"><span data-stu-id="88b7d-103">Copy an Azure SQL database</span></span>

<span data-ttu-id="88b7d-104">Azure SQL 데이터베이스 제공 동일 하거나 hello에 기존 Azure SQL의 일관성이 복사본을 만드는 여러 가지 방법을 데이터베이스 서버나 다른 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-104">Azure SQL Database provides several methods for creating a transactionally consistent copy of an existing Azure SQL database on either hello same server or a different server.</span></span> <span data-ttu-id="88b7d-105">Hello Azure 포털, PowerShell 또는 T-SQL을 사용 하 여 SQL 데이터베이스를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-105">You can copy a SQL database by using hello Azure portal, PowerShell, or T-SQL.</span></span> 

## <a name="overview"></a><span data-ttu-id="88b7d-106">개요</span><span class="sxs-lookup"><span data-stu-id="88b7d-106">Overview</span></span>

<span data-ttu-id="88b7d-107">데이터베이스 복사본은 복사 요청 hello hello 시간을 기준으로 hello 원본 데이터베이스의 스냅숏입니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-107">A database copy is a snapshot of hello source database as of hello time of hello copy request.</span></span> <span data-ttu-id="88b7d-108">선택할 수 있습니다 동일한 서버 또는 다른 서버, 서비스 계층과 성능 수준이, 또는 hello 내에서 다른 성능 수준 hello 동일한 서비스 계층 (버전).</span><span class="sxs-lookup"><span data-stu-id="88b7d-108">You can select hello same server or a different server, its service tier and performance level, or a different performance level within hello same service tier (edition).</span></span> <span data-ttu-id="88b7d-109">Hello 복사가 완료 된 후에 완벽 하 게 작동 되는, 독립적인 데이터베이스 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-109">After hello copy is complete, it becomes a fully functional, independent database.</span></span> <span data-ttu-id="88b7d-110">이 시점에서 업그레이드 하거나 tooany 버전 다운 그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-110">At this point, you can upgrade or downgrade it tooany edition.</span></span> <span data-ttu-id="88b7d-111">hello 로그인, 사용자 및 사용 권한 수 독립적으로 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-111">hello logins, users, and permissions can be managed independently.</span></span>  

## <a name="logins-in-hello-database-copy"></a><span data-ttu-id="88b7d-112">Hello 데이터베이스 복사본의 로그인</span><span class="sxs-lookup"><span data-stu-id="88b7d-112">Logins in hello database copy</span></span>

<span data-ttu-id="88b7d-113">데이터베이스 toohello를 복사 하는 경우 동일한 논리 서버, hello 두 데이터베이스 모두에 동일한 로그인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-113">When you copy a database toohello same logical server, hello same logins can be used on both databases.</span></span> <span data-ttu-id="88b7d-114">hello 보안 toocopy hello 데이터베이스를 사용 하 여 사용자에 hello 새 데이터베이스에 hello 데이터베이스 소유자가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-114">hello security principal you use toocopy hello database becomes hello database owner on hello new database.</span></span> <span data-ttu-id="88b7d-115">모든 데이터베이스 사용자, 해당 사용 권한 및의 보안 식별자 (Sid)가 toohello 데이터베이스 복사본을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-115">All database users, their permissions, and their security identifiers (SIDs) are copied toohello database copy.</span></span>  

<span data-ttu-id="88b7d-116">데이터베이스 tooa 다른 논리 서버로 복사할 때 hello 보안 hello 새 서버에서 사용자에 hello 새 데이터베이스에 hello 데이터베이스 소유자가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-116">When you copy a database tooa different logical server, hello security principal on hello new server becomes hello database owner on hello new database.</span></span> <span data-ttu-id="88b7d-117">사용 하는 경우 [포함 된 데이터베이스 사용자](sql-database-manage-logins.md) 데이터 액세스를 위해 다음과 같이 모두 hello 기본 및 보조 데이터베이스는 항상 hello 하는 hello 복사 된 후 완료 하면 되므로 동일한 사용자 자격 증명에 즉시 액세스할 수 있는 동일한 hello 사용 하 여 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-117">If you use [contained database users](sql-database-manage-logins.md) for data access, ensure that both hello primary and secondary databases always have hello same user credentials, so that after hello copy is complete you can immediately access it with hello same credentials.</span></span> 

<span data-ttu-id="88b7d-118">사용 하는 경우 [Azure Active Directory](../active-directory/active-directory-whatis.md), hello 복사본에 대 한 자격 증명을 관리 하기 위한 hello 요구를 완전히 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-118">If you use [Azure Active Directory](../active-directory/active-directory-whatis.md), you can completely eliminate hello need for managing credentials in hello copy.</span></span> <span data-ttu-id="88b7d-119">그러나 hello 데이터베이스 tooa 새 서버를 복사할 때 hello 로그인 기반 액세스 수 없으므로 작동 되지, hello 로그인 hello 새 서버에 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-119">However, when you copy hello database tooa new server, hello login-based access might not work, because hello logins do not exist on hello new server.</span></span> <span data-ttu-id="88b7d-120">toolearn 데이터베이스 tooa 다른 논리 서버를 복사 하는 경우 로그인을 관리 하는 방법에 대 한 참조 [어떻게 toomanage Azure SQL 데이터베이스 보안 재해 복구 후](sql-database-geo-replication-security-config.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-120">toolearn about managing logins when you copy a database tooa different logical server, see [How toomanage Azure SQL database security after disaster recovery](sql-database-geo-replication-security-config.md).</span></span> 

<span data-ttu-id="88b7d-121">Hello 복사 성공 후 및 다른 사용자가 다시 매핑하기 전에 hello hello 데이터베이스 소유자 hello 복사를 시작한 로그인 로그인 수 toohello 새 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="88b7d-121">After hello copying succeeds and before other users are remapped, only hello login that initiated hello copying, hello database owner, can log in toohello new database.</span></span> <span data-ttu-id="88b7d-122">tooresolve 로그인 hello 복사 작업을 완료 한 후 참조 [로그인을 해결](#resolve-logins)합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-122">tooresolve logins after hello copying operation is complete, see [Resolve logins](#resolve-logins).</span></span>

## <a name="copy-a-database-by-using-hello-azure-portal"></a><span data-ttu-id="88b7d-123">Hello Azure 포털을 사용 하 여 데이터베이스를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-123">Copy a database by using hello Azure portal</span></span>

<span data-ttu-id="88b7d-124">데이터베이스를 사용 하 여 Azure 포털에서 데이터베이스 열기 hello 페이지 hello 및 클릭 toocopy **복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-124">toocopy a database by using hello Azure portal, open hello page for your database, and then click **Copy**.</span></span> 

   ![데이터베이스 복사](./media/sql-database-copy/database-copy.png)

## <a name="copy-a-database-by-using-powershell"></a><span data-ttu-id="88b7d-126">PowerShell을 사용하여 데이터베이스 복사</span><span class="sxs-lookup"><span data-stu-id="88b7d-126">Copy a database by using PowerShell</span></span>

<span data-ttu-id="88b7d-127">PowerShell을 사용 하 여 hello를 사용 하 여 데이터베이스 toocopy [새로 AzureRmSqlDatabaseCopy](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="88b7d-127">toocopy a database by using PowerShell, use hello [New-AzureRmSqlDatabaseCopy](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) cmdlet.</span></span> 

```PowerShell
New-AzureRmSqlDatabaseCopy -ResourceGroupName "myResourceGroup" `
    -ServerName $sourceserver `
    -DatabaseName "MySampleDatabase" `
    -CopyResourceGroupName "myResourceGroup" `
    -CopyServerName $targetserver `
    -CopyDatabaseName "CopyOfMySampleDatabase"
```

<span data-ttu-id="88b7d-128">전체 샘플 스크립트에 대 한 참조 [데이터베이스 tooa 새 서버에 복사](scripts/sql-database-copy-database-to-new-server-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-128">For a complete sample script, see [Copy a database tooa new server](scripts/sql-database-copy-database-to-new-server-powershell.md).</span></span>

## <a name="copy-a-database-by-using-transact-sql"></a><span data-ttu-id="88b7d-129">Transact-SQL을 사용하여 데이터베이스 복사</span><span class="sxs-lookup"><span data-stu-id="88b7d-129">Copy a database by using Transact-SQL</span></span>

<span data-ttu-id="88b7d-130">Hello 서버 수준 보안 주체 로그인 이나 toocopy hello 데이터베이스를 만든 사람의 로그인 정보 hello와 데이터베이스 toohello 마스터에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-130">Log in toohello master database with hello server-level principal login or hello login that created hello database you want toocopy.</span></span> <span data-ttu-id="88b7d-131">Toosucceed를 복사 하는 데이터베이스에 대 한 hello 서버 수준 보안 주체가 없는 로그인 hello dbmanager 역할의 구성원 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-131">For database copying toosucceed, logins that are not hello server-level principal must be members of hello dbmanager role.</span></span> <span data-ttu-id="88b7d-132">로그인과 연결 toohello 서버에 대 한 자세한 내용은 참조 [로그인 관리](sql-database-manage-logins.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-132">For more information about logins and connecting toohello server, see [Manage logins](sql-database-manage-logins.md).</span></span>

<span data-ttu-id="88b7d-133">Hello hello 원본 데이터베이스 복사를 시작 [CREATE DATABASE](https://msdn.microsoft.com/library/ms176061.aspx) 문.</span><span class="sxs-lookup"><span data-stu-id="88b7d-133">Start copying hello source database with hello [CREATE DATABASE](https://msdn.microsoft.com/library/ms176061.aspx) statement.</span></span> <span data-ttu-id="88b7d-134">이 문을 실행 hello 데이터베이스 복사 프로세스가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-134">Executing this statement initiates hello database copying process.</span></span> <span data-ttu-id="88b7d-135">데이터베이스 복사는 비동기 프로세스 이므로 hello 데이터베이스 복사가 완료 되기 전에 hello CREATE DATABASE 문을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-135">Because copying a database is an asynchronous process, hello CREATE DATABASE statement returns before hello database copying is complete.</span></span>

### <a name="copy-a-sql-database-toohello-same-server"></a><span data-ttu-id="88b7d-136">SQL 데이터베이스 toohello 복사 동일한 서버</span><span class="sxs-lookup"><span data-stu-id="88b7d-136">Copy a SQL database toohello same server</span></span>
<span data-ttu-id="88b7d-137">Hello 서버 수준 보안 주체 로그인 이나 toocopy hello 데이터베이스를 만든 사람의 로그인 정보 hello와 데이터베이스 toohello 마스터에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-137">Log in toohello master database with hello server-level principal login or hello login that created hello database you want toocopy.</span></span> <span data-ttu-id="88b7d-138">Toosucceed를 복사 하는 데이터베이스에 대 한 hello 서버 수준 보안 주체가 없는 로그인 hello dbmanager 역할의 구성원 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-138">For database copying toosucceed, logins that are not hello server-level principal must be members of hello dbmanager role.</span></span>

<span data-ttu-id="88b7d-139">이 명령은 복사 Database1 tooa 새 데이터베이스 Database2 hello에 이름이 표시 된 같은 서버.</span><span class="sxs-lookup"><span data-stu-id="88b7d-139">This command copies Database1 tooa new database named Database2 on hello same server.</span></span> <span data-ttu-id="88b7d-140">데이터베이스의 hello 크기에 따라 작업을 복사 하는 hello 일부 시간 toocomplete를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-140">Depending on hello size of your database, hello copying operation might take some time toocomplete.</span></span>

    -- Execute on hello master database.
    -- Start copying.
    CREATE DATABASE Database1_copy AS COPY OF Database1;

### <a name="copy-a-sql-database-tooa-different-server"></a><span data-ttu-id="88b7d-141">SQL 데이터베이스 tooa 다른 서버에 복사</span><span class="sxs-lookup"><span data-stu-id="88b7d-141">Copy a SQL database tooa different server</span></span>

<span data-ttu-id="88b7d-142">여기서 hello 새 데이터베이스는 만든 toobe hello SQL 데이터베이스 서버 hello 대상 서버의 데이터베이스 toohello 마스터에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-142">Log in toohello master database of hello destination server, hello SQL database server where hello new database is toobe created.</span></span> <span data-ttu-id="88b7d-143">Hello 원본 SQL 데이터베이스 서버에서 hello 원본 데이터베이스의 데이터베이스 소유자 hello로 동일한 이름 및 암호 hello에 있는 로그인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-143">Use a login that has hello same name and password as hello database owner of hello source database on hello source SQL database server.</span></span> <span data-ttu-id="88b7d-144">또한 hello 대상 서버에서 로그인의 hello hello dbmanager 역할의 멤버 여야 하거나 hello 서버 수준 보안 주체 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-144">hello login on hello destination server must also be a member of hello dbmanager role or be hello server-level principal login.</span></span>

<span data-ttu-id="88b7d-145">이 명령은 2에 Database2 라는 server1 tooa 새 데이터베이스에 Database1를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-145">This command copies Database1 on server1 tooa new database named Database2 on server2.</span></span> <span data-ttu-id="88b7d-146">데이터베이스의 hello 크기에 따라 작업을 복사 하는 hello 일부 시간 toocomplete를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-146">Depending on hello size of your database, hello copying operation might take some time toocomplete.</span></span>

    -- Execute on hello master database of hello target server (server2)
    -- Start copying from Server1 tooServer2
    CREATE DATABASE Database1_copy AS COPY OF server1.Database1;


### <a name="monitor-hello-progress-of-hello-copying-operation"></a><span data-ttu-id="88b7d-147">작업을 복사 하는 hello hello 진행률 모니터링</span><span class="sxs-lookup"><span data-stu-id="88b7d-147">Monitor hello progress of hello copying operation</span></span>

<span data-ttu-id="88b7d-148">Hello sys.databases 및 sys.dm_database_copies 뷰를 쿼리하여 hello 복사 프로세스를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-148">Monitor hello copying process by querying hello sys.databases and sys.dm_database_copies views.</span></span> <span data-ttu-id="88b7d-149">진행 중인 hello 복사, 동안 hello **state_desc** hello 새 데이터베이스에 대 한 hello sys.databases 뷰의 열이 너무 설정 되어**COPYING**합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-149">While hello copying is in progress, hello **state_desc** column of hello sys.databases view for hello new database is set too**COPYING**.</span></span>

* <span data-ttu-id="88b7d-150">Hello 복사에 실패할 경우 hello **state_desc** hello 새 데이터베이스에 대 한 hello sys.databases 뷰의 열이 너무 설정 되어**의심**합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-150">If hello copying fails, hello **state_desc** column of hello sys.databases view for hello new database is set too**SUSPECT**.</span></span> <span data-ttu-id="88b7d-151">Hello 새로운 데이터베이스에서 DROP 문을 hello 실행과 나중에 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-151">Execute hello DROP statement on hello new database, and try again later.</span></span>
* <span data-ttu-id="88b7d-152">Hello 복사 성공 하면 hello **state_desc** hello 새 데이터베이스에 대 한 hello sys.databases 뷰의 열이 너무 설정 되어**온라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-152">If hello copying succeeds, hello **state_desc** column of hello sys.databases view for hello new database is set too**ONLINE**.</span></span> <span data-ttu-id="88b7d-153">hello 복사가 완료 되며 hello 새 데이터베이스는 hello 원본 데이터베이스와 독립적으로 변경 될 수 있는 일반 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-153">hello copying is complete, and hello new database is a regular database that can be changed independent of hello source database.</span></span>

> [!NOTE]
> <span data-ttu-id="88b7d-154">진행 중인 동안 toocancel hello 복사 기능을 결정 하는 경우 실행 hello [DROP DATABASE](https://msdn.microsoft.com/library/ms178613.aspx) hello 새 데이터베이스에서 문입니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-154">If you decide toocancel hello copying while it is in progress, execute hello [DROP DATABASE](https://msdn.microsoft.com/library/ms178613.aspx) statement on hello new database.</span></span> <span data-ttu-id="88b7d-155">또는 hello 복사 프로세스가 취소도 hello 원본 데이터베이스에서 hello DROP DATABASE 문을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-155">Alternatively, executing hello DROP DATABASE statement on hello source database also cancels hello copying process.</span></span>
> 

## <a name="resolve-logins"></a><span data-ttu-id="88b7d-156">로그인 확인</span><span class="sxs-lookup"><span data-stu-id="88b7d-156">Resolve logins</span></span>

<span data-ttu-id="88b7d-157">Hello를 사용 하 여 새 데이터베이스 hello hello 대상 서버에서 온라인 상태 이면 후 [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) hello에서 문을 tooremap hello 사용자는 새 toologins hello 대상 서버의 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-157">After hello new database is online on hello destination server, use hello [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) statement tooremap hello users from hello new database toologins on hello destination server.</span></span> <span data-ttu-id="88b7d-158">tooresolve 분리 된 사용자에 게 표시 [분리 된 사용자 문제 해결](https://msdn.microsoft.com/library/ms175475.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-158">tooresolve orphaned users, see [Troubleshoot Orphaned Users](https://msdn.microsoft.com/library/ms175475.aspx).</span></span> <span data-ttu-id="88b7d-159">참고 항목 [어떻게 toomanage Azure SQL 데이터베이스 보안 재해 복구 후](sql-database-geo-replication-security-config.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-159">See also [How toomanage Azure SQL database security after disaster recovery](sql-database-geo-replication-security-config.md).</span></span>

<span data-ttu-id="88b7d-160">Hello 원본 데이터베이스에서 가졌던 hello 사용 권한을 유지 하는 hello 새 데이터베이스의 모든 사용자.</span><span class="sxs-lookup"><span data-stu-id="88b7d-160">All users in hello new database retain hello permissions that they had in hello source database.</span></span> <span data-ttu-id="88b7d-161">hello 데이터베이스 복사본을 시작한 hello 사용자 hello 새 데이터베이스의 데이터베이스 소유자 hello 되며 새 보안 식별자 (SID)를 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-161">hello user who initiated hello database copy becomes hello database owner of hello new database and is assigned a new security identifier (SID).</span></span> <span data-ttu-id="88b7d-162">Hello 복사 성공 후 및 다른 사용자가 다시 매핑하기 전에 hello hello 데이터베이스 소유자 hello 복사를 시작한 로그인 로그인 수 toohello 새 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="88b7d-162">After hello copying succeeds and before other users are remapped, only hello login that initiated hello copying, hello database owner, can log in toohello new database.</span></span>

<span data-ttu-id="88b7d-163">toolearn 데이터베이스 tooa 다른 논리 서버를 복사할 때 사용자와 로그인을 관리 하는 방법에 대 한 참조 [어떻게 toomanage Azure SQL 데이터베이스 보안 재해 복구 후](sql-database-geo-replication-security-config.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-163">toolearn about managing users and logins when you copy a database tooa different logical server, see [How toomanage Azure SQL database security after disaster recovery](sql-database-geo-replication-security-config.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="88b7d-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="88b7d-164">Next steps</span></span>

* <span data-ttu-id="88b7d-165">로그인에 대 한 정보를 참조 하십시오. [로그인 관리](sql-database-manage-logins.md) 및 [어떻게 toomanage Azure SQL 데이터베이스 보안 재해 복구 후](sql-database-geo-replication-security-config.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-165">For information about logins, see [Manage logins](sql-database-manage-logins.md) and [How toomanage Azure SQL database security after disaster recovery](sql-database-geo-replication-security-config.md).</span></span>
* <span data-ttu-id="88b7d-166">tooexport 데이터베이스 참조 [hello 데이터베이스 tooa BACPAC 내보내기](sql-database-export.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="88b7d-166">tooexport a database, see [Export hello database tooa BACPAC](sql-database-export.md).</span></span>
