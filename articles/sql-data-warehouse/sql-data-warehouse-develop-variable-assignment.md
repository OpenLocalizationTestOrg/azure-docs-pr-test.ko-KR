---
title: "SQL 데이터 웨어하우스에 aaaAssign 변수 | Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 Transact-SQL 변수 할당을 위한 팁"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 81ddc7cf-a6ba-4585-91a3-b6ea50f49227
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 9de48739bb0af80ff2a117704b31512c680f78d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a>SQL 데이터 웨어하우스의 변수 할당
SQL 데이터 웨어하우스에 변수 hello를 사용 하 여 설정 `DECLARE` 문이나 hello `SET` 문.

Hello 다음 모두 완벽 하 게 올바른 방법 tooset 변수 값:

## <a name="setting-variables-with-declare"></a>DECLARE를 사용하여 변수 설정
DECLARE 변수 초기화 hello 가장 유연한 방법 tooset SQL 데이터 웨어하우스에 변수 값 중 하나입니다.

```sql
DECLARE @v  int = 0
;
```

한 번에 변수를 하나 이상 DECLARE tooset 사용할 수 있습니다. 사용할 수 없는 `SELECT` 또는 `UPDATE` toodo이:

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

초기화할 수 없으며 변수를 사용 하 여 hello에 동일한 DECLARE 문이 있습니다. 아래 tooillustrate hello 지점 hello 예제 **하지** 으로 허용 @p1 모두 초기화 되 고 hello에 사용 된 동일한 DECLARE 문을 합니다. 그러면 오류가 발생합니다.

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a>SET을 사용하여 값 설정
집합은 단일 변수를 설정하기 위한 매우 일반적인 방법입니다.

모든 아래 hello 예제는 올바른 방법 집합을 사용 하 여 변수를 설정입니다.

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

SET을 사용하여 한 번에 하나의 변수만 설정할 수 있습니다. 그러나 위에서 설명한 것처럼 복합 연산자가 허용됩니다.

## <a name="limitations"></a>제한 사항
변수 할당에 SELECT 또는 UPDATE를 사용할 수 없습니다.

## <a name="next-steps"></a>다음 단계
더 많은 개발 팁은 [개발 개요][development overview]를 참조하세요.

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
