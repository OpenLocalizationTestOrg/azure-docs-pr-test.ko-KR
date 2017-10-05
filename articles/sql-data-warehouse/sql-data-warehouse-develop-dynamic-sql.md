---
title: "SQL Data Warehouse의 동적 SQL | Microsoft Docs"
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
ms.openlocfilehash: 29228676373aee8dbc7b1b2a7d92ffc978333804
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="dynamic-sql-in-sql-data-warehouse"></a><span data-ttu-id="29d4e-103">SQL 데이터 웨어하우스의 동적 SQL</span><span class="sxs-lookup"><span data-stu-id="29d4e-103">Dynamic SQL in SQL Data Warehouse</span></span>
<span data-ttu-id="29d4e-104">SQL 데이터 웨어하우스용 응용 프로그램 코드를 개발할 때 유연하고 일반적인 모듈식 솔루션을 제공하기 위해 동적 SQL을 사용해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29d4e-104">When developing application code for SQL Data Warehouse you may need to use dynamic sql to help deliver flexible, generic and modular solutions.</span></span> <span data-ttu-id="29d4e-105">SQL 데이터 웨어하우스는 현재 Blob 데이터 형식을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29d4e-105">SQL Data Warehouse does not support blob data types at this time.</span></span> <span data-ttu-id="29d4e-106">따라서 Blob 유형에 varchar(max) 및 nvarchar(max) 형식이 모두 포함되므로 문자열 크기가 제한될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29d4e-106">This may limit the size of your strings as blob types include both varchar(max) and nvarchar(max) types.</span></span> <span data-ttu-id="29d4e-107">매우 큰 문자열을 작성할 때 이러한 형식을 응용 프로그램 코드에 사용하는 경우 코드를 청크로 나누고 EXEC 문을 대신 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29d4e-107">If you have used these types in your application code when building very large strings, you will need to break the code into chunks and use the EXEC statement instead.</span></span>

<span data-ttu-id="29d4e-108">간단한 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="29d4e-108">A simple example:</span></span>

```sql
DECLARE @sql_fragment1 VARCHAR(8000)=' SELECT name '
,       @sql_fragment2 VARCHAR(8000)=' FROM sys.system_views '
,       @sql_fragment3 VARCHAR(8000)=' WHERE name like ''%table%''';

EXEC( @sql_fragment1 + @sql_fragment2 + @sql_fragment3);
```

<span data-ttu-id="29d4e-109">문자열이 짧은 경우 일반적으로 [sp_executesql][sp_executesql]을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29d4e-109">If the string is short you can use [sp_executesql][sp_executesql] as normal.</span></span>

> [!NOTE]
> <span data-ttu-id="29d4e-110">동적 SQL로 실행되는 문은 모든 TSQL 유효성 검사 규칙에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="29d4e-110">Statements executed as dynamic SQL will still be subject to all TSQL validation rules.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="29d4e-111">다음 단계</span><span class="sxs-lookup"><span data-stu-id="29d4e-111">Next steps</span></span>
<span data-ttu-id="29d4e-112">더 많은 개발 팁은 [개발 개요][development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29d4e-112">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[sp_executesql]: https://msdn.microsoft.com/library/ms188001.aspx

<!--Other Web references-->
