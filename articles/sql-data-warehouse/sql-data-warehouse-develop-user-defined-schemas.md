---
title: "SQL 데이터 웨어하우스에 aaaUser 정의 스키마 | Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 Transact-SQL 스키마 사용을 위한 팁"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 52af5bd5-d5d3-4f9b-8704-06829fb924e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c411d6fed68e67c444a5871eab06182eaeb6dbf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a>SQL 데이터 웨어하우스의 사용자 정의 스키마
일반적인 데이터 웨어하우스 작업, 도메인 또는 보안을 기반으로 자주 사용 하 여 별도 데이터베이스 toocreate 응용 프로그램 경계입니다. 예를 들어, 기존의 SQL Server 데이터 웨어하우스는 스테이징 데이터베이스, 데이터 웨어하우스 데이터베이스 및 일부 데이터마트 데이터베이스를 포함할 수 있습니다. 이 토폴로지에서 각 데이터베이스 작업 부하 및 보안 경계 hello 아키텍처에서 작동합니다.

반면, SQL 데이터 웨어하우스 데이터베이스 내에 hello 전체 데이터 웨어하우스 작업을 실행합니다. 데이터베이스 간 조인은 허용되지 않습니다. 따라서 SQL 데이터 웨어하우스는 hello 웨어하우스 toobe hello 한 데이터베이스에 저장 된 사용 되는 모든 테이블을 예상 합니다.

> [!NOTE]
> SQL 데이터 웨어하우스는 모든 종류의 데이터베이스 간 쿼리를 지원하지 않습니다. 따라서이 패턴을 활용 하는 데이터 웨어하우스 구현 toobe 수정 해야 합니다.
> 
> 

## <a name="recommendations"></a>권장 사항
사용자 정의 스키마를 사용하여 워크로드, 보안, 도메인 및 기능 경계를 통합하기 위한 권장 사항입니다.

1. 한 SQL 데이터 웨어하우스 데이터베이스 toorun 전체 데이터 웨어하우스 작업 사용
2. 기존 데이터 웨어하우스 환경 toouse 한 SQL 데이터 웨어하우스 데이터베이스를 통합 합니다.
3. 활용 **사용자 정의 스키마** tooprovide hello 경계 이전에 데이터베이스를 사용 하 여를 구현 합니다.

사용자 정의 스키마를 이전에 사용하지 않은 경우, 초기 상태입니다. Hello SQL 데이터 웨어하우스 데이터베이스에 사용자 정의 스키마에 대 한 hello 기준으로 이전 데이터베이스 이름을 hello를 사용 하면 됩니다.

스키마가 이미 사용된 경우 몇 가지 옵션이 있습니다.

1. Hello 레거시 스키마 이름을 제거 하 고 새로 시작
2. Hello 레거시 스키마 이름에는 미리 보류 중인 hello 레거시 스키마 이름 toohello 테이블 이름으로 유지
3. 추가 스키마 toore에 hello 테이블에 대해 뷰를 구현 하 여 hello 레거시 스키마 이름을 유지-hello 이전 스키마 구조를 만듭니다.

> [!NOTE]
> 첫 번째 검사에서 옵션 3 hello 가장 매력적인 옵션 처럼 보일 수 있습니다. 그러나 hello 악마 hello 세부 정보입니다. 뷰는 SQL 데이터 웨어하우스에서만 읽혀집니다. 데이터 또는 테이블 수정 하지 않고도 모든 toobe hello 기본 테이블에 대해 수행 해야 합니다. 또한 옵션 3은 시스템으로의 뷰 레이어를 소개합니다. 아키텍처의 뷰 이미 사용 중인 경우이 몇 가지 사항을 고려해 야 toogive 할 수 있습니다.
> 
> 

### <a name="examples"></a>예제:
데이터베이스 이름을 기반으로 사용자 정의 스키마를 구현합니다.

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for hello data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in hello stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in hello edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

유지 레거시 스키마 폴더 이름을 여 toohello 테이블 이름입니다. Hello 작업 경계에 대 한 스키마를 사용 합니다.

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines hello data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend hello old schema name toohello table and create in hello staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend hello old schema name toohello table and create in hello data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

뷰를 사용하여 레거시 스키마 이름을 유지합니다.

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines hello data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines hello legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create hello base staging tables in hello staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create hello base data warehouse tables in hello data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in hello legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> 스키마 전략에 변경 내용을 hello 데이터베이스에 대 한 hello 보안 모델의 검토를 해야합니다. 대부분의 경우에서 hello 스키마 수준에서 사용 권한을 할당 하 여 수 toosimplify hello 보안 모델을 수 있습니다. 보다 세부적인 사용 권한이 필요한 경우 데이터베이스 역할을 사용할 수 있습니다.
> 
> 

## <a name="next-steps"></a>다음 단계
더 많은 개발 팁은 [개발 개요][development overview]를 참조하세요.

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
