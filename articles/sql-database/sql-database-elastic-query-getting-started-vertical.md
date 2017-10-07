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
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a>데이터베이스 간 쿼리 시작(수직 분할)(미리 보기)
Azure SQL 데이터베이스 탄력적 데이터베이스 쿼리 (미리 보기) 사용 하면 단일 연결 지점을 사용 하 여 여러 데이터베이스에 걸쳐 있는 toorun T-SQL 쿼리가 있습니다. 이 항목은 너무 적용[데이터베이스 수직 분할](sql-database-elastic-query-vertical-partitioning.md)합니다.  

완료 되 면 됩니다: 방법을 tooconfigure 및 Azure SQL 데이터베이스 tooperform 사용 하 여 쿼리를 포괄 하는 여러 관련 된 데이터베이스에 알아봅니다. 

Hello 탄력적 데이터베이스 쿼리 기능에 대 한 자세한 내용은 참조 하십시오 [Azure SQL 데이터베이스 탄력적 데이터베이스 쿼리 개요](sql-database-elastic-query-overview.md)합니다. 

## <a name="prerequisites"></a>필수 조건

사용자는 모든 외부 데이터 원본 ALTER 권한이 있어야 합니다. 이 사용 권한은 hello ALTER DATABASE 권한이 포함 되어 있습니다. ALTER ANY EXTERNAL DATA SOURCE 권한은 필요한 toorefer toohello 데이터 원본으로 사용 합니다.

## <a name="create-hello-sample-databases"></a>Hello 예제 데이터베이스 만들기
두 개의 데이터베이스 toocreate 필요와 toostart, **고객** 및 **Orders**, 동일한 또는 다른 논리 서버 hello에 합니다.   

Hello에 쿼리를 다음과 같은 hello 실행 **Orders** 데이터베이스 toocreate hello **OrderInformation** hello 예제 데이터 테이블 및 입력 합니다. 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

이제, 다음 hello에 대 한 쿼리를 실행 **고객** 데이터베이스 toocreate hello **CustomerInformation** hello 예제 데이터 테이블 및 입력 합니다. 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a>데이터베이스 개체 만들기
### <a name="database-scoped-master-key-and-credentials"></a>데이터베이스 범위 마스터 키 및 자격 증명
1. SQL Server Management Studio 또는 Visual Studio의 SQL Server Data Tools를 엽니다.
2. Toohello Orders 데이터베이스를 연결 하 고 다음 T-SQL 명령을 hello를 실행 합니다.
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    hello "username" 및 "password" hello username 있어야 하 고 암호 hello 고객 데이터베이스에 toologin를 사용 합니다.
    탄력적 쿼리를 통해 Azure Active Directory를 사용한 인증은 현재 지원되지 않습니다.

### <a name="external-data-sources"></a>외부 데이터 원본
외부 데이터 원본, toocreate hello hello Orders 데이터베이스에서 다음 명령을 실행 합니다. 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a>외부 테이블
Hello hello CustomerInformation 테이블 정의 일치 하는 hello Orders 데이터베이스에 외부 테이블을 만듭니다.

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a>탄력적 데이터베이스 T-SQL쿼리 샘플 실행
외부 데이터 원본 및 외부 테이블을 정의 하 고 나면 T-SQL tooquery를 외부 테이블 이제 사용할 수 있습니다. Hello Orders 데이터베이스에서이 쿼리를 실행 합니다. 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a>비용
현재 hello 탄력적 데이터베이스 쿼리 기능은 Azure SQL 데이터베이스의 hello 비용에 포함 됩니다.  

가격 정보는 [SQL 데이터베이스 가격 정보](https://azure.microsoft.com/pricing/details/sql-database)를 참조하세요. 

## <a name="next-steps"></a>다음 단계

* 탄력적 쿼리의 개요는 [탄력적 쿼리 개요](sql-database-elastic-query-overview.md)를 참조하세요.
* 수직 분할된 데이터에 대한 구문 및 예제 쿼리는 [수직 분할된 데이터 쿼리하기](sql-database-elastic-query-vertical-partitioning.md)를 참조하세요.
* 행 분할(분할) 자습서는 [행 분할(분할)을 위한 탄력적 데이터베이스 쿼리 시작하기](sql-database-elastic-query-getting-started.md)를 참조하세요.
* 행 분할된 데이터에 대한 구문 및 예제 쿼리는 [행 분할된 데이터 쿼리하기](sql-database-elastic-query-horizontal-partitioning.md)를 참조하세요.
* 단일 원격 Azure SQL Database 또는 수평 분할 구성표의 분할을 제공하는 데이터베이스 집합에서 TRANSACT-SQL 문을 실행하는 저장된 프로시저는 [sp\_실행 \_원격](https://msdn.microsoft.com/library/mt703714)을 참조하세요.