---
title: "Azure Analysis Services에서 데이터 모델 호환성 수준 | Microsoft Docs"
description: "테이블 형식 데이터 모델 호환성 수준을 이해합니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/16/2017
ms.author: owend
ms.openlocfilehash: b11ba54c2cdc2675ec535368e7076613a5290212
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a><span data-ttu-id="4d5db-103">Analysis Services 테이블 형식 모델에 대한 호환성 수준</span><span class="sxs-lookup"><span data-stu-id="4d5db-103">Compatibility level for Analysis Services tabular models</span></span>

<span data-ttu-id="4d5db-104">*호환성 수준*은 Analysis Services 엔진의 릴리스 관련 동작을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="4d5db-104">*Compatibility level* refers to release-specific behaviors in the Analysis Services engine.</span></span> <span data-ttu-id="4d5db-105">호환성 수준에 대한 변경은 일반적으로 주요 버전의 SQL Server와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="4d5db-105">Changes to the compatibility level typically coincide with major releases of SQL Server.</span></span> <span data-ttu-id="4d5db-106">이러한 변경은 두 플랫폼 간의 패리티를 유지하기 위해 Azure Analysis Services에도 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d5db-106">These changes are also implemented in Azure Analysis Services to maintain parity between both platforms.</span></span> <span data-ttu-id="4d5db-107">호환성 수준 변경은 테이블 형식 모델에서 사용할 수 있는 기능에도 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d5db-107">Compatibility level changes also affect features available in your tabular models.</span></span> <span data-ttu-id="4d5db-108">예를 들어 DirectQuery 및 테이블 형식 개체 메타데이터는 호환성 수준에 따라 서로 다른 구현을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="4d5db-108">For example, DirectQuery and tabular object metadata have different implementations depending on the compatibility level.</span></span> 

<span data-ttu-id="4d5db-109">Azure Analysis Services는 1200 및 1400 호환성 수준의 테이블 형식 모델을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4d5db-109">Azure Analysis Services supports tabular models at the 1200 and 1400 compatibility levels.</span></span>

<span data-ttu-id="4d5db-110">최신 호환성 수준은 1400입니다.</span><span class="sxs-lookup"><span data-stu-id="4d5db-110">The latest compatibility level is 1400.</span></span> <span data-ttu-id="4d5db-111">이 수준은 SQL Server 2017 Analysis Services와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="4d5db-111">This level coincides with SQL Server 2017 Analysis Services.</span></span> <span data-ttu-id="4d5db-112">1400 호환성 수준에서 주요 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4d5db-112">Major features in the 1400 compatibility level include:</span></span>

*  <span data-ttu-id="4d5db-113">TOM API 및 TMSL 스크립트에 대한 지원으로 데이터 연결 및 테이블 형식 모델로 가져오기에 대한 새로운 인프라.</span><span class="sxs-lookup"><span data-stu-id="4d5db-113">New infrastructure for data connectivity and import into tabular models with support for TOM APIs and TMSL scripting.</span></span> <span data-ttu-id="4d5db-114">이 새로운 기능을 통해 Azure Blob 저장소와 같은 추가 데이터 원본을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d5db-114">This new feature enables support for additional data sources such as Azure Blob storage.</span></span>
*  <span data-ttu-id="4d5db-115">데이터 가져오기 및 M 식을 사용하여 데이터 변환 및 데이터 매시업 기능.</span><span class="sxs-lookup"><span data-stu-id="4d5db-115">Data transformation and data mashup capabilities by using Get Data and M expressions.</span></span>
*  <span data-ttu-id="4d5db-116">측정값은 DAX 식을 사용하여 세부 정보 행 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4d5db-116">Measures support a Detail Rows property with a DAX expression.</span></span> <span data-ttu-id="4d5db-117">이 속성은 Microsoft Excel과 같은 클라이언트 도구를 활성화하여 집계된 보고서에서 자세한 데이터로 드릴다운합니다.</span><span class="sxs-lookup"><span data-stu-id="4d5db-117">This property enables client tools like Microsoft Excel to drill down to detailed data from an aggregated report.</span></span> <span data-ttu-id="4d5db-118">예를 들어 사용자가 지역 및 월에 대한 총 판매액을 볼 때 관련된 주문 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d5db-118">For example, when users view total sales for a region and month, they can view the associated order details.</span></span> 
*  <span data-ttu-id="4d5db-119">해당 항목 내의 데이터 외의 테이블 및 열 이름에 대한 개체 수준 보안.</span><span class="sxs-lookup"><span data-stu-id="4d5db-119">Object-level security for table and column names, in addition to the data within them.</span></span>
*  <span data-ttu-id="4d5db-120">불균형 계층 구조에 대한 향상된 지원.</span><span class="sxs-lookup"><span data-stu-id="4d5db-120">Enhanced support for ragged hierarchies.</span></span>
*  <span data-ttu-id="4d5db-121">성능 및 모니터링 향상.</span><span class="sxs-lookup"><span data-stu-id="4d5db-121">Performance and monitoring improvements.</span></span>
  
