---
title: "R, Python 및 T-SQL을 사용하여 SQL Server 데이터 과학 연습 | Microsoft Docs"
description: "예측 분석을 수행하기 위해 SQL Server에서 R, Python 및 T-SQL을 사용하는 과정을 안내하는 예제입니다."
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
ms.openlocfilehash: 333fd4ee6dcdcbfd347d6b5e8cb900474f6ec8cc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="sql-server-data-science-walkthroughs-using-r-python-and-t-sql"></a><span data-ttu-id="e3d74-103">R, Python 및 T-SQL을 사용하여 SQL Server 데이터 과학 연습</span><span class="sxs-lookup"><span data-stu-id="e3d74-103">SQL Server data science walkthroughs using R, Python and T-SQL</span></span>

<span data-ttu-id="e3d74-104">이 연습에서는 SQL Server, SQL Server R Services 및 SQL Server Python Services를 사용하여 예측 분석을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e3d74-104">These walkthroughs use SQL Server, SQL Server R Services, and SQL Server Python Services to do predictive analytics.</span></span> <span data-ttu-id="e3d74-105">R 및 Python 코드는 저장 프로시저에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3d74-105">R and Python code is deployed in stored procedures.</span></span> <span data-ttu-id="e3d74-106">Team Data Science Process에 설명된 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e3d74-106">They follow the steps outlined in the Team Data Science Process.</span></span> <span data-ttu-id="e3d74-107">Team Data Science Process의 개요는 [데이터 과학 프로세스](data-science-process-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3d74-107">For an overview of the Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> 

<span data-ttu-id="e3d74-108">Team Data Science Process를 실행하는 추가 데이터 과학 연습은 사용하는 **플랫폼**에 따라 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3d74-108">Additional data science walkthroughs that execute the Team Data Science Process are grouped by the **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-python-and-sql-queries-with-sql-server"></a><span data-ttu-id="e3d74-109">SQL Server과 함께 Python 및 SQL 쿼리를 사용하여 택시 팁 예측</span><span class="sxs-lookup"><span data-stu-id="e3d74-109">Predict taxi tips using Python and SQL queries with SQL Server</span></span> 

<span data-ttu-id="e3d74-110">[SQL Server 사용](machine-learning-data-science-process-sql-walkthrough.md) 연습에서는 SQL Server와 공개적으로 사용 가능한 NYC Taxi Trip 및 요금 데이터 집합을 사용하여 기계 학습 분류 및 회귀 모델을 구축하고 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e3d74-110">The [Use SQL Server](machine-learning-data-science-process-sql-walkthrough.md) walkthrough shows how you build and deploy machine learning classification and regression models using SQL Server and a publicly available NYC taxi trip and fare dataset.</span></span>


## <a name="predict-taxi-tips-using-microsoft-r-with-sql-server"></a><span data-ttu-id="e3d74-111">SQL Server와 함께 Microsoft R을 사용하여 택시 팁 예측</span><span class="sxs-lookup"><span data-stu-id="e3d74-111">Predict taxi tips using Microsoft R with SQL Server</span></span> 

<span data-ttu-id="e3d74-112">[SQL Server R 서비스 사용](https://msdn.microsoft.com/library/mt612857.aspx) 연습에서는 R 코드, SQL Server 데이터 및 사용자 지정 SQL 함수를 조합한 데이터 과학자를 제공하여 SQL Server에 R 모델을 구축하고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e3d74-112">The [Use SQL Server R Services](https://msdn.microsoft.com/library/mt612857.aspx) walkthrough provides data scientists with a combination of R code, SQL Server data, and custom SQL functions to build and deploy an R model to SQL Server.</span></span> <span data-ttu-id="e3d74-113">이 연습은 R 개발자에게 R Services(데이터베이스 내)를 소개하기 위해 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e3d74-113">The walkthrough is designed to introduce R developers to R Services (In-Database).</span></span>


## <a name="predict-taxi-tips-using-r-from-t-sql-or-stored-procedures-with-sql-server"></a><span data-ttu-id="e3d74-114">SQL Server와 함께 T SQL 또는 저장 프로시저에서 R을 사용하여 택시 팁 예측</span><span class="sxs-lookup"><span data-stu-id="e3d74-114">Predict taxi tips using R from T-SQL or stored procedures with SQL Server</span></span>

<span data-ttu-id="e3d74-115">[R 및 SQL Server에 대한 데이터 과학 연습](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/walkthrough-data-science-end-to-end-walkthrough)은 R 솔루션을 작동시키는 SQL Server R Services를 사용하여 Transact-SQL과 함께 고급 분석 솔루션을 구축하는 경험을 SQL 프로그래머에게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e3d74-115">The [Data science walkthrough for R and SQL Server](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/walkthrough-data-science-end-to-end-walkthrough) provides SQL programmers with experience building an advanced analytics solution with Transact-SQL using SQL Server R Services to operationalize an R solution.</span></span> 


## <a name="predict-taxi-tips-using-python-in-sql-server-stored-procedures"></a><span data-ttu-id="e3d74-116">SQL Server 저장 프로시저에서 Python을 사용하여 택시 팁 예측</span><span class="sxs-lookup"><span data-stu-id="e3d74-116">Predict taxi tips using Python in SQL Server stored procedures</span></span>

<span data-ttu-id="e3d74-117">[SQL Server Python 서비스와 함께 T-SQL 사용](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers) 연습에서는 SQL 프로그래머에게 SQL Server에서의 Machine Learning 솔루션 구축 경험을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e3d74-117">The [Use T-SQL with SQL Server Python Services](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers) walkthrough provides SQL programmers with experience building a machine learning solution in SQL Server.</span></span> <span data-ttu-id="e3d74-118">저장된 프로시저에 Python 코드를 추가하여 Python을 응용 프로그램으로 통합하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e3d74-118">It demonstrates how to incorporate Python into an application by adding Python code to stored procedures.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e3d74-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e3d74-119">Next steps</span></span>

<span data-ttu-id="e3d74-120">Team Data Science Process를 구성하는 주요 구성의 논의는 [Team Data Science Process 개요](data-science-process-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3d74-120">For a discussion of the key components that comprise the Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="e3d74-121">데이터 과학 프로젝트를 구성하는 데 사용할 수 있는 Team Data Science Process 수명 주기의 논의는 [Team Data Science Process 수명 주기](data-science-process-lifecycle.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3d74-121">For a discussion of the Team Data Science Process lifecycle that you can use to structure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="e3d74-122">수명 주기는 일반적으로 프로젝트가 실행될 때 시작부터 끝까지 따라야 하는 단계를 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e3d74-122">The lifecycle outlines the steps, from start to finish, that projects usually follow when they are executed.</span></span> 