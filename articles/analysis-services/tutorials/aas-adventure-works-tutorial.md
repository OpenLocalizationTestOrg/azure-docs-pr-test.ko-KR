---
title: "aaa \"Azure Analysis Services Adventure Works 자습서 | \"Microsoft Docs"
description: "Azure Analysis Services에 대 한 hello Adventure Works 자습서 소개"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: 2df8b3ab4e8c4ffbe0086418d60fd2e2abd35e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-analysis-services---adventure-works-tutorial"></a><span data-ttu-id="9d799-103">Azure Analysis Services - Adventure Works 자습서</span><span class="sxs-lookup"><span data-stu-id="9d799-103">Azure Analysis Services - Adventure Works tutorial</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="9d799-104">이 자습서에서는 방법 단원을 제공 toocreate hello 1400 호환성 수준에서 테이블 형식 모델을 사용 하 여 배포 [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-104">This tutorial provides lessons on how toocreate and deploy a tabular model at hello 1400 compatibility level by using [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).</span></span>  

<span data-ttu-id="9d799-105">새로운 tooAnalysis 서비스 및 테이블 형식 모델링을 하는 경우이 자습서를 완료 hello 가장 빠른 방법은 toolearn 어떻게는 toocreate 및 기본 테이블 형식 모델을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-105">If you're new tooAnalysis Services and tabular modeling, completing this tutorial is hello quickest way toolearn how toocreate and deploy a basic tabular model.</span></span> <span data-ttu-id="9d799-106">Hello 필수 되 면 두 toothree 시간 toocomplete 간에 소요 될 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-106">Once you have hello prerequisites in-place, it should take between two toothree hours toocomplete.</span></span>  
  
## <a name="what-you-learn"></a><span data-ttu-id="9d799-107">학습 내용</span><span class="sxs-lookup"><span data-stu-id="9d799-107">What you learn</span></span>   
  
-   <span data-ttu-id="9d799-108">Hello에 toocreate 새 테이블 형식 모델 프로젝트 어떻게 **1400 호환성 수준이** SSDT에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-108">How toocreate a new tabular model project at hello **1400 compatibility level** in SSDT.</span></span>
  
-   <span data-ttu-id="9d799-109">어떻게 tooimport 데이터를 테이블 형식 모델 프로젝트에는 관계형 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-109">How tooimport data from a relational database into a tabular model project.</span></span>  
  
-   <span data-ttu-id="9d799-110">어떻게 toocreate 고 hello 모델의 테이블 간에 관계를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-110">How toocreate and manage relationships between tables in hello model.</span></span>  
  
-   <span data-ttu-id="9d799-111">어떻게 toocreate 계산 열, 측정값 및 핵심 성과 지표는 데 도움이 되는 중요 한 비즈니스 메트릭을 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-111">How toocreate calculated columns, measures, and Key Performance Indicators that help users analyze critical business metrics.</span></span>  
  
-   <span data-ttu-id="9d799-112">어떻게 toocreate 비즈니스 사용자와 응용 프로그램별 뷰포인트를 제공 하 여 모델 데이터를 검색 하는 사용자가 보다 쉽게 수 있도록 하는 계층 및 큐브 뷰를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-112">How toocreate and manage perspectives and hierarchies that help users more easily browse model data by providing business and application-specific viewpoints.</span></span>  
  
-   <span data-ttu-id="9d799-113">어떻게 toocreate 파티션이 있는 테이블 데이터 더 작은 논리적 부분으로 분할 다른 파티션과 별개로 처리할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-113">How toocreate partitions that divide table data into smaller logical parts that can be processed independent from other partitions.</span></span>  
  
-   <span data-ttu-id="9d799-114">어떻게 toosecure 사용자 멤버와 역할을 만들어 개체와 데이터를 모델링 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-114">How toosecure model objects and data by creating roles with user members.</span></span>  
  
-   <span data-ttu-id="9d799-115">어떻게 toodeploy 테이블 형식 모델 tooan **Azure Analysis Services** 서버 또는 온-프레미스 SQL Server 2017 Analysis Services 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-115">How toodeploy a tabular model tooan **Azure Analysis Services** server or an on-premises SQL Server 2017 Analysis Services server.</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="9d799-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9d799-116">Prerequisites</span></span>  
<span data-ttu-id="9d799-117">toocomplete 해야이 자습서에서는:</span><span class="sxs-lookup"><span data-stu-id="9d799-117">toocomplete this tutorial, you need:</span></span>  
  
