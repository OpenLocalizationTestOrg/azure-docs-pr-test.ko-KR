---
title: "SQL Data Warehouse에서 데이터베이스 보호 | Microsoft Docs"
description: "솔루션 개발을 위해 Azure SQL 데이터 웨어하우스에서 데이터베이스를 보호하는 팁"
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 8fa2f5ca-4cf5-4418-99a2-4dc745799850
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 6ea45c40bc428282faf24b4a08f8b0d345adb3fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="secure-a-database-in-sql-data-warehouse"></a><span data-ttu-id="f728a-103">SQL 데이터 웨어하우스에서 데이터베이스 보호</span><span class="sxs-lookup"><span data-stu-id="f728a-103">Secure a database in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f728a-104">보안 개요</span><span class="sxs-lookup"><span data-stu-id="f728a-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="f728a-105">인증</span><span class="sxs-lookup"><span data-stu-id="f728a-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="f728a-106">암호화(포털)</span><span class="sxs-lookup"><span data-stu-id="f728a-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="f728a-107">암호화(T-SQL)</span><span class="sxs-lookup"><span data-stu-id="f728a-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="f728a-108">이 문서는 Azure SQL 데이터 웨어하우스 데이터베이스 보호에 대한 기본 사항을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-108">This article walks through the basics of securing your Azure SQL Data Warehouse database.</span></span> <span data-ttu-id="f728a-109">특히, 이 문서는 데이터베이스에서 액세스 제한, 데이터 보호 및 작업 모니터링을 위한 리소스로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-109">In particular, this article will get you started with resources for limiting access, protecting data, and monitoring activities on a database.</span></span>

## <a name="connection-security"></a><span data-ttu-id="f728a-110">연결 보안</span><span class="sxs-lookup"><span data-stu-id="f728a-110">Connection security</span></span>
<span data-ttu-id="f728a-111">연결 보안은 방화벽 규칙 및 연결 암호화를 사용하여 데이터베이스에 대한 연결을 제한하고 보호하는 방법을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-111">Connection Security refers to how you restrict and secure connections to your database using firewall rules and connection encryption.</span></span>

<span data-ttu-id="f728a-112">방화벽 규칙은 서버와 데이터베이스에서 명시적으로 허용 목록에 없는 IP 주소로부터의 연결 시도를 거부하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-112">Firewall rules are used by both the server and the database to reject connection attempts from IP addresses that have not been explicitly whitelisted.</span></span> <span data-ttu-id="f728a-113">응용 프로그램 또는 클라이언트 컴퓨터의 공용 IP 주소에서 연결할 수 있도록 허용하려면 먼저 Azure 포털, REST API 또는 PowerShell을 사용하여 서버 수준 방화벽 규칙을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-113">To allow connections from your application or client machine's public IP address, you must first create a server-level firewall rule using the Azure Portal, REST API, or PowerShell.</span></span> <span data-ttu-id="f728a-114">서버 방화벽을 통해 허용되는 IP 주소 범위를 최대한 많이 제한하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-114">As a best practice, you should restrict the IP address ranges allowed through your server firewall as much as possible.</span></span>  <span data-ttu-id="f728a-115">로컬 컴퓨터에서 Azure SQL 데이터 웨어하우스로 액세스하려면 네트워크의 방화벽과 로컬 컴퓨터가 TCP 포트 1433으로 나가는 통신을 허용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-115">To access Azure SQL Data Warehouse from your local computer, ensure the firewall on your network and local computer allows outgoing communication on TCP port 1433.</span></span>  <span data-ttu-id="f728a-116">자세한 내용은 [Azure SQL Database 방화벽][Azure SQL Database firewall], [sp_set_firewall_rule][sp_set_firewall_rule] 및 [sp_set_database_firewall_rule][sp_set_database_firewall_rule]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f728a-116">For more information, see [Azure SQL Database firewall][Azure SQL Database firewall], [sp_set_firewall_rule][sp_set_firewall_rule], and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span></span>

<span data-ttu-id="f728a-117">SQL 데이터 웨어하우스에 대한 연결은 기본적으로 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-117">Connections to your SQL Data Warehouse are encrypted by default.</span></span>  <span data-ttu-id="f728a-118">암호화를 사용하지 않도록 연결 설정을 수정해도 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-118">Modifying connection settings to disable encryption are ignored.</span></span>

