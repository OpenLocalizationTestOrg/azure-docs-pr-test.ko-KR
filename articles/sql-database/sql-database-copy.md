---
title: "Azure SQL Database 복사 | Microsoft Docs"
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
ms.openlocfilehash: 8c1e3c80b9f24089dc99463d6ea8ae5d0ea7b19d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="copy-an-azure-sql-database"></a><span data-ttu-id="7b955-103">Azure SQL 데이터베이스 복사</span><span class="sxs-lookup"><span data-stu-id="7b955-103">Copy an Azure SQL database</span></span>

<span data-ttu-id="7b955-104">Azure SQL Database는 동일한 서버 또는 다른 서버에서 기존 Azure SQL Database의 트랜잭션 측면에서 일관된 복사본을 만들기 위한 여러 가지 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-104">Azure SQL Database provides several methods for creating a transactionally consistent copy of an existing Azure SQL database on either the same server or a different server.</span></span> <span data-ttu-id="7b955-105">Azure Portal, PowerShell 또는 T-SQL을 사용하여 SQL Database를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-105">You can copy a SQL database by using the Azure portal, PowerShell, or T-SQL.</span></span> 

## <a name="overview"></a><span data-ttu-id="7b955-106">개요</span><span class="sxs-lookup"><span data-stu-id="7b955-106">Overview</span></span>

<span data-ttu-id="7b955-107">데이터베이스 복사본은 복사 요청 당시의 원본 데이터베이스의 스냅숏입니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-107">A database copy is a snapshot of the source database as of the time of the copy request.</span></span> <span data-ttu-id="7b955-108">동일한 서버 또는 다른 서버, 해당 서비스 계층 및 성능 수준 또는 동일한 서비스 계층(버전) 내 다른 성능 수준을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-108">You can select the same server or a different server, its service tier and performance level, or a different performance level within the same service tier (edition).</span></span> <span data-ttu-id="7b955-109">복사가 완료되면 완전히 작동하는 독립 데이터베이스가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-109">After the copy is complete, it becomes a fully functional, independent database.</span></span> <span data-ttu-id="7b955-110">이 시점에서 모든 버전으로 업그레이드하거나 다운그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-110">At this point, you can upgrade or downgrade it to any edition.</span></span> <span data-ttu-id="7b955-111">로그인, 사용자 및 사용 권한은 독립적으로 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-111">The logins, users, and permissions can be managed independently.</span></span>  

## <a name="logins-in-the-database-copy"></a><span data-ttu-id="7b955-112">데이터베이스 복사본에서 로그인</span><span class="sxs-lookup"><span data-stu-id="7b955-112">Logins in the database copy</span></span>

<span data-ttu-id="7b955-113">데이터베이스를 동일한 논리적 서버에 복사할 때 두 데이터베이스에서 동일한 로그인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-113">When you copy a database to the same logical server, the same logins can be used on both databases.</span></span> <span data-ttu-id="7b955-114">데이터베이스를 복사하는 데 사용하는 보안 주체는 새 데이터베이스의 데이터베이스 소유자가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-114">The security principal you use to copy the database becomes the database owner on the new database.</span></span> <span data-ttu-id="7b955-115">모든 데이터베이스 사용자, 권한 및 보안 식별자(SID)가 데이터베이스 사본에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-115">All database users, their permissions, and their security identifiers (SIDs) are copied to the database copy.</span></span>  

<span data-ttu-id="7b955-116">다른 논리 서버로 데이터베이스를 복사할 때 새 서버의 보안 주체가 새 데이터베이스의 데이터베이스 소유자가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-116">When you copy a database to a different logical server, the security principal on the new server becomes the database owner on the new database.</span></span> <span data-ttu-id="7b955-117">데이터 액세스에 [포함된 데이터베이스 사용자](sql-database-manage-logins.md)를 사용하는 경우 복사가 완료된 후 동일한 자격 증명으로 액세스할 수 있도록 주 데이터베이스와 보조 데이터베이스에서 항상 동일한 사용자 자격 증명을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-117">If you use [contained database users](sql-database-manage-logins.md) for data access, ensure that both the primary and secondary databases always have the same user credentials, so that after the copy is complete you can immediately access it with the same credentials.</span></span> 

