---
title: "Azure Analysis Services Adventure Works 자습서 | Microsoft Docs"
description: "Azure Analysis Services에 대한 Adventure Works 자습서 소개"
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
ms.openlocfilehash: 257e0bc442f29bfe6683fb0511deac50d92c1720
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-analysis-services---adventure-works-tutorial"></a><span data-ttu-id="b2946-103">Azure Analysis Services - Adventure Works 자습서</span><span class="sxs-lookup"><span data-stu-id="b2946-103">Azure Analysis Services - Adventure Works tutorial</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="b2946-104">이 자습서에서는 [SSDT(SQL Server 데이터 도구)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)를 사용하여 1400 호환성 수준에서 테이블 형식 모델을 만들고 배포하는 방법에 대한 단원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-104">This tutorial provides lessons on how to create and deploy a tabular model at the 1400 compatibility level by using [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).</span></span>  

<span data-ttu-id="b2946-105">Analysis Services 및 테이블 형식 모델링을 처음 접하는 경우 이 자습서를 완료하는 것이 기본 테이블 형식 모델을 만들고 배포하는 가장 빠른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-105">If you're new to Analysis Services and tabular modeling, completing this tutorial is the quickest way to learn how to create and deploy a basic tabular model.</span></span> <span data-ttu-id="b2946-106">필수 구성 요소를 마련한 후 완료하는 데 2-3시간 사이가 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-106">Once you have the prerequisites in-place, it should take between two to three hours to complete.</span></span>  
  
## <a name="what-you-learn"></a><span data-ttu-id="b2946-107">학습 내용</span><span class="sxs-lookup"><span data-stu-id="b2946-107">What you learn</span></span>   
  
-   <span data-ttu-id="b2946-108">SSDT에서 **1400 호환성 수준**으로 새 테이블 형식 모델 프로젝트를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="b2946-108">How to create a new tabular model project at the **1400 compatibility level** in SSDT.</span></span>
  
-   <span data-ttu-id="b2946-109">관계형 데이터베이스에서 테이블 형식 모델 프로젝트로 데이터를 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="b2946-109">How to import data from a relational database into a tabular model project.</span></span>  
  
-   <span data-ttu-id="b2946-110">모델의 테이블 간에 관계를 만들고 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="b2946-110">How to create and manage relationships between tables in the model.</span></span>  
  
-   <span data-ttu-id="b2946-111">계산된 열, 측정값 및 사용자가 중요한 비즈니스 메트릭을 분석하는 데 도움이 되는 핵심 성과 지표를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="b2946-111">How to create calculated columns, measures, and Key Performance Indicators that help users analyze critical business metrics.</span></span>  
  
-   <span data-ttu-id="b2946-112">비즈니스 및 응용 프로그램별 관점을 제공하여 사용자가 모델 데이터를 보다 쉽게 찾아볼 수 있도록 큐브 뷰 및 계층 구조를 만들고 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="b2946-112">How to create and manage perspectives and hierarchies that help users more easily browse model data by providing business and application-specific viewpoints.</span></span>  
  
-   <span data-ttu-id="b2946-113">다른 파티션과 독립적으로 처리할 수 있는 더 작은 논리 부분으로 테이블 데이터를 분할하는 파티션을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="b2946-113">How to create partitions that divide table data into smaller logical parts that can be processed independent from other partitions.</span></span>  
  
-   <span data-ttu-id="b2946-114">사용자 멤버와 역할을 만들어 모델 개체와 데이터를 보호하는 방법</span><span class="sxs-lookup"><span data-stu-id="b2946-114">How to secure model objects and data by creating roles with user members.</span></span>  
  
-   <span data-ttu-id="b2946-115">테이블 형식 모델을 **Azure Analysis Services** 서버나 온-프레미스 SQL Server 2017 Analysis Services 서버에 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="b2946-115">How to deploy a tabular model to an **Azure Analysis Services** server or an on-premises SQL Server 2017 Analysis Services server.</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="b2946-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b2946-116">Prerequisites</span></span>  
<span data-ttu-id="b2946-117">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-117">To complete this tutorial, you need:</span></span>  
  
