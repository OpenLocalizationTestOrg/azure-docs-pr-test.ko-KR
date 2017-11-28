---
title: "SQL 데이터 웨어하우스 aaaAuthentication tooAzure | Microsoft Docs"
description: "Azure Active Directory (AAD) 및 SQL Server 인증 tooAzure SQL 데이터 웨어하우스 합니다."
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
tags: 
ms.assetid: fefaaa75-2d0c-4e5d-aadb-410342d1ad73
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.custom: security
ms.date: 03/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 66673ce1d4761243755254c8f64de1078a0ea82e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-tooazure-sql-data-warehouse"></a><span data-ttu-id="4e3f0-103">인증 tooAzure SQL 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="4e3f0-103">Authentication tooAzure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4e3f0-104">보안 개요</span><span class="sxs-lookup"><span data-stu-id="4e3f0-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="4e3f0-105">인증</span><span class="sxs-lookup"><span data-stu-id="4e3f0-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="4e3f0-106">암호화(포털)</span><span class="sxs-lookup"><span data-stu-id="4e3f0-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="4e3f0-107">암호화(T-SQL)</span><span class="sxs-lookup"><span data-stu-id="4e3f0-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="4e3f0-108">tooconnect tooSQL 데이터 웨어하우스를 전달 해야 보안 자격 증명의 인증을 위해.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-108">tooconnect tooSQL Data Warehouse, you must pass in security credentials for authentication purposes.</span></span> <span data-ttu-id="4e3f0-109">연결을 설정할 때 특정 연결 설정이 쿼리 세션을 설정하는 일부로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-109">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span></span>  

<span data-ttu-id="4e3f0-110">보안에 대 한 자세한 내용은 방법과 tooenable 연결 tooyour 데이터 웨어하우스 참조 [SQL 데이터 웨어하우스의 데이터베이스를 보호할][Secure a database in SQL Data Warehouse]합니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-110">For more information on security and how tooenable connections tooyour data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>

## <a name="sql-authentication"></a><span data-ttu-id="4e3f0-111">SQL 인증</span><span class="sxs-lookup"><span data-stu-id="4e3f0-111">SQL authentication</span></span>
<span data-ttu-id="4e3f0-112">tooconnect tooSQL 데이터 웨어하우스 hello 다음 정보를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-112">tooconnect tooSQL Data Warehouse, you must provide hello following information:</span></span>

* <span data-ttu-id="4e3f0-113">정규화된 서버 이름</span><span class="sxs-lookup"><span data-stu-id="4e3f0-113">Fully qualified servername</span></span>
* <span data-ttu-id="4e3f0-114">SQL 인증 지정</span><span class="sxs-lookup"><span data-stu-id="4e3f0-114">Specify SQL authentication</span></span>
* <span data-ttu-id="4e3f0-115">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="4e3f0-115">Username</span></span>
* <span data-ttu-id="4e3f0-116">암호</span><span class="sxs-lookup"><span data-stu-id="4e3f0-116">Password</span></span>
* <span data-ttu-id="4e3f0-117">기본 데이터베이스(옵션)</span><span class="sxs-lookup"><span data-stu-id="4e3f0-117">Default database (optional)</span></span>

<span data-ttu-id="4e3f0-118">기본적으로 연결 되 toohello *마스터* 데이터베이스와 사용자 데이터베이스 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-118">By default your connection connects toohello *master* database and not your user database.</span></span> <span data-ttu-id="4e3f0-119">tooconnect tooyour 사용자 데이터베이스를 선택할 수 있습니다 toodo 다음 두 가지 중 하나:</span><span class="sxs-lookup"><span data-stu-id="4e3f0-119">tooconnect tooyour user database, you can choose toodo one of two things:</span></span>

* <span data-ttu-id="4e3f0-120">Hello SSDT, SSMS 또는 응용 프로그램 연결 문자열에서 SQL Server 개체 탐색기로 서버를 등록할 때 hello 기본 데이터베이스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-120">Specify hello default database when registering your server with hello SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span></span> <span data-ttu-id="4e3f0-121">Hello InitialCatalog 매개 변수는 ODBC 연결에 대 한 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-121">For example, include hello InitialCatalog parameter for an ODBC connection.</span></span>
* <span data-ttu-id="4e3f0-122">SSDT에는 세션을 만들기 전에 hello 사용자 데이터베이스를 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-122">Highlight hello user database before creating a session in SSDT.</span></span>

