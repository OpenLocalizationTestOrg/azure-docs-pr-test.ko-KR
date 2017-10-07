---
title: "R, Python 및 T-SQL을 사용 하 여 aaaSQL 서버 데이터 과학 연습 | Microsoft Docs"
description: "Hello 안내는 예제 SQL Server toodo 예측 분석에서는 R, Python 및 T-SQL을 사용 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: 009354304da6cd02c4fd3cf948b7fa7d488cc4e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-data-science-walkthroughs-using-r-python-and-t-sql"></a><span data-ttu-id="4abd2-103">R, Python 및 T-SQL을 사용하여 SQL Server 데이터 과학 연습</span><span class="sxs-lookup"><span data-stu-id="4abd2-103">SQL Server data science walkthroughs using R, Python and T-SQL</span></span>

<span data-ttu-id="4abd2-104">이 연습에서는 SQL Server, SQL Server R Services 및 SQL Server Python 서비스 toodo 예측 분석을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4abd2-104">These walkthroughs use SQL Server, SQL Server R Services, and SQL Server Python Services toodo predictive analytics.</span></span> <span data-ttu-id="4abd2-105">R 및 Python 코드는 저장 프로시저에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="4abd2-105">R and Python code is deployed in stored procedures.</span></span> <span data-ttu-id="4abd2-106">Hello 팀 데이터 과학 프로세스에에서 설명 된 hello 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4abd2-106">They follow hello steps outlined in hello Team Data Science Process.</span></span> <span data-ttu-id="4abd2-107">Hello 팀 데이터 과학 프로세스의 개요를 참조 하십시오. [데이터 과학 프로세스](data-science-process-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4abd2-107">For an overview of hello Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> 

<span data-ttu-id="4abd2-108">Hello 팀 데이터 과학 프로세스를 실행 하는 추가 데이터 과학 연습 hello 별로 그룹화 되어 **플랫폼** 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="4abd2-108">Additional data science walkthroughs that execute hello Team Data Science Process are grouped by hello **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-python-and-sql-queries-with-sql-server"></a><span data-ttu-id="4abd2-109">SQL Server과 함께 Python 및 SQL 쿼리를 사용하여 택시 팁 예측</span><span class="sxs-lookup"><span data-stu-id="4abd2-109">Predict taxi tips using Python and SQL queries with SQL Server</span></span> 

<span data-ttu-id="4abd2-110">hello [사용 하 여 SQL Server](machine-learning-data-science-process-sql-walkthrough.md) 연습 빌드하고 배포할 컴퓨터 학습 분류 보여주며, SQL Server 및 공개적으로 사용할 수 있는 NYC를 사용 하 여 회귀 모델 택시 여행 및 요금 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="4abd2-110">hello [Use SQL Server](machine-learning-data-science-process-sql-walkthrough.md) walkthrough shows how you build and deploy machine learning classification and regression models using SQL Server and a publicly available NYC taxi trip and fare dataset.</span></span>


## <a name="predict-taxi-tips-using-microsoft-r-with-sql-server"></a><span data-ttu-id="4abd2-111">SQL Server와 함께 Microsoft R을 사용하여 택시 팁 예측</span><span class="sxs-lookup"><span data-stu-id="4abd2-111">Predict taxi tips using Microsoft R with SQL Server</span></span> 

<span data-ttu-id="4abd2-112">hello [사용 하 여 SQL Server R Services](https://msdn.microsoft.com/library/mt612857.aspx) 연습에서는 데이터 과학자는 R 코드를 SQL Server 데이터를 조합 하 여 제공 및 사용자 지정 SQL toobuild 함수 및 R 모델 tooSQL 서버를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="4abd2-112">hello [Use SQL Server R Services](https://msdn.microsoft.com/library/mt612857.aspx) walkthrough provides data scientists with a combination of R code, SQL Server data, and custom SQL functions toobuild and deploy an R model tooSQL Server.</span></span> <span data-ttu-id="4abd2-113">연습 hello은 설계 된 toointroduce R 개발자 tooR Services (In-database).</span><span class="sxs-lookup"><span data-stu-id="4abd2-113">hello walkthrough is designed toointroduce R developers tooR Services (In-Database).</span></span>


## <a name="predict-taxi-tips-using-r-from-t-sql-or-stored-procedures-with-sql-server"></a><span data-ttu-id="4abd2-114">SQL Server와 함께 T SQL 또는 저장 프로시저에서 R을 사용하여 택시 팁 예측</span><span class="sxs-lookup"><span data-stu-id="4abd2-114">Predict taxi tips using R from T-SQL or stored procedures with SQL Server</span></span>

<span data-ttu-id="4abd2-115">hello [R 및 SQL Server에 대 한 데이터 과학 연습](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/walkthrough-data-science-end-to-end-walkthrough) transact-sql는 고급 분석 솔루션을 구축 experience와 함께 SQL 프로그래머를 제공 합니다. SQL Server R Services toooperationalize R 솔루션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4abd2-115">hello [Data science walkthrough for R and SQL Server](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/walkthrough-data-science-end-to-end-walkthrough) provides SQL programmers with experience building an advanced analytics solution with Transact-SQL using SQL Server R Services toooperationalize an R solution.</span></span> 


## <a name="predict-taxi-tips-using-python-in-sql-server-stored-procedures"></a><span data-ttu-id="4abd2-116">SQL Server 저장 프로시저에서 Python을 사용하여 택시 팁 예측</span><span class="sxs-lookup"><span data-stu-id="4abd2-116">Predict taxi tips using Python in SQL Server stored procedures</span></span>

<span data-ttu-id="4abd2-117">hello [SQL Server Python 서비스와 함께 사용 하 여 T-SQL](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers) 연습에서는 기계 학습에서 SQL Server 솔루션을 구축 experience와 함께 SQL 프로그래머를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4abd2-117">hello [Use T-SQL with SQL Server Python Services](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers) walkthrough provides SQL programmers with experience building a machine learning solution in SQL Server.</span></span> <span data-ttu-id="4abd2-118">코드를 보여 줍니다 방법을 tooincorporate Python Python toostored 프로시저 코드를 추가 하 여 응용 프로그램으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4abd2-118">It demonstrates how tooincorporate Python into an application by adding Python code toostored procedures.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4abd2-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4abd2-119">Next steps</span></span>

<span data-ttu-id="4abd2-120">Hello 팀 데이터 과학 프로세스를 구성 하는 hello 주요 구성 요소의 논의 알려면 [팀 데이터 과학 프로세스 개요](data-science-process-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4abd2-120">For a discussion of hello key components that comprise hello Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="4abd2-121">데이터 과학 프로젝트, 참조에 대 한 설명은 한 toostructure를 사용할 수 있는 hello 팀 데이터 과학 프로세스 수명 주기 [팀 데이터 과학 프로세스 수명 주기](data-science-process-lifecycle.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4abd2-121">For a discussion of hello Team Data Science Process lifecycle that you can use toostructure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="4abd2-122">hello 수명 주기에서 다음에 나오는 프로젝트 일반적으로 실행 될 때 시작 toofinish hello 단계를 간략하게 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4abd2-122">hello lifecycle outlines hello steps, from start toofinish, that projects usually follow when they are executed.</span></span> 