-   <span data-ttu-id="b2946-118">모델을 배포할 Azure Analysis Services 또는 SQL Server 2017 Analysis Services 인스턴스</span><span class="sxs-lookup"><span data-stu-id="b2946-118">An Azure Analysis Services or SQL Server 2017 Analysis Services instance to deploy your model to.</span></span> <span data-ttu-id="b2946-119">[Azure Analysis Services 평가판](https://azure.microsoft.com/services/analysis-services/)을 등록하고 [서버를 만듭니다](../analysis-services-create-server.md).</span><span class="sxs-lookup"><span data-stu-id="b2946-119">Sign up for a free [Azure Analysis Services trial](https://azure.microsoft.com/services/analysis-services/) and [create a server](../analysis-services-create-server.md).</span></span> <span data-ttu-id="b2946-120">또는 [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp)를 등록하여 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-120">Or, sign up and download [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp).</span></span> 

-   <span data-ttu-id="b2946-121">[AdventureWorksDW2014 예제 데이터베이스](http://go.microsoft.com/fwlink/?LinkID=335807)가 있는 SQL Server 또는 Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b2946-121">A SQL Server Data Warehouse or Azure SQL Data Warehouse with the [AdventureWorksDW2014 sample database](http://go.microsoft.com/fwlink/?LinkID=335807).</span></span> <span data-ttu-id="b2946-122">이 예제 데이터베이스에는 이 자습서를 완료하는 데 필요한 데이터가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-122">This sample database includes the data necessary to complete this tutorial.</span></span> <span data-ttu-id="b2946-123">[SQL Server 평가판](https://www.microsoft.com/sql-server/sql-server-downloads)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-123">Download [SQL Server free editions](https://www.microsoft.com/sql-server/sql-server-downloads).</span></span> <span data-ttu-id="b2946-124">또는 [Azure SQL Database 평가판](https://azure.microsoft.com/services/sql-database/)을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-124">Or, sign up for a free [Azure SQL Database trial](https://azure.microsoft.com/services/sql-database/).</span></span> 

    <span data-ttu-id="b2946-125">**중요:** 온-프레미스 SQL Server에 예제 데이터베이스를 설치하고 Azure Analysis Services 서버에 모델을 배포하는 경우 [온-프레미스 데이터 게이트웨이](../analysis-services-gateway.md)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-125">**Important:** If you install the sample database on an on-premises SQL Server, and you deploy your model to an Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>

-   <span data-ttu-id="b2946-126">최신 버전의 [SSDT(SQL Server 데이터 도구)](https://msdn.microsoft.com/library/mt204009.aspx).</span><span class="sxs-lookup"><span data-stu-id="b2946-126">The latest version of [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).</span></span>

-   <span data-ttu-id="b2946-127">최신 버전의 [SSMS(SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="b2946-127">The latest version of [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>    

-   <span data-ttu-id="b2946-128">[Power BI Desktop](https://powerbi.microsoft.com/desktop/) 또는 Excel과 같은 클라이언트 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="b2946-128">A client application such as [Power BI Desktop](https://powerbi.microsoft.com/desktop/) or Excel.</span></span> 

## <a name="scenario"></a><span data-ttu-id="b2946-129">시나리오</span><span class="sxs-lookup"><span data-stu-id="b2946-129">Scenario</span></span>  
<span data-ttu-id="b2946-130">이 자습서는 가상의 회사인 Adventure Works Cycles를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-130">This tutorial is based on Adventure Works Cycles, a fictitious company.</span></span> <span data-ttu-id="b2946-131">Adventure Works는 자전거, 부품 및 액세서리를 생산하여 북아메리카, 유럽 및 아시아의 상업 시장에 유통하는 대규모 다국적 제조 회사입니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-131">Adventure Works is a large, multinational manufacturing company that produces and distributes bicycles, parts, and accessories to commercial markets in North America, Europe, and Asia.</span></span> <span data-ttu-id="b2946-132">회사는 500명의 작업자를 고용합니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-132">The company employs 500 workers.</span></span> <span data-ttu-id="b2946-133">또한 Adventure Works는 시장 기반 전체에 대한 여러 지역별 영업 팀을 고용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-133">Additionally, Adventure Works employs several regional sales teams throughout its market base.</span></span> <span data-ttu-id="b2946-134">프로젝트는 AdventureWorksDW 데이터베이스에서 영업 및 마케팅 사용자가 인터넷 판매 데이터를 분석하기 위한 테이블 형식의 모델을 작성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-134">Your project is to create a tabular model for sales and marketing users to analyze Internet sales data in the AdventureWorksDW database.</span></span>  
  
<span data-ttu-id="b2946-135">자습서를 완료하려면 다양한 단원을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-135">To complete the tutorial, you must complete various lessons.</span></span> <span data-ttu-id="b2946-136">각 단원에는 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-136">In each lesson, there are tasks.</span></span> <span data-ttu-id="b2946-137">단원을 완료하려면 각 작업을 순서대로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-137">Completing each task in order is necessary for completing the lesson.</span></span> <span data-ttu-id="b2946-138">특정 단원에서 유사한 결과를 얻는 몇 가지 작업이 있을 수 있지만 각 작업을 완료하는 방법은 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-138">While in a particular lesson there may be several tasks that accomplish a similar outcome, but how you complete each task is slightly different.</span></span> <span data-ttu-id="b2946-139">이 메서드는 보통 작업을 완료하고 이전 단원 및 작업에서 배운 기술을 사용하여 문제를 해결할 수 있는 방법이 여러 가지가 있음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-139">This method shows there is often more than one way to complete a task, and to challenge you by using skills you've learned in previous lessons and tasks.</span></span>  
  
<span data-ttu-id="b2946-140">이 단원의 목적은 SSDT에 포함된 다양한 기능을 사용하여 기본 테이블 형식 모델을 작성하는 과정을 안내하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-140">The purpose of the lessons is to guide you through authoring a basic tabular model by using many of the features included in SSDT.</span></span> <span data-ttu-id="b2946-141">각 단원은 이전 단원을 토대로 작성되므로 단원을 순서대로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-141">Because each lesson builds upon the previous lesson, you should complete the lessons in order.</span></span>
  
<span data-ttu-id="b2946-142">이 자습서는 SSMS를 사용하여 서버 또는 데이터베이스를 관리하거나 클라이언트 응용 프로그램을 사용하여 모델 데이터를 검색하는 Azure Portal의 서버를 관리하는 방법에 대한 단원을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-142">This tutorial does not provide lessons about managing a server in Azure portal, managing a server or database by using SSMS, or using a client application to browse model data.</span></span> 


## <a name="lessons"></a><span data-ttu-id="b2946-143">단원</span><span class="sxs-lookup"><span data-stu-id="b2946-143">Lessons</span></span>  
<span data-ttu-id="b2946-144">이 자습서에는 다음 단원이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-144">This tutorial includes the following lessons:</span></span>  
  
|<span data-ttu-id="b2946-145">단원</span><span class="sxs-lookup"><span data-stu-id="b2946-145">Lesson</span></span>|<span data-ttu-id="b2946-146">예상 완료 시간</span><span class="sxs-lookup"><span data-stu-id="b2946-146">Estimated time to complete</span></span>|  
|----------|------------------------------|  
|[<span data-ttu-id="b2946-147">1 - 새 테이블 형식 모델 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="b2946-147">1 - Create a new tabular model project</span></span>](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)|<span data-ttu-id="b2946-148">10분</span><span class="sxs-lookup"><span data-stu-id="b2946-148">10 minutes</span></span>|  
|[<span data-ttu-id="b2946-149">2 - 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="b2946-149">2 - Get data</span></span>](../tutorials/aas-lesson-2-get-data.md)|<span data-ttu-id="b2946-150">10분</span><span class="sxs-lookup"><span data-stu-id="b2946-150">10 minutes</span></span>|  
|[<span data-ttu-id="b2946-151">3 - 날짜 테이블로 표시</span><span class="sxs-lookup"><span data-stu-id="b2946-151">3 - Mark as Date Table</span></span>](../tutorials/aas-lesson-3-mark-as-date-table.md)|<span data-ttu-id="b2946-152">3분</span><span class="sxs-lookup"><span data-stu-id="b2946-152">3 minutes</span></span>|  
|[<span data-ttu-id="b2946-153">4 - 관계 만들기</span><span class="sxs-lookup"><span data-stu-id="b2946-153">4 - Create relationships</span></span>](../tutorials/aas-lesson-4-create-relationships.md)|<span data-ttu-id="b2946-154">10분</span><span class="sxs-lookup"><span data-stu-id="b2946-154">10 minutes</span></span>|  
|[<span data-ttu-id="b2946-155">5 - 계산된 열 만들기</span><span class="sxs-lookup"><span data-stu-id="b2946-155">5 - Create calculated columns</span></span>](../tutorials/aas-lesson-5-create-calculated-columns.md)|<span data-ttu-id="b2946-156">15분</span><span class="sxs-lookup"><span data-stu-id="b2946-156">15 minutes</span></span>|
|[<span data-ttu-id="b2946-157">6 - 측정값 만들기</span><span class="sxs-lookup"><span data-stu-id="b2946-157">6 - Create measures</span></span>](../tutorials/aas-lesson-6-create-measures.md)|<span data-ttu-id="b2946-158">30분</span><span class="sxs-lookup"><span data-stu-id="b2946-158">30 minutes</span></span>|  
|[<span data-ttu-id="b2946-159">7 - KPI(핵심 성과 지표) 만들기</span><span class="sxs-lookup"><span data-stu-id="b2946-159">7 - Create Key Performance Indicators (KPI)</span></span>](../tutorials/aas-lesson-7-create-key-performance-indicators.md)|<span data-ttu-id="b2946-160">15분</span><span class="sxs-lookup"><span data-stu-id="b2946-160">15 minutes</span></span>|  
|[<span data-ttu-id="b2946-161">8 - 큐브 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="b2946-161">8 - Create perspectives</span></span>](../tutorials/aas-lesson-8-create-perspectives.md)|<span data-ttu-id="b2946-162">5분</span><span class="sxs-lookup"><span data-stu-id="b2946-162">5 minutes</span></span>|  
|[<span data-ttu-id="b2946-163">9 - 계층 구조 만들기</span><span class="sxs-lookup"><span data-stu-id="b2946-163">9 - Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)|<span data-ttu-id="b2946-164">20분</span><span class="sxs-lookup"><span data-stu-id="b2946-164">20 minutes</span></span>|  
|[<span data-ttu-id="b2946-165">10 - 파티션 만들기</span><span class="sxs-lookup"><span data-stu-id="b2946-165">10 - Create partitions</span></span>](../tutorials/aas-lesson-10-create-partitions.md)|<span data-ttu-id="b2946-166">15분</span><span class="sxs-lookup"><span data-stu-id="b2946-166">15 minutes</span></span>|  
|[<span data-ttu-id="b2946-167">11 - 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="b2946-167">11 - Create roles</span></span>](../tutorials/aas-lesson-11-create-roles.md)|<span data-ttu-id="b2946-168">15분</span><span class="sxs-lookup"><span data-stu-id="b2946-168">15 minutes</span></span>|  
|[<span data-ttu-id="b2946-169">12 - Excel에서 분석</span><span class="sxs-lookup"><span data-stu-id="b2946-169">12 - Analyze in Excel</span></span>](../tutorials/aas-lesson-12-analyze-in-excel.md)|<span data-ttu-id="b2946-170">5분</span><span class="sxs-lookup"><span data-stu-id="b2946-170">5 minutes</span></span>| 
|[<span data-ttu-id="b2946-171">13 - 배포</span><span class="sxs-lookup"><span data-stu-id="b2946-171">13 - Deploy</span></span>](../tutorials/aas-lesson-13-deploy.md)|<span data-ttu-id="b2946-172">5분</span><span class="sxs-lookup"><span data-stu-id="b2946-172">5 minutes</span></span>|  
  
## <a name="supplemental-lessons"></a><span data-ttu-id="b2946-173">추가 단원</span><span class="sxs-lookup"><span data-stu-id="b2946-173">Supplemental lessons</span></span>  
<span data-ttu-id="b2946-174">자습서를 완료하는 데 이러한 단원이 필요하지는 않지만 고급 테이블 형식 모델 작성 기능을 이해하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2946-174">These lessons are not required to complete the tutorial, but can be helpful in better understanding advanced tabular model authoring features.</span></span>  
  
|<span data-ttu-id="b2946-175">단원</span><span class="sxs-lookup"><span data-stu-id="b2946-175">Lesson</span></span>|<span data-ttu-id="b2946-176">예상 완료 시간</span><span class="sxs-lookup"><span data-stu-id="b2946-176">Estimated time to complete</span></span>|  
|----------|------------------------------|  
|[<span data-ttu-id="b2946-177">세부 정보 행</span><span class="sxs-lookup"><span data-stu-id="b2946-177">Detail Rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)|<span data-ttu-id="b2946-178">10분</span><span class="sxs-lookup"><span data-stu-id="b2946-178">10 minutes</span></span>|
|[<span data-ttu-id="b2946-179">동적 보안</span><span class="sxs-lookup"><span data-stu-id="b2946-179">Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)|<span data-ttu-id="b2946-180">30분</span><span class="sxs-lookup"><span data-stu-id="b2946-180">30 minutes</span></span>|
|[<span data-ttu-id="b2946-181">불규칙한 계층 구조</span><span class="sxs-lookup"><span data-stu-id="b2946-181">Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)|<span data-ttu-id="b2946-182">20분</span><span class="sxs-lookup"><span data-stu-id="b2946-182">20 minutes</span></span>| 

  
## <a name="next-steps"></a><span data-ttu-id="b2946-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b2946-183">Next steps</span></span>  
<span data-ttu-id="b2946-184">시작하려면 [단원 1: 새 테이블 형식 모델 프로젝트 만들기](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2946-184">To get started, see [Lesson 1: Create a New Tabular Model Project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
  
  