## <a name="authentication"></a><span data-ttu-id="f728a-119">인증</span><span class="sxs-lookup"><span data-stu-id="f728a-119">Authentication</span></span>
<span data-ttu-id="f728a-120">인증은 데이터베이스에 연결할 때 사용자의 ID를 증명하는 방법을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-120">Authentication refers to how you prove your identity when connecting to the database.</span></span> <span data-ttu-id="f728a-121">SQL Data Warehouse는 현재 Azure Active Directory뿐 아니라 사용자 이름 및 암호를 사용하는 SQL Server 인증도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-121">SQL Data Warehouse currently supports SQL Server Authentication with a username and password as well as a Azure Active Directory.</span></span> 

<span data-ttu-id="f728a-122">데이터베이스의 논리 서버를 만들 때 사용자 이름 및 암호를 사용하여 "서버 관리자" 로그인을 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-122">When you created the logical server for your database, you specified a "server admin" login with a username and password.</span></span> <span data-ttu-id="f728a-123">이러한 자격 증명을 사용하면, SQL Server 인증을 통해 해당 서버의 모든 데이터베이스에 데이터베이스 소유자 또는 "dbo"로 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-123">Using these credentials, you can authenticate to any database on that server as the database owner, or "dbo" through SQL Server Authentication.</span></span>

<span data-ttu-id="f728a-124">그러나 조직의 사용자는 다른 계정으로 인증하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-124">However, as a best practice, your organization’s users should use a different account to authenticate.</span></span> <span data-ttu-id="f728a-125">이렇게 하면 응용 프로그램에 부여되는 사용 권한을 제한하여 응용 프로그램 코드가 SQL 삽입 공격에 취약한 경우 악의적인 활동의 위험을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-125">This way you can limit the permissions granted to the application and reduce the risks of malicious activity in case your application code is vulnerable to a SQL injection attack.</span></span> 

<span data-ttu-id="f728a-126">SQL Server 인증 사용자를 만들려면 서버 관리자 로그인을 사용하여 서버의 **master** 데이터베이스에 연결하고 새 서버 로그인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-126">To create a SQL Server Authenticated user, connect to the **master** database on your server with your server admin login and create a new server login.</span></span>  <span data-ttu-id="f728a-127">또한 Azure SQL Data Warehouse 사용자에 대해 마스터 데이터베이스에 사용자를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-127">Additionally, it is a good idea to create a user in the master database for Azure SQL Data Warehouse users.</span></span> <span data-ttu-id="f728a-128">마스터에서 사용자를 만들면 데이터베이스 이름을 지정하지 않아도 사용자가 SSMS 등의 도구를 사용하여 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-128">Creating a user in master allows a user to login using tools like SSMS without specifying a database name.</span></span>  <span data-ttu-id="f728a-129">또한 개체 탐색기를 사용하여 SQL server의 모든 데이터베이스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-129">It also allows them to use the object explorer to view all databases on a SQL server.</span></span>

```sql
-- Connect to master database and create a login
CREATE LOGIN ApplicationLogin WITH PASSWORD = 'Str0ng_password';
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

<span data-ttu-id="f728a-130">그런 다음, 서버 관리자 로그인을 사용하여 **SQL 데이터 웨어하우스 데이터베이스** 에 연결하고 방금 만든 서버 로그인에 따라 데이터베이스 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-130">Then, connect to your **SQL Data Warehouse database** with your server admin login and create a database user based on the server login you just created.</span></span>

```sql
-- Connect to SQL DW database and create a database user
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

<span data-ttu-id="f728a-131">로그인 또는 새 데이터베이스 만들기 등의 추가 작업을 수행하려는 사용자는 마스터 데이터베이스의 `Loginmanager` 및 `dbmanager` 역할에도 할당되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-131">If a user will be doing additional operations such as creating logins or creating new databases, they will also need to be assigned to the `Loginmanager` and `dbmanager` roles in the master database.</span></span> <span data-ttu-id="f728a-132">이러한 추가 역할 및 SQL Database에 인증하는 방법에 대한 자세한 내용은 [Azure SQL Database에서 데이터베이스 및 로그인 관리][Managing databases and logins in Azure SQL Database]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f728a-132">For more information on these additonal roles and authenticating to a SQL Database, see [Managing databases and logins in Azure SQL Database][Managing databases and logins in Azure SQL Database].</span></span>  <span data-ttu-id="f728a-133">SQL Data Warehouse용 Azure AD에 대한 자세한 내용은 [Azure Active Directory 인증을 사용하여 SQL Data Warehouse에 연결][Connecting to SQL Data Warehouse By Using Azure Active Directory Authentication]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f728a-133">For more details on Azure AD for SQL Data Warehouse, see [Connecting to SQL Data Warehouse By Using Azure Active Directory Authentication][Connecting to SQL Data Warehouse By Using Azure Active Directory Authentication].</span></span>

