---
title: "Azure SQL Data Warehouse에 대한 인증 | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스에 대한 AAD(Azure Active Directory) 및 SQL Server 인증"
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
ms.openlocfilehash: 92f48027051bc4aff4d6b8d66fdd6de81bba3657
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="authentication-to-azure-sql-data-warehouse"></a><span data-ttu-id="3239b-103">Azure SQL 데이터 웨어하우스에 대한 인증</span><span class="sxs-lookup"><span data-stu-id="3239b-103">Authentication to Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3239b-104">보안 개요</span><span class="sxs-lookup"><span data-stu-id="3239b-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="3239b-105">인증</span><span class="sxs-lookup"><span data-stu-id="3239b-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="3239b-106">암호화(포털)</span><span class="sxs-lookup"><span data-stu-id="3239b-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="3239b-107">암호화(T-SQL)</span><span class="sxs-lookup"><span data-stu-id="3239b-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="3239b-108">SQL 데이터 웨어하우스에 연결하려면 인증 목적으로 보안 자격 증명을 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-108">To connect to SQL Data Warehouse, you must pass in security credentials for authentication purposes.</span></span> <span data-ttu-id="3239b-109">연결을 설정할 때 특정 연결 설정이 쿼리 세션을 설정하는 일부로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-109">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span></span>  

<span data-ttu-id="3239b-110">보안에 대한 자세한 내용과 데이터 웨어하우스에 대한 연결을 설정하는 방법은 [SQL Data Warehouse에서 데이터베이스 보호][Secure a database in SQL Data Warehouse]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3239b-110">For more information on security and how to enable connections to your data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>

## <a name="sql-authentication"></a><span data-ttu-id="3239b-111">SQL 인증</span><span class="sxs-lookup"><span data-stu-id="3239b-111">SQL authentication</span></span>
<span data-ttu-id="3239b-112">SQL 데이터 웨어하우스에 연결하려면 다음 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-112">To connect to SQL Data Warehouse, you must provide the following information:</span></span>

* <span data-ttu-id="3239b-113">정규화된 서버 이름</span><span class="sxs-lookup"><span data-stu-id="3239b-113">Fully qualified servername</span></span>
* <span data-ttu-id="3239b-114">SQL 인증 지정</span><span class="sxs-lookup"><span data-stu-id="3239b-114">Specify SQL authentication</span></span>
* <span data-ttu-id="3239b-115">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="3239b-115">Username</span></span>
* <span data-ttu-id="3239b-116">암호</span><span class="sxs-lookup"><span data-stu-id="3239b-116">Password</span></span>
* <span data-ttu-id="3239b-117">기본 데이터베이스(옵션)</span><span class="sxs-lookup"><span data-stu-id="3239b-117">Default database (optional)</span></span>

<span data-ttu-id="3239b-118">기본적으로 사용자의 연결은 사용자의 사용자 데이터베이스가 아닌 *master* 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-118">By default your connection connects to the *master* database and not your user database.</span></span> <span data-ttu-id="3239b-119">사용자의 사용자 데이터베이스에 연결하려면 다음과 같은 두 가지 작업 중 하나를 수행하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-119">To connect to your user database, you can choose to do one of two things:</span></span>

* <span data-ttu-id="3239b-120">SSDT, SSMS 또는 응용 프로그램 연결 문자열에서 SQL Server 개체 탐색기에 서버를 등록할 때 기본 데이터베이스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-120">Specify the default database when registering your server with the SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span></span> <span data-ttu-id="3239b-121">예를 들어 ODBC 연결에 대해 InitialCatalog 매개 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-121">For example, include the InitialCatalog parameter for an ODBC connection.</span></span>
* <span data-ttu-id="3239b-122">SSDT에서 세션을 만들기 전에 사용자 데이터베이스를 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-122">Highlight the user database before creating a session in SSDT.</span></span>

> [!NOTE]
> <span data-ttu-id="3239b-123">연결을 위한 데이터베이스 변경의 경우 Transact-SQL 문 **USE MyDatabase;** 는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-123">The Transact-SQL statement **USE MyDatabase;** is not supported for changing the database for a connection.</span></span> <span data-ttu-id="3239b-124">SSDT를 사용하여 SQL Data Warehouse에 연결하는 지침은 [Visual Studio로 쿼리][Query with Visual Studio] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3239b-124">For guidance connecting to SQL Data Warehouse with SSDT, refer to the [Query with Visual Studio][Query with Visual Studio] article.</span></span>
> 
> 

## <a name="azure-active-directory-aad-authentication"></a><span data-ttu-id="3239b-125">AAD(Azure Active Directory) 인증</span><span class="sxs-lookup"><span data-stu-id="3239b-125">Azure Active Directory (AAD) authentication</span></span>
<span data-ttu-id="3239b-126">[Azure Active Directory][What is Azure Active Directory] 인증은 Azure AD(Azure Active Directory)의 ID를 사용하여 Microsoft Azure SQL Data Warehouse에 연결하는 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-126">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting to Microsoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="3239b-127">Azure Active Directory 인증을 사용하면 데이터베이스 사용자 및 다른 Microsoft 서비스의 ID를 하나의 중앙 위치에서 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-127">With Azure Active Directory authentication, you can centrally manage the identities of database users and other Microsoft services in one central location.</span></span> <span data-ttu-id="3239b-128">중앙 ID 관리는 SQL 데이터 웨어하우스 사용자 관리를 위한 단일 위치를 제공하며 권한 관리를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-128">Central ID management provides a single place to manage SQL Data Warehouse users and simplifies permission management.</span></span> 

### <a name="benefits"></a><span data-ttu-id="3239b-129">이점</span><span class="sxs-lookup"><span data-stu-id="3239b-129">Benefits</span></span>
<span data-ttu-id="3239b-130">Azure Active Directory의 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-130">Azure Active Directory benefits include:</span></span>

