---
title: "SQL 데이터 웨어하우스의 절차에서는 aaaStored | Microsoft Docs"
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
ms.openlocfilehash: 416252dd3dea95c66aa5e886860b933b22578002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a>SQL 데이터 웨어하우스의 저장된 프로시저
SQL 데이터 웨어하우스 SQL Server에서 hello Transact SQL 기능을 많이 지원 합니다. 더욱 중요 한 확장 솔루션의 tooleverage toomaximize hello 성능을 하겠습니다 특정 기능은 있습니다.

그러나 toomaintain hello 배율 및 SQL 데이터 웨어하우스 성능은 또한 몇 가지 기능 및 동작의 차이 지원 되지 않는 다른 사용자가 있는 기능.

이 문서에서는 tooimplement SQL 데이터 웨어하우스 내에서 프로시저를 저장 하는 방법을 설명 합니다.

## <a name="introducing-stored-procedures"></a>저장된 프로시저 소개
저장된 프로시저는 SQL 코드를 캡슐화 하는 데 효과적인 방법 데이터를 저장 하기 닫기 tooyour hello 데이터 웨어하우스의 합니다. 관리 가능한 단위로 hello 코드를 캡슐화 하 여 저장된 프로시저는 개발자가 솔루션; 모듈화 도움말 코드의 큰 re-usability를 촉진 합니다. 각 저장된 프로시저 매개 변수 toomake 그대로 사용할 수도 훨씬 더 유연 합니다.

SQL 데이터 웨어하우스는 단순하고 효율적인 저장된 프로시저 구현을 제공합니다. hello 가장 큰 차이점 비교 tooSQL 서버는 저장된 프로시저를 hello 하는 미리 컴파일된 코드가 아닙니다. 데이터 웨어하우스에서 hello 컴파일 시간이 일반적으로 고려 하는입니다. 것이 더 중요 큰 데이터 볼륨에 대해 작동할 때 hello 저장 프로시저 코드 최적화 올바르게 됩니다. hello 목표 toosave 시간, 분 및 초 하지 밀리초입니다. 이 프로토콜은 따라서 저장된 프로시저의 더 유용한 toothink으로 SQL 논리에 대 한 컨테이너입니다.     

SQL 데이터 웨어하우스를 실행 하는 경우 저장된 프로시저 hello SQL 문의 분석, 변환 및 런타임 시 최적화. 이 프로세스 중 각 문이 분산 쿼리로 변환됩니다. hello hello 데이터에 대해 실제로 실행 되는 SQL 코드는 다른 toohello 쿼리를 제출 합니다.

## <a name="nesting-stored-procedures"></a>중첩 저장 프로시저
때 저장된 프로시저는 다른 저장된 프로시저를 호출 하거나 hello 내부 저장 프로시저 또는 toobe 중첩 된 블록의 코드 호출 이라고 하는 다음 동적 sql을 실행 합니다.

SQL 데이터 웨어하우스는 최대 8개의 중첩 수준을 지원합니다. 이 약간 다른 tooSQL 서버입니다. SQL Server의 중첩 수준 hello은 32입니다.

hello 상위 수준 저장된 프로시저 호출에는 toonest 수준을 1 것과 같습니다.

```sql
EXEC prc_nesting
```
Hello 저장 하는 경우 프로시저를 호출 하는 다른 EXEC을 사용 하면 다음 hello 중첩 수준 too2 늘어납니다.

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
두 번째 절차 hello 다음 몇 가지 동적 sql을 실행 하는 경우 다음 이렇게 하면 증가 hello 중첩 수준 too3

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

SQL Data Warehouse는 현재 @@NESTLEVEL을 지원하지 않습니다. 사용자가 직접 tookeep 중첩 수준의 트랙을 해야 합니다. Hello 8 중첩 수준 제한에 도달 합니다 있지만 있습니다를 수행 하는 경우는 코드 toore 일이 필요 하 고 "개체가 결합"는이 시간 동안 8 가능성이있지 않습니다.

## <a name="insertexecute"></a>INSERT..EXECUTE
SQL 데이터 웨어하우스에는 INSERT 문 사용 하는 저장된 프로시저의 tooconsume hello 결과 집합이 허용 하지 않습니다. 그러나 대체 방법을 사용할 수 있습니다.

Toohello 다음 문서를 참조 하십시오 [임시 테이블] 방법에 예제를 보려면 toodo이 합니다.

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