## <a name="authorization"></a><span data-ttu-id="f728a-134">권한 부여</span><span class="sxs-lookup"><span data-stu-id="f728a-134">Authorization</span></span>
<span data-ttu-id="f728a-135">권한 부여는 Azure SQL 데이터 웨어하우스 데이터베이스 내에서 수행할 수 있는 작업을 가리키며 사용자 계정의 역할 멤버 자격과 사용 권한에 의해 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-135">Authorization refers to what you can do within an Azure SQL Data Warehouse database, and this is controlled by your user account's role memberships and permissions.</span></span> <span data-ttu-id="f728a-136">사용자에게 필요한 최소한의 권한을 부여하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-136">As a best practice, you should grant users the least privileges necessary.</span></span> <span data-ttu-id="f728a-137">Azure SQL 데이터 웨어하우스를 사용하면 T-SQL에서 역할을 통해 쉽게 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-137">Azure SQL Data Warehouse makes this easy to manage with roles in T-SQL:</span></span>

```sql
EXEC sp_addrolemember 'db_datareader', 'ApplicationUser'; -- allows ApplicationUser to read data
EXEC sp_addrolemember 'db_datawriter', 'ApplicationUser'; -- allows ApplicationUser to write data
```

<span data-ttu-id="f728a-138">연결 중인 서버 관리자 계정은 데이터베이스 내에서 작업을 수행할 권한이 있는 db_owner의 구성원입니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-138">The server admin account you are connecting with is a member of db_owner, which has authority to do anything within the database.</span></span> <span data-ttu-id="f728a-139">스키마 업그레이드 및 기타 관리 작업을 배포하기 위해서는 이 계정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-139">Save this account for deploying schema upgrades and other management operations.</span></span> <span data-ttu-id="f728a-140">응용 프로그램에서 해당 응용 프로그램에 필요한 최소한의 권한이 있는 데이터베이스에 연결하려면 보다 제한된 사용 권한을 가진 "ApplicationUser" 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-140">Use the "ApplicationUser" account with more limited permissions to connect from your application to the database with the least privileges needed by your application.</span></span>

<span data-ttu-id="f728a-141">사용자가 Azure SQL 데이터베이스로 수행할 수 있는 작업을 더욱 제한할 수 있는 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-141">There are ways to further limit what a user can do with Azure SQL Database:</span></span>

* <span data-ttu-id="f728a-142">세분화된 [권한][Permissions]을 사용하면 개별 열, 테이블, 뷰, 프로시저 및 데이터베이스의 다른 개체에서 수행할 수 있는 작업을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-142">Granular [Permissions][Permissions] let you control which operations you can do on individual columns, tables, views, procedures, and other objects in the database.</span></span> <span data-ttu-id="f728a-143">세분화된 사용 권한을 사용하여 최대한으로 제어하고 최소한의 필요 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-143">Use granular permissions to have the most control and grant the minimum permissions necessary.</span></span> <span data-ttu-id="f728a-144">세분화된 사용 권한 시스템은 다소 복잡하며 효과적으로 사용하려면 약간의 연구가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-144">The granular permission system is somewhat complicated and will require some study to use effectively.</span></span>
* <span data-ttu-id="f728a-145">db_datareader 및 db_datawriter 이외의 [데이터베이스 역할][Database roles]은 더 강력한 응용 프로그램 사용자 계정이나 덜 강력한 관리 계정을 만드는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-145">[Database roles][Database roles] other than db_datareader and db_datawriter can be used to create more powerful application user accounts or less powerful management accounts.</span></span> <span data-ttu-id="f728a-146">기본 제공되는 고정 데이터베이스 역할은 사용 권한을 부여하는 쉬운 방법을 제공하지만 필요한 것보다 많은 사용 권한이 부여될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-146">The built-in fixed database roles provide an easy way to grant permissions, but can result in granting more permissions than are necessary.</span></span>
* <span data-ttu-id="f728a-147">[저장 프로시저][Stored procedures]는 데이터베이스에서 수행할 수 있는 작업을 제한하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-147">[Stored procedures][Stored procedures] can be used to limit the actions that can be taken on the database.</span></span>