-   <span data-ttu-id="9d799-118">Azure Analysis Services 또는 SQL Server 2017 Analysis Services 모델에 toodeploy 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="9d799-118">An Azure Analysis Services or SQL Server 2017 Analysis Services instance toodeploy your model to.</span></span> <span data-ttu-id="9d799-119">[Azure Analysis Services 평가판](https://azure.microsoft.com/services/analysis-services/)을 등록하고 [서버를 만듭니다](../analysis-services-create-server.md).</span><span class="sxs-lookup"><span data-stu-id="9d799-119">Sign up for a free [Azure Analysis Services trial](https://azure.microsoft.com/services/analysis-services/) and [create a server](../analysis-services-create-server.md).</span></span> <span data-ttu-id="9d799-120">또는 [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp)를 등록하여 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-120">Or, sign up and download [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp).</span></span> 

-   <span data-ttu-id="9d799-121">SQL Server 데이터 웨어하우스 또는 hello로 Azure SQL 데이터 웨어하우스 [AdventureWorksDW2014 예제 데이터베이스](http://go.microsoft.com/fwlink/?LinkID=335807)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-121">A SQL Server Data Warehouse or Azure SQL Data Warehouse with hello [AdventureWorksDW2014 sample database](http://go.microsoft.com/fwlink/?LinkID=335807).</span></span> <span data-ttu-id="9d799-122">이 예제 데이터베이스 hello 데이터 필요한 toocomplete이이 자습서에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-122">This sample database includes hello data necessary toocomplete this tutorial.</span></span> <span data-ttu-id="9d799-123">[SQL Server 평가판](https://www.microsoft.com/sql-server/sql-server-downloads)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-123">Download [SQL Server free editions](https://www.microsoft.com/sql-server/sql-server-downloads).</span></span> <span data-ttu-id="9d799-124">또는 [Azure SQL Database 평가판](https://azure.microsoft.com/services/sql-database/)을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-124">Or, sign up for a free [Azure SQL Database trial](https://azure.microsoft.com/services/sql-database/).</span></span> 

    <span data-ttu-id="9d799-125">**중요:** hello 예제 데이터베이스는 온-프레미스 SQL Server에 설치 하 고 모델 tooan Azure Analysis Services 서버를 배포 하는 [온-프레미스 데이터 게이트웨이](../analysis-services-gateway.md) 가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-125">**Important:** If you install hello sample database on an on-premises SQL Server, and you deploy your model tooan Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>

-   <span data-ttu-id="9d799-126">최신 버전의 hello [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-126">hello latest version of [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).</span></span>

-   <span data-ttu-id="9d799-127">최신 버전의 hello [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-127">hello latest version of [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>    

-   <span data-ttu-id="9d799-128">[Power BI Desktop](https://powerbi.microsoft.com/desktop/) 또는 Excel과 같은 클라이언트 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="9d799-128">A client application such as [Power BI Desktop](https://powerbi.microsoft.com/desktop/) or Excel.</span></span> 

## <a name="scenario"></a><span data-ttu-id="9d799-129">시나리오</span><span class="sxs-lookup"><span data-stu-id="9d799-129">Scenario</span></span>  
<span data-ttu-id="9d799-130">이 자습서는 가상의 회사인 Adventure Works Cycles를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-130">This tutorial is based on Adventure Works Cycles, a fictitious company.</span></span> <span data-ttu-id="9d799-131">Adventure Works를 생성 하 고 자전거, 파트 및 액세서리 toocommercial 시장 북미, 유럽 및 아시아에서 배포 하는 대규모의 다국적 제조 회사입니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-131">Adventure Works is a large, multinational manufacturing company that produces and distributes bicycles, parts, and accessories toocommercial markets in North America, Europe, and Asia.</span></span> <span data-ttu-id="9d799-132">hello 있으며 직원 수는 500 명입니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-132">hello company employs 500 workers.</span></span> <span data-ttu-id="9d799-133">또한 Adventure Works는 시장 기반 전체에 대한 여러 지역별 영업 팀을 고용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-133">Additionally, Adventure Works employs several regional sales teams throughout its market base.</span></span> <span data-ttu-id="9d799-134">프로젝트 toocreate 판매 및 마케팅 사용자 tooanalyze hello AdventureWorksDW 데이터베이스의 인터넷 매출 데이터에 대 한 테이블 형식 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-134">Your project is toocreate a tabular model for sales and marketing users tooanalyze Internet sales data in hello AdventureWorksDW database.</span></span>  
  
<span data-ttu-id="9d799-135">toocomplete hello 자습서에서는 다양 한 단원을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-135">toocomplete hello tutorial, you must complete various lessons.</span></span> <span data-ttu-id="9d799-136">각 단원에는 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-136">In each lesson, there are tasks.</span></span> <span data-ttu-id="9d799-137">순서로 각 태스크를 완료 하는 것은 hello 단원을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-137">Completing each task in order is necessary for completing hello lesson.</span></span> <span data-ttu-id="9d799-138">특정 단원에서 유사한 결과를 얻는 몇 가지 작업이 있을 수 있지만 각 작업을 완료하는 방법은 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-138">While in a particular lesson there may be several tasks that accomplish a similar outcome, but how you complete each task is slightly different.</span></span> <span data-ttu-id="9d799-139">이 종종는 방법 보여 줍니다 두 개 이상의 한 가지 방법은 toocomplete 작업, 및 toochallenge 이전 단원 및 작업에서 배운 기술을 사용 하 여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-139">This method shows there is often more than one way toocomplete a task, and toochallenge you by using skills you've learned in previous lessons and tasks.</span></span>  
  
<span data-ttu-id="9d799-140">hello hello 단원의 목적은 tooguide SSDT에 포함 된 hello 기능을 많이 사용 하 여 기본 테이블 형식 모델 제작 하는 과정입니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-140">hello purpose of hello lessons is tooguide you through authoring a basic tabular model by using many of hello features included in SSDT.</span></span> <span data-ttu-id="9d799-141">각 단원 hello 이전 단원에는 빌드, 때문에 hello 단원을 순서 대로 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-141">Because each lesson builds upon hello previous lesson, you should complete hello lessons in order.</span></span>
  
<span data-ttu-id="9d799-142">이 자습서 단원 SSMS를 사용 하거나 클라이언트를 사용 하 여 서버 또는 데이터베이스를 관리 하는 Azure 포털의 서버를 관리 하는 방법에 대 한 응용 프로그램 toobrowse 모델 데이터 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-142">This tutorial does not provide lessons about managing a server in Azure portal, managing a server or database by using SSMS, or using a client application toobrowse model data.</span></span> 


## <a name="lessons"></a><span data-ttu-id="9d799-143">단원</span><span class="sxs-lookup"><span data-stu-id="9d799-143">Lessons</span></span>  
<span data-ttu-id="9d799-144">이 자습서는 다음 단원 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-144">This tutorial includes hello following lessons:</span></span>  
  
|<span data-ttu-id="9d799-145">단원</span><span class="sxs-lookup"><span data-stu-id="9d799-145">Lesson</span></span>|<span data-ttu-id="9d799-146">예상된 시간 toocomplete</span><span class="sxs-lookup"><span data-stu-id="9d799-146">Estimated time toocomplete</span></span>|  
|----------|------------------------------|  
|[<span data-ttu-id="9d799-147">1 - 새 테이블 형식 모델 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="9d799-147">1 - Create a new tabular model project</span></span>](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)|<span data-ttu-id="9d799-148">10분</span><span class="sxs-lookup"><span data-stu-id="9d799-148">10 minutes</span></span>|  
|[<span data-ttu-id="9d799-149">2 - 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="9d799-149">2 - Get data</span></span>](../tutorials/aas-lesson-2-get-data.md)|<span data-ttu-id="9d799-150">10분</span><span class="sxs-lookup"><span data-stu-id="9d799-150">10 minutes</span></span>|  
|[<span data-ttu-id="9d799-151">3 - 날짜 테이블로 표시</span><span class="sxs-lookup"><span data-stu-id="9d799-151">3 - Mark as Date Table</span></span>](../tutorials/aas-lesson-3-mark-as-date-table.md)|<span data-ttu-id="9d799-152">3분</span><span class="sxs-lookup"><span data-stu-id="9d799-152">3 minutes</span></span>|  
|[<span data-ttu-id="9d799-153">4 - 관계 만들기</span><span class="sxs-lookup"><span data-stu-id="9d799-153">4 - Create relationships</span></span>](../tutorials/aas-lesson-4-create-relationships.md)|<span data-ttu-id="9d799-154">10분</span><span class="sxs-lookup"><span data-stu-id="9d799-154">10 minutes</span></span>|  
|[<span data-ttu-id="9d799-155">5 - 계산된 열 만들기</span><span class="sxs-lookup"><span data-stu-id="9d799-155">5 - Create calculated columns</span></span>](../tutorials/aas-lesson-5-create-calculated-columns.md)|<span data-ttu-id="9d799-156">15분</span><span class="sxs-lookup"><span data-stu-id="9d799-156">15 minutes</span></span>|
|[<span data-ttu-id="9d799-157">6 - 측정값 만들기</span><span class="sxs-lookup"><span data-stu-id="9d799-157">6 - Create measures</span></span>](../tutorials/aas-lesson-6-create-measures.md)|<span data-ttu-id="9d799-158">30분</span><span class="sxs-lookup"><span data-stu-id="9d799-158">30 minutes</span></span>|  
|[<span data-ttu-id="9d799-159">7 - KPI(핵심 성과 지표) 만들기</span><span class="sxs-lookup"><span data-stu-id="9d799-159">7 - Create Key Performance Indicators (KPI)</span></span>](../tutorials/aas-lesson-7-create-key-performance-indicators.md)|<span data-ttu-id="9d799-160">15분</span><span class="sxs-lookup"><span data-stu-id="9d799-160">15 minutes</span></span>|  
|[<span data-ttu-id="9d799-161">8 - 큐브 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="9d799-161">8 - Create perspectives</span></span>](../tutorials/aas-lesson-8-create-perspectives.md)|<span data-ttu-id="9d799-162">5분</span><span class="sxs-lookup"><span data-stu-id="9d799-162">5 minutes</span></span>|  
|[<span data-ttu-id="9d799-163">9 - 계층 구조 만들기</span><span class="sxs-lookup"><span data-stu-id="9d799-163">9 - Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)|<span data-ttu-id="9d799-164">20분</span><span class="sxs-lookup"><span data-stu-id="9d799-164">20 minutes</span></span>|  
|[<span data-ttu-id="9d799-165">10 - 파티션 만들기</span><span class="sxs-lookup"><span data-stu-id="9d799-165">10 - Create partitions</span></span>](../tutorials/aas-lesson-10-create-partitions.md)|<span data-ttu-id="9d799-166">15분</span><span class="sxs-lookup"><span data-stu-id="9d799-166">15 minutes</span></span>|  
|[<span data-ttu-id="9d799-167">11 - 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="9d799-167">11 - Create roles</span></span>](../tutorials/aas-lesson-11-create-roles.md)|<span data-ttu-id="9d799-168">15분</span><span class="sxs-lookup"><span data-stu-id="9d799-168">15 minutes</span></span>|  
|[<span data-ttu-id="9d799-169">12 - Excel에서 분석</span><span class="sxs-lookup"><span data-stu-id="9d799-169">12 - Analyze in Excel</span></span>](../tutorials/aas-lesson-12-analyze-in-excel.md)|<span data-ttu-id="9d799-170">5분</span><span class="sxs-lookup"><span data-stu-id="9d799-170">5 minutes</span></span>| 
|[<span data-ttu-id="9d799-171">13 - 배포</span><span class="sxs-lookup"><span data-stu-id="9d799-171">13 - Deploy</span></span>](../tutorials/aas-lesson-13-deploy.md)|<span data-ttu-id="9d799-172">5분</span><span class="sxs-lookup"><span data-stu-id="9d799-172">5 minutes</span></span>|  
  
## <a name="supplemental-lessons"></a><span data-ttu-id="9d799-173">추가 단원</span><span class="sxs-lookup"><span data-stu-id="9d799-173">Supplemental lessons</span></span>  
<span data-ttu-id="9d799-174">이러한 단원 필요한 toocomplete hello 자습서 없는 하지만 더 나은 이해 고급 테이블 형식 모델 제작 기능에에서 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-174">These lessons are not required toocomplete hello tutorial, but can be helpful in better understanding advanced tabular model authoring features.</span></span>  
  
|<span data-ttu-id="9d799-175">단원</span><span class="sxs-lookup"><span data-stu-id="9d799-175">Lesson</span></span>|<span data-ttu-id="9d799-176">예상된 시간 toocomplete</span><span class="sxs-lookup"><span data-stu-id="9d799-176">Estimated time toocomplete</span></span>|  
|----------|------------------------------|  
|[<span data-ttu-id="9d799-177">세부 정보 행</span><span class="sxs-lookup"><span data-stu-id="9d799-177">Detail Rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)|<span data-ttu-id="9d799-178">10분</span><span class="sxs-lookup"><span data-stu-id="9d799-178">10 minutes</span></span>|
|[<span data-ttu-id="9d799-179">동적 보안</span><span class="sxs-lookup"><span data-stu-id="9d799-179">Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)|<span data-ttu-id="9d799-180">30분</span><span class="sxs-lookup"><span data-stu-id="9d799-180">30 minutes</span></span>|
|[<span data-ttu-id="9d799-181">불규칙한 계층 구조</span><span class="sxs-lookup"><span data-stu-id="9d799-181">Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)|<span data-ttu-id="9d799-182">20분</span><span class="sxs-lookup"><span data-stu-id="9d799-182">20 minutes</span></span>| 

  
## <a name="next-steps"></a><span data-ttu-id="9d799-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9d799-183">Next steps</span></span>  
<span data-ttu-id="9d799-184">시작 tooget 참조 [1 단원: 새 테이블 형식 모델 프로젝트](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d799-184">tooget started, see [Lesson 1: Create a New Tabular Model Project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
  
  

