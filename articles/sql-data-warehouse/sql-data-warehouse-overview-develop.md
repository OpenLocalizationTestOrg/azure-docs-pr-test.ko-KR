---
title: "Azure에서 데이터 웨어하우스를 개발 하기 위한 aaaResources | Microsoft Docs"
description: "SQL 데이터 웨어하우스에 대한 개발 개념, 디자인 결정, 권장 사항 및 코딩 기술입니다."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: barbkess
editor: 
ms.assetid: 996e3afc-c21c-4e21-b9df-997f953f6dfd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: develop
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 67e3a6a3e2664919c3445ea5d5eba251054de020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="design-decisions-and-coding-techniques-for-sql-data-warehouse"></a>SQL 데이터 웨어하우스에 대한 디자인 결정 및 코딩 기술
SQL 데이터 웨어하우스에 대 한 중요 한 설계 결정 사항, 권장 사항 및 코딩 기술 toobetter 이해 이러한 개발 문서를 통해를 사용 합니다.

## <a name="key-design-decisions"></a>주요 디자인 결정
hello 다음 문서 강조 hello 주요 개념 및 디자인 결정 사항을 toounderstand SQL 데이터 웨어하우스를 사용 하 여 분산된 된 데이터 웨어하우스를 hello 개발에 대 한 일부:

* [연결][connections]
* [동시성][concurrency]
* [트랜잭션][transactions]
* [사용자 정의 스키마][user-defined schemas]
* [테이블 배포][table distribution]
* [테이블 인덱스][table indexes]
* [테이블 파티션][table partitions]
* [CTAS][CTAS]
* [통계][statistics]

## <a name="development-recommendations-and-coding-techniques"></a>개발 권장 사항 및 코딩 기술
이러한 문서에는 SQL 데이터 웨어하우스 개발을 위한 구체적인 코딩 기술, 팁 및 권장 사항이 요약되어 있습니다.

* [저장 프로시저][stored procedures]
* [레이블][labels]
* [뷰][views]
* [임시 테이블][temporary tables]
* [동적 SQL][dynamic SQL]
* [반복][looping]
* [옵션으로 그룹화][group by options]
* [변수 할당][variable assignment]

## <a name="next-steps"></a>다음 단계
Hello 개발 문서를 통해 되 면 hello 통해 수행 [TRANSACT-SQL 참조] [ Transact-SQL reference] SQL 데이터 웨어하우스에 대 한 지원 hello 구문에 대 한 자세한 내용은 페이지입니다.

<!--Image references-->

<!--Article references-->
[concurrency]: ./sql-data-warehouse-develop-concurrency.md
[connections]: ./sql-data-warehouse-connect-overview.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[dynamic SQL]: ./sql-data-warehouse-develop-dynamic-sql.md
[group by options]: ./sql-data-warehouse-develop-group-by-options.md
[labels]: ./sql-data-warehouse-develop-label.md
[looping]: ./sql-data-warehouse-develop-loops.md
[statistics]: ./sql-data-warehouse-tables-statistics.md
[stored procedures]: ./sql-data-warehouse-develop-stored-procedures.md
[table distribution]: ./sql-data-warehouse-tables-distribute.md
[table indexes]: ./sql-data-warehouse-tables-index.md
[table partitions]: ./sql-data-warehouse-tables-partition.md
[temporary tables]: ./sql-data-warehouse-tables-temporary.md
[transactions]: ./sql-data-warehouse-develop-transactions.md
[user-defined schemas]: ./sql-data-warehouse-develop-user-defined-schemas.md
[variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[views]: ./sql-data-warehouse-develop-views.md
[Transact-SQL reference]: ./sql-data-warehouse-overview-reference.md

<!--MSDN references-->
[renaming objects]: https://msdn.microsoft.com/library/mt631611.aspx

<!--Other Web references-->
