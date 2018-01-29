---
title: "SQL Data Warehouse에서 레이블을 사용하여 쿼리 계측 | Microsoft Docs"
description: "솔루션 개발을 위해 Azure SQL 데이터 웨어하우스에서 레이블을 사용하여 쿼리를 계측하기 위한 팁."
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
ms.openlocfilehash: 9e75bbe528a427724a623305fbd45e2277e9d0af
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="use-labels-to-instrument-queries-in-sql-data-warehouse"></a>SQL 데이터 웨어하우스에서 레이블을 사용하여 쿼리 계측
SQL 데이터 웨어하우스는 쿼리 레이블이라는 개념을 지원합니다. 좀더 깊이 들어가기 전에 한 예를 살펴보겠습니다.

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

이 마지막 줄은 쿼리에 문자열 '내 쿼리 레이블' 태그를 추가합니다. 레이블은 DMV를 통해 쿼리가 가능하므로 이 태그는 특히 유용합니다. 이 기능은 문제 쿼리를 추적하는 메커니즘을 제공하며 ETL 실행을 통해 진행률을 식별하는 데에도 도움이 됩니다.

여기서 좋은 명명 규칙이 큰 도움이 됩니다. 예를 들어 ' PROJECT : PROCEDURE : STATEMENT : COMMENT' 같은 문은 원본 제어의 모든 코드 중에서 쿼리를 고유하게 식별하는 데 도움이 될 수 있습니다.

레이블 기준으로 검색하려면 동적 관리 보기를 사용하는 다음과 같은 쿼리를 사용할 수 있습니다.

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> 쿼리할 때 반드시 단어 레이블을 대괄호 또는 큰따옴표로 묶어야 합니다. 레이블은 예약어이며 구분하지 않으면 오류를 야기합니다.
> 
> 

## <a name="next-steps"></a>다음 단계
더 많은 개발 팁은 [개발 개요][development overview]를 참조하세요.

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