<span data-ttu-id="f728a-148">Azure 클래식 포털에서 또는 Azure 리소스 관리자 API를 사용하여 데이터베이스 및 논리 서버를 관리하는 것은 포털 사용자 계정의 역할 할당에 의해 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-148">Managing databases and logical servers from the Azure Classic Portal or using the Azure Resource Manager API is controlled by your portal user account's role assignments.</span></span> <span data-ttu-id="f728a-149">이 항목에 대한 자세한 내용은 [Azure Portal의 역할 기반 액세스 제어][Role-based access control in Azure Portal]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f728a-149">For more information on this topic, see [Role-based access control in Azure Portal][Role-based access control in Azure Portal].</span></span>

## <a name="encryption"></a><span data-ttu-id="f728a-150">암호화</span><span class="sxs-lookup"><span data-stu-id="f728a-150">Encryption</span></span>
<span data-ttu-id="f728a-151">Azure SQL Data Warehouse TDE(투명한 데이터 암호화)는 미사용 데이터에 대한 실시간 암호화 및 암호 해독을 수행하여 악의적인 활동의 위협으로부터 보호하는 데 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-151">Azure SQL Data Warehouse Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of your data at rest.</span></span>  <span data-ttu-id="f728a-152">데이터베이스를 암호화할 때, 응용 프로그램을 변경할 필요 없이 연관된 백업 및 트랜잭션 로그 파일이 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-152">When you encrypt your database, associated backups and transaction log files are encrypted without requiring any changes to your applications.</span></span> <span data-ttu-id="f728a-153">TDE는 데이터베이스 암호화 키라는 대칭 키를 사용하여 전체 데이터베이스의 저장소를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-153">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span></span> <span data-ttu-id="f728a-154">SQL 데이터베이스에서 데이터베이스 암호화 키는 기본 제공 서버 인증서에 의해 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-154">In SQL Database the database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="f728a-155">기본 제공 서버 인증서는 각 SQL 데이터베이스 서버에 대해 고유합니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-155">The built-in server certificate is unique for each SQL Database server.</span></span> <span data-ttu-id="f728a-156">Microsoft는 적어도 90일마다 이러한 인증서를 자동으로 회전합니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-156">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="f728a-157">SQL 데이터 웨어하우스에서 사용되는 암호화 알고리즘은 AES 256입니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-157">The encryption algorithm used by SQL Data Warehouse is AES-256.</span></span> <span data-ttu-id="f728a-158">TDE에 대한 일반적인 설명은 [투명한 데이터 암호화][Transparent Data Encryption]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f728a-158">For a general description of TDE, see [Transparent Data Encryption][Transparent Data Encryption].</span></span>

<span data-ttu-id="f728a-159">[Azure Portal][Encryption with Portal] 또는 [T-SQL][Encryption with TSQL]을 사용하여 데이터베이스를 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f728a-159">You can encrypt your database using the [Azure Portal][Encryption with Portal] or [T-SQL][Encryption with TSQL].</span></span>

## <a name="next-steps"></a><span data-ttu-id="f728a-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f728a-160">Next steps</span></span>
<span data-ttu-id="f728a-161">다양한 프로토콜의 SQL Data Warehouse에 연결하는 방법에 대한 정보와 예제는 [SQL Data Warehouse에 연결][Connect to SQL Data Warehouse]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f728a-161">For details and examples on connecting to your SQL Data Warehouse with different protocols, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span></span>

<!--Image references-->

<!--Article references-->
[Connect to SQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Encryption with Portal]: ./sql-data-warehouse-encryption-tde.md
[Encryption with TSQL]: ./sql-data-warehouse-encryption-tde-tsql.md
[Connecting to SQL Data Warehouse By Using Azure Active Directory Authentication]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[Azure SQL Database firewall]: https://msdn.microsoft.com/library/ee621782.aspx
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx
[Database roles]: https://msdn.microsoft.com/library/ms189121.aspx
[Managing databases and logins in Azure SQL Database]: https://msdn.microsoft.com/library/ee336235.aspx
[Permissions]: https://msdn.microsoft.com/library/ms191291.aspx
[Stored procedures]: https://msdn.microsoft.com/library/ms190782.aspx
[Transparent Data Encryption]: https://msdn.microsoft.com/library/bb934049.aspx
[Azure portal]: https://portal.azure.com/

<!--Other Web references-->
[Role-based access control in Azure Portal]: https://azure.microsoft.com/documentation/articles/role-based-access-control-configure
