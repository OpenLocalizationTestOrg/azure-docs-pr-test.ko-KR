---
title: "SQL 데이터 웨어하우스에 SQL aaaDynamic | Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 동적 SQL 사용 팁."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: a948c2c3-3cd1-4373-90a9-79e59414b778
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 4d66eecb37621510f657d1ec9a2a935daaa16052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-sql-in-sql-data-warehouse"></a>SQL 데이터 웨어하우스의 동적 SQL
필요한 다음과 같은 행위는 SQL 데이터 웨어하우스에 대 한 응용 프로그램 코드를 개발할 때 toouse 동적 sql toohelp 배달 유연 하 고 제네릭 모듈식 솔루션입니다. SQL 데이터 웨어하우스는 현재 Blob 데이터 형식을 지원하지 않습니다. : Blob 형식 모두 varchar (max) 및 nvarchar (max) 형식에 포함 된 문자열의 hello 크기를 제한할 수 있습니다이 합니다. 이러한 형식은 응용 프로그램 코드에서 매우 큰 문자열을 작성할 때를 사용한 경우 청크 및 사용 하 여 hello EXEC 문을 toobreak hello 코드 대신 해야 합니다.

간단한 예는 다음과 같습니다.

```sql
DECLARE @sql_fragment1 VARCHAR(8000)=' SELECT name '
,       @sql_fragment2 VARCHAR(8000)=' FROM sys.system_views '
,       @sql_fragment3 VARCHAR(8000)=' WHERE name like ''%table%''';

EXEC( @sql_fragment1 + @sql_fragment2 + @sql_fragment3);
```

Hello 문자열은 짧은 경우 사용할 수 있습니다 [sp_executesql] [ sp_executesql] 정상적으로 합니다.

> [!NOTE]
> 동적 SQL로 실행 되는 문은 제목 tooall TSQL 유효성 검사 규칙을 수 있습니다.
> 
> 

## <a name="next-steps"></a>다음 단계
더 많은 개발 팁은 [개발 개요][development overview]를 참조하세요.

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[sp_executesql]: https://msdn.microsoft.com/library/ms188001.aspx

<!--Other Web references-->