> [!NOTE]
> <span data-ttu-id="4e3f0-123">Transact-sql 문의 hello **사용 MyDatabase;** 연결을 위한 hello 데이터베이스 변경에 대 한 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-123">hello Transact-SQL statement **USE MyDatabase;** is not supported for changing hello database for a connection.</span></span> <span data-ttu-id="4e3f0-124">SSDT를 사용 하 여 tooSQL 데이터 웨어하우스에 연결 하는 지침 참조 toohello [Visual Studio와 함께 쿼리] [ Query with Visual Studio] 문서.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-124">For guidance connecting tooSQL Data Warehouse with SSDT, refer toohello [Query with Visual Studio][Query with Visual Studio] article.</span></span>
> 
> 

## <a name="azure-active-directory-aad-authentication"></a><span data-ttu-id="4e3f0-125">AAD(Azure Active Directory) 인증</span><span class="sxs-lookup"><span data-stu-id="4e3f0-125">Azure Active Directory (AAD) authentication</span></span>
<span data-ttu-id="4e3f0-126">[Azure Active Directory] [ What is Azure Active Directory] 인증은 Azure Active Directory (Azure AD)에 id를 사용 하 여 Azure SQL 데이터 웨어하우스 tooMicrosoft 연결의 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-126">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting tooMicrosoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="4e3f0-127">Azure Active Directory 인증을 사용 하면 데이터베이스 사용자의 신원을 hello 및 하나의 중앙 위치에서 다른 Microsoft 서비스를 중앙에서 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-127">With Azure Active Directory authentication, you can centrally manage hello identities of database users and other Microsoft services in one central location.</span></span> <span data-ttu-id="4e3f0-128">ID 관리를 중앙 toomanage SQL 데이터 웨어하우스 사용자를 한 위치를 제공 하 고 사용 권한 관리를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-128">Central ID management provides a single place toomanage SQL Data Warehouse users and simplifies permission management.</span></span> 

### <a name="benefits"></a><span data-ttu-id="4e3f0-129">이점</span><span class="sxs-lookup"><span data-stu-id="4e3f0-129">Benefits</span></span>
<span data-ttu-id="4e3f0-130">Azure Active Directory의 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-130">Azure Active Directory benefits include:</span></span>

* <span data-ttu-id="4e3f0-131">대체 tooSQL 서버 인증을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-131">Provides an alternative tooSQL Server authentication.</span></span>
* <span data-ttu-id="4e3f0-132">사용 하면 데이터베이스 서버에 대해 hello 확산 됨에 따라 사용자 id를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-132">Helps stop hello proliferation of user identities across database servers.</span></span>
* <span data-ttu-id="4e3f0-133">한 위치에서의 암호 회전이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-133">Allows password rotation in a single place</span></span>
* <span data-ttu-id="4e3f0-134">외부(AAD) 그룹을 사용하여 데이터베이스 사용 권한을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-134">Manage database permissions using external (AAD) groups.</span></span>
* <span data-ttu-id="4e3f0-135">Windows 통합 인증 또는 Azure Active Directory에서 지원하는 기타 인증을 사용하여 암호 저장을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-135">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span></span>
* <span data-ttu-id="4e3f0-136">사용 하 여 hello 데이터베이스 수준에서 데이터베이스 사용자 tooauthenticate id를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-136">Uses contained database users tooauthenticate identities at hello database level.</span></span>
* <span data-ttu-id="4e3f0-137">데이터 웨어하우스 tooSQL 연결 응용 프로그램에 대 한 토큰 기반 인증을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-137">Supports token-based authentication for applications connecting tooSQL Data Warehouse.</span></span>
* <span data-ttu-id="4e3f0-138">SQL Server Management Studio에 대한 Active Directory 유니버설 인증을 통해 Multi-Factor Authentication을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-138">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span></span> <span data-ttu-id="4e3f0-139">Multi-Factor Authentication에 대한 설명을 보려면 [SQL 데이터베이스 및 SQL 데이터 웨어하우스를 사용한 Azure AD MFA에 대한 SSMS 지원](../sql-database/sql-database-ssms-mfa-authentication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-139">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4e3f0-140">Azure Active Directory는 비교적 새로운 기능으로, 몇 가지 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-140">Azure Active Directory is still relatively new and has some limitations.</span></span> <span data-ttu-id="4e3f0-141">Azure Active Directory에 사용자 환경에 가장 잘 맞는 tooensure 참조 [Azure AD 기능 및 제한 사항][Azure AD features and limitations], 특히 hello 추가로 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-141">tooensure that Azure Active Directory is a good fit for your environment, see [Azure AD features and limitations][Azure AD features and limitations], specifically hello Additional considerations.</span></span>
> 
> 