* <span data-ttu-id="3239b-131">SQL Server 인증에 대한 대안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-131">Provides an alternative to SQL Server authentication.</span></span>
* <span data-ttu-id="3239b-132">데이터베이스 서버 전체에서 사용자 ID의 확산을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-132">Helps stop the proliferation of user identities across database servers.</span></span>
* <span data-ttu-id="3239b-133">한 위치에서의 암호 회전이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-133">Allows password rotation in a single place</span></span>
* <span data-ttu-id="3239b-134">외부(AAD) 그룹을 사용하여 데이터베이스 사용 권한을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-134">Manage database permissions using external (AAD) groups.</span></span>
* <span data-ttu-id="3239b-135">Windows 통합 인증 또는 Azure Active Directory에서 지원하는 기타 인증을 사용하여 암호 저장을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-135">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span></span>
* <span data-ttu-id="3239b-136">포함된 데이터베이스 사용자를 통해 데이터베이스 수준에서 ID를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-136">Uses contained database users to authenticate identities at the database level.</span></span>
* <span data-ttu-id="3239b-137">SQL 데이터 웨어하우스에 연결되는 응용 프로그램에 대한 토큰 기반 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-137">Supports token-based authentication for applications connecting to SQL Data Warehouse.</span></span>
* <span data-ttu-id="3239b-138">SQL Server Management Studio에 대한 Active Directory 유니버설 인증을 통해 Multi-Factor Authentication을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-138">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span></span> <span data-ttu-id="3239b-139">Multi-Factor Authentication에 대한 설명을 보려면 [SQL 데이터베이스 및 SQL 데이터 웨어하우스를 사용한 Azure AD MFA에 대한 SSMS 지원](../sql-database/sql-database-ssms-mfa-authentication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3239b-139">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3239b-140">Azure Active Directory는 비교적 새로운 기능으로, 몇 가지 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-140">Azure Active Directory is still relatively new and has some limitations.</span></span> <span data-ttu-id="3239b-141">Azure Active Directory가 사용자 환경에 적합한지 확인하려면 [Azure AD 기능 및 제한 사항][Azure AD features and limitations], 특히 추가 고려 사항을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3239b-141">To ensure that Azure Active Directory is a good fit for your environment, see [Azure AD features and limitations][Azure AD features and limitations], specifically the Additional considerations.</span></span>
> 
> 

### <a name="configuration-steps"></a><span data-ttu-id="3239b-142">구성 단계</span><span class="sxs-lookup"><span data-stu-id="3239b-142">Configuration steps</span></span>
<span data-ttu-id="3239b-143">다음 단계에 따라 Azure Active Directory 인증을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-143">Follow these steps to configure Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="3239b-144">Azure Active Directory 만들기 및 채우기</span><span class="sxs-lookup"><span data-stu-id="3239b-144">Create and populate an Azure Active Directory</span></span>
2. <span data-ttu-id="3239b-145">옵션: 현재 Azure 구독과 연결된 Active Directory를 연결하거나 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-145">Optional: Associate or change the active directory that is currently associated with your Azure Subscription</span></span>
3. <span data-ttu-id="3239b-146">Azure SQL 데이터 웨어하우스에 대한 Azure Active Directory 관리자 만들기</span><span class="sxs-lookup"><span data-stu-id="3239b-146">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span></span>
4. <span data-ttu-id="3239b-147">클라이언트 컴퓨터 구성</span><span class="sxs-lookup"><span data-stu-id="3239b-147">Configure your client computers</span></span>
5. <span data-ttu-id="3239b-148">Azure AD ID에 매핑된 데이터베이스에서 포함된 데이터베이스 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3239b-148">Create contained database users in your database mapped to Azure AD identities</span></span>
6. <span data-ttu-id="3239b-149">Azure AD ID를 사용하여 데이터 웨어하우스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-149">Connect to your data warehouse by using Azure AD identities</span></span>

<span data-ttu-id="3239b-150">현재 Azure Active Directory 사용자는 SSDT 개체 탐색기에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-150">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span></span> <span data-ttu-id="3239b-151">해결 방법으로 [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx)에서 사용자를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-151">As a workaround, view the users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span>

### <a name="find-the-details"></a><span data-ttu-id="3239b-152">세부 정보 찾기</span><span class="sxs-lookup"><span data-stu-id="3239b-152">Find the details</span></span>
* <span data-ttu-id="3239b-153">Azure Active Directory 인증을 구성하고 사용하는 단계는 Azure SQL Database 및 Azure SQL Data Warehouse의 경우와 거의 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-153">The steps to configure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="3239b-154">[Azure Active Directory 인증을 사용하여 SQL 데이터베이스 또는 SQL 데이터 웨어하우스 연결](../sql-database/sql-database-aad-authentication.md)항목의 자세한 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-154">Follow the detailed steps in the topic [Connecting to SQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span></span>
* <span data-ttu-id="3239b-155">사용자 지정 데이터베이스 역할을 만들고 역할에 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-155">Create custom database roles and add users to the roles.</span></span> <span data-ttu-id="3239b-156">그런 다음 역할에 세부적인 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="3239b-156">Then grant granular permissions to the roles.</span></span> <span data-ttu-id="3239b-157">자세한 내용은 [데이터베이스 엔진 권한 시작](https://msdn.microsoft.com/library/mt667986.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3239b-157">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3239b-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3239b-158">Next steps</span></span>
<span data-ttu-id="3239b-159">Visual Studio 및 다른 응용 프로그램으로 데이터 웨어하우스 쿼리를 시작하려면 [Visual Studio를 사용하여 쿼리][Query with Visual Studio]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3239b-159">To start querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
