---
title: "데이터베이스 간 쿼리 (수직 분할) aaaGet 시작 | Microsoft Docs"
description: "수직 분할 데이터베이스를 어떻게 사용 하 여 toouse 탄력적 데이터베이스 쿼리"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: e5b44b10-c432-4f96-b20e-08615ff4d5dd
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: torsteng
ms.openlocfilehash: 9e6183268e8bf87e3ac28f502711fcc05a7a3f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a><span data-ttu-id="a53bc-103">데이터베이스 간 쿼리 시작(수직 분할)(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="a53bc-103">Get started with cross-database queries (vertical partitioning) (preview)</span></span>
<span data-ttu-id="a53bc-104">Azure SQL 데이터베이스 탄력적 데이터베이스 쿼리 (미리 보기) 사용 하면 단일 연결 지점을 사용 하 여 여러 데이터베이스에 걸쳐 있는 toorun T-SQL 쿼리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a53bc-104">Elastic database query (preview) for Azure SQL Database allows you toorun T-SQL queries that span multiple databases using a single connection point.</span></span> <span data-ttu-id="a53bc-105">이 항목은 너무 적용[데이터베이스 수직 분할](sql-database-elastic-query-vertical-partitioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a53bc-105">This topic applies too[vertically partitioned databases](sql-database-elastic-query-vertical-partitioning.md).</span></span>  

<span data-ttu-id="a53bc-106">완료 되 면 됩니다: 방법을 tooconfigure 및 Azure SQL 데이터베이스 tooperform 사용 하 여 쿼리를 포괄 하는 여러 관련 된 데이터베이스에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a53bc-106">When completed, you will: learn how tooconfigure and use an Azure SQL Database tooperform queries that span multiple related databases.</span></span> 

<span data-ttu-id="a53bc-107">Hello 탄력적 데이터베이스 쿼리 기능에 대 한 자세한 내용은 참조 하십시오 [Azure SQL 데이터베이스 탄력적 데이터베이스 쿼리 개요](sql-database-elastic-query-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a53bc-107">For more information about hello elastic database query feature, please see  [Azure SQL Database elastic database query overview](sql-database-elastic-query-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a53bc-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a53bc-108">Prerequisites</span></span>

<span data-ttu-id="a53bc-109">사용자는 모든 외부 데이터 원본 ALTER 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a53bc-109">You must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="a53bc-110">이 사용 권한은 hello ALTER DATABASE 권한이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a53bc-110">This permission is included with hello ALTER DATABASE permission.</span></span> <span data-ttu-id="a53bc-111">ALTER ANY EXTERNAL DATA SOURCE 권한은 필요한 toorefer toohello 데이터 원본으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a53bc-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="create-hello-sample-databases"></a><span data-ttu-id="a53bc-112">Hello 예제 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="a53bc-112">Create hello sample databases</span></span>
<span data-ttu-id="a53bc-113">두 개의 데이터베이스 toocreate 필요와 toostart, **고객** 및 **Orders**, 동일한 또는 다른 논리 서버 hello에 합니다.</span><span class="sxs-lookup"><span data-stu-id="a53bc-113">toostart with, we need toocreate two databases, **Customers** and **Orders**, either in hello same or different logical servers.</span></span>   

<span data-ttu-id="a53bc-114">Hello에 쿼리를 다음과 같은 hello 실행 **Orders** 데이터베이스 toocreate hello **OrderInformation** hello 예제 데이터 테이블 및 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a53bc-114">Execute hello following queries on hello **Orders** database toocreate hello **OrderInformation** table and input hello sample data.</span></span> 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

<span data-ttu-id="a53bc-115">이제, 다음 hello에 대 한 쿼리를 실행 **고객** 데이터베이스 toocreate hello **CustomerInformation** hello 예제 데이터 테이블 및 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a53bc-115">Now, execute following query on hello **Customers** database toocreate hello **CustomerInformation** table and input hello sample data.</span></span> 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a><span data-ttu-id="a53bc-116">데이터베이스 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="a53bc-116">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="a53bc-117">데이터베이스 범위 마스터 키 및 자격 증명</span><span class="sxs-lookup"><span data-stu-id="a53bc-117">Database scoped master key and credentials</span></span>
1. <span data-ttu-id="a53bc-118">SQL Server Management Studio 또는 Visual Studio의 SQL Server Data Tools를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a53bc-118">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="a53bc-119">Toohello Orders 데이터베이스를 연결 하 고 다음 T-SQL 명령을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a53bc-119">Connect toohello Orders database and execute hello following T-SQL commands:</span></span>
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    <span data-ttu-id="a53bc-120">hello "username" 및 "password" hello username 있어야 하 고 암호 hello 고객 데이터베이스에 toologin를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a53bc-120">hello "username" and "password" should be hello username and password used toologin into hello Customers database.</span></span>
    <span data-ttu-id="a53bc-121">탄력적 쿼리를 통해 Azure Active Directory를 사용한 인증은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a53bc-121">Authentication using Azure Active Directory with elastic queries is not currently supported.</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="a53bc-122">외부 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="a53bc-122">External data sources</span></span>
<span data-ttu-id="a53bc-123">외부 데이터 원본, toocreate hello hello Orders 데이터베이스에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a53bc-123">toocreate an external data source, execute hello following command on hello Orders database:</span></span> 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a><span data-ttu-id="a53bc-124">외부 테이블</span><span class="sxs-lookup"><span data-stu-id="a53bc-124">External tables</span></span>
<span data-ttu-id="a53bc-125">Hello hello CustomerInformation 테이블 정의 일치 하는 hello Orders 데이터베이스에 외부 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a53bc-125">Create an external table on hello Orders database, which matches hello definition of hello CustomerInformation table:</span></span>

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="a53bc-126">탄력적 데이터베이스 T-SQL쿼리 샘플 실행</span><span class="sxs-lookup"><span data-stu-id="a53bc-126">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="a53bc-127">외부 데이터 원본 및 외부 테이블을 정의 하 고 나면 T-SQL tooquery를 외부 테이블 이제 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a53bc-127">Once you have defined your external data source and your external tables you can now use T-SQL tooquery your external tables.</span></span> <span data-ttu-id="a53bc-128">Hello Orders 데이터베이스에서이 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a53bc-128">Execute this query on hello Orders database:</span></span> 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a><span data-ttu-id="a53bc-129">비용</span><span class="sxs-lookup"><span data-stu-id="a53bc-129">Cost</span></span>
<span data-ttu-id="a53bc-130">현재 hello 탄력적 데이터베이스 쿼리 기능은 Azure SQL 데이터베이스의 hello 비용에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a53bc-130">Currently, hello elastic database query feature is included into hello cost of your Azure SQL Database.</span></span>  

<span data-ttu-id="a53bc-131">가격 정보는 [SQL 데이터베이스 가격 정보](https://azure.microsoft.com/pricing/details/sql-database)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a53bc-131">For pricing information see [SQL Database Pricing](https://azure.microsoft.com/pricing/details/sql-database).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a53bc-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a53bc-132">Next steps</span></span>

* <span data-ttu-id="a53bc-133">탄력적 쿼리의 개요는 [탄력적 쿼리 개요](sql-database-elastic-query-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a53bc-133">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="a53bc-134">수직 분할된 데이터에 대한 구문 및 예제 쿼리는 [수직 분할된 데이터 쿼리하기](sql-database-elastic-query-vertical-partitioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a53bc-134">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="a53bc-135">행 분할(분할) 자습서는 [행 분할(분할)을 위한 탄력적 데이터베이스 쿼리 시작하기](sql-database-elastic-query-getting-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a53bc-135">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="a53bc-136">행 분할된 데이터에 대한 구문 및 예제 쿼리는 [행 분할된 데이터 쿼리하기](sql-database-elastic-query-horizontal-partitioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a53bc-136">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="a53bc-137">단일 원격 Azure SQL Database 또는 수평 분할 구성표의 분할을 제공하는 데이터베이스 집합에서 TRANSACT-SQL 문을 실행하는 저장된 프로시저는 [sp\_실행 \_원격](https://msdn.microsoft.com/library/mt703714)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a53bc-137">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>