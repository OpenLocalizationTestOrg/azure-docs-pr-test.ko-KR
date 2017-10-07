---
title: "SQL 데이터 웨어하우스의 데이터베이스 aaaSecure | Microsoft Docs"
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
ms.openlocfilehash: 5ef4d760e00be46bfe7808bc95dbe1e4b3a51165
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-database-in-sql-data-warehouse"></a><span data-ttu-id="2ff84-103">SQL 데이터 웨어하우스에서 데이터베이스 보호</span><span class="sxs-lookup"><span data-stu-id="2ff84-103">Secure a database in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2ff84-104">보안 개요</span><span class="sxs-lookup"><span data-stu-id="2ff84-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="2ff84-105">인증</span><span class="sxs-lookup"><span data-stu-id="2ff84-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="2ff84-106">암호화(포털)</span><span class="sxs-lookup"><span data-stu-id="2ff84-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="2ff84-107">암호화(T-SQL)</span><span class="sxs-lookup"><span data-stu-id="2ff84-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="2ff84-108">이 문서는 Azure SQL 데이터 웨어하우스 데이터베이스를 보호의 hello 기초 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-108">This article walks through hello basics of securing your Azure SQL Data Warehouse database.</span></span> <span data-ttu-id="2ff84-109">특히, 이 문서는 데이터베이스에서 액세스 제한, 데이터 보호 및 작업 모니터링을 위한 리소스로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-109">In particular, this article will get you started with resources for limiting access, protecting data, and monitoring activities on a database.</span></span>

## <a name="connection-security"></a><span data-ttu-id="2ff84-110">연결 보안</span><span class="sxs-lookup"><span data-stu-id="2ff84-110">Connection security</span></span>
<span data-ttu-id="2ff84-111">연결 보안 참조 toohow 제한 하 고 방화벽 규칙 및 연결 암호화를 사용 하 여 연결 tooyour 데이터베이스 보안을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-111">Connection Security refers toohow you restrict and secure connections tooyour database using firewall rules and connection encryption.</span></span>

<span data-ttu-id="2ff84-112">방화벽 규칙은 모두 hello 서버와 hello 데이터베이스 tooreject의에서 연결 시도 되지 않은 명시적으로 허용 목록 IP 주소에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-112">Firewall rules are used by both hello server and hello database tooreject connection attempts from IP addresses that have not been explicitly whitelisted.</span></span> <span data-ttu-id="2ff84-113">응용 프로그램 또는 클라이언트 컴퓨터의 공용 IP 주소에서 tooallow 연결을 먼저 만들어야 합니다 hello Azure 포털, REST API 또는 PowerShell을 사용 하 여 서버 수준 방화벽 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-113">tooallow connections from your application or client machine's public IP address, you must first create a server-level firewall rule using hello Azure Portal, REST API, or PowerShell.</span></span> <span data-ttu-id="2ff84-114">모범 사례로, 가능한 한 서버 방화벽을 통해 허용 hello IP 주소 범위를 제한 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-114">As a best practice, you should restrict hello IP address ranges allowed through your server firewall as much as possible.</span></span>  <span data-ttu-id="2ff84-115">로컬 컴퓨터에서 Azure SQL 데이터 웨어하우스 tooaccess 확인 hello 방화벽 네트워크와 로컬 컴퓨터에서 TCP 포트 1433에서 나가는 통신을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-115">tooaccess Azure SQL Data Warehouse from your local computer, ensure hello firewall on your network and local computer allows outgoing communication on TCP port 1433.</span></span>  <span data-ttu-id="2ff84-116">자세한 내용은 [Azure SQL Database 방화벽][Azure SQL Database firewall], [sp_set_firewall_rule][sp_set_firewall_rule] 및 [sp_set_database_firewall_rule][sp_set_database_firewall_rule]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ff84-116">For more information, see [Azure SQL Database firewall][Azure SQL Database firewall], [sp_set_firewall_rule][sp_set_firewall_rule], and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span></span>

<span data-ttu-id="2ff84-117">연결 tooyour SQL 데이터 웨어하우스는 기본적으로 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-117">Connections tooyour SQL Data Warehouse are encrypted by default.</span></span>  <span data-ttu-id="2ff84-118">연결 설정 toodisable 수정 암호화는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-118">Modifying connection settings toodisable encryption are ignored.</span></span>

