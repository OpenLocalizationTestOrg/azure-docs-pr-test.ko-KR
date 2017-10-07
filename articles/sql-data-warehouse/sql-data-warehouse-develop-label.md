---
title: "aaaUse SQL 데이터 웨어하우스에 tooinstrument 쿼리 레이블 | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스 레이블을 tooinstrument 쿼리를 사용 하 여 솔루션을 개발 하기 위한 팁입니다."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 44988de8-04c1-4fed-92be-e1935661a4e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 82e7ea98e1417134227f1d7c529fdaf2f1df3853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-labels-tooinstrument-queries-in-sql-data-warehouse"></a>SQL 데이터 웨어하우스에 레이블을 tooinstrument 쿼리를 사용 하 여
SQL 데이터 웨어하우스는 쿼리 레이블이라는 개념을 지원합니다. 좀더 깊이 들어가기 전에 한 예를 살펴보겠습니다.

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

이 마지막 줄 태그 hello 문자열 ' 내 쿼리 레이블 ' toohello 쿼리를 사용 합니다. Hello 레이블 쿼리 수 hello Dmv 통해 있으면 특히 유용 합니다. 문제가 되는 쿼리 아래로 메커니즘 tootrack 제공 및 toohelp ETL 실행을 통해 진행률을 확인할 수 있습니다.

여기서 좋은 명명 규칙이 큰 도움이 됩니다. 예를 들어 다음과 같은 ' 프로젝트: 프로시저: 문을: 주석 ' toouniquely 모든 hello 코드를 소스 제어에서에 hello 쿼리를 식별에 도움이 될 것입니다.

다음 쿼리를 사용 하는 hello를 사용할 수 있습니다 레이블에 의해 toosearch 동적 관리 뷰를 hello:

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> 쿼리할 때 대괄호 또는 큰따옴표로 hello 단어 레이블을 래핑하는 반드시 합니다. 레이블은 예약어이며 구분하지 않으면 오류를 야기합니다.
> 
> 

## <a name="next-steps"></a>다음 단계
더 많은 개발 팁은 [개발 개요][development overview]를 참조하세요.

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
