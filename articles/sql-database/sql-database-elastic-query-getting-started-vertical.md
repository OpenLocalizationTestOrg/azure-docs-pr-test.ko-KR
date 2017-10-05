---
title: "데이터베이스 간 쿼리 시작(수직 분할) | Microsoft Docs"
description: "수직 분할 데이터베이스에서 탄력적 데이터베이스 쿼리를 사용하는 방법"
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
ms.openlocfilehash: 17158c4960e9ba9251524659c90af9aec1316774
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a><span data-ttu-id="955a1-103">데이터베이스 간 쿼리 시작(수직 분할)(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="955a1-103">Get started with cross-database queries (vertical partitioning) (preview)</span></span>
<span data-ttu-id="955a1-104">Azure SQL 데이터베이스에 탄력적 데이터베이스 쿼리 (미리 보기)를 사용 하면 단일 연결 지점을 사용하여 여러 데이터베이스에 걸쳐 있는 T-SQL 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="955a1-104">Elastic database query (preview) for Azure SQL Database allows you to run T-SQL queries that span multiple databases using a single connection point.</span></span> <span data-ttu-id="955a1-105">이 항목은 [데이터베이스 수직 분할](sql-database-elastic-query-vertical-partitioning.md)에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="955a1-105">This topic applies to [vertically partitioned databases](sql-database-elastic-query-vertical-partitioning.md).</span></span>  

<span data-ttu-id="955a1-106">완료되면 여러 관계형 데이터베이스에 걸쳐 있는 쿼리를 수행 하는 Azure SQL 데이터베이스를 사용과 구성방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="955a1-106">When completed, you will: learn how to configure and use an Azure SQL Database to perform queries that span multiple related databases.</span></span> 

<span data-ttu-id="955a1-107">탄력적 데이터베이스 쿼리 기능에 대한 자세한 내용은 [Azure SQL Database 탄력적 데이터베이스 쿼리 개요](sql-database-elastic-query-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="955a1-107">For more information about the elastic database query feature, please see  [Azure SQL Database elastic database query overview](sql-database-elastic-query-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="955a1-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="955a1-108">Prerequisites</span></span>

<span data-ttu-id="955a1-109">사용자는 모든 외부 데이터 원본 ALTER 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="955a1-109">You must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="955a1-110">이 사용 권한은 ALTER DATABASE 권한에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="955a1-110">This permission is included with the ALTER DATABASE permission.</span></span> <span data-ttu-id="955a1-111">기본 데이터 원본을 참조하기 위해 ALTER ANY EXTERNAL DATA SOURCE 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="955a1-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="create-the-sample-databases"></a><span data-ttu-id="955a1-112">샘플 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="955a1-112">Create the sample databases</span></span>
<span data-ttu-id="955a1-113">먼저 동일하거나 다른 논리적 서버에 있는 이름이 **고객** 및 **주문**인 두 데이터베이스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="955a1-113">To start with, we need to create two databases, **Customers** and **Orders**, either in the same or different logical servers.</span></span>   

<span data-ttu-id="955a1-114">**주문** 데이터베이스에서 다음 쿼리를 실행하여 **주문 정보** 테이블을 만들고 샘플 데이터를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="955a1-114">Execute the following queries on the **Orders** database to create the **OrderInformation** table and input the sample data.</span></span> 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

<span data-ttu-id="955a1-115">이제 **고객** 데이터베이스에서 다음 쿼리를 실행하여 **고객 정보** 테이블을 만들고 샘플 데이터를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="955a1-115">Now, execute following query on the **Customers** database to create the **CustomerInformation** table and input the sample data.</span></span> 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a><span data-ttu-id="955a1-116">데이터베이스 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="955a1-116">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="955a1-117">데이터베이스 범위 마스터 키 및 자격 증명</span><span class="sxs-lookup"><span data-stu-id="955a1-117">Database scoped master key and credentials</span></span>
1. <span data-ttu-id="955a1-118">SQL Server Management Studio 또는 Visual Studio의 SQL Server Data Tools를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="955a1-118">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="955a1-119">주문 데이터베이스에 연결하고 T-SQL 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="955a1-119">Connect to the Orders database and execute the following T-SQL commands:</span></span>
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    <span data-ttu-id="955a1-120">“사용자 이름”과 “암호”는 고객 데이터베이스 로그인에 사용되는 사용자 이름과 암호여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="955a1-120">The "username" and "password" should be the username and password used to login into the Customers database.</span></span>
    <span data-ttu-id="955a1-121">탄력적 쿼리를 통해 Azure Active Directory를 사용한 인증은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="955a1-121">Authentication using Azure Active Directory with elastic queries is not currently supported.</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="955a1-122">외부 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="955a1-122">External data sources</span></span>
<span data-ttu-id="955a1-123">외부 데이터 소스를 만들려면 주문 데이터베이스에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="955a1-123">To create an external data source, execute the following command on the Orders database:</span></span> 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a><span data-ttu-id="955a1-124">외부 테이블</span><span class="sxs-lookup"><span data-stu-id="955a1-124">External tables</span></span>
<span data-ttu-id="955a1-125">주문 데이터베이스에서 고객 정보 테이블의 정의와 일치하는 외부 테이블을 만듭니다. </span><span class="sxs-lookup"><span data-stu-id="955a1-125">Create an external table on the Orders database, which matches the definition of the CustomerInformation table:</span></span>

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="955a1-126">탄력적 데이터베이스 T-SQL쿼리 샘플 실행</span><span class="sxs-lookup"><span data-stu-id="955a1-126">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="955a1-127">외부 데이터 원본 및 외부 테이블을 정의한 후에는 T-SQL을 사용하여 외부 테이블을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="955a1-127">Once you have defined your external data source and your external tables you can now use T-SQL to query your external tables.</span></span> <span data-ttu-id="955a1-128">주문 데이터베이스에 다음 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="955a1-128">Execute this query on the Orders database:</span></span> 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a><span data-ttu-id="955a1-129">비용</span><span class="sxs-lookup"><span data-stu-id="955a1-129">Cost</span></span>
<span data-ttu-id="955a1-130">현재 Azure SQL 데이터베이스 가격에는 탄력적 데이터베이스 쿼리 기능이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="955a1-130">Currently, the elastic database query feature is included into the cost of your Azure SQL Database.</span></span>  

<span data-ttu-id="955a1-131">가격 정보는 [SQL 데이터베이스 가격 정보](https://azure.microsoft.com/pricing/details/sql-database)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="955a1-131">For pricing information see [SQL Database Pricing](https://azure.microsoft.com/pricing/details/sql-database).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="955a1-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="955a1-132">Next steps</span></span>

* <span data-ttu-id="955a1-133">탄력적 쿼리의 개요는 [탄력적 쿼리 개요](sql-database-elastic-query-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="955a1-133">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="955a1-134">수직 분할된 데이터에 대한 구문 및 예제 쿼리는 [수직 분할된 데이터 쿼리하기](sql-database-elastic-query-vertical-partitioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="955a1-134">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="955a1-135">행 분할(분할) 자습서는 [행 분할(분할)을 위한 탄력적 데이터베이스 쿼리 시작하기](sql-database-elastic-query-getting-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="955a1-135">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="955a1-136">행 분할된 데이터에 대한 구문 및 예제 쿼리는 [행 분할된 데이터 쿼리하기](sql-database-elastic-query-horizontal-partitioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="955a1-136">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="955a1-137">단일 원격 Azure SQL Database 또는 수평 분할 구성표의 분할을 제공하는 데이터베이스 집합에서 TRANSACT-SQL 문을 실행하는 저장된 프로시저는 [sp\_실행 \_원격](https://msdn.microsoft.com/library/mt703714)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="955a1-137">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>