## <a name="authentication"></a><span data-ttu-id="2ff84-119">인증</span><span class="sxs-lookup"><span data-stu-id="2ff84-119">Authentication</span></span>
<span data-ttu-id="2ff84-120">인증 참조 toohow toohello 데이터베이스를 연결할 때 사용자의 신원을 증명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-120">Authentication refers toohow you prove your identity when connecting toohello database.</span></span> <span data-ttu-id="2ff84-121">SQL Data Warehouse는 현재 Azure Active Directory뿐 아니라 사용자 이름 및 암호를 사용하는 SQL Server 인증도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-121">SQL Data Warehouse currently supports SQL Server Authentication with a username and password as well as a Azure Active Directory.</span></span> 

<span data-ttu-id="2ff84-122">데이터베이스에 대 한 hello 논리 서버를 만들 때 "서버 관리자" 로그인 사용자 이름 및 암호를 지정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-122">When you created hello logical server for your database, you specified a "server admin" login with a username and password.</span></span> <span data-ttu-id="2ff84-123">이러한 자격 증명을 사용 하 여 tooany 데이터베이스 hello 데이터베이스 소유자 또는 SQL Server 인증을 통해 "dbo"로 해당 서버에 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-123">Using these credentials, you can authenticate tooany database on that server as hello database owner, or "dbo" through SQL Server Authentication.</span></span>

<span data-ttu-id="2ff84-124">그러나 모범 사례로, 조직의 사용자가 다른 계정 tooauthenticate를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-124">However, as a best practice, your organization’s users should use a different account tooauthenticate.</span></span> <span data-ttu-id="2ff84-125">이렇게 toohello 응용 프로그램을 부여 하는 hello 사용 권한을 제한 하 고 응용 프로그램 코드는 취약 한 tooa SQL 주입 공격 하는 경우 악의적인 활동의 hello 위험을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-125">This way you can limit hello permissions granted toohello application and reduce hello risks of malicious activity in case your application code is vulnerable tooa SQL injection attack.</span></span> 

<span data-ttu-id="2ff84-126">SQL Server 인증 사용자를 toocreate 연결 toohello **마스터** 데이터베이스 서버를 서버 관리자 로그인 하 고 새 서버 로그인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-126">toocreate a SQL Server Authenticated user, connect toohello **master** database on your server with your server admin login and create a new server login.</span></span>  <span data-ttu-id="2ff84-127">또한 Azure SQL 데이터 웨어하우스 사용자에 대 한 hello master 데이터베이스에서 좋습니다 toocreate 사용자 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-127">Additionally, it is a good idea toocreate a user in hello master database for Azure SQL Data Warehouse users.</span></span> <span data-ttu-id="2ff84-128">Master에 사용자를 만들면 SSMS와 같은 도구를 사용 하 여 데이터베이스 이름을 지정 하지 않고 사용자 toologin이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-128">Creating a user in master allows a user toologin using tools like SSMS without specifying a database name.</span></span>  <span data-ttu-id="2ff84-129">또한 있게 toouse hello 개체 탐색기 tooview에 모든 데이터베이스를 SQL server.</span><span class="sxs-lookup"><span data-stu-id="2ff84-129">It also allows them toouse hello object explorer tooview all databases on a SQL server.</span></span>

```sql
-- Connect toomaster database and create a login
CREATE LOGIN ApplicationLogin WITH PASSWORD = 'Str0ng_password';
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

<span data-ttu-id="2ff84-130">그런 다음 tooyour 연결 **SQL 데이터 웨어하우스 데이터베이스** 서버 관리자 로그인과 방금 만든 hello server 로그인 기반 데이터베이스 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-130">Then, connect tooyour **SQL Data Warehouse database** with your server admin login and create a database user based on hello server login you just created.</span></span>

```sql
-- Connect tooSQL DW database and create a database user
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

<span data-ttu-id="2ff84-131">사용자는 로그인 만들기 또는 새 데이터베이스 만들기 등의 추가 작업을 수행 하는 경우 할당 된 toobe toohello 해야 됩니다 `Loginmanager` 및 `dbmanager` hello master 데이터베이스의 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-131">If a user will be doing additional operations such as creating logins or creating new databases, they will also need toobe assigned toohello `Loginmanager` and `dbmanager` roles in hello master database.</span></span> <span data-ttu-id="2ff84-132">이러한 추가 역할 및 인증 tooa SQL 데이터베이스에 대 한 자세한 내용은 참조 하십시오. [Azure SQL 데이터베이스에서 데이터베이스 및 로그인 관리][Managing databases and logins in Azure SQL Database]합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-132">For more information on these additonal roles and authenticating tooa SQL Database, see [Managing databases and logins in Azure SQL Database][Managing databases and logins in Azure SQL Database].</span></span>  <span data-ttu-id="2ff84-133">SQL 데이터 웨어하우스에 대 한 Azure AD에 대 한 자세한 내용은 참조 하십시오. [데이터 웨어하우스를 사용 하 여 Azure Active Directory 인증 여 tooSQL 연결][Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication]합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-133">For more details on Azure AD for SQL Data Warehouse, see [Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication][Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication].</span></span>