### <a name="configuration-steps"></a><span data-ttu-id="4e3f0-142">구성 단계</span><span class="sxs-lookup"><span data-stu-id="4e3f0-142">Configuration steps</span></span>
<span data-ttu-id="4e3f0-143">이러한 단계 tooconfigure Azure Active Directory 인증을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-143">Follow these steps tooconfigure Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="4e3f0-144">Azure Active Directory 만들기 및 채우기</span><span class="sxs-lookup"><span data-stu-id="4e3f0-144">Create and populate an Azure Active Directory</span></span>
2. <span data-ttu-id="4e3f0-145">옵션: 연결 하거나 현재 Azure 구독과 연결 되어 있는 hello active directory 변경</span><span class="sxs-lookup"><span data-stu-id="4e3f0-145">Optional: Associate or change hello active directory that is currently associated with your Azure Subscription</span></span>
3. <span data-ttu-id="4e3f0-146">Azure SQL 데이터 웨어하우스에 대한 Azure Active Directory 관리자 만들기</span><span class="sxs-lookup"><span data-stu-id="4e3f0-146">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span></span>
4. <span data-ttu-id="4e3f0-147">클라이언트 컴퓨터 구성</span><span class="sxs-lookup"><span data-stu-id="4e3f0-147">Configure your client computers</span></span>
5. <span data-ttu-id="4e3f0-148">AD id에 매핑된 데이터베이스 tooAzure 포함 된 데이터베이스 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="4e3f0-148">Create contained database users in your database mapped tooAzure AD identities</span></span>
6. <span data-ttu-id="4e3f0-149">Azure AD id를 사용 하 여 tooyour 데이터 웨어하우스에 연결</span><span class="sxs-lookup"><span data-stu-id="4e3f0-149">Connect tooyour data warehouse by using Azure AD identities</span></span>

<span data-ttu-id="4e3f0-150">현재 Azure Active Directory 사용자는 SSDT 개체 탐색기에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-150">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span></span> <span data-ttu-id="4e3f0-151">이 문제를 해결에 hello 사용자 보기 [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-151">As a workaround, view hello users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span>

### <a name="find-hello-details"></a><span data-ttu-id="4e3f0-152">Hello 세부 정보 찾기</span><span class="sxs-lookup"><span data-stu-id="4e3f0-152">Find hello details</span></span>
* <span data-ttu-id="4e3f0-153">Azure SQL 데이터베이스 및 Azure SQL 데이터 웨어하우스 용 hello 단계 tooconfigure 및 사용 하 여 Azure Active Directory 인증 거의 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-153">hello steps tooconfigure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="4e3f0-154">에 따라 자세한 hello 항목의 단계는 hello [연결 tooSQL 데이터베이스 또는 SQL 데이터 웨어하우스를 사용 하 여 Azure Active Directory 인증 여](../sql-database/sql-database-aad-authentication.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-154">Follow hello detailed steps in hello topic [Connecting tooSQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span></span>
* <span data-ttu-id="4e3f0-155">사용자 정의 데이터베이스 역할을 만들고 사용자 toohello 역할을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-155">Create custom database roles and add users toohello roles.</span></span> <span data-ttu-id="4e3f0-156">그런 다음 세부적인 권한을 toohello 역할을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-156">Then grant granular permissions toohello roles.</span></span> <span data-ttu-id="4e3f0-157">자세한 내용은 [데이터베이스 엔진 권한 시작](https://msdn.microsoft.com/library/mt667986.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-157">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e3f0-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4e3f0-158">Next steps</span></span>
<span data-ttu-id="4e3f0-159">Visual Studio 및 다른 응용 프로그램을 사용 하 여 데이터 웨어하우스 쿼리 toostart 참조 [Visual Studio와 함께 쿼리][Query with Visual Studio]합니다.</span><span class="sxs-lookup"><span data-stu-id="4e3f0-159">toostart querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
