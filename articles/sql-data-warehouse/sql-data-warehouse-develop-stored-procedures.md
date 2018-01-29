---
title: "SQL Data Warehouse의 저장 프로시저 | Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 저장 프로시저 구현을 위한 팁"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 9b238789-6efe-4820-bf77-5a5da2afa0e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: e42d80f0ca35f3fbb67389c66d072bc40d8a8d2c
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a>SQL 데이터 웨어하우스의 저장된 프로시저
SQL 데이터 웨어하우스는 SQL Server에 있는 여러 TRANSACT-SQL 기능을 지원합니다. 무엇보다도 솔루션의 성능을 최대화하기 위해 활용하고자 하는 특정 기능 확장 사항이 있습니다.

그러나 SQL 데이터 웨어하우스의 크기와 성능을 유지하기 위해, 동작의 차이가 있는 일부 기능 및 지원되지 않는 일부 다른 기능이 있습니다.

이 문서에서는 SQL 데이터 웨어하우스 내 저장된 프로시저를 구현하는 방법을 설명합니다.

## <a name="introducing-stored-procedures"></a>저장된 프로시저 소개
저장된 프로시저는 SQL 코드를 캡슐화하여 데이터 웨어하우스의 데이터에 가까이 저장하는 좋은 방법입니다. 관리 가능한 단위로 코드를 캡슐화하여 저장된 프로시저를 사용하면 개발자가 솔루션을 모듈화하여 코드의 더 큰 재유용성을 용이하게 합니다. 각 저장된 프로시저로 매개 변수를 더 유연하게 할 수도 있습니다.

SQL 데이터 웨어하우스는 단순하고 효율적인 저장된 프로시저 구현을 제공합니다. SQL Server와 비교하여 가장 큰 차이점은 저장된 프로시저가 미리 컴파일된 코드가 아닙니다. 일반적으로 데이터 웨어하우스에서는 컴파일 시간을 덜 염려해도 됩니다. 큰 데이터 볼륨에 대해 작동할 때 저장된 프로시저 코드가 올바르게 최적화되는 것이 더욱 중요합니다. 시간, 분 및 초(밀리초가 아닌)를 저장하는 것이 목표입니다. 그러므로 저장된 프로시저를 SQL 논리에 대한 컨테이너로 생각하는 것이 더욱 도움이 됩니다.     

SQL 데이터 웨어하우스는 저장된 프로시저를 실행할 때 SQL 문이 구문 분석되고 변환되고 런타임 시 최적화됩니다. 이 프로세스 중 각 문이 분산 쿼리로 변환됩니다. 데이터에 대해 실제로 실행되는 SQL 코드는 전송된 쿼리와 다릅니다.

## <a name="nesting-stored-procedures"></a>중첩 저장 프로시저
저장된 프로시저가 다른 저장된 프로시저를 호출하거나 동적 sql을 실행하면 내부 저장된 프로시저 또는 코드 호출을 중첩된 것이라고 합니다.

SQL 데이터 웨어하우스는 최대 8개의 중첩 수준을 지원합니다. 이는 SQL Server와 약간 다릅니다. SQL Server의 중첩 수준은 32입니다.

상위 수준 저장된 프로시저 호출은 중첩 수준 1과 같습니다.

```sql
EXEC prc_nesting
```
저장된 프로시저는 또한 다른 EXEC 호출을 만든 다음 중첩 수준을 2로 증가시킵니다.

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
그 다음 두 번째 프로시저가 일부 동적 SQL을 실행하면 다음 중첩 수준이 3으로 증가합니다.

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

SQL Data Warehouse는 현재 @@NESTLEVEL을 지원하지 않습니다. 따라서 중첩 수준을 직접 추적해야 합니다. 8개의 중첩 수준 제한에 도달한 것 같지 않지만 도달한 경우 이 제한 내에 적합하도록 사용자 코드를 다시 작업하고 "평면화"해야 합니다.

## <a name="insertexecute"></a>INSERT..EXECUTE
SQL 데이터 웨어하우스는 INSERT 문을 사용하여 저장된 프로시저의 결과 집합을 사용하도록 허용하지 않습니다. 그러나 대체 방법을 사용할 수 있습니다.

이 작업을 수행하는 방법의 예는 [임시 테이블] 의 다음 문서를 참조하세요.

## <a name="limitations"></a>제한 사항
SQL 데이터 웨어하우스에서 구현되지 않은 TRANSACT-SQL 저장된 프로시저의 일부 측면이 있습니다.

아래에 이 계정과 키의 예제가 나와 있습니다.

* 임시 저장 프로시저
* 숫자가 매겨진 저장 프로시저
* 확장된 저장 프로시저
* CLR 저장 프로시저
* 암호화 옵션
* 복제 옵션
* 테이블 반환 매개 변수
* 읽기 전용 매개 변수
* 기본 매개 변수
* 실행 컨텍스트
* return 문

## <a name="next-steps"></a>다음 단계
더 많은 개발 팁은 [개발 개요][development overview]를 참조하세요.

<!--Image references-->

<!--Article references-->
[임시 테이블]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
