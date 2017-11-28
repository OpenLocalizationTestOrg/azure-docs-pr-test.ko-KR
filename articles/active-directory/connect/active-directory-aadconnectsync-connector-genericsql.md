---
title: "aaaGeneric SQL 커넥터 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 tooconfigure Microsoft 일반 SQL 커넥터입니다."
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
ms.openlocfilehash: 2eab8f0894e83ab4738b9f2deb05b03cdc9a9d43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-technical-reference"></a><span data-ttu-id="5d434-103">일반 SQL 커넥터 기술 참조</span><span class="sxs-lookup"><span data-stu-id="5d434-103">Generic SQL Connector technical reference</span></span>
<span data-ttu-id="5d434-104">이 문서에서는 hello 제네릭 SQL 커넥터를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-104">This article describes hello Generic SQL Connector.</span></span> <span data-ttu-id="5d434-105">hello 문서 toohello 제품 다음이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-105">hello article applies toohello following products:</span></span>

* <span data-ttu-id="5d434-106">Microsoft Identity Manager 2016 (MIM2016)</span><span class="sxs-lookup"><span data-stu-id="5d434-106">Microsoft Identity Manager 2016 (MIM2016)</span></span>
* <span data-ttu-id="5d434-107">Forefront Identity Manager 2010 R2 (FIM2010R2)</span><span class="sxs-lookup"><span data-stu-id="5d434-107">Forefront Identity Manager 2010 R2 (FIM2010R2)</span></span>
  * <span data-ttu-id="5d434-108">핫픽스 4.1.3671.0 이상 [KB3092178](https://support.microsoft.com/kb/3092178)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-108">Must use hotfix 4.1.3671.0 or later [KB3092178](https://support.microsoft.com/kb/3092178).</span></span>

<span data-ttu-id="5d434-109">Hello 커넥터 MIM2016 및 FIM2010R2 hello에서 다운로드할 수는 [Microsoft 다운로드 센터](http://go.microsoft.com/fwlink/?LinkId=717495)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-109">For MIM2016 and FIM2010R2, hello Connector is available as a download from hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).</span></span>

<span data-ttu-id="5d434-110">toosee 작업에서이 커넥터 참조 hello [단계별 제네릭 SQL 커넥터](active-directory-aadconnectsync-connector-genericsql-step-by-step.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="5d434-110">toosee this Connector in action, see hello [Generic SQL Connector step-by-step](active-directory-aadconnectsync-connector-genericsql-step-by-step.md) article.</span></span>

## <a name="overview-of-hello-generic-sql-connector"></a><span data-ttu-id="5d434-111">Hello 제네릭 SQL 커넥터 개요</span><span class="sxs-lookup"><span data-stu-id="5d434-111">Overview of hello Generic SQL Connector</span></span>
<span data-ttu-id="5d434-112">일반 SQL 커넥터 hello는 ODBC 연결을 제공 하는 데이터베이스 시스템과 toointegrate hello 동기화 서비스를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-112">hello Generic SQL Connector enables you toointegrate hello synchronization service with a database system that offers ODBC connectivity.</span></span>  

<span data-ttu-id="5d434-113">상위 수준 측면에서 같은 기능 hello hello hello 커넥터의 현재 버전에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-113">From a high-level perspective, hello following features are supported by hello current release of hello connector:</span></span>

| <span data-ttu-id="5d434-114">기능</span><span class="sxs-lookup"><span data-stu-id="5d434-114">Feature</span></span> | <span data-ttu-id="5d434-115">지원</span><span class="sxs-lookup"><span data-stu-id="5d434-115">Support</span></span> |
| --- | --- |
| <span data-ttu-id="5d434-116">연결된 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="5d434-116">Connected data source</span></span> |<span data-ttu-id="5d434-117">hello 커넥터 모든 64 비트 ODBC 드라이버를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-117">hello Connector is supported with all 64-bit ODBC drivers.</span></span> <span data-ttu-id="5d434-118">Hello 다음으로 테스트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-118">It has been tested with hello following:</span></span> <li><span data-ttu-id="5d434-119">Microsoft SQL Server 및 SQL Azure</span><span class="sxs-lookup"><span data-stu-id="5d434-119">Microsoft SQL Server & SQL Azure</span></span></li><li><span data-ttu-id="5d434-120">IBM DB2 10.x</span><span class="sxs-lookup"><span data-stu-id="5d434-120">IBM DB2 10.x</span></span></li><li><span data-ttu-id="5d434-121">IBM DB2 9.x</span><span class="sxs-lookup"><span data-stu-id="5d434-121">IBM DB2 9.x</span></span></li><li><span data-ttu-id="5d434-122">Oracle 10 및 11g</span><span class="sxs-lookup"><span data-stu-id="5d434-122">Oracle 10 & 11g</span></span></li><li><span data-ttu-id="5d434-123">MySQL 5.x</span><span class="sxs-lookup"><span data-stu-id="5d434-123">MySQL 5.x</span></span></li> |
| <span data-ttu-id="5d434-124">시나리오</span><span class="sxs-lookup"><span data-stu-id="5d434-124">Scenarios</span></span> |<li><span data-ttu-id="5d434-125">개체 수명 주기 관리</span><span class="sxs-lookup"><span data-stu-id="5d434-125">Object Lifecycle Management</span></span></li><li><span data-ttu-id="5d434-126">암호 관리</span><span class="sxs-lookup"><span data-stu-id="5d434-126">Password Management</span></span></li> |
| <span data-ttu-id="5d434-127">작업</span><span class="sxs-lookup"><span data-stu-id="5d434-127">Operations</span></span> |<li><span data-ttu-id="5d434-128">전체 가져오기 및 델타 가져오기, 내보내기</span><span class="sxs-lookup"><span data-stu-id="5d434-128">Full Import and Delta Import, Export</span></span></li><li><span data-ttu-id="5d434-129">내보내기: 추가, 삭제, 업데이트 및 바꾸기</span><span class="sxs-lookup"><span data-stu-id="5d434-129">For Export: Add, Delete, Update, and Replace</span></span></li><li><span data-ttu-id="5d434-130">암호 설정, 암호 변경</span><span class="sxs-lookup"><span data-stu-id="5d434-130">Set Password, Change Password</span></span></li> |
| <span data-ttu-id="5d434-131">스키마</span><span class="sxs-lookup"><span data-stu-id="5d434-131">Schema</span></span> |<li><span data-ttu-id="5d434-132">개체 및 특성의 동적 검색</span><span class="sxs-lookup"><span data-stu-id="5d434-132">Dynamic discovery of objects and attributes</span></span></li> |

### <a name="prerequisites"></a><span data-ttu-id="5d434-133">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5d434-133">Prerequisites</span></span>
<span data-ttu-id="5d434-134">Hello 커넥터를 사용 하기 전에 hello 동기화 서버에 hello 다음 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-134">Before you use hello Connector, make sure you have hello following on hello synchronization server:</span></span>

* <span data-ttu-id="5d434-135">Microsoft.NET 4.5.2 Framework 이상</span><span class="sxs-lookup"><span data-stu-id="5d434-135">Microsoft .NET 4.5.2 Framework or later</span></span>
* <span data-ttu-id="5d434-136">64비트 ODBC 클라이언트 드라이버</span><span class="sxs-lookup"><span data-stu-id="5d434-136">64-bit ODBC client drivers</span></span>

### <a name="permissions-in-connected-data-source"></a><span data-ttu-id="5d434-137">연결된 데이터 원본의 사용 권한</span><span class="sxs-lookup"><span data-stu-id="5d434-137">Permissions in connected data source</span></span>
<span data-ttu-id="5d434-138">toocreate 또는 일반 SQL 커넥터에서 지원 되는 hello 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-138">toocreate or perform any of hello supported tasks in Generic SQL connector, you must have:</span></span>

* <span data-ttu-id="5d434-139">db_datareader</span><span class="sxs-lookup"><span data-stu-id="5d434-139">db_datareader</span></span>
* <span data-ttu-id="5d434-140">db_datawriter</span><span class="sxs-lookup"><span data-stu-id="5d434-140">db_datawriter</span></span>

### <a name="ports-and-protocols"></a><span data-ttu-id="5d434-141">포트 및 프로토콜</span><span class="sxs-lookup"><span data-stu-id="5d434-141">Ports and protocols</span></span>
<span data-ttu-id="5d434-142">ODBC 드라이버 toowork hello에 필요한 hello 포트, hello 데이터베이스 공급 업체의 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5d434-142">For hello ports required for hello ODBC driver toowork, consult hello database vendor's documentation.</span></span>

## <a name="create-a-new-connector"></a><span data-ttu-id="5d434-143">새 커넥터 만들기</span><span class="sxs-lookup"><span data-stu-id="5d434-143">Create a new Connector</span></span>
<span data-ttu-id="5d434-144">일반 SQL 커넥터 tooCreate에 **동기화 서비스** 선택 **관리 에이전트** 및 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-144">tooCreate a Generic SQL connector, in **Synchronization Service** select **Management Agent** and **Create**.</span></span> <span data-ttu-id="5d434-145">선택 hello **일반 SQL (Microsoft)** 커넥터입니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-145">Select hello **Generic SQL (Microsoft)** Connector.</span></span>

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/createconnector.png)

### <a name="connectivity"></a><span data-ttu-id="5d434-147">연결</span><span class="sxs-lookup"><span data-stu-id="5d434-147">Connectivity</span></span>
<span data-ttu-id="5d434-148">hello 커넥터 연결에 대 한 ODBC DSN 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-148">hello Connector uses an ODBC DSN file for connectivity.</span></span> <span data-ttu-id="5d434-149">사용 하 여 hello DSN 파일 만들기 **ODBC 데이터 원본** hello 시작 메뉴에서 찾을 **관리 도구**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-149">Create hello DSN file using **ODBC Data Sources** found in hello start menu under **Administrative Tools**.</span></span> <span data-ttu-id="5d434-150">만들 hello 관리 도구에는 **파일 DSN** toohello 커넥터 제공할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-150">In hello administrative tool, create a **File DSN** so it can be provided toohello Connector.</span></span>

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/connectivity.png)

<span data-ttu-id="5d434-152">hello 연결 화면은 hello 먼저 새 제네릭 SQL 커넥터를 만들 때입니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-152">hello Connectivity screen is hello first when you create a new Generic SQL Connector.</span></span> <span data-ttu-id="5d434-153">먼저 다음 정보는 tooprovide hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-153">You first need tooprovide hello following information:</span></span>

* <span data-ttu-id="5d434-154">DSN 파일 경로</span><span class="sxs-lookup"><span data-stu-id="5d434-154">DSN file path</span></span>
* <span data-ttu-id="5d434-155">인증</span><span class="sxs-lookup"><span data-stu-id="5d434-155">Authentication</span></span>
  * <span data-ttu-id="5d434-156">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="5d434-156">User Name</span></span>
  * <span data-ttu-id="5d434-157">암호</span><span class="sxs-lookup"><span data-stu-id="5d434-157">Password</span></span>

<span data-ttu-id="5d434-158">hello 데이터베이스는 다음 인증 방법 중 하나를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-158">hello database should support one of these authentication methods:</span></span>

* <span data-ttu-id="5d434-159">**Windows 인증**: 데이터베이스를 인증 하는 hello hello Windows 자격 증명 tooverify hello 사용자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-159">**Windows authentication**: hello authenticating database uses hello Windows credentials tooverify hello user.</span></span> <span data-ttu-id="5d434-160">지정 된 hello 사용자 이름과 암호는 hello 데이터베이스와 함께 사용 되는 tooauthenticate 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-160">hello user name/password specified is used tooauthenticate with hello database.</span></span> <span data-ttu-id="5d434-161">이 계정 사용 권한을 toohello 데이터베이스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-161">This account needs permissions toohello database.</span></span>
* <span data-ttu-id="5d434-162">**SQL 인증**: hello 데이터베이스 사용 하 여 hello 사용자 이름/암호 인증 한 hello 연결 화면 tooconnect toohello 데이터베이스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-162">**SQL authentication**: hello authenticating database uses hello user name/password defined one hello Connectivity screen tooconnect toohello database.</span></span> <span data-ttu-id="5d434-163">Hello DSN 파일에서 hello 사용자 이름/암호를 저장 하는 경우 hello 자격 증명 hello 연결 화면에 제공 된 우선 순위를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-163">If you store hello user name/pasword in hello DSN file, hello credentials provided on hello Connectivity screen have precedence.</span></span>
* <span data-ttu-id="5d434-164">**Azure SQL 데이터베이스 인증**: 자세한 내용은 참조 [연결할 데이터베이스를 사용 하 여 Azure Active Directory 인증 여 tooSQL](../../sql-database/sql-database-aad-authentication.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-164">**Azure SQL Database authentication**: For more information, see [Connect tooSQL Database By Using Azure Active Directory Authentication](../../sql-database/sql-database-aad-authentication.md).</span></span>

<span data-ttu-id="5d434-165">**DN이 앵커**:이 옵션을 선택 하는 경우 hello DN hello 앵커 특성으로도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-165">**DN is Anchor**: If you select this option, hello DN is also used as hello anchor attribute.</span></span> <span data-ttu-id="5d434-166">이 간단한 구현에 사용할 수 있습니다 하지만 제한 다음 hello에:</span><span class="sxs-lookup"><span data-stu-id="5d434-166">It can be used for a simple implementation but also has hello following limitation:</span></span>

* <span data-ttu-id="5d434-167">커넥터는 하나의 개체 유형만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-167">Connector supports only one object type.</span></span> <span data-ttu-id="5d434-168">따라서 특성 참조만 할 수 있는 참조 hello 동일한 개체 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-168">Therefore any reference attributes can only reference hello same object type.</span></span>

<span data-ttu-id="5d434-169">**내보내기 형식: Replace 개체**: 내보내기 작업 중 일부 특성에만 변경 될 때 모든 특성을 가진 hello 전체 개체를 내보내고 대체 hello 기존 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-169">**Export Type: Object Replace**: During export, when only some attributes have changed, hello entire object with all attributes is exported and replaces hello existing object.</span></span>

### <a name="schema-1-detect-object-types"></a><span data-ttu-id="5d434-170">스키마1(개체 형식 검색)</span><span class="sxs-lookup"><span data-stu-id="5d434-170">Schema 1 (Detect object types)</span></span>
<span data-ttu-id="5d434-171">이 페이지에서는 tooconfigure 하려는 방법을 hello 커넥터는 hello 데이터베이스에서 진행 중인 toofind hello 다른 개체 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-171">On this page, you are going tooconfigure how hello Connector is going toofind hello different object types in hello database.</span></span>

<span data-ttu-id="5d434-172">모든 개체 형식은 파티션으로 표시되며 **파티션 및 계층 구성**에서 자세히 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-172">Every object type is presented as a partition and configured further on **Configure Partitions and Hierarchies**.</span></span>

![schema1a](./media/active-directory-aadconnectsync-connector-genericsql/schema1a.png)

<span data-ttu-id="5d434-174">**개체 유형 검색 방법**: hello 커넥터 이러한 개체 유형 검색 방법을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-174">**Object Type detection method**: hello Connector supports these object type detection methods.</span></span>

* <span data-ttu-id="5d434-175">**고정 값**: hello 쉼표로 구분 된 목록 사용 하 여 개체 유형 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-175">**Fixed Value**: You provide hello list of object types with a comma-separated list.</span></span> <span data-ttu-id="5d434-176">예: `User,Group,Department`</span><span class="sxs-lookup"><span data-stu-id="5d434-176">For example: `User,Group,Department`.</span></span>  
  <span data-ttu-id="5d434-177">![schema1b](./media/active-directory-aadconnectsync-connector-genericsql/schema1b.png)</span><span class="sxs-lookup"><span data-stu-id="5d434-177">![schema1b](./media/active-directory-aadconnectsync-connector-genericsql/schema1b.png)</span></span>
* <span data-ttu-id="5d434-178">**테이블/뷰/저장 프로시저**: hello hello 테이블/뷰/저장 프로시저의 이름과 다음 hello 개체 유형 목록을 제공 하는 hello 열 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-178">**Table/View/Stored Procedure**: Provide hello name of hello table/view/stored procedure and then hello column name that provides hello list of object types.</span></span> <span data-ttu-id="5d434-179">저장된 프로시저를 사용 하는 경우 다음도 매개 변수를 제공에 대 한 hello 형태로 표시 **[이름]: [방향]: [Value]**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-179">If you use a stored procedure, then also provide parameters for it in hello format **[Name]:[Direction]:[Value]**.</span></span> <span data-ttu-id="5d434-180">별도 줄 (사용 하 여 Ctrl + Enter tooget 새 줄에) 각 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-180">Provide each parameter on a separate line (use Ctrl+Enter tooget a new line).</span></span>  
  <span data-ttu-id="5d434-181">![schema1c](./media/active-directory-aadconnectsync-connector-genericsql/schema1c.png)</span><span class="sxs-lookup"><span data-stu-id="5d434-181">![schema1c](./media/active-directory-aadconnectsync-connector-genericsql/schema1c.png)</span></span>
* <span data-ttu-id="5d434-182">**SQL 쿼리**:이 옵션을 사용 예를 들어 개체 유형의 단일 열을 반환 하는 SQL 쿼리 tooprovide 있습니다 `SELECT [Column Name] FROM TABLENAME`합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-182">**SQL Query**: This option allows you tooprovide a SQL query that returns a single column with object types, for example `SELECT [Column Name] FROM TABLENAME`.</span></span> <span data-ttu-id="5d434-183">hello 반환 문자열 (varchar) 형식의 열 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-183">hello returned column must be of type string (varchar).</span></span>

### <a name="schema-2-detect-attribute-types"></a><span data-ttu-id="5d434-184">스키마2(특성 형식 검색)</span><span class="sxs-lookup"><span data-stu-id="5d434-184">Schema 2 (Detect attribute types)</span></span>
<span data-ttu-id="5d434-185">이 페이지에서는 보아야 tooconfigure 특성 이름을 어떻게 hello 및 형식 toobe 감지 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-185">On this page, you are going tooconfigure how hello attribute names and types are going toobe detected.</span></span> <span data-ttu-id="5d434-186">hello 이전 페이지에서 검색 된 모든 개체 유형에 대해 hello 구성 옵션 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-186">hello configuration options are listed for every object type detected on hello previous page.</span></span>

![schema2a](./media/active-directory-aadconnectsync-connector-genericsql/schema2a.png)

<span data-ttu-id="5d434-188">**특성 유형 검색 방법**: hello 커넥터 스키마 1 화면에서 검색 된 개체 형식별으로 이러한 특성 유형 검색 메서드를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-188">**Attribute Type detection method**: hello Connector supports these attribute type detection methods with every detected object type in Schema 1 screen.</span></span>

* <span data-ttu-id="5d434-189">**테이블/뷰/저장 프로시저**: 사용된 toofind hello 특성 이름 이어야 하는 hello 테이블/뷰/저장 프로시저의 hello 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-189">**Table/View/Stored Procedure**: Provide hello name of hello table/view/stored procedure that should be used toofind hello attribute names.</span></span> <span data-ttu-id="5d434-190">저장된 프로시저를 사용 하는 경우 다음도 매개 변수를 제공에 대 한 hello 형태로 표시 **[이름]: [방향]: [Value]**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-190">If you use a stored procedure, then also provide parameters for it in hello format **[Name]:[Direction]:[Value]**.</span></span> <span data-ttu-id="5d434-191">별도 줄 (사용 하 여 Ctrl + Enter tooget 새 줄에) 각 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-191">Provide each parameter on a separate line (use Ctrl+Enter tooget a new line).</span></span> <span data-ttu-id="5d434-192">다중 값된 특성에 toodetect hello 특성 이름은 쉼표로 구분 된 목록이 테이블 또는 뷰를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-192">toodetect hello attribute names in a multi-valued attribute, provide a comma-separated list of Tables or Views.</span></span> <span data-ttu-id="5d434-193">부모 및 자식 테이블에 동일한 열 이름이 있는 경우 다중값 시나리오가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-193">Multivalued scenarios are not supported when parent and child table have same column names.</span></span>
* <span data-ttu-id="5d434-194">**SQL 쿼리**:이 옵션을 사용 예를 들어 특성 이름 가진 단일 열을 반환 하는 SQL 쿼리 tooprovide 있습니다 `SELECT [Column Name] FROM TABLENAME`합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-194">**SQL query**: This option allows you tooprovide a SQL query that returns a single column with attribute names, for example `SELECT [Column Name] FROM TABLENAME`.</span></span> <span data-ttu-id="5d434-195">hello 반환 문자열 (varchar) 형식의 열 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-195">hello returned column must be of type string (varchar).</span></span>

### <a name="schema-3-define-anchor-and-dn"></a><span data-ttu-id="5d434-196">스키마3(앵커 및 DN 정의)</span><span class="sxs-lookup"><span data-stu-id="5d434-196">Schema 3 (Define anchor and DN)</span></span>
<span data-ttu-id="5d434-197">이 페이지에 각 검색 된 개체 유형에 대해 tooconfigure 앵커 및 DN 특성 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-197">This page allows you tooconfigure anchor and DN attribute for each detected object type.</span></span> <span data-ttu-id="5d434-198">여러 특성 hello 앵커 toomake 템플릿 고유한 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-198">You can select multiple attributes toomake hello anchor unique.</span></span>

![schema3a](./media/active-directory-aadconnectsync-connector-genericsql/schema3a.png)

* <span data-ttu-id="5d434-200">다중값 및 부울 특성은 나열되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-200">Multi-valued and Boolean attributes are not listed.</span></span>
* <span data-ttu-id="5d434-201">하지 않는 한 앵커 및 DN 특성과 동일한 특성을 사용할 수 없습니다 **DN이 앵커** hello 연결 페이지에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-201">Same attribute cannot use for DN and anchor, unless **DN is Anchor** is selected on hello Connectivity page.</span></span>
* <span data-ttu-id="5d434-202">경우 **DN이 앵커** 선택 hello 연결 페이지에서이 페이지는 유일한 hello DN 특성 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-202">If **DN is Anchor** is selected on hello Connectivity page, this page requires only hello DN attribute.</span></span> <span data-ttu-id="5d434-203">이 특성은 hello 앵커 특성으로도 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-203">This attribute would also be used as hello anchor attribute.</span></span>

  ![schema3b](./media/active-directory-aadconnectsync-connector-genericsql/schema3b.png)

### <a name="schema-4-define-attribute-type-reference-and-direction"></a><span data-ttu-id="5d434-205">스키마4(특성 형식, 참조 및 방향 정의)</span><span class="sxs-lookup"><span data-stu-id="5d434-205">Schema 4 (Define attribute type, reference, and direction)</span></span>
<span data-ttu-id="5d434-206">이 페이지에서는 정수, 이진 또는 부울, 및 각 특성에 대 한 방향을 같은 tooconfigure hello 특성 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-206">This page allows you tooconfigure hello attribute type, such as integer, binary, or Boolean, and direction for each attribute.</span></span> <span data-ttu-id="5d434-207">**스키마2** 페이지에서 모든 특성은 다중값 특성을 포함하여 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-207">All attributes from page **schema 2** are listed including multi-valued attributes.</span></span>

![schema4a](./media/active-directory-aadconnectsync-connector-genericsql/schema4a.png)

* <span data-ttu-id="5d434-209">**데이터 형식**: toomap hello 특성 유형 toothose 형식은 hello 동기화 엔진에 알려진를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-209">**DataType**: Used toomap hello attribute type toothose types known by hello sync engine.</span></span> <span data-ttu-id="5d434-210">hello 기본 toouse hello hello SQL 스키마에서 검색 하는 대로 동일한 형식 이지만 날짜/시간 및 참조는 쉽게 감지 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-210">hello default is toouse hello same type as detected in hello SQL schema, but DateTime and Reference are not easily detectable.</span></span> <span data-ttu-id="5d434-211">Toospecify, 해야 **DateTime** 또는 **참조**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-211">For those, you need toospecify **DateTime** or **Reference**.</span></span>
* <span data-ttu-id="5d434-212">**방향**: hello 특성 방향 tooImport, 내보내기, 또는 ImportExport 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-212">**Direction**: You can set hello attribute direction tooImport, Export, or ImportExport.</span></span> <span data-ttu-id="5d434-213">ImportExport는 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-213">ImportExport is default.</span></span>

![schema4b](./media/active-directory-aadconnectsync-connector-genericsql/schema4b.png)

<span data-ttu-id="5d434-215">참고:</span><span class="sxs-lookup"><span data-stu-id="5d434-215">Notes:</span></span>

* <span data-ttu-id="5d434-216">특성 유형을 hello 커넥터에서 검색 되지 않는, hello 문자열 데이터 형식이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-216">If an attribute type is not detectable by hello Connector, it uses hello String data type.</span></span>
* <span data-ttu-id="5d434-217">**중첩 테이블** 은 열이 하나인 데이터베이스 테이블을 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-217">**Nested tables** can be considered one-column database tables.</span></span> <span data-ttu-id="5d434-218">Oracle는 임의의 순서로 중첩된 테이블의 hello 행을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-218">Oracle stores hello rows of a nested table in no particular order.</span></span> <span data-ttu-id="5d434-219">그러나 PL/SQL 변수로 hello 중첩된 테이블을 검색 하는 경우 hello 행 1부터 시작 하는 연속 아래 첨자 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-219">However, when you retrieve hello nested table into a PL/SQL variable, hello rows are given consecutive subscripts starting at 1.</span></span> <span data-ttu-id="5d434-220">배열 유사 액세스 tooindividual 행을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-220">That gives you array-like access tooindividual rows.</span></span>
* <span data-ttu-id="5d434-221">**VARRYS** hello 커넥터에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-221">**VARRYS** are not supported in hello connector.</span></span>

### <a name="schema-5-define-partition-for-reference-attributes"></a><span data-ttu-id="5d434-222">스키마5(참조 특성에 대한 파티션 정의)</span><span class="sxs-lookup"><span data-stu-id="5d434-222">Schema 5 (Define partition for reference attributes)</span></span>
<span data-ttu-id="5d434-223">이 페이지에서는 모든 참조 특성에 대해 특성이 참조하는 파티션(개체 형식)을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-223">On this page, you configure for all reference attributes which partition (object type) an attribute is referring to.</span></span>

![schema5](./media/active-directory-aadconnectsync-connector-genericsql/schema5.png)

<span data-ttu-id="5d434-225">사용 하는 경우 **DN이 앵커**, hello 하나에서 참조 하 고 동일한 개체 유형 hello를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-225">If you use **DN is anchor**, then you must use hello same object type as hello one you are referring from.</span></span> <span data-ttu-id="5d434-226">다른 개체 형식을 참조할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-226">You cannot reference another object type.</span></span>

>[!NOTE]
<span data-ttu-id="5d434-227">에 대 한 옵션은 이제 hello 2017 년 3 월 업데이트 부터는 "*"이이 옵션을 선택한 다음 모든 가능한 멤버 유형은 가져오게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-227">Starting in hello March 2017 update there is now an option for "*" When this option is chosen then all possible member types will be imported.</span></span>

![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/any-option.png)

>[!IMPORTANT]
 <span data-ttu-id="5d434-229">2017 년 5 월을 기준으로 hello "*" 즉, **옵션** 변경한 toosupport 가져오거나 내보내고 흐름.</span><span class="sxs-lookup"><span data-stu-id="5d434-229">As of May 2017 hello “*” aka **any option** has been changed toosupport import and export flow.</span></span> <span data-ttu-id="5d434-230">Toouse이이 옵션을 사용할 경우 다중 값된 테이블/뷰 hello 개체 유형을 포함 하는 특성이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-230">If you want toouse this option your multi-valued table/view should have an attribute that contains hello object type.</span></span>

![](./media/active-directory-aadconnectsync-connector-genericsql/any-02.png)

 </br> <span data-ttu-id="5d434-231">경우 "*" hello 개체 형식과 hello 열의 hello 이름을 지정 해야 하는 다음을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-231">If "*" is selected then hello name of hello column with hello object type must also be specified.</span></span></br> ![](./media/active-directory-aadconnectsync-connector-genericsql/any-03.png)

<span data-ttu-id="5d434-232">가져온 후 다음, 다음과 유사한 toohello 이미지를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-232">After import you will see something similar toohello image below:</span></span>

  ![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/after-import.png)



### <a name="global-parameters"></a><span data-ttu-id="5d434-234">글로벌 매개 변수</span><span class="sxs-lookup"><span data-stu-id="5d434-234">Global Parameters</span></span>
<span data-ttu-id="5d434-235">hello 글로벌 매개 변수 페이지를 사용 하는 tooconfigure 델타 가져오기 암호 방법과 날짜/시간 형식.</span><span class="sxs-lookup"><span data-stu-id="5d434-235">hello Global Parameters page is used tooconfigure Delta Import, Date/Time format, and Password method.</span></span>

![globalparameters1](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters1.png)



<span data-ttu-id="5d434-237">일반 SQL 커넥터 hello hello 델타 가져오기에 대 한 메서드를 다음을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-237">hello Generic SQL Connector supports hello following methods for Delta Import:</span></span>

* <span data-ttu-id="5d434-238">**트리거**: [트리거를 사용하여 델타 뷰 생성](https://technet.microsoft.com/library/cc708665.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d434-238">**Trigger**: See [Generating Delta Views Using Triggers](https://technet.microsoft.com/library/cc708665.aspx).</span></span>
* <span data-ttu-id="5d434-239">**워터 마크**: 모든 데이터베이스에 사용할 수 있는 일반적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-239">**Watermark**: A generic approach that can be used with any database.</span></span> <span data-ttu-id="5d434-240">미리 hello 데이터베이스 공급 업체에 따라 hello 워터 마크 쿼리가 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-240">hello watermark query is pre-populated based on hello database vendor.</span></span> <span data-ttu-id="5d434-241">워터 마크 열은 사용되는 모든 테이블/보기에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-241">A watermark column must be present on every table/view used.</span></span> <span data-ttu-id="5d434-242">이 열으로 삽입 및 업데이트 toohello 테이블 및 해당 종속 추적 해야 합니다 (다중 값 또는 하위) 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-242">This column must track inserts and updates toohello tables as and its dependent (multi-valued or child) tables.</span></span> <span data-ttu-id="5d434-243">hello 시계 동기화 서비스와 hello 데이터베이스 서버 간 동기화 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-243">hello clocks between Synchronization Service and hello database server must be synchronized.</span></span> <span data-ttu-id="5d434-244">그렇지 않은 경우 hello 델타 가져오기에 일부 항목을 생략 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-244">If not, some entries in hello delta import might be omitted.</span></span>  
  <span data-ttu-id="5d434-245">제한 사항:</span><span class="sxs-lookup"><span data-stu-id="5d434-245">Limitation:</span></span>
  * <span data-ttu-id="5d434-246">워터 마크 전략은 삭제된 개체를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-246">Watermark strategy does not support deleted objects.</span></span>
* <span data-ttu-id="5d434-247">**스냅숏**: (Microsoft SQL Server로만 작동) [스냅숏을 사용하여 델타 뷰 생성](https://technet.microsoft.com/library/cc720640.aspx)</span><span class="sxs-lookup"><span data-stu-id="5d434-247">**Snapshot**: (Works only with Microsoft SQL Server) [Generating Delta Views Using Snapshots](https://technet.microsoft.com/library/cc720640.aspx)</span></span>
* <span data-ttu-id="5d434-248">**변경 내용 추적**: (Microsoft SQL Server로만 작동) [About 변경 내용 추적](https://msdn.microsoft.com/library/bb933875.aspx)</span><span class="sxs-lookup"><span data-stu-id="5d434-248">**Change Tracking**: (Works only with Microsoft SQL Server) [About Change Tracking](https://msdn.microsoft.com/library/bb933875.aspx)</span></span>  
  <span data-ttu-id="5d434-249">제한 사항:</span><span class="sxs-lookup"><span data-stu-id="5d434-249">Limitations:</span></span>
  * <span data-ttu-id="5d434-250">앵커 및 DN 특성 hello hello 테이블에서 선택한 개체에 대 한 기본 키의 일부 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-250">Anchor & DN attribute must be part of primary key for hello selected object in hello table.</span></span>
  * <span data-ttu-id="5d434-251">변경 내용 추적을 사용하여 가져오기 및 내보내기를 수행하는 동안 SQL 쿼리가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-251">SQL query is unsupported during Import and Export with Change Tracking.</span></span>

<span data-ttu-id="5d434-252">**추가 매개 변수**: hello 데이터베이스 서버에 있는 위치를 나타내는 데이터베이스 서버 표준 시간대를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-252">**Additional Parameters**: Specify hello Database Server Time Zone indicating where your Database server is located.</span></span> <span data-ttu-id="5d434-253">이 값은 사용 toosupport hello 날짜 및 시간 특성의 다양 한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-253">This value is used toosupport hello various formats of date & time attributes.</span></span>

<span data-ttu-id="5d434-254">hello 커넥터 UTC 형식으로 날짜와 날짜 및 시간을 항상 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-254">hello Connector always stores date and date-time in UTC format.</span></span> <span data-ttu-id="5d434-255">hello 날짜 및 시간 toobe 수 toocorrectly 변환할 hello 데이터베이스 서버 및 사용 하는 hello 형식을 hello 표준 시간대를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-255">toobe able toocorrectly convert hello date and times, hello time zone of hello database server and hello format used must be specified.</span></span> <span data-ttu-id="5d434-256">hello 형식.Net 형식을 표현 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-256">hello format should be expressed in .Net format.</span></span>

<span data-ttu-id="5d434-257">내보내기 중 모든 날짜 시간 특성 toohello 커넥터 UTC 시간 형식으로 제공 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-257">During export every date time attribute must be provided toohello Connector in UTC time format.</span></span>

![globalparameters2](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters2.png)

<span data-ttu-id="5d434-259">**암호 구성**: 암호 동기화 기능을 제공 하는 hello 커넥터 및 지원 설정 하 고 암호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-259">**Password Configuration**: hello connector provides password synchronization capabilities and supports set and change password.</span></span>

<span data-ttu-id="5d434-260">hello 커넥터 toosupport 암호 동기화를 두 가지 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-260">hello Connector provides two methods toosupport password synchronization:</span></span>

* <span data-ttu-id="5d434-261">**저장 프로시저**:이 방법은 두 개의 저장된 프로시저 toosupport 집합 및 암호를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-261">**Stored Procedure**: This method requires two stored procedures toosupport Set & Change password.</span></span> <span data-ttu-id="5d434-262">추가 대 한 모든 매개 변수를 입력 하 고 hello 암호 작업에서 변경 **암호 SP 설정** 및 **암호 SP 변경** 아래 예제에서는 각각 기준으로 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-262">Type all parameters for add and change hello password operation in **Set Password SP** and **Change Password SP** Parameters respectively as per below example.</span></span>
  <span data-ttu-id="5d434-263">![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters3.png)</span><span class="sxs-lookup"><span data-stu-id="5d434-263">![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters3.png)</span></span>
* <span data-ttu-id="5d434-264">**암호 확장**:이 메서드를 사용 하려면 암호 확장 DLL (tooprovide hello hello를 구현 하는 확장 DLL 이름 필요한 [IMAExtensible2Password](https://msdn.microsoft.com/library/microsoft.metadirectoryservices.imaextensible2password.aspx) 인터페이스).</span><span class="sxs-lookup"><span data-stu-id="5d434-264">**Password Extension**: This method requires Password extension DLL (you need tooprovide hello Extension DLL Name that is implementing hello [IMAExtensible2Password](https://msdn.microsoft.com/library/microsoft.metadirectoryservices.imaextensible2password.aspx) interface).</span></span> <span data-ttu-id="5d434-265">암호 확장 어셈블리 hello 커넥터 런타임 시 hello DLL을 로드할 수 있도록 확장 폴더에 배치 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-265">Password extension assembly must be placed in extension folder so that hello connector can load hello DLL at runtime.</span></span>
  <span data-ttu-id="5d434-266">![globalparameters4](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters4.png)</span><span class="sxs-lookup"><span data-stu-id="5d434-266">![globalparameters4](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters4.png)</span></span>

<span data-ttu-id="5d434-267">Hello에 대 한 암호 관리 tooenable hello 있습니다 **확장 구성** 페이지.</span><span class="sxs-lookup"><span data-stu-id="5d434-267">You also have tooenable hello Password Management on hello **Configure Extension** page.</span></span>
<span data-ttu-id="5d434-268">![globalparameters5](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters5.png)</span><span class="sxs-lookup"><span data-stu-id="5d434-268">![globalparameters5](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters5.png)</span></span>

### <a name="configure-partitions-and-hierarchies"></a><span data-ttu-id="5d434-269">파티션 및 계층 구조 구성</span><span class="sxs-lookup"><span data-stu-id="5d434-269">Configure Partitions and Hierarchies</span></span>
<span data-ttu-id="5d434-270">Hello 파티션 및 계층 구조 페이지에서 모든 개체 유형을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-270">On hello partitions and hierarchies page, select all object types.</span></span> <span data-ttu-id="5d434-271">각 개체 형식은 고유한 파티션입니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-271">Each object type is its own partition.</span></span>

![partitions1](./media/active-directory-aadconnectsync-connector-genericsql/partitions1.png)

<span data-ttu-id="5d434-273">Hello에 정의 된 hello 값을 재정의할 수도 있습니다 **연결** 또는 **글로벌 매개 변수** 페이지.</span><span class="sxs-lookup"><span data-stu-id="5d434-273">You can also override hello values defined on hello **Connectivity** or **Global Parameters** page.</span></span>

![partitions2](./media/active-directory-aadconnectsync-connector-genericsql/partitions2.png)

### <a name="configure-anchors"></a><span data-ttu-id="5d434-275">앵커 구성</span><span class="sxs-lookup"><span data-stu-id="5d434-275">Configure Anchors</span></span>
<span data-ttu-id="5d434-276">이 페이지는 hello 앵커 이미 정의 되어 있으므로 읽기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-276">This page is read-only since hello anchor has already been defined.</span></span> <span data-ttu-id="5d434-277">hello 선택한 앵커 특성은 항상 추가 hello 개체 유형 tooensure와 것에서으로 유지 고유 개체 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-277">hello selected anchor attribute is always appended with hello object type tooensure it remains unique across object types.</span></span>

![anchors](./media/active-directory-aadconnectsync-connector-genericsql/anchors.png)

## <a name="configure-run-step-parameter"></a><span data-ttu-id="5d434-279">실행 단계 매개 변수 구성</span><span class="sxs-lookup"><span data-stu-id="5d434-279">Configure Run Step Parameter</span></span>
<span data-ttu-id="5d434-280">이러한 단계는 hello hello 커넥터에서 실행 프로필에서 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-280">These steps are configured on hello run profiles on hello Connector.</span></span> <span data-ttu-id="5d434-281">이러한 구성 데이터 가져오기 및 내보내기의 실제 작업을 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-281">These configurations do hello actual work of importing and exporting data.</span></span>

### <a name="full-and-delta-import"></a><span data-ttu-id="5d434-282">전체 및 델타 가져오기</span><span class="sxs-lookup"><span data-stu-id="5d434-282">Full and Delta Import</span></span>
<span data-ttu-id="5d434-283">일반 SQL 커넥터는 다음의 메서드를 사용하여 전체 및 델타 가져오기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-283">Generic SQL Connector support Full and Delta Import using these methods:</span></span>

* <span data-ttu-id="5d434-284">테이블</span><span class="sxs-lookup"><span data-stu-id="5d434-284">Table</span></span>
* <span data-ttu-id="5d434-285">보기</span><span class="sxs-lookup"><span data-stu-id="5d434-285">View</span></span>
* <span data-ttu-id="5d434-286">저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="5d434-286">Stored Procedure</span></span>
* <span data-ttu-id="5d434-287">SQL 쿼리</span><span class="sxs-lookup"><span data-stu-id="5d434-287">SQL Query</span></span>

![runstep1](./media/active-directory-aadconnectsync-connector-genericsql/runstep1.png)

<span data-ttu-id="5d434-289">**테이블/뷰**</span><span class="sxs-lookup"><span data-stu-id="5d434-289">**Table/View**</span></span>  
<span data-ttu-id="5d434-290">tooimport 다중 값된 속성 개체에 대해 tooprovide hello 쉼표로 구분 된 테이블/뷰 이름에 있으면 **다중값 이름 테이블/뷰** 및 각 조인 조건 hello에 **Join 조건**hello 부모 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-290">tooimport multi-valued attributes for an object, you have tooprovide hello comma-separated table/view name in **Name of Multi-Valued table/views** and respective join conditions in hello **Join condition** with hello parent table.</span></span>

<span data-ttu-id="5d434-291">예: tooimport hello Employee 개체 및 해당 모든 다중 값된 특성 원하는합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-291">Example: You want tooimport hello Employee object and all its multi-valued attributes.</span></span> <span data-ttu-id="5d434-292">직원(주 테이블) 및 부서(다중값)라는 두 개의 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-292">There are two tables, named Employee (main table) and Department (multi-valued).</span></span>
<span data-ttu-id="5d434-293">다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-293">Do hello following:</span></span>

* <span data-ttu-id="5d434-294">**테이블/뷰/SP**에서 **직원**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-294">Type **Employee** in **Table/View/SP**.</span></span>
* <span data-ttu-id="5d434-295">**다중값 테이블/뷰 이름**에서 부서를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-295">Type Department in **Name of Multi-Valued table/views**.</span></span>
* <span data-ttu-id="5d434-296">직원 및 부서 간 hello 조인 조건을 입력 **조인 조건**, 예를 들어 `Employee.DEPTID=Department.DepartmentID`합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-296">Type hello join condition between Employee & Department in **Join Condition**, for example `Employee.DEPTID=Department.DepartmentID`.</span></span>
  <span data-ttu-id="5d434-297">![runstep2](./media/active-directory-aadconnectsync-connector-genericsql/runstep2.png)</span><span class="sxs-lookup"><span data-stu-id="5d434-297">![runstep2](./media/active-directory-aadconnectsync-connector-genericsql/runstep2.png)</span></span>

<span data-ttu-id="5d434-298">**저장 프로시저**</span><span class="sxs-lookup"><span data-stu-id="5d434-298">**Stored procedures**</span></span>  
<span data-ttu-id="5d434-299">![runstep3](./media/active-directory-aadconnectsync-connector-genericsql/runstep3.png)</span><span class="sxs-lookup"><span data-stu-id="5d434-299">![runstep3](./media/active-directory-aadconnectsync-connector-genericsql/runstep3.png)</span></span>

* <span data-ttu-id="5d434-300">많은 데이터를 설정한 경우이 저장 프로시저와 tooimplement 페이지 매김을 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-300">If you have much data, it is recommended tooimplement pagination with your Stored Procedures.</span></span>
* <span data-ttu-id="5d434-301">저장 프로시저 toosupport 페이지 매김 tooprovide 시작 인덱스와 끝 인덱스 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-301">For your Stored Procedure toosupport pagination, you need tooprovide Start Index and End Index.</span></span> <span data-ttu-id="5d434-302">참고: [많은 양의 데이터를 효율적으로 페이징](https://msdn.microsoft.com/library/bb445504.aspx).</span><span class="sxs-lookup"><span data-stu-id="5d434-302">See: [Efficiently Paging Through Large Amounts of Data](https://msdn.microsoft.com/library/bb445504.aspx).</span></span>
* <span data-ttu-id="5d434-303">@StartIndex 및 @EndIndex은(는) 실행 시 **구성 단계** 페이지에 구성된 해당 페이지 크기 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-303">@StartIndex and @EndIndex are replaced at execution time with respective page size value configured on **Configure Step** page.</span></span> <span data-ttu-id="5d434-304">예를 들어 hello 커넥터 첫 페이지와 hello 페이지 크기를 검색 하는 경우 설정 되어 500으로 이러한 상황에서 @StartIndex 1 것 및 @EndIndex 500 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-304">For example, when hello connector retrieves first page and hello page size is set 500, in such situation @StartIndex would be 1 and @EndIndex 500.</span></span> <span data-ttu-id="5d434-305">이러한 값의 후속 페이지를 검색 하는 커넥터 늘린 hello 변경 @StartIndex & @EndIndex 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-305">These values increase when connector retrieves subsequent pages and change hello @StartIndex & @EndIndex value.</span></span>
* <span data-ttu-id="5d434-306">hello 매개 변수를 제공, tooexecute 저장 프로시저에 매개 변수가 `[Name]:[Direction]:[Value]` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-306">tooexecute parameterized Stored Procedure, provide hello parameters in `[Name]:[Direction]:[Value]` format.</span></span> <span data-ttu-id="5d434-307">(사용 하 여 Ctrl + Enter tooget 새 줄) 별도 줄에 각 매개 변수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-307">Enter each parameter on a separate line (Use Ctrl + Enter tooget a new line).</span></span>
* <span data-ttu-id="5d434-308">또한 일반 SQL 커넥터는 Microsoft SQL Server의 연결된 서버에서 가져오기 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-308">Generic SQL connector also supports Import operation from Linked Servers in Microsoft SQL Server.</span></span> <span data-ttu-id="5d434-309">연결 된 서버에 테이블에서 정보를 검색, 테이블 hello 형식으로 제공 해야:`[ServerName].[Database].[Schema].[TableName]`</span><span class="sxs-lookup"><span data-stu-id="5d434-309">If information should be retrieved from a Table in Linked server, then Table should be provided in hello format: `[ServerName].[Database].[Schema].[TableName]`</span></span>
* <span data-ttu-id="5d434-310">일반 SQL 커넥터는 실행 단계 정보와 스키마 탐색 간에 구조가 비슷한(모두 별칭 이름 및 데이터 형식) 개체만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-310">Generic SQL Connector supports only those objects that have similar structure (both alias name and data type) between run steps information and schema detection.</span></span> <span data-ttu-id="5d434-311">Hello 선택한 경우에 스키마 및 실행된 단계에서 제공 된 정보 로부터 개체 다르면 SQL 커넥터는 없습니다 toosupport 이러한 유형의 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-311">If hello selected object from schema and provided information at run step is different, then SQL Connector is unable toosupport this type of scenarios.</span></span>

<span data-ttu-id="5d434-312">**SQL 쿼리**</span><span class="sxs-lookup"><span data-stu-id="5d434-312">**SQL Query**</span></span>  
<span data-ttu-id="5d434-313">![runstep4](./media/active-directory-aadconnectsync-connector-genericsql/runstep4.png)</span><span class="sxs-lookup"><span data-stu-id="5d434-313">![runstep4](./media/active-directory-aadconnectsync-connector-genericsql/runstep4.png)</span></span>

![runstep5](./media/active-directory-aadconnectsync-connector-genericsql/runstep5.png)

* <span data-ttu-id="5d434-315">여러 결과 집합 쿼리는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-315">Multiple result sets queries not supported.</span></span>
* <span data-ttu-id="5d434-316">SQL 쿼리 지원 페이지 매김 hello 설명과 시작 인덱스와 끝 인덱스 변수 toosupport 페이지 매김으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-316">SQL query supports hello pagination and provide start Index and End Index as a variable toosupport pagination.</span></span>

### <a name="delta-import"></a><span data-ttu-id="5d434-317">델타 가져오기</span><span class="sxs-lookup"><span data-stu-id="5d434-317">Delta Import</span></span>
![runstep6](./media/active-directory-aadconnectsync-connector-genericsql/runstep6.png)

<span data-ttu-id="5d434-319">델타 가져오기 구성은 전체 가져오기에 비해 몇 가지 추가 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-319">Delta Import configuration requires some more configuration compared with Full Import.</span></span>

* <span data-ttu-id="5d434-320">Hello 트리거 또는 스냅숏 방법을 tootrack 델타 변경 내용을 선택 하는 경우 데이터베이스에 스냅숏 또는 기록 테이블을 제공 합니다 **스냅숏 또는 기록 테이블에 해당 하는 데이터베이스의 이름** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-320">If you choose hello Trigger or Snapshot approach tootrack delta changes, then provide History Table or Snapshot database in **History Table or Snapshot database name** box.</span></span>
* <span data-ttu-id="5d434-321">또한 해야 기록 테이블과 부모 테이블 간의 조인 조건을 tooprovide 예`Employee.ID=History.EmployeeID`</span><span class="sxs-lookup"><span data-stu-id="5d434-321">You also need tooprovide join condition between History table and Parent table, for example `Employee.ID=History.EmployeeID`</span></span>
* <span data-ttu-id="5d434-322">hello 기록 테이블에서 hello 부모 테이블에서 tootrack hello 트랜잭션 hello 작업 정보 (추가/업데이트/삭제)를 포함 하는 hello 열 이름을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-322">tootrack hello transaction on hello parent table from hello history table, you must provide hello column name that contains hello operation information (Add/Update/Delete).</span></span>
* <span data-ttu-id="5d434-323">워터 마크 tootrack 델타 변경 내용을 선택 하면 다음에 hello 작업 정보를 포함 하는 hello 열 이름을 제공 **수 위 표시 열 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-323">If you choose Watermark tootrack delta changes, then provide hello column name that contains hello operation information in **Water Mark Column Name**.</span></span>
* <span data-ttu-id="5d434-324">hello **변경 유형 특성** 종류를 변경 하는 hello에 열이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-324">hello **change Type attribute** column is required for hello change type.</span></span> <span data-ttu-id="5d434-325">이 열이 매핑되는 hello 기본 테이블에서 발생 하는 변경 또는 다중 값 테이블 tooa hello 델타 보기 형식을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-325">This column maps a change that occurs in hello primary table or multi-value table tooa change type in hello delta view.</span></span> <span data-ttu-id="5d434-326">이 열에는 특성-수준 변경 또는 추가, 수정, hello Modify_Attribute 변경 유형을 포함 될 수 있습니다 또는 삭제 변경 개체 수준 변경 형식에 대 한 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-326">This column can contain hello Modify_Attribute change type for attribute-level change or an Add, Modify, or Delete change type for an object-level change type.</span></span> <span data-ttu-id="5d434-327">Hello 기본값 추가, 수정가 하거나 삭제 하면이 옵션을 사용 하 여 해당 값을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-327">If it is something other than hello default value Add, Modify, or Delete, then you can define those values using this option.</span></span>

### <a name="export"></a><span data-ttu-id="5d434-328">내보내기</span><span class="sxs-lookup"><span data-stu-id="5d434-328">Export</span></span>
![runstep7](./media/active-directory-aadconnectsync-connector-genericsql/runstep7.png)

<span data-ttu-id="5d434-330">일반 SQL 커넥터는 다음과 같이 네 가지 지원된 방법을 사용하여 내보내기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-330">Generic SQL Connector support Export using four supported methods such as:</span></span>

* <span data-ttu-id="5d434-331">테이블</span><span class="sxs-lookup"><span data-stu-id="5d434-331">Table</span></span>
* <span data-ttu-id="5d434-332">보기</span><span class="sxs-lookup"><span data-stu-id="5d434-332">View</span></span>
* <span data-ttu-id="5d434-333">저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="5d434-333">Stored Procedure</span></span>
* <span data-ttu-id="5d434-334">SQL 쿼리</span><span class="sxs-lookup"><span data-stu-id="5d434-334">SQL Query</span></span>

<span data-ttu-id="5d434-335">**테이블/뷰**</span><span class="sxs-lookup"><span data-stu-id="5d434-335">**Table/View**</span></span>  
<span data-ttu-id="5d434-336">Hello 테이블/뷰 옵션을 선택 하면 hello 커넥터 hello 각각의 쿼리 toodo hello 내보내기를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-336">If you choose hello Table/View option, then hello connector generates hello respective queries toodo hello Export.</span></span>

<span data-ttu-id="5d434-337">**저장 프로시저**</span><span class="sxs-lookup"><span data-stu-id="5d434-337">**Stored procedures**</span></span>  
<span data-ttu-id="5d434-338">![runstep8](./media/active-directory-aadconnectsync-connector-genericsql/runstep8.png)</span><span class="sxs-lookup"><span data-stu-id="5d434-338">![runstep8](./media/active-directory-aadconnectsync-connector-genericsql/runstep8.png)</span></span>

<span data-ttu-id="5d434-339">Hello 저장 프로시저 옵션을 선택 하면 세 가지 서로 다른 저장 프로시저 tooperform Insert/Update/Delete 작업 내보내기에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-339">If you choose hello Stored Procedure option, Export requires three different Stored procedures tooperform Insert/Update/Delete operations.</span></span>

* <span data-ttu-id="5d434-340">**SP 이름을 추가**: 모든 개체에 hello 해당 테이블에서 삽입을 위한 tooconnector 제공 하는 경우이 SP 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-340">**Add SP Name**: This SP runs if any object comes tooconnector for insertion in hello respective table.</span></span>
* <span data-ttu-id="5d434-341">**SP 이름을 업데이트**: 개체 업데이트 hello 해당 테이블에 대 한 tooconnector 상태가 된 경우이 SP 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-341">**Update SP Name**: This SP runs if any object comes tooconnector for update in hello respective table.</span></span>
* <span data-ttu-id="5d434-342">**SP 이름을 삭제**: 임의의 개체 제공 tooconnector hello 해당 테이블에서 삭제 되 면이 SP 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-342">**Delete SP Name**: This SP runs if any object comes tooconnector for deletion in hello respective table.</span></span>
* <span data-ttu-id="5d434-343">매개 변수 값 toohello 저장 프로시저를 사용 하는 hello 스키마에서 선택한 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-343">Attribute selected from hello schema used as a parameter value toohello stored procedure.</span></span> <span data-ttu-id="5d434-344">예를 들어 `EmployeeName: INPUT: @EmployeeName` (EmployeeName hello 커넥터 스키마에서 선택 및 내보내기 수행 하는 동안 hello 해당 값을 대체 하는 hello 커넥터)</span><span class="sxs-lookup"><span data-stu-id="5d434-344">For example, `EmployeeName: INPUT: @EmployeeName` (EmployeeName is selected in hello connector schema and hello connector replaces hello respective value while doing export)</span></span>
* <span data-ttu-id="5d434-345">toorun 저장된 프로시저 매개 변수가 있는, 매개 변수에서 제공 `[Name]:[Direction]:[Value]` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-345">toorun parameterized stored procedure, provide parameters in `[Name]:[Direction]:[Value]` format.</span></span> <span data-ttu-id="5d434-346">(사용 하 여 Ctrl + Enter tooget 새 줄) 별도 줄에 각 매개 변수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-346">Enter each parameter on a separate line (Use Ctrl + Enter tooget a new line).</span></span>

<span data-ttu-id="5d434-347">**SQL query**</span><span class="sxs-lookup"><span data-stu-id="5d434-347">**SQL query**</span></span>  
<span data-ttu-id="5d434-348">![runstep9](./media/active-directory-aadconnectsync-connector-genericsql/runstep9.png)</span><span class="sxs-lookup"><span data-stu-id="5d434-348">![runstep9](./media/active-directory-aadconnectsync-connector-genericsql/runstep9.png)</span></span>

<span data-ttu-id="5d434-349">Hello SQL 쿼리 옵션을 선택 하면 세 가지 tooperform 삽입/업데이트/삭제 작업을 쿼리하여 내보내기 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-349">If you choose hello SQL query option, Export requires three different queries tooperform Insert/Update/Delete operations.</span></span>

* <span data-ttu-id="5d434-350">**삽입 쿼리**: 개체 tooconnector hello 해당 테이블에 삽입을 위해 제공 하는 경우이 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-350">**Insert Query**: This query runs if any object comes tooconnector for insertion in hello respective table.</span></span>
* <span data-ttu-id="5d434-351">**업데이트 쿼리**: 개체 업데이트 hello 해당 테이블에 대 한 tooconnector 상태가 된 경우이 쿼리가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-351">**Update Query**: This query runs if any object comes tooconnector for update in hello respective table.</span></span>
* <span data-ttu-id="5d434-352">**삭제 쿼리**: 개체 상태가 tooconnector hello 해당 테이블에서 삭제 된 경우이 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-352">**Delete Query**: This query runs if any object comes tooconnector for deletion in hello respective table.</span></span>
* <span data-ttu-id="5d434-353">예를 들어 매개 변수 값 toohello 쿼리를 사용 하는 hello 스키마에서 선택한 특성`Insert into Employee (ID, Name) Values (@ID, @EmployeeName)`</span><span class="sxs-lookup"><span data-stu-id="5d434-353">Attribute selected from hello schema used as a parameter value toohello query, for example `Insert into Employee (ID, Name) Values (@ID, @EmployeeName)`</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5d434-354">문제 해결</span><span class="sxs-lookup"><span data-stu-id="5d434-354">Troubleshooting</span></span>
* <span data-ttu-id="5d434-355">참조 hello tooenable 로깅 tootroubleshoot 커넥터 hello 하는 방법에 대 한 내용은 [어떻게 커넥터에 대 한 ETW 추적 tooEnable](http://go.microsoft.com/fwlink/?LinkId=335731)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d434-355">For information on how tooenable logging tootroubleshoot hello connector, see hello [How tooEnable ETW Tracing for Connectors](http://go.microsoft.com/fwlink/?LinkId=335731).</span></span>