<span data-ttu-id="7b955-118">[Azure Active Directory](../active-directory/active-directory-whatis.md)를 사용하는 경우 복사본에서 자격 증명을 관리할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-118">If you use [Azure Active Directory](../active-directory/active-directory-whatis.md), you can completely eliminate the need for managing credentials in the copy.</span></span> <span data-ttu-id="7b955-119">그러나 데이터베이스를 새 서버로 복사할 때 새 서버에 로그인이 존재하지 않으므로 로그인 기반 액세스가 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-119">However, when you copy the database to a new server, the login-based access might not work, because the logins do not exist on the new server.</span></span> <span data-ttu-id="7b955-120">다른 논리 서버로 데이터베이스를 복사할 때 로그인을 관리하는 방법에 대한 자세한 내용은 [재해 복구 후에 Azure SQL Database 보안을 관리하는 방법](sql-database-geo-replication-security-config.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b955-120">To learn about managing logins when you copy a database to a different logical server, see [How to manage Azure SQL database security after disaster recovery](sql-database-geo-replication-security-config.md).</span></span> 

<span data-ttu-id="7b955-121">복사 성공 후 다른 사용자를 다시 매핑하기 전에는 데이터베이스 소유자인 복사를 시작한 로그인만 새 데이터베이스에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-121">After the copying succeeds and before other users are remapped, only the login that initiated the copying, the database owner, can log in to the new database.</span></span> <span data-ttu-id="7b955-122">복사 작업이 완료된 후 로그인을 확인하려면 [로그인 확인](#resolve-logins)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b955-122">To resolve logins after the copying operation is complete, see [Resolve logins](#resolve-logins).</span></span>

## <a name="copy-a-database-by-using-the-azure-portal"></a><span data-ttu-id="7b955-123">Azure Portal을 사용하여 데이터베이스 복사</span><span class="sxs-lookup"><span data-stu-id="7b955-123">Copy a database by using the Azure portal</span></span>

<span data-ttu-id="7b955-124">Azure Portal을 사용하여 데이터베이스를 복사하려면 데이터베이스에 대한 페이지를 열고 **복사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-124">To copy a database by using the Azure portal, open the page for your database, and then click **Copy**.</span></span> 

   ![데이터베이스 복사](./media/sql-database-copy/database-copy.png)

## <a name="copy-a-database-by-using-powershell"></a><span data-ttu-id="7b955-126">PowerShell을 사용하여 데이터베이스 복사</span><span class="sxs-lookup"><span data-stu-id="7b955-126">Copy a database by using PowerShell</span></span>

<span data-ttu-id="7b955-127">PowerShell을 사용하여 데이터베이스를 복사하려면 [New-AzureRmSqlDatabaseCopy](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-127">To copy a database by using PowerShell, use the [New-AzureRmSqlDatabaseCopy](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) cmdlet.</span></span> 

```PowerShell
New-AzureRmSqlDatabaseCopy -ResourceGroupName "myResourceGroup" `
    -ServerName $sourceserver `
    -DatabaseName "MySampleDatabase" `
    -CopyResourceGroupName "myResourceGroup" `
    -CopyServerName $targetserver `
    -CopyDatabaseName "CopyOfMySampleDatabase"
```

<span data-ttu-id="7b955-128">전체 샘플 스크립트는 [새 서버에 데이터베이스 복사](scripts/sql-database-copy-database-to-new-server-powershell.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b955-128">For a complete sample script, see [Copy a database to a new server](scripts/sql-database-copy-database-to-new-server-powershell.md).</span></span>

## <a name="copy-a-database-by-using-transact-sql"></a><span data-ttu-id="7b955-129">Transact-SQL을 사용하여 데이터베이스 복사</span><span class="sxs-lookup"><span data-stu-id="7b955-129">Copy a database by using Transact-SQL</span></span>

<span data-ttu-id="7b955-130">서버 수준 보안 주체 로그인이나 복사하려는 데이터베이스에서 만든 로그인을 사용하여 master 데이터베이스에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-130">Log in to the master database with the server-level principal login or the login that created the database you want to copy.</span></span> <span data-ttu-id="7b955-131">데이터베이스 복사가 성공하려면 서버 수준 보안 주체가 아닌 로그인이 dbmanager 역할의 구성원이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-131">For database copying to succeed, logins that are not the server-level principal must be members of the dbmanager role.</span></span> <span data-ttu-id="7b955-132">서버에 로그인 및 연결하는 방법에 대한 자세한 내용은 [로그인 관리](sql-database-manage-logins.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b955-132">For more information about logins and connecting to the server, see [Manage logins](sql-database-manage-logins.md).</span></span>

<span data-ttu-id="7b955-133">[CREATE DATABASE](https://msdn.microsoft.com/library/ms176061.aspx) 문으로 원본 데이터베이스 복사를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-133">Start copying the source database with the [CREATE DATABASE](https://msdn.microsoft.com/library/ms176061.aspx) statement.</span></span> <span data-ttu-id="7b955-134">이 문을 실행하면 데이터베이스 복사 프로세스가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-134">Executing this statement initiates the database copying process.</span></span> <span data-ttu-id="7b955-135">데이터베이스 복사는 비동기 프로세스이므로 CREATE DATABASE 문은 데이터베이스가 복사가 완료되기 전에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-135">Because copying a database is an asynchronous process, the CREATE DATABASE statement returns before the database copying is complete.</span></span>

### <a name="copy-a-sql-database-to-the-same-server"></a><span data-ttu-id="7b955-136">동일한 서버에 SQL 데이터베이스 복사</span><span class="sxs-lookup"><span data-stu-id="7b955-136">Copy a SQL database to the same server</span></span>
<span data-ttu-id="7b955-137">서버 수준 보안 주체 로그인이나 복사하려는 데이터베이스에서 만든 로그인을 사용하여 master 데이터베이스에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-137">Log in to the master database with the server-level principal login or the login that created the database you want to copy.</span></span> <span data-ttu-id="7b955-138">데이터베이스 복사가 성공하려면 서버 수준 보안 주체가 아닌 로그인이 dbmanager 역할의 구성원이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-138">For database copying to succeed, logins that are not the server-level principal must be members of the dbmanager role.</span></span>

<span data-ttu-id="7b955-139">이 명령은 Database1을 동일한 서버에서 이름이 Database2인 새 데이터베이스에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-139">This command copies Database1 to a new database named Database2 on the same server.</span></span> <span data-ttu-id="7b955-140">데이터베이스 크기에 따라 복사 작업을 완료하는 데 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-140">Depending on the size of your database, the copying operation might take some time to complete.</span></span>

    -- Execute on the master database.
    -- Start copying.
    CREATE DATABASE Database1_copy AS COPY OF Database1;

### <a name="copy-a-sql-database-to-a-different-server"></a><span data-ttu-id="7b955-141">SQL 데이터베이스를 다른 서버에 복사</span><span class="sxs-lookup"><span data-stu-id="7b955-141">Copy a SQL database to a different server</span></span>

<span data-ttu-id="7b955-142">새 데이터베이스를 만들 SQL Database 서버인 대상 서버의 master 데이터베이스에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-142">Log in to the master database of the destination server, the SQL database server where the new database is to be created.</span></span> <span data-ttu-id="7b955-143">원본 SQL Database 서버에서 원본 데이터베이스의 데이터베이스 소유자와 이름 및 암호가 같은 로그인을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-143">Use a login that has the same name and password as the database owner of the source database on the source SQL database server.</span></span> <span data-ttu-id="7b955-144">대상 서버의 로그인도 dbmanager 역할의 구성원이거나 서버 수준 보안 주체 로그인이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-144">The login on the destination server must also be a member of the dbmanager role or be the server-level principal login.</span></span>

<span data-ttu-id="7b955-145">이 명령은 server1의 Database1을 server2의 이름이 Database2인 새 데이터베이스에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-145">This command copies Database1 on server1 to a new database named Database2 on server2.</span></span> <span data-ttu-id="7b955-146">데이터베이스 크기에 따라 복사 작업을 완료하는 데 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-146">Depending on the size of your database, the copying operation might take some time to complete.</span></span>

    -- Execute on the master database of the target server (server2)
    -- Start copying from Server1 to Server2
    CREATE DATABASE Database1_copy AS COPY OF server1.Database1;


### <a name="monitor-the-progress-of-the-copying-operation"></a><span data-ttu-id="7b955-147">복사 작업 진행률 모니터링</span><span class="sxs-lookup"><span data-stu-id="7b955-147">Monitor the progress of the copying operation</span></span>

<span data-ttu-id="7b955-148">sys.databases 및 sys.dm_database_copies 뷰 쿼리를 통해 복사 프로세스를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-148">Monitor the copying process by querying the sys.databases and sys.dm_database_copies views.</span></span> <span data-ttu-id="7b955-149">복사가 진행 중인 동안 새 데이터베이스의 sys.databases 뷰에 대한 **state_desc** 열은 **COPYING**으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-149">While the copying is in progress, the **state_desc** column of the sys.databases view for the new database is set to **COPYING**.</span></span>

* <span data-ttu-id="7b955-150">복사가 실패하면 새 데이터베이스의 sys.databases 뷰에 대한 **state_desc** 열은 **SUSPECT**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-150">If the copying fails, the **state_desc** column of the sys.databases view for the new database is set to **SUSPECT**.</span></span> <span data-ttu-id="7b955-151">새 데이터베이스에서 DROP 문을 실행하고 나중에 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-151">Execute the DROP statement on the new database, and try again later.</span></span>
* <span data-ttu-id="7b955-152">복사에 성공하면 새 데이터베이스의 sys.databases 뷰에 대한 **state_desc** 열은 **ONLINE**으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-152">If the copying succeeds, the **state_desc** column of the sys.databases view for the new database is set to **ONLINE**.</span></span> <span data-ttu-id="7b955-153">복사가 완료되었으며 새 데이터베이스가 원본 데이터베이스와는 독립적으로 변경 가능한 일반 데이터베이스가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-153">The copying is complete, and the new database is a regular database that can be changed independent of the source database.</span></span>

> [!NOTE]
> <span data-ttu-id="7b955-154">진행 중인 복사를 취소하려면 새 데이터베이스에서 [DROP DATABASE](https://msdn.microsoft.com/library/ms178613.aspx) 문을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-154">If you decide to cancel the copying while it is in progress, execute the [DROP DATABASE](https://msdn.microsoft.com/library/ms178613.aspx) statement on the new database.</span></span> <span data-ttu-id="7b955-155">또는 원본 데이터베이스에서 DROP DATABASE 문을 실행해도 복사 프로세스가 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-155">Alternatively, executing the DROP DATABASE statement on the source database also cancels the copying process.</span></span>
> 

## <a name="resolve-logins"></a><span data-ttu-id="7b955-156">로그인 확인</span><span class="sxs-lookup"><span data-stu-id="7b955-156">Resolve logins</span></span>

<span data-ttu-id="7b955-157">대상 서버에서 새 데이터베이스가 온라인 상태가 되면 [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) 문을 사용하여 새 데이터베이스의 사용자를 대상 서버의 로그인과 다시 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-157">After the new database is online on the destination server, use the [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) statement to remap the users from the new database to logins on the destination server.</span></span> <span data-ttu-id="7b955-158">분리된 사용자를 확인하려면 [분리된 사용자 문제 해결](https://msdn.microsoft.com/library/ms175475.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b955-158">To resolve orphaned users, see [Troubleshoot Orphaned Users](https://msdn.microsoft.com/library/ms175475.aspx).</span></span> <span data-ttu-id="7b955-159">[재해 복구 후에 Azure SQL 데이터베이스 보안을 관리하는 방법](sql-database-geo-replication-security-config.md)도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b955-159">See also [How to manage Azure SQL database security after disaster recovery](sql-database-geo-replication-security-config.md).</span></span>

<span data-ttu-id="7b955-160">새 데이터베이스의 모든 사용자가 원본 데이터베이스에서 가졌던 사용 권한을 그대로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-160">All users in the new database retain the permissions that they had in the source database.</span></span> <span data-ttu-id="7b955-161">데이터베이스 복사를 실행한 사용자가 새 데이터베이스의 소유자가 되며 새 보안 식별자(SID)를 할당 받습니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-161">The user who initiated the database copy becomes the database owner of the new database and is assigned a new security identifier (SID).</span></span> <span data-ttu-id="7b955-162">복사 성공 후 다른 사용자를 다시 매핑하기 전에는 데이터베이스 소유자인 복사를 시작한 로그인만 새 데이터베이스에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b955-162">After the copying succeeds and before other users are remapped, only the login that initiated the copying, the database owner, can log in to the new database.</span></span>

<span data-ttu-id="7b955-163">다른 논리 서버로 데이터베이스를 복사할 때 사용자 및 로그인을 관리하는 방법에 대한 자세한 내용은 [재해 복구 후에 Azure SQL Database 보안을 관리하는 방법](sql-database-geo-replication-security-config.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b955-163">To learn about managing users and logins when you copy a database to a different logical server, see [How to manage Azure SQL database security after disaster recovery](sql-database-geo-replication-security-config.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b955-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7b955-164">Next steps</span></span>

* <span data-ttu-id="7b955-165">로그인에 대한 자세한 내용은 [로그인 관리](sql-database-manage-logins.md) 및 [재해 복구 후에 Azure SQL Database 보안을 관리하는 방법](sql-database-geo-replication-security-config.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b955-165">For information about logins, see [Manage logins](sql-database-manage-logins.md) and [How to manage Azure SQL database security after disaster recovery](sql-database-geo-replication-security-config.md).</span></span>
* <span data-ttu-id="7b955-166">데이터베이스를 내보내려면 [데이터베이스를 BACPAC로 내보내기](sql-database-export.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b955-166">To export a database, see [Export the database to a BACPAC](sql-database-export.md).</span></span>
