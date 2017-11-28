---
title: "Azure SQL Data Warehouse의 사용자 쿼리 모니터링 | Microsoft Docs"
description: "고려 사항, 모범 사례 및 Azure SQL 데이터 웨어하우스의 사용자 쿼리 모니터링 작업 개요입니다."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 1d0960db-5dcf-4a08-b1dc-6c5d3d5a616d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 65509a65c2b34553822cc02d7a7fa5a614adc57f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-user-queries-in-azure-sql-data-warehouse"></a><span data-ttu-id="f5f71-103">Azure SQL 데이터 웨어하우스의 사용자 쿼리 모니터링</span><span class="sxs-lookup"><span data-stu-id="f5f71-103">Monitor user queries in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="f5f71-104">고려 사항, 모범 사례 및 SQL 데이터 웨어하우스의 사용자 쿼리 모니터링 작업 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f71-104">Overview of the considerations, best practices, and tasks for monitoring user queries in SQL Data Warehouse.</span></span>

| <span data-ttu-id="f5f71-105">Category</span><span class="sxs-lookup"><span data-stu-id="f5f71-105">Category</span></span> | <span data-ttu-id="f5f71-106">작업 또는 고려 사항</span><span class="sxs-lookup"><span data-stu-id="f5f71-106">Task or consideration</span></span> | <span data-ttu-id="f5f71-107">설명</span><span class="sxs-lookup"><span data-stu-id="f5f71-107">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f5f71-108">성능 저하</span><span class="sxs-lookup"><span data-stu-id="f5f71-108">Slow performance</span></span> |<span data-ttu-id="f5f71-109">장기 실행 사용자 쿼리 찾기</span><span class="sxs-lookup"><span data-stu-id="f5f71-109">Find a long-running user query</span></span> |<span data-ttu-id="f5f71-110">[장기 실행 쿼리 찾기][Find long-running queries]</span><span class="sxs-lookup"><span data-stu-id="f5f71-110">[Find long-running queries][Find long-running queries]</span></span> |
| <span data-ttu-id="f5f71-111">동시성</span><span class="sxs-lookup"><span data-stu-id="f5f71-111">Concurrency</span></span> |<span data-ttu-id="f5f71-112">사용자 쿼리에 동시 리소스 할당</span><span class="sxs-lookup"><span data-stu-id="f5f71-112">Assign concurrent resources to user queries</span></span> |<span data-ttu-id="f5f71-113">[동시성 및 워크로드 관리][Concurrency and workload management]</span><span class="sxs-lookup"><span data-stu-id="f5f71-113">[Concurrency and workload management][Concurrency and workload management]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f5f71-114">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f5f71-114">Next steps</span></span>
<span data-ttu-id="f5f71-115">추가 관리 팁을 보려면 [관리 개요][Management overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5f71-115">For more management tips, head over to the [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Find long-running queries]: sql-data-warehouse-manage-monitor.md
[Concurrency and workload management]: sql-data-warehouse-develop-concurrency.md
[Management overview]: sql-data-warehouse-overview-manage.md

<!--MSDN references-->


<!--Other Web references-->