## <a name="authorization"></a><span data-ttu-id="2ff84-134">권한 부여</span><span class="sxs-lookup"><span data-stu-id="2ff84-134">Authorization</span></span>
<span data-ttu-id="2ff84-135">권한 부여 toowhat는 Azure SQL 데이터 웨어하우스 데이터베이스 내에서 수행할 수 있습니다 및이 사용자 계정의 역할 멤버 자격과 권한에 의해 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-135">Authorization refers toowhat you can do within an Azure SQL Data Warehouse database, and this is controlled by your user account's role memberships and permissions.</span></span> <span data-ttu-id="2ff84-136">모범 사례로, 사용자가 hello를 필요한 최소한의 권한만 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-136">As a best practice, you should grant users hello least privileges necessary.</span></span> <span data-ttu-id="2ff84-137">Azure SQL 데이터 웨어하우스 T-SQL에서이 쉽게 toomanage 역할과 함께 사용 하면:</span><span class="sxs-lookup"><span data-stu-id="2ff84-137">Azure SQL Data Warehouse makes this easy toomanage with roles in T-SQL:</span></span>

```sql
EXEC sp_addrolemember 'db_datareader', 'ApplicationUser'; -- allows ApplicationUser tooread data
EXEC sp_addrolemember 'db_datawriter', 'ApplicationUser'; -- allows ApplicationUser toowrite data
```

<span data-ttu-id="2ff84-138">hello 서버 관리자 계정으로 연결 하는 hello 데이터베이스 내의 모든 기관 toodo가 db_owner의 멤버인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-138">hello server admin account you are connecting with is a member of db_owner, which has authority toodo anything within hello database.</span></span> <span data-ttu-id="2ff84-139">스키마 업그레이드 및 기타 관리 작업을 배포하기 위해서는 이 계정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-139">Save this account for deploying schema upgrades and other management operations.</span></span> <span data-ttu-id="2ff84-140">Hello로 응용 프로그램 toohello 데이터베이스에서 좀 더 제한적된 사용 권한 tooconnect hello "ApplicationUser" 계정을 사용 응용 프로그램에 필요한 최소 권한입니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-140">Use hello "ApplicationUser" account with more limited permissions tooconnect from your application toohello database with hello least privileges needed by your application.</span></span>

<span data-ttu-id="2ff84-141">toofurther도 같은 방법으로 사용자가 Azure SQL 데이터베이스와 함께 수행할 수 있는 작업</span><span class="sxs-lookup"><span data-stu-id="2ff84-141">There are ways toofurther limit what a user can do with Azure SQL Database:</span></span>

* <span data-ttu-id="2ff84-142">세분화 된 [권한을] [ Permissions] 제어 작업을 수행할 수 있습니다 수행에 개별 열, 테이블, 뷰, 프로시저 및 hello 데이터베이스에서 다른 개체를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-142">Granular [Permissions][Permissions] let you control which operations you can do on individual columns, tables, views, procedures, and other objects in hello database.</span></span> <span data-ttu-id="2ff84-143">사용 하 여 세분화 된 사용 권한 toohave 대부분 제어 hello 및 hello 필요한 최소한의 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-143">Use granular permissions toohave hello most control and grant hello minimum permissions necessary.</span></span> <span data-ttu-id="2ff84-144">hello 세분화 된 권한 시스템은 다소 복잡 하 고 일부 연구 toouse를 효과적으로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-144">hello granular permission system is somewhat complicated and will require some study toouse effectively.</span></span>
* <span data-ttu-id="2ff84-145">[데이터베이스 역할] [ Database roles] db_datareader 및 db_datawriter 사용된 toocreate 수 이외의 보다 강력한 응용 프로그램 사용자 계정 또는 성능이 낮은 관리 계정.</span><span class="sxs-lookup"><span data-stu-id="2ff84-145">[Database roles][Database roles] other than db_datareader and db_datawriter can be used toocreate more powerful application user accounts or less powerful management accounts.</span></span> <span data-ttu-id="2ff84-146">hello 기본 제공 고정된 데이터베이스 역할을 쉽게 toogrant 사용 권한을 제공 하지만 필요한 것 보다 많은 권한이 부여 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-146">hello built-in fixed database roles provide an easy way toogrant permissions, but can result in granting more permissions than are necessary.</span></span>
* <span data-ttu-id="2ff84-147">[저장 프로시저] [ Stored procedures] 사용된 toolimit hello 데이터베이스에서 수행할 수 있는 hello 동작 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-147">[Stored procedures][Stored procedures] can be used toolimit hello actions that can be taken on hello database.</span></span>