## <a name="set-compatibility-level"></a><span data-ttu-id="4d5db-122">호환성 수준 설정</span><span class="sxs-lookup"><span data-stu-id="4d5db-122">Set compatibility level</span></span> 
 <span data-ttu-id="4d5db-123">SSDT에서 새 테이블 형식 모델 프로젝트를 만들 때 **테이블 형식 모델 디자이너** 대화 상자에서 호환성 수준을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d5db-123">When creating a new tabular model project in SSDT, you can specify the compatibility level on the **Tabular model designer** dialog.</span></span> 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 <span data-ttu-id="4d5db-125">**이 메시지를 다시 표시 안 함** 옵션을 선택하는 경우 모든 후속 프로젝트는 기본적으로 지정한 호환성 수준을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d5db-125">If you select the **Do not show this message again** option, all subsequent projects use the compatibility level you specified as the default.</span></span> <span data-ttu-id="4d5db-126">**도구** > **옵션**의 SSDT에서 기본 호환성 수준을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d5db-126">You can change the default compatibility level in SSDT in **Tools** > **Options**.</span></span>  
  
 <span data-ttu-id="4d5db-127">SSDT에서 기존 테이블 형식 모델 프로젝트를 업그레이드하려면 모델 **속성** 창에서 **호환성 수준** 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4d5db-127">To upgrade an existing tabular model project in SSDT, set  the **Compatibility Level** property in the model **Properties** window.</span></span> <span data-ttu-id="4d5db-128">호환성 수준 업그레이드는 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4d5db-128">Keep in-mind, upgrading the compatibility level is irreversible.</span></span>
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a><span data-ttu-id="4d5db-129">SQL Server Management Studio에서 테이블 형식 모델 데이터베이스에 대한 호환성 수준 확인</span><span class="sxs-lookup"><span data-stu-id="4d5db-129">Check compatibility level for a tabular model database in SQL Server Management Studio</span></span> 
 <span data-ttu-id="4d5db-130">SSMS에서 데이터베이스 이름 > **속성** > **호환성 수준**을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d5db-130">In SSMS, right-click the database name > **Properties** > **Compatibility Level**.</span></span>  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a><span data-ttu-id="4d5db-131">SSMS에서 서버에 대해 지원되는 호환성 수준 확인</span><span class="sxs-lookup"><span data-stu-id="4d5db-131">Check supported compatibility level for a server in SSMS</span></span>  
 <span data-ttu-id="4d5db-132">SSMS에서 서버 이름 > **속성** > **지원되는 호환성 수준**을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d5db-132">In SSMS, right-click the server name>  **Properties** > **Supported Compatibility Level**.</span></span>  
  
 <span data-ttu-id="4d5db-133">이 속성을 서버에서 실행되는 데이터베이스의 가장 높은 호환성 수준을 지정합니다(미리 보기 제외).</span><span class="sxs-lookup"><span data-stu-id="4d5db-133">This property specifies the highest compatibility level of a database that will run on the server (excluding preview).</span></span> <span data-ttu-id="4d5db-134">지원되는 호환성 수준을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4d5db-134">The supported compatibility level cannot be changed.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="4d5db-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4d5db-135">Next steps</span></span>
  <span data-ttu-id="4d5db-136">[Azure Portal에서 모델 만들기](analysis-services-create-model-portal.md) </span><span class="sxs-lookup"><span data-stu-id="4d5db-136">[Create a model in Azure portal](analysis-services-create-model-portal.md) </span></span>  
  [<span data-ttu-id="4d5db-137">Analysis Services 관리</span><span class="sxs-lookup"><span data-stu-id="4d5db-137">Manage Analysis Services</span></span>](analysis-services-manage.md)  
