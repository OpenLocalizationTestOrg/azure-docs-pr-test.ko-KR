---
title: "데이터베이스 응용 프로그램 개발 개요 aaaSQL | Microsoft Docs"
description: "사용 가능한 연결 라이브러리 및 tooSQL 데이터베이스 연결 응용 프로그램에 대 한 모범 사례에 알아봅니다."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: genemi
ms.assetid: 67c02204-d1bd-4622-acce-92115a7cde03
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: 17f04db600828f90c42c750c9abdb92cfa4ca817
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-application-development-overview"></a><span data-ttu-id="da776-103">SQL Database 응용 프로그램 개발 개요</span><span class="sxs-lookup"><span data-stu-id="da776-103">SQL Database application development overview</span></span>
<span data-ttu-id="da776-104">이 문서는 개발자는 코드 tooconnect tooAzure SQL 데이터베이스를 작성할 때 알고 있어야 합니다. 기본 고려 hello 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="da776-104">This article walks through hello basic considerations that a developer should be aware of when writing code tooconnect tooAzure SQL Database.</span></span>

> [!TIP]
> <span data-ttu-id="da776-105">방법 toocreate는 서버는 서버 기반 방화벽을 서버 속성 보기를 만듭니다 쿼리 hello master 데이터베이스, SQL Server Management Studio를 사용 하 여 연결, 빈 데이터베이스와 예제 데이터베이스를 만들 데이터베이스 속성을 쿼리할 자습서 표시, 연결 SQL Server Management Studio 및 쿼리 hello 예제 데이터베이스를 사용 하 여 참조 [자습서 가져오기](sql-database-get-started-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="da776-105">For a tutorial showing you how toocreate a server, create a server-based firewall, view server properties, connect using SQL Server Management Studio, query hello master database, create a sample database and a blank database, query database properties, connect using SQL Server Management Studio, and query hello sample database, see [Get Started Tutorial](sql-database-get-started-portal.md).</span></span>
>

## <a name="language-and-platform"></a><span data-ttu-id="da776-106">언어 및 플랫폼</span><span class="sxs-lookup"><span data-stu-id="da776-106">Language and platform</span></span>
<span data-ttu-id="da776-107">다양한 프로그래밍 언어 및 플랫폼에 대한 코드 샘플을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da776-107">There are code samples available for various programming languages and platforms.</span></span> <span data-ttu-id="da776-108">링크 toohello 코드 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da776-108">You can find links toohello code samples at:</span></span> 

* <span data-ttu-id="da776-109">추가 정보: [SQL 데이터베이스 및 SQL Server용 연결 라이브러리](sql-database-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="da776-109">More Information: [Connection libraries for SQL Database and SQL Server](sql-database-libraries.md)</span></span>

## <a name="tools"></a><span data-ttu-id="da776-110">도구</span><span class="sxs-lookup"><span data-stu-id="da776-110">Tools</span></span> 
<span data-ttu-id="da776-111">[cheetah](https://github.com/wunderlist/cheetah), [sql-cli](https://www.npmjs.com/package/sql-cli), [VS Code](https://code.visualstudio.com/)와 같은 오픈 소스 도구를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da776-111">You can leverage open source tools like [cheetah](https://github.com/wunderlist/cheetah), [sql-cli](https://www.npmjs.com/package/sql-cli), [VS Code](https://code.visualstudio.com/).</span></span> <span data-ttu-id="da776-112">또한 Azure SQL Database는 [Visual Studio](https://www.visualstudio.com/downloads/) 및 [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx)와 같은 Microsoft 도구로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="da776-112">Additionally, Azure SQL Database works with Microsoft tools like [Visual Studio](https://www.visualstudio.com/downloads/) and  [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).</span></span>  <span data-ttu-id="da776-113">Hello Azure 관리 포털, PowerShell을 사용할 수도 있습니다 수 있도록 도와 REST Api 추가 생산성을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da776-113">You can also use hello Azure Management Portal, PowerShell, and REST APIs help you gain additional productivity.</span></span>

## <a name="resource-limitations"></a><span data-ttu-id="da776-114">리소스 제한</span><span class="sxs-lookup"><span data-stu-id="da776-114">Resource limitations</span></span>
<span data-ttu-id="da776-115">다른 두 가지 메커니즘을 사용 하 여 hello 리소스 사용 가능한 tooa 데이터베이스를 관리 하는 azure SQL 데이터베이스: 리소스 거 버 넌 스 및 제한을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="da776-115">Azure SQL Database manages hello resources available tooa database using two different mechanisms: Resources Governance and Enforcement of Limits.</span></span>

* <span data-ttu-id="da776-116">추가 정보: [Azure SQL 데이터베이스 리소스 한도](sql-database-resource-limits.md)</span><span class="sxs-lookup"><span data-stu-id="da776-116">More Information: [Azure SQL Database resource limits](sql-database-resource-limits.md)</span></span>

## <a name="security"></a><span data-ttu-id="da776-117">보안</span><span class="sxs-lookup"><span data-stu-id="da776-117">Security</span></span>
<span data-ttu-id="da776-118">Azure SQL 데이터베이스는 액세스를 제한하고, 데이터를 보호하고, SQL 데이터베이스의 활동을 모니터링하는 리소스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="da776-118">Azure SQL Database provides resources for limiting access, protecting data, and monitoring activities on a SQL Database.</span></span>

* <span data-ttu-id="da776-119">추가 정보: [SQL 데이터베이스 보안 설정](sql-database-security-overview.md)</span><span class="sxs-lookup"><span data-stu-id="da776-119">More Information: [Securing your SQL Database](sql-database-security-overview.md)</span></span>

## <a name="authentication"></a><span data-ttu-id="da776-120">인증</span><span class="sxs-lookup"><span data-stu-id="da776-120">Authentication</span></span>
* <span data-ttu-id="da776-121">Azure SQL 데이터베이스는 SQL Server 인증 사용자 및 로그인과 [Azure Active Directory 인증](sql-database-aad-authentication.md) 사용자 및 로그인을 둘 다 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="da776-121">Azure SQL Database supports both SQL Server authentication users and logins, as well as [Azure Active Directory authentication](sql-database-aad-authentication.md) users and logins.</span></span>
* <span data-ttu-id="da776-122">Toospecify 기본값 toohello 대신 특정 데이터베이스를 필요한 *마스터* 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="da776-122">You need toospecify a particular database, instead of defaulting toohello *master* database.</span></span>
* <span data-ttu-id="da776-123">Hello Transact SQL을 사용할 수 없습니다 **사용 myDatabaseName;** SQL 데이터베이스 tooswitch tooanother 데이터베이스에서 문을 합니다.</span><span class="sxs-lookup"><span data-stu-id="da776-123">You cannot use hello Transact-SQL **USE myDatabaseName;** statement on SQL Database tooswitch tooanother database.</span></span>
* <span data-ttu-id="da776-124">추가 정보: [SQL 데이터베이스 보안: 데이터베이스 액세스 및 로그인 보안 관리](sql-database-manage-logins.md)</span><span class="sxs-lookup"><span data-stu-id="da776-124">More information: [SQL Database security: Manage database access and login security](sql-database-manage-logins.md)</span></span>

## <a name="resiliency"></a><span data-ttu-id="da776-125">복원력</span><span class="sxs-lookup"><span data-stu-id="da776-125">Resiliency</span></span>
<span data-ttu-id="da776-126">일시적인 오류가 발생 하는 tooSQL 데이터베이스를 연결 하는 동안 코드 hello 호출을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="da776-126">When a transient error occurs while connecting tooSQL Database, your code should retry hello call.</span></span>  <span data-ttu-id="da776-127">재시도 논리 백오프 논리를 사용 하 여, 부담이 되지 않는 있도록 동시에 다시 시도 하는 여러 클라이언트가 포함 된 SQL 데이터베이스 hello 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="da776-127">We recommend that retry logic use backoff logic, so that it does not overwhelm hello SQL Database with multiple clients retrying simultaneously.</span></span>

* <span data-ttu-id="da776-128">코드 샘플: 보여주는 코드 샘플에 다시 시도 논리를 hello에서 선택한 언어에 대 한 예제 참조: [SQL 데이터베이스 및 SQL Server에 대 한 연결 라이브러리](sql-database-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="da776-128">Code samples:  For code samples that illustrate retry logic, see samples for hello language of your choice at: [Connection libraries for SQL Database and SQL Server](sql-database-libraries.md)</span></span>
* <span data-ttu-id="da776-129">추가 정보: [SQL 데이터베이스 클라이언트 프로그램에 대한 오류 메시지](sql-database-develop-error-messages.md)</span><span class="sxs-lookup"><span data-stu-id="da776-129">More information: [Error messages for SQL Database client programs](sql-database-develop-error-messages.md)</span></span>

## <a name="managing-connections"></a><span data-ttu-id="da776-130">연결 관리</span><span class="sxs-lookup"><span data-stu-id="da776-130">Managing connections</span></span>
* <span data-ttu-id="da776-131">클라이언트 연결 논리에서 30 초 hello 기본 제한 시간 toobe를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="da776-131">In your client connection logic, override hello default timeout toobe 30 seconds.</span></span>  <span data-ttu-id="da776-132">15 초의 hello 기본값은 부족할에 종속 된 연결 hello 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="da776-132">hello default of 15 seconds is too short for connections that depend on hello internet.</span></span>
* <span data-ttu-id="da776-133">사용 하는 경우는 [연결 풀](http://msdn.microsoft.com/library/8xx3tyca.aspx)있는지 tooclose hello 연결 hello를 사용 하지 않는, 내용과 tooreuse을 준비 하는 프로그램 인스턴트 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="da776-133">If you are using a [connection pool](http://msdn.microsoft.com/library/8xx3tyca.aspx), be sure tooclose hello connection hello instant your program is not actively using it, and is not preparing tooreuse it.</span></span>

## <a name="network-considerations"></a><span data-ttu-id="da776-134">네트워크 고려 사항</span><span class="sxs-lookup"><span data-stu-id="da776-134">Network considerations</span></span>
* <span data-ttu-id="da776-135">클라이언트 프로그램을 호스팅하는 hello 컴퓨터에서 포트 1433에서 보내는 TCP 통신을 허용 하는 hello 방화벽을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="da776-135">On hello computer that hosts your client program, ensure hello firewall allows outgoing TCP communication on port 1433.</span></span>  <span data-ttu-id="da776-136">추가 정보: [Azure SQL 데이터베이스 방화벽 구성](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="da776-136">More information: [Configure an Azure SQL Database firewall](sql-database-configure-firewall-settings.md)</span></span>
* <span data-ttu-id="da776-137">클라이언트 프로그램에 연결 된 경우 tooSQL 데이터베이스 클라이언트는 Azure 가상 컴퓨터 (VM)에서 실행 되는 동안 VM hello에 특정 포트 범위를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da776-137">If your client program connects tooSQL Database while your client runs on an Azure virtual machine (VM), you must open certain port ranges on hello VM.</span></span> <span data-ttu-id="da776-138">추가 정보: [ADO.NET 4.5 및 SQL Database에 대한 1433 이외의 포트](sql-database-develop-direct-route-ports-adonet-v12.md)</span><span class="sxs-lookup"><span data-stu-id="da776-138">More information: [Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md)</span></span>
* <span data-ttu-id="da776-139">경우에 따라 클라이언트 연결 tooAzure SQL 데이터베이스는 hello 프록시를 무시 하 고 hello 데이터베이스와 직접 상호 작용 합니다.</span><span class="sxs-lookup"><span data-stu-id="da776-139">Client connections tooAzure SQL Database sometimes bypass hello proxy and interact directly with hello database.</span></span> <span data-ttu-id="da776-140">1433 이외의 포트가 중요해집니다.</span><span class="sxs-lookup"><span data-stu-id="da776-140">Ports other than 1433 become important.</span></span> <span data-ttu-id="da776-141">자세한 내용은 [Azure SQL Database 연결 아키텍처](sql-database-connectivity-architecture.md) 및 [ADO.NET 4.5 및 SQL Database에 대한 1433 이외의 포트](sql-database-develop-direct-route-ports-adonet-v12.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da776-141">For more information, [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md) and [Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>

## <a name="data-sharding-with-elastic-scale"></a><span data-ttu-id="da776-142">탄력적인 확장을 사용한 데이터 분할</span><span class="sxs-lookup"><span data-stu-id="da776-142">Data sharding with elastic scale</span></span>
<span data-ttu-id="da776-143">Elastic Scale out (및) 크기 조정 hello 과정이 간단해 집니다.</span><span class="sxs-lookup"><span data-stu-id="da776-143">Elastic Scale simplifies hello process of scaling out (and in).</span></span> 

* [<span data-ttu-id="da776-144">Azure SQL 데이터베이스를 사용한 다중 테넌트 SaaS 응용 프로그램 디자인 패턴</span><span class="sxs-lookup"><span data-stu-id="da776-144">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [<span data-ttu-id="da776-145">데이터 종속 라우팅</span><span class="sxs-lookup"><span data-stu-id="da776-145">Data dependent routing</span></span>](sql-database-elastic-scale-data-dependent-routing.md)
* [<span data-ttu-id="da776-146">Azure SQL 데이터베이스 탄력적인 확장 미리 보기 시작</span><span class="sxs-lookup"><span data-stu-id="da776-146">Get Started with Azure SQL Database Elastic Scale Preview</span></span>](sql-database-elastic-scale-get-started.md)

## <a name="next-steps"></a><span data-ttu-id="da776-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="da776-147">Next steps</span></span>
<span data-ttu-id="da776-148">모든 hello 탐색 [SQL 데이터베이스의 기능](sql-database-technical-overview.md)</span><span class="sxs-lookup"><span data-stu-id="da776-148">Explore all hello [capabilities of SQL Database](sql-database-technical-overview.md)</span></span>