<span data-ttu-id="2ff84-148">Hello Azure 클래식 포털에서에서 데이터베이스 및 논리 서버를 관리 하거나 hello Azure 리소스 관리자 API를 사용 하 여 포털 사용자 계정의 역할 할당에 의해 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-148">Managing databases and logical servers from hello Azure Classic Portal or using hello Azure Resource Manager API is controlled by your portal user account's role assignments.</span></span> <span data-ttu-id="2ff84-149">이 항목에 대한 자세한 내용은 [Azure Portal의 역할 기반 액세스 제어][Role-based access control in Azure Portal]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ff84-149">For more information on this topic, see [Role-based access control in Azure Portal][Role-based access control in Azure Portal].</span></span>

## <a name="encryption"></a><span data-ttu-id="2ff84-150">암호화</span><span class="sxs-lookup"><span data-stu-id="2ff84-150">Encryption</span></span>
<span data-ttu-id="2ff84-151">Azure SQL 데이터 웨어하우스 투명 한 데이터 암호화 (TDE)는 실시간 암호화 및 미사용 데이터의 암호 해독을 수행 하 여 악의적인 활동의 hello 위협 으로부터 보호 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-151">Azure SQL Data Warehouse Transparent Data Encryption (TDE) helps protect against hello threat of malicious activity by performing real-time encryption and decryption of your data at rest.</span></span>  <span data-ttu-id="2ff84-152">데이터베이스를 암호화 하는 경우 모든 변경 내용을 tooyour 응용 프로그램을 요구 하지 않고 연결 된 백업 및 트랜잭션 로그 파일 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-152">When you encrypt your database, associated backups and transaction log files are encrypted without requiring any changes tooyour applications.</span></span> <span data-ttu-id="2ff84-153">TDE 키 호출된 hello 대칭 데이터베이스 암호화 키를 사용 하 여 전체 데이터베이스의 hello 저장소를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-153">TDE encrypts hello storage of an entire database by using a symmetric key called hello database encryption key.</span></span> <span data-ttu-id="2ff84-154">SQL 데이터베이스의 hello 데이터베이스 암호화 키는 기본 제공 서버 인증서로 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-154">In SQL Database hello database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="2ff84-155">hello 기본 제공 서버 인증서는 각 SQL 데이터베이스 서버에 대해 고유 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-155">hello built-in server certificate is unique for each SQL Database server.</span></span> <span data-ttu-id="2ff84-156">Microsoft는 적어도 90일마다 이러한 인증서를 자동으로 회전합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-156">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="2ff84-157">SQL 데이터 웨어하우스 사용 되는 hello 암호화 알고리즘은 AES 256입니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-157">hello encryption algorithm used by SQL Data Warehouse is AES-256.</span></span> <span data-ttu-id="2ff84-158">TDE에 대한 일반적인 설명은 [투명한 데이터 암호화][Transparent Data Encryption]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ff84-158">For a general description of TDE, see [Transparent Data Encryption][Transparent Data Encryption].</span></span>

<span data-ttu-id="2ff84-159">Hello를 사용 하 여 데이터베이스를 암호화할 수 [Azure 포털] [ Encryption with Portal] 또는 [T-SQL][Encryption with TSQL]합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-159">You can encrypt your database using hello [Azure Portal][Encryption with Portal] or [T-SQL][Encryption with TSQL].</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ff84-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2ff84-160">Next steps</span></span>
<span data-ttu-id="2ff84-161">세부 정보 및 서로 다른 프로토콜을 사용 하 여 SQL 데이터 웨어하우스 tooyour 연결에 대 한 예제를 참조 하세요. [tooSQL 데이터 웨어하우스 연결][Connect tooSQL Data Warehouse]합니다.</span><span class="sxs-lookup"><span data-stu-id="2ff84-161">For details and examples on connecting tooyour SQL Data Warehouse with different protocols, see [Connect tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span></span>

<!--Image references-->

<!--Article references-->
[Connect tooSQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Encryption with Portal]: ./sql-data-warehouse-encryption-tde.md
[Encryption with TSQL]: ./sql-data-warehouse-encryption-tde-tsql.md
[Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication]: ./sql-data-warehouse-authentication.md

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
