---
title: "일반 SQL 커넥터 | Microsoft Docs"
description: "이 문서에서는 Microsoft의 일반 SQL 커넥터를 구성하는 방법을 설명합니다."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: fd8ccef3-6605-47ba-9219-e0c74ffc0ec9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a84096ba53a308855beedd76d9dec827c025cd57
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="generic-sql-connector-technical-reference"></a><span data-ttu-id="ce8cd-103">일반 SQL 커넥터 기술 참조</span><span class="sxs-lookup"><span data-stu-id="ce8cd-103">Generic SQL Connector technical reference</span></span>
<span data-ttu-id="ce8cd-104">이 문서에서는 일반 SQL 커넥터를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-104">This article describes the Generic SQL Connector.</span></span> <span data-ttu-id="ce8cd-105">이 문서는 다음 제품에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-105">The article applies to the following products:</span></span>

* <span data-ttu-id="ce8cd-106">Microsoft Identity Manager 2016 (MIM2016)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-106">Microsoft Identity Manager 2016 (MIM2016)</span></span>
* <span data-ttu-id="ce8cd-107">Forefront Identity Manager 2010 R2 (FIM2010R2)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-107">Forefront Identity Manager 2010 R2 (FIM2010R2)</span></span>
  * <span data-ttu-id="ce8cd-108">핫픽스 4.1.3671.0 이상 [KB3092178](https://support.microsoft.com/kb/3092178)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-108">Must use hotfix 4.1.3671.0 or later [KB3092178](https://support.microsoft.com/kb/3092178).</span></span>

<span data-ttu-id="ce8cd-109">MIM2016와 FIM2010R2의 경우 커넥터는 [Microsoft 다운로드 센터](http://go.microsoft.com/fwlink/?LinkId=717495)에서 다운로드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-109">For MIM2016 and FIM2010R2, the Connector is available as a download from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).</span></span>

<span data-ttu-id="ce8cd-110">작업에서 이 커넥터를 보려면 [Generic SQL Connector step-by-step(일반 SQL 커넥터 단계별)](active-directory-aadconnectsync-connector-genericsql-step-by-step.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-110">To see this Connector in action, see the [Generic SQL Connector step-by-step](active-directory-aadconnectsync-connector-genericsql-step-by-step.md) article.</span></span>

## <a name="overview-of-the-generic-sql-connector"></a><span data-ttu-id="ce8cd-111">일반 SQL 커넥터의 개요</span><span class="sxs-lookup"><span data-stu-id="ce8cd-111">Overview of the Generic SQL Connector</span></span>
<span data-ttu-id="ce8cd-112">일반 SQL 커넥터를 사용하면 ODBC 연결을 제공하는 데이터베이스 시스템과 동기화 서비스를 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-112">The Generic SQL Connector enables you to integrate the synchronization service with a database system that offers ODBC connectivity.</span></span>  

<span data-ttu-id="ce8cd-113">전체적인 관점에서 보면 커넥터의 현재 릴리스에서 다음과 같은 기능이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-113">From a high-level perspective, the following features are supported by the current release of the connector:</span></span>

| <span data-ttu-id="ce8cd-114">기능</span><span class="sxs-lookup"><span data-stu-id="ce8cd-114">Feature</span></span> | <span data-ttu-id="ce8cd-115">지원</span><span class="sxs-lookup"><span data-stu-id="ce8cd-115">Support</span></span> |
| --- | --- |
| <span data-ttu-id="ce8cd-116">연결된 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="ce8cd-116">Connected data source</span></span> |<span data-ttu-id="ce8cd-117">이 커넥터는 모든 64비트 ODBC 드라이버와 함께 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-117">The Connector is supported with all 64-bit ODBC drivers.</span></span> <span data-ttu-id="ce8cd-118">다음으로 테스트되었습니다: </span><span class="sxs-lookup"><span data-stu-id="ce8cd-118">It has been tested with the following:</span></span> <li><span data-ttu-id="ce8cd-119">Microsoft SQL Server 및 SQL Azure</span><span class="sxs-lookup"><span data-stu-id="ce8cd-119">Microsoft SQL Server & SQL Azure</span></span></li><li><span data-ttu-id="ce8cd-120">IBM DB2 10.x</span><span class="sxs-lookup"><span data-stu-id="ce8cd-120">IBM DB2 10.x</span></span></li><li><span data-ttu-id="ce8cd-121">IBM DB2 9.x</span><span class="sxs-lookup"><span data-stu-id="ce8cd-121">IBM DB2 9.x</span></span></li><li><span data-ttu-id="ce8cd-122">Oracle 10 및 11g</span><span class="sxs-lookup"><span data-stu-id="ce8cd-122">Oracle 10 & 11g</span></span></li><li><span data-ttu-id="ce8cd-123">MySQL 5.x</span><span class="sxs-lookup"><span data-stu-id="ce8cd-123">MySQL 5.x</span></span></li> |
| <span data-ttu-id="ce8cd-124">시나리오</span><span class="sxs-lookup"><span data-stu-id="ce8cd-124">Scenarios</span></span> |<li><span data-ttu-id="ce8cd-125">개체 수명 주기 관리</span><span class="sxs-lookup"><span data-stu-id="ce8cd-125">Object Lifecycle Management</span></span></li><li><span data-ttu-id="ce8cd-126">암호 관리</span><span class="sxs-lookup"><span data-stu-id="ce8cd-126">Password Management</span></span></li> |
| <span data-ttu-id="ce8cd-127">작업</span><span class="sxs-lookup"><span data-stu-id="ce8cd-127">Operations</span></span> |<li><span data-ttu-id="ce8cd-128">전체 가져오기 및 델타 가져오기, 내보내기</span><span class="sxs-lookup"><span data-stu-id="ce8cd-128">Full Import and Delta Import, Export</span></span></li><li><span data-ttu-id="ce8cd-129">내보내기: 추가, 삭제, 업데이트 및 바꾸기</span><span class="sxs-lookup"><span data-stu-id="ce8cd-129">For Export: Add, Delete, Update, and Replace</span></span></li><li><span data-ttu-id="ce8cd-130">암호 설정, 암호 변경</span><span class="sxs-lookup"><span data-stu-id="ce8cd-130">Set Password, Change Password</span></span></li> |
| <span data-ttu-id="ce8cd-131">스키마</span><span class="sxs-lookup"><span data-stu-id="ce8cd-131">Schema</span></span> |<li><span data-ttu-id="ce8cd-132">개체 및 특성의 동적 검색</span><span class="sxs-lookup"><span data-stu-id="ce8cd-132">Dynamic discovery of objects and attributes</span></span></li> |

### <a name="prerequisites"></a><span data-ttu-id="ce8cd-133">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ce8cd-133">Prerequisites</span></span>
<span data-ttu-id="ce8cd-134">커넥터를 사용하기 전에 동기화 서버에 다음 사항이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-134">Before you use the Connector, make sure you have the following on the synchronization server:</span></span>

* <span data-ttu-id="ce8cd-135">Microsoft.NET 4.5.2 Framework 이상</span><span class="sxs-lookup"><span data-stu-id="ce8cd-135">Microsoft .NET 4.5.2 Framework or later</span></span>
* <span data-ttu-id="ce8cd-136">64비트 ODBC 클라이언트 드라이버</span><span class="sxs-lookup"><span data-stu-id="ce8cd-136">64-bit ODBC client drivers</span></span>

### <a name="permissions-in-connected-data-source"></a><span data-ttu-id="ce8cd-137">연결된 데이터 원본의 사용 권한</span><span class="sxs-lookup"><span data-stu-id="ce8cd-137">Permissions in connected data source</span></span>
<span data-ttu-id="ce8cd-138">일반 SQL 커넥터에 지원되는 작업을 만들거나 수행하려면 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-138">To create or perform any of the supported tasks in Generic SQL connector, you must have:</span></span>

* <span data-ttu-id="ce8cd-139">db_datareader</span><span class="sxs-lookup"><span data-stu-id="ce8cd-139">db_datareader</span></span>
* <span data-ttu-id="ce8cd-140">db_datawriter</span><span class="sxs-lookup"><span data-stu-id="ce8cd-140">db_datawriter</span></span>

### <a name="ports-and-protocols"></a><span data-ttu-id="ce8cd-141">포트 및 프로토콜</span><span class="sxs-lookup"><span data-stu-id="ce8cd-141">Ports and protocols</span></span>
<span data-ttu-id="ce8cd-142">ODBC 드라이버가 작동하는 데 필요한 포트는 데이터베이스 공급 업체의 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-142">For the ports required for the ODBC driver to work, consult the database vendor's documentation.</span></span>

## <a name="create-a-new-connector"></a><span data-ttu-id="ce8cd-143">새 커넥터 만들기</span><span class="sxs-lookup"><span data-stu-id="ce8cd-143">Create a new Connector</span></span>
<span data-ttu-id="ce8cd-144">일반 SQL 커넥터를 만들려면 **동기화 서비스**에서 **관리 에이전트** 및 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-144">To Create a Generic SQL connector, in **Synchronization Service** select **Management Agent** and **Create**.</span></span> <span data-ttu-id="ce8cd-145">**일반 SQL(Microsoft)** 커넥터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-145">Select the **Generic SQL (Microsoft)** Connector.</span></span>

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/createconnector.png)

### <a name="connectivity"></a><span data-ttu-id="ce8cd-147">연결</span><span class="sxs-lookup"><span data-stu-id="ce8cd-147">Connectivity</span></span>
<span data-ttu-id="ce8cd-148">커넥터는 연결에 ODBC DSN 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-148">The Connector uses an ODBC DSN file for connectivity.</span></span> <span data-ttu-id="ce8cd-149">**관리 도구**의 시작 메뉴에 위치한 **ODBC 데이터 원본**을 사용하여 DSN 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-149">Create the DSN file using **ODBC Data Sources** found in the start menu under **Administrative Tools**.</span></span> <span data-ttu-id="ce8cd-150">관리 도구에서 커넥터에 제공할 수 있도록 **파일 DSN**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-150">In the administrative tool, create a **File DSN** so it can be provided to the Connector.</span></span>

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/connectivity.png)

<span data-ttu-id="ce8cd-152">연결 화면은 새 일반 SQL 커넥터를 만들 때의 첫 번째 화면입니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-152">The Connectivity screen is the first when you create a new Generic SQL Connector.</span></span> <span data-ttu-id="ce8cd-153">우선 다음 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-153">You first need to provide the following information:</span></span>

* <span data-ttu-id="ce8cd-154">DSN 파일 경로</span><span class="sxs-lookup"><span data-stu-id="ce8cd-154">DSN file path</span></span>
* <span data-ttu-id="ce8cd-155">인증</span><span class="sxs-lookup"><span data-stu-id="ce8cd-155">Authentication</span></span>
  * <span data-ttu-id="ce8cd-156">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="ce8cd-156">User Name</span></span>
  * <span data-ttu-id="ce8cd-157">암호</span><span class="sxs-lookup"><span data-stu-id="ce8cd-157">Password</span></span>

<span data-ttu-id="ce8cd-158">데이터베이스는 다음과 같은 인증 방법 중 하나를 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-158">The database should support one of these authentication methods:</span></span>

* <span data-ttu-id="ce8cd-159">**Windows 인증**: 인증하는 데이터베이스는 Windows 자격 증명을 사용하여 사용자를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-159">**Windows authentication**: The authenticating database uses the Windows credentials to verify the user.</span></span> <span data-ttu-id="ce8cd-160">지정된 사용자 이름/암호가 데이터베이스 인증에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-160">The user name/password specified is used to authenticate with the database.</span></span> <span data-ttu-id="ce8cd-161">이 계정에는 데이터베이스에 대한 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-161">This account needs permissions to the database.</span></span>
* <span data-ttu-id="ce8cd-162">**SQL 인증**: 인증하는 데이터베이스는 사용자 이름/암호가 정의된 연결 화면을 사용하여 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-162">**SQL authentication**: The authenticating database uses the user name/password defined one the Connectivity screen to connect to the database.</span></span> <span data-ttu-id="ce8cd-163">DSN 파일에서 사용자 이름/암호를 저장하는 경우 연결 화면에 제공된 자격 증명은 우선 순위를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-163">If you store the user name/pasword in the DSN file, the credentials provided on the Connectivity screen have precedence.</span></span>
* <span data-ttu-id="ce8cd-164">**Azure SQL Database 인증**: 자세한 내용은 [Azure Active Directory 인증을 사용하여 SQL Database에 연결](../../sql-database/sql-database-aad-authentication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-164">**Azure SQL Database authentication**: For more information, see [Connect to SQL Database By Using Azure Active Directory Authentication](../../sql-database/sql-database-aad-authentication.md).</span></span>

<span data-ttu-id="ce8cd-165">**DN이 앵커**: 이 옵션을 선택하면 DN이 앵커 특성으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-165">**DN is Anchor**: If you select this option, the DN is also used as the anchor attribute.</span></span> <span data-ttu-id="ce8cd-166">간단한 구현을 위해 사용할 수 있지만 다음과 같은 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-166">It can be used for a simple implementation but also has the following limitation:</span></span>

* <span data-ttu-id="ce8cd-167">커넥터는 하나의 개체 유형만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-167">Connector supports only one object type.</span></span> <span data-ttu-id="ce8cd-168">따라서 참조 특성은 동일한 개체 형식을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-168">Therefore any reference attributes can only reference the same object type.</span></span>

<span data-ttu-id="ce8cd-169">**내보내기 형식: 개체 대체**: 내보내는 동안 일부 특성이 변경된 경우 모든 특성을 가진 전체 개체는 내보내지고 기존 개체를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-169">**Export Type: Object Replace**: During export, when only some attributes have changed, the entire object with all attributes is exported and replaces the existing object.</span></span>

### <a name="schema-1-detect-object-types"></a><span data-ttu-id="ce8cd-170">스키마1(개체 형식 검색)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-170">Schema 1 (Detect object types)</span></span>
<span data-ttu-id="ce8cd-171">이 페이지에서는 커넥터가 데이터베이스의 다른 개체 형식을 검색하는 방법을 구성하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-171">On this page, you are going to configure how the Connector is going to find the different object types in the database.</span></span>

<span data-ttu-id="ce8cd-172">모든 개체 형식은 파티션으로 표시되며 **파티션 및 계층 구성**에서 자세히 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-172">Every object type is presented as a partition and configured further on **Configure Partitions and Hierarchies**.</span></span>

![schema1a](./media/active-directory-aadconnectsync-connector-genericsql/schema1a.png)

<span data-ttu-id="ce8cd-174">**개체 형식 검색 방법**: 커넥터가 이러한 개체 형식 검색 방법을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-174">**Object Type detection method**: The Connector supports these object type detection methods.</span></span>

* <span data-ttu-id="ce8cd-175">**고정 값**: 쉼표로 구분된 목록을 사용하여 개체 유형 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-175">**Fixed Value**: You provide the list of object types with a comma-separated list.</span></span> <span data-ttu-id="ce8cd-176">예: `User,Group,Department`.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-176">For example: `User,Group,Department`.</span></span>  
  <span data-ttu-id="ce8cd-177">![schema1b](./media/active-directory-aadconnectsync-connector-genericsql/schema1b.png)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-177">![schema1b](./media/active-directory-aadconnectsync-connector-genericsql/schema1b.png)</span></span>
* <span data-ttu-id="ce8cd-178">**테이블/뷰/저장 프로시저**: 테이블/뷰/저장 프로시저의 이름 및 개체 형식 목록을 제공하는 열 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-178">**Table/View/Stored Procedure**: Provide the name of the table/view/stored procedure and then the column name that provides the list of object types.</span></span> <span data-ttu-id="ce8cd-179">저장 프로시저를 사용하면 또한 **[Name]:[Direction]:[Value]** 형식에서 매개 변수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-179">If you use a stored procedure, then also provide parameters for it in the format **[Name]:[Direction]:[Value]**.</span></span> <span data-ttu-id="ce8cd-180">별도 줄에 각 매개 변수를 제공합니다.(Ctrl + Enter를 사용하여 새 줄 가져옴)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-180">Provide each parameter on a separate line (use Ctrl+Enter to get a new line).</span></span>  
  <span data-ttu-id="ce8cd-181">![schema1c](./media/active-directory-aadconnectsync-connector-genericsql/schema1c.png)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-181">![schema1c](./media/active-directory-aadconnectsync-connector-genericsql/schema1c.png)</span></span>
* <span data-ttu-id="ce8cd-182">**SQL 쿼리**: 이 옵션을 사용하면 개체 형식을 가진 단일 열을 반환하는 SQL 쿼리를 제공할 수 있습니다.예: `SELECT [Column Name] FROM TABLENAME`.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-182">**SQL Query**: This option allows you to provide a SQL query that returns a single column with object types, for example `SELECT [Column Name] FROM TABLENAME`.</span></span> <span data-ttu-id="ce8cd-183">반환된 열은 형식 문자열(varchar)이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-183">The returned column must be of type string (varchar).</span></span>

### <a name="schema-2-detect-attribute-types"></a><span data-ttu-id="ce8cd-184">스키마2(특성 형식 검색)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-184">Schema 2 (Detect attribute types)</span></span>
<span data-ttu-id="ce8cd-185">이 페이지에서 특성 이름 및 형식이 검색될 방법을 구성하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-185">On this page, you are going to configure how the attribute names and types are going to be detected.</span></span> <span data-ttu-id="ce8cd-186">구성 옵션은 이전 페이지에서 검색된 모든 개체 형식에 대해 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-186">The configuration options are listed for every object type detected on the previous page.</span></span>

![schema2a](./media/active-directory-aadconnectsync-connector-genericsql/schema2a.png)

<span data-ttu-id="ce8cd-188">**특성 형식 검색 방법**: 커넥터는 스키마1 화면에서 검색된 개체를 사용하여 이러한 특성 형식 검색 방법을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-188">**Attribute Type detection method**: The Connector supports these attribute type detection methods with every detected object type in Schema 1 screen.</span></span>

* <span data-ttu-id="ce8cd-189">**테이블/뷰/저장 프로시저**: 특성 이름을 사용해야 하는 테이블/뷰/저장 프로시저의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-189">**Table/View/Stored Procedure**: Provide the name of the table/view/stored procedure that should be used to find the attribute names.</span></span> <span data-ttu-id="ce8cd-190">저장 프로시저를 사용하면 또한 **[Name]:[Direction]:[Value]** 형식에서 매개 변수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-190">If you use a stored procedure, then also provide parameters for it in the format **[Name]:[Direction]:[Value]**.</span></span> <span data-ttu-id="ce8cd-191">별도 줄에 각 매개 변수를 제공합니다.(Ctrl + Enter를 사용하여 새 줄 가져옴)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-191">Provide each parameter on a separate line (use Ctrl+Enter to get a new line).</span></span> <span data-ttu-id="ce8cd-192">다중값 특성의 특성 이름을 검색하려면 테이블 또는 뷰의 쉼표로 구분된 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-192">To detect the attribute names in a multi-valued attribute, provide a comma-separated list of Tables or Views.</span></span> <span data-ttu-id="ce8cd-193">부모 및 자식 테이블에 동일한 열 이름이 있는 경우 다중값 시나리오가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-193">Multivalued scenarios are not supported when parent and child table have same column names.</span></span>
* <span data-ttu-id="ce8cd-194">**SQL 쿼리**: 이 옵션을 사용하면 특성 이름을 가진 단일 열을 반환하는 SQL 쿼리를 제공할 수 있습니다.예: `SELECT [Column Name] FROM TABLENAME`.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-194">**SQL query**: This option allows you to provide a SQL query that returns a single column with attribute names, for example `SELECT [Column Name] FROM TABLENAME`.</span></span> <span data-ttu-id="ce8cd-195">반환된 열은 형식 문자열(varchar)이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-195">The returned column must be of type string (varchar).</span></span>

### <a name="schema-3-define-anchor-and-dn"></a><span data-ttu-id="ce8cd-196">스키마3(앵커 및 DN 정의)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-196">Schema 3 (Define anchor and DN)</span></span>
<span data-ttu-id="ce8cd-197">이 페이지에서는 각 검색된 개체 형식에 대해 앵커 및 DN 특성을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-197">This page allows you to configure anchor and DN attribute for each detected object type.</span></span> <span data-ttu-id="ce8cd-198">앵커를 고유하게 만드는 여러 특성을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-198">You can select multiple attributes to make the anchor unique.</span></span>

![schema3a](./media/active-directory-aadconnectsync-connector-genericsql/schema3a.png)

* <span data-ttu-id="ce8cd-200">다중값 및 부울 특성은 나열되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-200">Multi-valued and Boolean attributes are not listed.</span></span>
* <span data-ttu-id="ce8cd-201">**DN이 앵커** 가 연결 페이지에서 선택되지 않는 한 동일한 특성은 앵커 및 DN 특성에 사용될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-201">Same attribute cannot use for DN and anchor, unless **DN is Anchor** is selected on the Connectivity page.</span></span>
* <span data-ttu-id="ce8cd-202">**DN이 앵커** 가 연결 페이지에서 선택되면 이 페이지는 DN 특성에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-202">If **DN is Anchor** is selected on the Connectivity page, this page requires only the DN attribute.</span></span> <span data-ttu-id="ce8cd-203">이 특성은 앵커 특성으로도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-203">This attribute would also be used as the anchor attribute.</span></span>

  ![schema3b](./media/active-directory-aadconnectsync-connector-genericsql/schema3b.png)

### <a name="schema-4-define-attribute-type-reference-and-direction"></a><span data-ttu-id="ce8cd-205">스키마4(특성 형식, 참조 및 방향 정의)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-205">Schema 4 (Define attribute type, reference, and direction)</span></span>
<span data-ttu-id="ce8cd-206">이 페이지를 사용하면 정수, 이진 또는 부울 값과 같은 특성 형식 및 각 특성에 대한 방향을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-206">This page allows you to configure the attribute type, such as integer, binary, or Boolean, and direction for each attribute.</span></span> <span data-ttu-id="ce8cd-207">**스키마2** 페이지에서 모든 특성은 다중값 특성을 포함하여 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-207">All attributes from page **schema 2** are listed including multi-valued attributes.</span></span>

![schema4a](./media/active-directory-aadconnectsync-connector-genericsql/schema4a.png)

* <span data-ttu-id="ce8cd-209">**DataType**: 동기화 엔진에 의해 알려진 해당 형식에 특성 형식을 매핑하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-209">**DataType**: Used to map the attribute type to those types known by the sync engine.</span></span> <span data-ttu-id="ce8cd-210">기본값은 SQL 스키마에서 검색하는 대로 동일한 형식을 사용하지만 날짜/시간 및 참조는 쉽게 감지할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-210">The default is to use the same type as detected in the SQL schema, but DateTime and Reference are not easily detectable.</span></span> <span data-ttu-id="ce8cd-211">이 경우에 **DateTime** 또는 **참조**를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-211">For those, you need to specify **DateTime** or **Reference**.</span></span>
* <span data-ttu-id="ce8cd-212">**방향**: 방향 특성을 가져오기, 내보내기 또는 ImportExport로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-212">**Direction**: You can set the attribute direction to Import, Export, or ImportExport.</span></span> <span data-ttu-id="ce8cd-213">ImportExport는 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-213">ImportExport is default.</span></span>

![schema4b](./media/active-directory-aadconnectsync-connector-genericsql/schema4b.png)

<span data-ttu-id="ce8cd-215">참고:</span><span class="sxs-lookup"><span data-stu-id="ce8cd-215">Notes:</span></span>

* <span data-ttu-id="ce8cd-216">특성 형식을 커넥터에서 감지할 수 없는 경우 문자열 데이터 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-216">If an attribute type is not detectable by the Connector, it uses the String data type.</span></span>
* <span data-ttu-id="ce8cd-217">**중첩 테이블** 은 열이 하나인 데이터베이스 테이블을 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-217">**Nested tables** can be considered one-column database tables.</span></span> <span data-ttu-id="ce8cd-218">Oracle은 특정 순서 없이 중첩 테이블의 행을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-218">Oracle stores the rows of a nested table in no particular order.</span></span> <span data-ttu-id="ce8cd-219">그러나 PL/SQL 변수로 중첩 테이블을 검색하는 경우 행은 1부터 시작하는 지정된 연속 첨자입니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-219">However, when you retrieve the nested table into a PL/SQL variable, the rows are given consecutive subscripts starting at 1.</span></span> <span data-ttu-id="ce8cd-220">개별 행에 배열형 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-220">That gives you array-like access to individual rows.</span></span>
* <span data-ttu-id="ce8cd-221">**VARRYS** 는 커넥터에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-221">**VARRYS** are not supported in the connector.</span></span>

### <a name="schema-5-define-partition-for-reference-attributes"></a><span data-ttu-id="ce8cd-222">스키마5(참조 특성에 대한 파티션 정의)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-222">Schema 5 (Define partition for reference attributes)</span></span>
<span data-ttu-id="ce8cd-223">이 페이지에서는 모든 참조 특성에 대해 특성이 참조하는 파티션(개체 형식)을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-223">On this page, you configure for all reference attributes which partition (object type) an attribute is referring to.</span></span>

![schema5](./media/active-directory-aadconnectsync-connector-genericsql/schema5.png)

<span data-ttu-id="ce8cd-225">**DN이 앵커**를 사용하는 경우 참조하는 것과 동일한 개체 형식을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-225">If you use **DN is anchor**, then you must use the same object type as the one you are referring from.</span></span> <span data-ttu-id="ce8cd-226">다른 개체 형식을 참조할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-226">You cannot reference another object type.</span></span>

>[!NOTE]
<span data-ttu-id="ce8cd-227">2017년 3월 업데이트부터 "*"에 대한 옵션이 추가됩니다. 이 옵션을 선택하면 모든 가능한 멤버 유형을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-227">Starting in the March 2017 update there is now an option for "*" When this option is chosen then all possible member types will be imported.</span></span>

![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/any-option.png)

>[!IMPORTANT]
 <span data-ttu-id="ce8cd-229">2017년 5월을 기준으로 "*", 즉 **옵션**이 흐름 내보내기 및 가져오기를 지원하도록 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-229">As of May 2017 the “*” aka **any option** has been changed to support import and export flow.</span></span> <span data-ttu-id="ce8cd-230">이 옵션을 사용하려는 경우 다중 값 테이블/뷰에 개체 형식을 포함하는 특성이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-230">If you want to use this option your multi-valued table/view should have an attribute that contains the object type.</span></span>

![](./media/active-directory-aadconnectsync-connector-genericsql/any-02.png)

 </br> <span data-ttu-id="ce8cd-231">"*"를 선택하면 해당 개체 형식의 열 이름도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-231">If "*" is selected then the name of the column with the object type must also be specified.</span></span></br> ![](./media/active-directory-aadconnectsync-connector-genericsql/any-03.png)

<span data-ttu-id="ce8cd-232">가져온 후 아래 이미지와 유사한 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-232">After import you will see something similar to the image below:</span></span>

  ![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/after-import.png)



### <a name="global-parameters"></a><span data-ttu-id="ce8cd-234">글로벌 매개 변수</span><span class="sxs-lookup"><span data-stu-id="ce8cd-234">Global Parameters</span></span>
<span data-ttu-id="ce8cd-235">글로벌 매개 변수 페이지는 델타 가져오기, 날짜/시간 형식 및 암호 메서드를 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-235">The Global Parameters page is used to configure Delta Import, Date/Time format, and Password method.</span></span>

![globalparameters1](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters1.png)



<span data-ttu-id="ce8cd-237">일반 SQL 커넥터는 델타 가져오기에 대한 다음 메서드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-237">The Generic SQL Connector supports the following methods for Delta Import:</span></span>

* <span data-ttu-id="ce8cd-238">**트리거**: [트리거를 사용하여 델타 뷰 생성](https://technet.microsoft.com/library/cc708665.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-238">**Trigger**: See [Generating Delta Views Using Triggers](https://technet.microsoft.com/library/cc708665.aspx).</span></span>
* <span data-ttu-id="ce8cd-239">**워터 마크**: 모든 데이터베이스에 사용할 수 있는 일반적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-239">**Watermark**: A generic approach that can be used with any database.</span></span> <span data-ttu-id="ce8cd-240">워터 마크 쿼리는 데이터베이스 공급 업체에 따라 미리 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-240">The watermark query is pre-populated based on the database vendor.</span></span> <span data-ttu-id="ce8cd-241">워터 마크 열은 사용되는 모든 테이블/보기에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-241">A watermark column must be present on every table/view used.</span></span> <span data-ttu-id="ce8cd-242">이 열은 테이블 및 종속(다중값 또는 하위) 테이블에 대한 삽입 및 업데이트를 추적해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-242">This column must track inserts and updates to the tables as and its dependent (multi-valued or child) tables.</span></span> <span data-ttu-id="ce8cd-243">동기화 서비스와 데이터베이스 서버 간에 시계는 동기화되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-243">The clocks between Synchronization Service and the database server must be synchronized.</span></span> <span data-ttu-id="ce8cd-244">그렇지 않은 경우 델타 가져오기의 일부 항목은 생략될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-244">If not, some entries in the delta import might be omitted.</span></span>  
  <span data-ttu-id="ce8cd-245">제한 사항:</span><span class="sxs-lookup"><span data-stu-id="ce8cd-245">Limitation:</span></span>
  * <span data-ttu-id="ce8cd-246">워터 마크 전략은 삭제된 개체를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-246">Watermark strategy does not support deleted objects.</span></span>
* <span data-ttu-id="ce8cd-247">**스냅숏**: (Microsoft SQL Server로만 작동) [스냅숏을 사용하여 델타 뷰 생성](https://technet.microsoft.com/library/cc720640.aspx)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-247">**Snapshot**: (Works only with Microsoft SQL Server) [Generating Delta Views Using Snapshots](https://technet.microsoft.com/library/cc720640.aspx)</span></span>
* <span data-ttu-id="ce8cd-248">**변경 내용 추적**: (Microsoft SQL Server로만 작동) [About 변경 내용 추적](https://msdn.microsoft.com/library/bb933875.aspx)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-248">**Change Tracking**: (Works only with Microsoft SQL Server) [About Change Tracking](https://msdn.microsoft.com/library/bb933875.aspx)</span></span>  
  <span data-ttu-id="ce8cd-249">제한 사항:</span><span class="sxs-lookup"><span data-stu-id="ce8cd-249">Limitations:</span></span>
  * <span data-ttu-id="ce8cd-250">앵커 및 DN 특성은 테이블에서 선택한 개체에 대한 기본 키의 일부여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-250">Anchor & DN attribute must be part of primary key for the selected object in the table.</span></span>
  * <span data-ttu-id="ce8cd-251">변경 내용 추적을 사용하여 가져오기 및 내보내기를 수행하는 동안 SQL 쿼리가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-251">SQL query is unsupported during Import and Export with Change Tracking.</span></span>

<span data-ttu-id="ce8cd-252">**추가 매개 변수**: 데이터베이스 서버가 있는 위치를 나타내는 데이터베이스 서버 표준 시간대를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-252">**Additional Parameters**: Specify the Database Server Time Zone indicating where your Database server is located.</span></span> <span data-ttu-id="ce8cd-253">이 값은 다양한 형식의 날짜 및 시간 특성을 지원하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-253">This value is used to support the various formats of date & time attributes.</span></span>

<span data-ttu-id="ce8cd-254">커넥터는 항상 날짜 및 날짜-시간을 UTC 형식으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-254">The Connector always stores date and date-time in UTC format.</span></span> <span data-ttu-id="ce8cd-255">날짜 및 시간을 올바르게 변환할 수 있으려면 데이터베이스 서버의 표준 시간대 및 형식을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-255">To be able to correctly convert the date and times, the time zone of the database server and the format used must be specified.</span></span> <span data-ttu-id="ce8cd-256">형식은 .Net 형식으로 표현되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-256">The format should be expressed in .Net format.</span></span>

<span data-ttu-id="ce8cd-257">내보내는 동안 모든 날짜 시간 특성은 커넥터에 UTC 시간 형식으로 제공되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-257">During export every date time attribute must be provided to the Connector in UTC time format.</span></span>

![globalparameters2](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters2.png)

<span data-ttu-id="ce8cd-259">**암호 구성**: 커넥터는 암호 동기화 기능을 제공하고 암호 설정 및 변경을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-259">**Password Configuration**: The connector provides password synchronization capabilities and supports set and change password.</span></span>

<span data-ttu-id="ce8cd-260">커넥터는 암호 동기화를 지원하는 다음과 같은 두 가지 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-260">The Connector provides two methods to support password synchronization:</span></span>

* <span data-ttu-id="ce8cd-261">**저장 프로시저**: 이 메서드는 암호 집합 및 변경을 지원하기 위해 두 개의 저장 프로시저가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-261">**Stored Procedure**: This method requires two stored procedures to support Set & Change password.</span></span> <span data-ttu-id="ce8cd-262">아래 예제처럼 **암호 SP 설정** 및 **암호 SP 변경** 매개 변수에서 각각 암호 작업을 추가하고 변경하려는 모든 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-262">Type all parameters for add and change the password operation in **Set Password SP** and **Change Password SP** Parameters respectively as per below example.</span></span>
  <span data-ttu-id="ce8cd-263">![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters3.png)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-263">![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters3.png)</span></span>
* <span data-ttu-id="ce8cd-264">**암호 확장**: 이 방법은 암호 확장 DLL이 필요합니다([IMAExtensible2Password](https://msdn.microsoft.com/library/microsoft.metadirectoryservices.imaextensible2password.aspx) 인터페이스를 구현하는 확장 DLL 이름을 제공해야 합니다.).</span><span class="sxs-lookup"><span data-stu-id="ce8cd-264">**Password Extension**: This method requires Password extension DLL (you need to provide the Extension DLL Name that is implementing the [IMAExtensible2Password](https://msdn.microsoft.com/library/microsoft.metadirectoryservices.imaextensible2password.aspx) interface).</span></span> <span data-ttu-id="ce8cd-265">암호 확장 어셈블리는 확장 폴더에 배치되어야 하므로 커넥터는 런타임 시 DLL을 로드할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-265">Password extension assembly must be placed in extension folder so that the connector can load the DLL at runtime.</span></span>
  <span data-ttu-id="ce8cd-266">![globalparameters4](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters4.png)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-266">![globalparameters4](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters4.png)</span></span>

<span data-ttu-id="ce8cd-267">또한 **구성 확장** 페이지에서 암호 관리를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-267">You also have to enable the Password Management on the **Configure Extension** page.</span></span>
<span data-ttu-id="ce8cd-268">![globalparameters5](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters5.png)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-268">![globalparameters5](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters5.png)</span></span>

### <a name="configure-partitions-and-hierarchies"></a><span data-ttu-id="ce8cd-269">파티션 및 계층 구성</span><span class="sxs-lookup"><span data-stu-id="ce8cd-269">Configure Partitions and Hierarchies</span></span>
<span data-ttu-id="ce8cd-270">파티션 및 계층 구조 페이지에서 모든 개체 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-270">On the partitions and hierarchies page, select all object types.</span></span> <span data-ttu-id="ce8cd-271">각 개체 형식은 고유한 파티션입니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-271">Each object type is its own partition.</span></span>

![partitions1](./media/active-directory-aadconnectsync-connector-genericsql/partitions1.png)

<span data-ttu-id="ce8cd-273">또한 **연결** 또는 **글로벌 매개 변수** 페이지에 정의된 값을 재정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-273">You can also override the values defined on the **Connectivity** or **Global Parameters** page.</span></span>

![partitions2](./media/active-directory-aadconnectsync-connector-genericsql/partitions2.png)

### <a name="configure-anchors"></a><span data-ttu-id="ce8cd-275">앵커 구성</span><span class="sxs-lookup"><span data-stu-id="ce8cd-275">Configure Anchors</span></span>
<span data-ttu-id="ce8cd-276">앵커가 이미 정의되어 있으므로 이 페이지는 읽기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-276">This page is read-only since the anchor has already been defined.</span></span> <span data-ttu-id="ce8cd-277">선택된 앵커 특성은 항상 개체 형식을 사용하여 추가되어 개체 형식에 걸쳐 고유하게 유지되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-277">The selected anchor attribute is always appended with the object type to ensure it remains unique across object types.</span></span>

![anchors](./media/active-directory-aadconnectsync-connector-genericsql/anchors.png)

## <a name="configure-run-step-parameter"></a><span data-ttu-id="ce8cd-279">실행 단계 매개 변수 구성</span><span class="sxs-lookup"><span data-stu-id="ce8cd-279">Configure Run Step Parameter</span></span>
<span data-ttu-id="ce8cd-280">이 단계는 커넥터의 실행 프로필에서 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-280">These steps are configured on the run profiles on the Connector.</span></span> <span data-ttu-id="ce8cd-281">이러한 구성은 데이터 가져오기 및 내보내기의 실제 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-281">These configurations do the actual work of importing and exporting data.</span></span>

### <a name="full-and-delta-import"></a><span data-ttu-id="ce8cd-282">전체 및 델타 가져오기</span><span class="sxs-lookup"><span data-stu-id="ce8cd-282">Full and Delta Import</span></span>
<span data-ttu-id="ce8cd-283">일반 SQL 커넥터는 다음의 메서드를 사용하여 전체 및 델타 가져오기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-283">Generic SQL Connector support Full and Delta Import using these methods:</span></span>

* <span data-ttu-id="ce8cd-284">테이블</span><span class="sxs-lookup"><span data-stu-id="ce8cd-284">Table</span></span>
* <span data-ttu-id="ce8cd-285">보기</span><span class="sxs-lookup"><span data-stu-id="ce8cd-285">View</span></span>
* <span data-ttu-id="ce8cd-286">저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="ce8cd-286">Stored Procedure</span></span>
* <span data-ttu-id="ce8cd-287">SQL 쿼리</span><span class="sxs-lookup"><span data-stu-id="ce8cd-287">SQL Query</span></span>

![runstep1](./media/active-directory-aadconnectsync-connector-genericsql/runstep1.png)

<span data-ttu-id="ce8cd-289">**테이블/뷰**</span><span class="sxs-lookup"><span data-stu-id="ce8cd-289">**Table/View**</span></span>  
<span data-ttu-id="ce8cd-290">개체에 대한 다중값 특성을 가져오려면 **다중값 테이블/뷰의 이름**에서 쉼표로 구분된 테이블/뷰 이름 및 상위 테이블을 통해 **조인 조건**에서 해당하는 조인 조건을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-290">To import multi-valued attributes for an object, you have to provide the comma-separated table/view name in **Name of Multi-Valued table/views** and respective join conditions in the **Join condition** with the parent table.</span></span>

<span data-ttu-id="ce8cd-291">예제: Employee 개체 및 해당하는 모든 다중값 특성을 가져오려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-291">Example: You want to import the Employee object and all its multi-valued attributes.</span></span> <span data-ttu-id="ce8cd-292">직원(주 테이블) 및 부서(다중값)라는 두 개의 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-292">There are two tables, named Employee (main table) and Department (multi-valued).</span></span>
<span data-ttu-id="ce8cd-293">다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-293">Do the following:</span></span>

* <span data-ttu-id="ce8cd-294">**테이블/뷰/SP**에서 **직원**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-294">Type **Employee** in **Table/View/SP**.</span></span>
* <span data-ttu-id="ce8cd-295">**다중값 테이블/뷰 이름**에서 부서를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-295">Type Department in **Name of Multi-Valued table/views**.</span></span>
* <span data-ttu-id="ce8cd-296">**조인 조건**의 직원과 부서 간에 조인 조건을 입력합니다. 예: `Employee.DEPTID=Department.DepartmentID`.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-296">Type the join condition between Employee & Department in **Join Condition**, for example `Employee.DEPTID=Department.DepartmentID`.</span></span>
  <span data-ttu-id="ce8cd-297">![runstep2](./media/active-directory-aadconnectsync-connector-genericsql/runstep2.png)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-297">![runstep2](./media/active-directory-aadconnectsync-connector-genericsql/runstep2.png)</span></span>

<span data-ttu-id="ce8cd-298">**저장 프로시저**</span><span class="sxs-lookup"><span data-stu-id="ce8cd-298">**Stored procedures**</span></span>  
<span data-ttu-id="ce8cd-299">![runstep3](./media/active-directory-aadconnectsync-connector-genericsql/runstep3.png)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-299">![runstep3](./media/active-directory-aadconnectsync-connector-genericsql/runstep3.png)</span></span>

* <span data-ttu-id="ce8cd-300">많은 양의 데이터가 있는 경우 저장 프로시저를 사용하여 페이지 매김을 구현하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-300">If you have much data, it is recommended to implement pagination with your Stored Procedures.</span></span>
* <span data-ttu-id="ce8cd-301">저장 프로시저의 경우 페이지 매김을 지원하려면 시작 인덱스 및 끝 인덱스를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-301">For your Stored Procedure to support pagination, you need to provide Start Index and End Index.</span></span> <span data-ttu-id="ce8cd-302">참고: [많은 양의 데이터를 효율적으로 페이징](https://msdn.microsoft.com/library/bb445504.aspx).</span><span class="sxs-lookup"><span data-stu-id="ce8cd-302">See: [Efficiently Paging Through Large Amounts of Data](https://msdn.microsoft.com/library/bb445504.aspx).</span></span>
* <span data-ttu-id="ce8cd-303">@StartIndex 및 @EndIndex은(는) 실행 시 **구성 단계** 페이지에 구성된 해당 페이지 크기 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-303">@StartIndex and @EndIndex are replaced at execution time with respective page size value configured on **Configure Step** page.</span></span> <span data-ttu-id="ce8cd-304">예를 들어, 커넥터가 첫 번째 페이지를 검색하고 페이지 크기가 500으로 설정된 경우 이러한 상황에서 @StartIndex은(는) 1 및 @EndIndex 500입니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-304">For example, when the connector retrieves first page and the page size is set 500, in such situation @StartIndex would be 1 and @EndIndex 500.</span></span> <span data-ttu-id="ce8cd-305">커넥터가 후속 페이지를 검색하고 @StartIndex 및 @EndIndex 값을 변경하는 경우 이러한 값은 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-305">These values increase when connector retrieves subsequent pages and change the @StartIndex & @EndIndex value.</span></span>
* <span data-ttu-id="ce8cd-306">매개 변수가 있는 저장 프로시저를 실행하려면 매개 변수를 `[Name]:[Direction]:[Value]` 형식으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-306">To execute parameterized Stored Procedure, provide the parameters in `[Name]:[Direction]:[Value]` format.</span></span> <span data-ttu-id="ce8cd-307">별도 줄에 각 매개 변수를 입력합니다.(Ctrl + Enter를 사용하여 새 줄 가져옴)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-307">Enter each parameter on a separate line (Use Ctrl + Enter to get a new line).</span></span>
* <span data-ttu-id="ce8cd-308">또한 일반 SQL 커넥터는 Microsoft SQL Server의 연결된 서버에서 가져오기 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-308">Generic SQL connector also supports Import operation from Linked Servers in Microsoft SQL Server.</span></span> <span data-ttu-id="ce8cd-309">정보가 연결된 서버의 테이블에서 검색되어야 하는 경우 테이블은 다음 형식으로 제공되어야 합니다. `[ServerName].[Database].[Schema].[TableName]`</span><span class="sxs-lookup"><span data-stu-id="ce8cd-309">If information should be retrieved from a Table in Linked server, then Table should be provided in the format: `[ServerName].[Database].[Schema].[TableName]`</span></span>
* <span data-ttu-id="ce8cd-310">일반 SQL 커넥터는 실행 단계 정보와 스키마 탐색 간에 구조가 비슷한(모두 별칭 이름 및 데이터 형식) 개체만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-310">Generic SQL Connector supports only those objects that have similar structure (both alias name and data type) between run steps information and schema detection.</span></span> <span data-ttu-id="ce8cd-311">실행된 단계에서 스키마 및 제공된 정보로 선택한 개체가 다른 경우 SQL 커넥터는 이러한 형식의 시나리오를 지원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-311">If the selected object from schema and provided information at run step is different, then SQL Connector is unable to support this type of scenarios.</span></span>

<span data-ttu-id="ce8cd-312">**SQL 쿼리**</span><span class="sxs-lookup"><span data-stu-id="ce8cd-312">**SQL Query**</span></span>  
<span data-ttu-id="ce8cd-313">![runstep4](./media/active-directory-aadconnectsync-connector-genericsql/runstep4.png)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-313">![runstep4](./media/active-directory-aadconnectsync-connector-genericsql/runstep4.png)</span></span>

![runstep5](./media/active-directory-aadconnectsync-connector-genericsql/runstep5.png)

* <span data-ttu-id="ce8cd-315">여러 결과 집합 쿼리는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-315">Multiple result sets queries not supported.</span></span>
* <span data-ttu-id="ce8cd-316">SQL 쿼리는 페이지 매김을 지원하고 시작 인덱스 및 끝 인덱스 변수를 제공하여 페이지 매김을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-316">SQL query supports the pagination and provide start Index and End Index as a variable to support pagination.</span></span>

### <a name="delta-import"></a><span data-ttu-id="ce8cd-317">델타 가져오기</span><span class="sxs-lookup"><span data-stu-id="ce8cd-317">Delta Import</span></span>
![runstep6](./media/active-directory-aadconnectsync-connector-genericsql/runstep6.png)

<span data-ttu-id="ce8cd-319">델타 가져오기 구성은 전체 가져오기에 비해 몇 가지 추가 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-319">Delta Import configuration requires some more configuration compared with Full Import.</span></span>

* <span data-ttu-id="ce8cd-320">트리거 또는 스냅숏 접근 방식을 선택하여 델타 변경 내용을 추적하는 경우 **기록 테이블 또는 스냅숏 데이터베이스 이름** 상자에서 기록 테이블 또는 스냅숏 데이터베이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-320">If you choose the Trigger or Snapshot approach to track delta changes, then provide History Table or Snapshot database in **History Table or Snapshot database name** box.</span></span>
* <span data-ttu-id="ce8cd-321">또한 기록 테이블과 상위 테이블 간의 조인 조건을 제공해야 합니다. 예:`Employee.ID=History.EmployeeID`</span><span class="sxs-lookup"><span data-stu-id="ce8cd-321">You also need to provide join condition between History table and Parent table, for example `Employee.ID=History.EmployeeID`</span></span>
* <span data-ttu-id="ce8cd-322">기록 테이블에서 상위 테이블의 트랜잭션을 추적하려면 작업 정보(추가/업데이트/삭제)를 포함하는 열 이름을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-322">To track the transaction on the parent table from the history table, you must provide the column name that contains the operation information (Add/Update/Delete).</span></span>
* <span data-ttu-id="ce8cd-323">워터 마크를 선택하여 델타 변경 내용을 추적하는 경우 **워터 마크 열 이름**에서 작업 정보를 포함하는 열 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-323">If you choose Watermark to track delta changes, then provide the column name that contains the operation information in **Water Mark Column Name**.</span></span>
* <span data-ttu-id="ce8cd-324">**형식 특성 변경** 열은 형식 변경에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-324">The **change Type attribute** column is required for the change type.</span></span> <span data-ttu-id="ce8cd-325">이 열은 기본 테이블 또는 다중값 테이블에서 발생하는 변경을 델타 뷰의 변경 형식에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-325">This column maps a change that occurs in the primary table or multi-value table to a change type in the delta view.</span></span> <span data-ttu-id="ce8cd-326">이 열은 특성 수준 변경에 대해 Modify_Attribute 변경 유형을 포함할 수 있거나 개체 수준 변경 형식에 대한 변경 형식을 추가, 수정 또는 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-326">This column can contain the Modify_Attribute change type for attribute-level change or an Add, Modify, or Delete change type for an object-level change type.</span></span> <span data-ttu-id="ce8cd-327">기본값 추가, 수정, 삭제 이외의 경우 사용자는 이 옵션을 사용하여 해당 값을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-327">If it is something other than the default value Add, Modify, or Delete, then you can define those values using this option.</span></span>

### <a name="export"></a><span data-ttu-id="ce8cd-328">내보내기</span><span class="sxs-lookup"><span data-stu-id="ce8cd-328">Export</span></span>
![runstep7](./media/active-directory-aadconnectsync-connector-genericsql/runstep7.png)

<span data-ttu-id="ce8cd-330">일반 SQL 커넥터는 다음과 같이 네 가지 지원된 방법을 사용하여 내보내기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-330">Generic SQL Connector support Export using four supported methods such as:</span></span>

* <span data-ttu-id="ce8cd-331">테이블</span><span class="sxs-lookup"><span data-stu-id="ce8cd-331">Table</span></span>
* <span data-ttu-id="ce8cd-332">보기</span><span class="sxs-lookup"><span data-stu-id="ce8cd-332">View</span></span>
* <span data-ttu-id="ce8cd-333">저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="ce8cd-333">Stored Procedure</span></span>
* <span data-ttu-id="ce8cd-334">SQL 쿼리</span><span class="sxs-lookup"><span data-stu-id="ce8cd-334">SQL Query</span></span>

<span data-ttu-id="ce8cd-335">**테이블/뷰**</span><span class="sxs-lookup"><span data-stu-id="ce8cd-335">**Table/View**</span></span>  
<span data-ttu-id="ce8cd-336">테이블/뷰 옵션을 선택한 경우 커넥터는 해당 쿼리를 생성하여 내보내기 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-336">If you choose the Table/View option, then the connector generates the respective queries to do the Export.</span></span>

<span data-ttu-id="ce8cd-337">**저장 프로시저**</span><span class="sxs-lookup"><span data-stu-id="ce8cd-337">**Stored procedures**</span></span>  
<span data-ttu-id="ce8cd-338">![runstep8](./media/active-directory-aadconnectsync-connector-genericsql/runstep8.png)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-338">![runstep8](./media/active-directory-aadconnectsync-connector-genericsql/runstep8.png)</span></span>

<span data-ttu-id="ce8cd-339">저장 프로시저 옵션을 선택한 경우 내보내기에는 삽입/업데이트/삭제 작업을 수행할 세 가지 다른 저장 프로시저가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-339">If you choose the Stored Procedure option, Export requires three different Stored procedures to perform Insert/Update/Delete operations.</span></span>

* <span data-ttu-id="ce8cd-340">**SP 이름 추가**: 개체가 해당 테이블에서 삽입하려는 커넥터에 제공되는 경우 이 SP가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-340">**Add SP Name**: This SP runs if any object comes to connector for insertion in the respective table.</span></span>
* <span data-ttu-id="ce8cd-341">**SP 이름 업데이트**: 개체가 해당 테이블에서 업데이트하려는 커넥터에 제공되는 경우 이 SP가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-341">**Update SP Name**: This SP runs if any object comes to connector for update in the respective table.</span></span>
* <span data-ttu-id="ce8cd-342">**SP 이름 삭제**: 개체가 해당 테이블에서 삭제하려는 커넥터에 제공되는 경우 이 SP가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-342">**Delete SP Name**: This SP runs if any object comes to connector for deletion in the respective table.</span></span>
* <span data-ttu-id="ce8cd-343">저장 프로시저에 매개 변수 값으로 사용되는 스키마에서 선택된 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-343">Attribute selected from the schema used as a parameter value to the stored procedure.</span></span> <span data-ttu-id="ce8cd-344">예를 들어, `EmployeeName: INPUT: @EmployeeName` (EmployeeName을 커넥터 스키마에서 선택하고 내보내기를 수행하는 동안 커넥터가 해당 값을 바꿉니다.)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-344">For example, `EmployeeName: INPUT: @EmployeeName` (EmployeeName is selected in the connector schema and the connector replaces the respective value while doing export)</span></span>
* <span data-ttu-id="ce8cd-345">매개 변수가 있는 저장 프로시저를 실행하려면 매개 변수를 `[Name]:[Direction]:[Value]` 형식으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-345">To run parameterized stored procedure, provide parameters in `[Name]:[Direction]:[Value]` format.</span></span> <span data-ttu-id="ce8cd-346">별도 줄에 각 매개 변수를 입력합니다.(Ctrl + Enter를 사용하여 새 줄 가져옴)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-346">Enter each parameter on a separate line (Use Ctrl + Enter to get a new line).</span></span>

<span data-ttu-id="ce8cd-347">**SQL query**</span><span class="sxs-lookup"><span data-stu-id="ce8cd-347">**SQL query**</span></span>  
<span data-ttu-id="ce8cd-348">![runstep9](./media/active-directory-aadconnectsync-connector-genericsql/runstep9.png)</span><span class="sxs-lookup"><span data-stu-id="ce8cd-348">![runstep9](./media/active-directory-aadconnectsync-connector-genericsql/runstep9.png)</span></span>

<span data-ttu-id="ce8cd-349">SQL 쿼리 옵션을 선택한 경우 내보내기에는 삽입/업데이트/삭제 작업을 수행할 세 가지 다른 쿼리가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-349">If you choose the SQL query option, Export requires three different queries to perform Insert/Update/Delete operations.</span></span>

* <span data-ttu-id="ce8cd-350">**쿼리 삽입**: 개체가 해당 테이블에서 삽입하려는 커넥터에 제공되는 경우 이 쿼리가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-350">**Insert Query**: This query runs if any object comes to connector for insertion in the respective table.</span></span>
* <span data-ttu-id="ce8cd-351">**쿼리 업데이트**: 개체가 해당 테이블에서 업데이트하려는 커넥터에 제공되는 경우 이 쿼리가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-351">**Update Query**: This query runs if any object comes to connector for update in the respective table.</span></span>
* <span data-ttu-id="ce8cd-352">**쿼리 삭제**: 개체가 해당 테이블에서 삭제하려는 커넥터에 제공되는 경우 이 쿼리가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-352">**Delete Query**: This query runs if any object comes to connector for deletion in the respective table.</span></span>
* <span data-ttu-id="ce8cd-353">쿼리에 매개 변수 값으로 사용되는 스키마에서 선택된 특성입니다. 예: `Insert into Employee (ID, Name) Values (@ID, @EmployeeName)`</span><span class="sxs-lookup"><span data-stu-id="ce8cd-353">Attribute selected from the schema used as a parameter value to the query, for example `Insert into Employee (ID, Name) Values (@ID, @EmployeeName)`</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ce8cd-354">문제 해결</span><span class="sxs-lookup"><span data-stu-id="ce8cd-354">Troubleshooting</span></span>
* <span data-ttu-id="ce8cd-355">커넥터의 문제를 해결하기 위해 로깅을 사용하는 방법에 대한 자세한 내용은 [커넥터에 ETW 추적을 사용하는 방법](http://go.microsoft.com/fwlink/?LinkId=335731)참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ce8cd-355">For information on how to enable logging to troubleshoot the connector, see the [How to Enable ETW Tracing for Connectors](http://go.microsoft.com/fwlink/?LinkId=335731).</span></span>
