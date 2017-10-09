---
title: "Azure Analysis Services에서 aaaData 모델 호환성 수준 | Microsoft Docs"
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
ms.openlocfilehash: bfaf0c60666729d1e6e0baf082c046ea9faa4e86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a><span data-ttu-id="d395b-103">Analysis Services 테이블 형식 모델에 대한 호환성 수준</span><span class="sxs-lookup"><span data-stu-id="d395b-103">Compatibility level for Analysis Services tabular models</span></span>

<span data-ttu-id="d395b-104">*호환성 수준이* hello Analysis Services 엔진 toorelease 관련 동작을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d395b-104">*Compatibility level* refers toorelease-specific behaviors in hello Analysis Services engine.</span></span> <span data-ttu-id="d395b-105">변경 내용을 toohello 호환성 수준이 일반적으로 주요 버전의 SQL Server와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d395b-105">Changes toohello compatibility level typically coincide with major releases of SQL Server.</span></span> <span data-ttu-id="d395b-106">이러한 변경은 두 플랫폼 간의 toomaintain 패리티 Azure Analysis Services에에서도 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d395b-106">These changes are also implemented in Azure Analysis Services toomaintain parity between both platforms.</span></span> <span data-ttu-id="d395b-107">호환성 수준 변경은 테이블 형식 모델에서 사용할 수 있는 기능에도 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d395b-107">Compatibility level changes also affect features available in your tabular models.</span></span> <span data-ttu-id="d395b-108">예를 들어 DirectQuery 및 테이블 형식 개체 메타 데이터는 서로 다른 구현이 hello 호환성 수준에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="d395b-108">For example, DirectQuery and tabular object metadata have different implementations depending on hello compatibility level.</span></span> 

<span data-ttu-id="d395b-109">Azure Analysis Services hello 1400 및 1200 호환성 수준의 테이블 형식 모델을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d395b-109">Azure Analysis Services supports tabular models at hello 1200 and 1400 compatibility levels.</span></span>

<span data-ttu-id="d395b-110">hello 최신 호환성 수준은 1400 합니다.</span><span class="sxs-lookup"><span data-stu-id="d395b-110">hello latest compatibility level is 1400.</span></span> <span data-ttu-id="d395b-111">이 수준은 SQL Server 2017 Analysis Services와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="d395b-111">This level coincides with SQL Server 2017 Analysis Services.</span></span> <span data-ttu-id="d395b-112">Hello 1400 호환성 수준에서 주요 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d395b-112">Major features in hello 1400 compatibility level include:</span></span>

*  <span data-ttu-id="d395b-113">TOM API 및 TMSL 스크립트에 대한 지원으로 데이터 연결 및 테이블 형식 모델로 가져오기에 대한 새로운 인프라.</span><span class="sxs-lookup"><span data-stu-id="d395b-113">New infrastructure for data connectivity and import into tabular models with support for TOM APIs and TMSL scripting.</span></span> <span data-ttu-id="d395b-114">이 새로운 기능을 통해 Azure Blob 저장소와 같은 추가 데이터 원본을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d395b-114">This new feature enables support for additional data sources such as Azure Blob storage.</span></span>
*  <span data-ttu-id="d395b-115">데이터 가져오기 및 M 식을 사용하여 데이터 변환 및 데이터 매시업 기능.</span><span class="sxs-lookup"><span data-stu-id="d395b-115">Data transformation and data mashup capabilities by using Get Data and M expressions.</span></span>
*  <span data-ttu-id="d395b-116">측정값은 DAX 식을 사용하여 세부 정보 행 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d395b-116">Measures support a Detail Rows property with a DAX expression.</span></span> <span data-ttu-id="d395b-117">이 속성은 집계 된 보고서에서 toodetailed 데이터 Microsoft Excel toodrill와 같은 클라이언트 도구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d395b-117">This property enables client tools like Microsoft Excel toodrill down toodetailed data from an aggregated report.</span></span> <span data-ttu-id="d395b-118">예를 들어 지역 및 월에 대 한 총 판매액을 보면 관련 된 hello 주문 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d395b-118">For example, when users view total sales for a region and month, they can view hello associated order details.</span></span> 
*  <span data-ttu-id="d395b-119">테이블 및 열에 대 한 개체 수준 보안 이름이 또한 toohello 데이터 그 안에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d395b-119">Object-level security for table and column names, in addition toohello data within them.</span></span>
*  <span data-ttu-id="d395b-120">불균형 계층 구조에 대한 향상된 지원.</span><span class="sxs-lookup"><span data-stu-id="d395b-120">Enhanced support for ragged hierarchies.</span></span>
*  <span data-ttu-id="d395b-121">성능 및 모니터링 향상.</span><span class="sxs-lookup"><span data-stu-id="d395b-121">Performance and monitoring improvements.</span></span>
  
## <a name="set-compatibility-level"></a><span data-ttu-id="d395b-122">호환성 수준 설정</span><span class="sxs-lookup"><span data-stu-id="d395b-122">Set compatibility level</span></span> 
 <span data-ttu-id="d395b-123">SSDT에서 새 테이블 형식 모델 프로젝트를 만들 때 hello에 hello 호환성 수준을 지정할 수 있습니다 **테이블 형식 모델 디자이너** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="d395b-123">When creating a new tabular model project in SSDT, you can specify hello compatibility level on hello **Tabular model designer** dialog.</span></span> 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 <span data-ttu-id="d395b-125">Hello를 선택 하는 경우 **이 메시지를 다시 표시 안 함** 옵션을 모든 후속 프로젝트 hello 기본값으로 지정 하는 hello 호환성 수준을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d395b-125">If you select hello **Do not show this message again** option, all subsequent projects use hello compatibility level you specified as hello default.</span></span> <span data-ttu-id="d395b-126">Ssdt의 hello 기본 호환성 수준을 변경할 수 있습니다 **도구** > **옵션**합니다.</span><span class="sxs-lookup"><span data-stu-id="d395b-126">You can change hello default compatibility level in SSDT in **Tools** > **Options**.</span></span>  
  
 <span data-ttu-id="d395b-127">tooupgrade 집합 hello SSDT에서는 기존 테이블 형식 모델 프로젝트 **호환성 수준이** hello 모델의 속성 **속성** 창.</span><span class="sxs-lookup"><span data-stu-id="d395b-127">tooupgrade an existing tabular model project in SSDT, set  hello **Compatibility Level** property in hello model **Properties** window.</span></span> <span data-ttu-id="d395b-128">에 유의 해야, hello 호환성 수준이 업그레이드은 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d395b-128">Keep in-mind, upgrading hello compatibility level is irreversible.</span></span>
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a><span data-ttu-id="d395b-129">SQL Server Management Studio에서 테이블 형식 모델 데이터베이스에 대한 호환성 수준 확인</span><span class="sxs-lookup"><span data-stu-id="d395b-129">Check compatibility level for a tabular model database in SQL Server Management Studio</span></span> 
 <span data-ttu-id="d395b-130">SSMS에서 hello 데이터베이스 이름을 마우스 오른쪽 단추로 클릭 > **속성** > **호환성 수준이**합니다.</span><span class="sxs-lookup"><span data-stu-id="d395b-130">In SSMS, right-click hello database name > **Properties** > **Compatibility Level**.</span></span>  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a><span data-ttu-id="d395b-131">SSMS에서 서버에 대해 지원되는 호환성 수준 확인</span><span class="sxs-lookup"><span data-stu-id="d395b-131">Check supported compatibility level for a server in SSMS</span></span>  
 <span data-ttu-id="d395b-132">SSMS에서 hello 서버 이름 마우스 오른쪽 단추로 클릭 > **속성** > **호환성 수준을 지원**합니다.</span><span class="sxs-lookup"><span data-stu-id="d395b-132">In SSMS, right-click hello server name>  **Properties** > **Supported Compatibility Level**.</span></span>  
  
 <span data-ttu-id="d395b-133">이 속성에는 hello hello 서버 (미리 보기 제외)에서 실행 되는 데이터베이스의 가장 높은 호환성 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d395b-133">This property specifies hello highest compatibility level of a database that will run on hello server (excluding preview).</span></span> <span data-ttu-id="d395b-134">지원 되는 hello 호환성 수준을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d395b-134">hello supported compatibility level cannot be changed.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="d395b-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d395b-135">Next steps</span></span>
  <span data-ttu-id="d395b-136">[Azure Portal에서 모델 만들기](analysis-services-create-model-portal.md) </span><span class="sxs-lookup"><span data-stu-id="d395b-136">[Create a model in Azure portal](analysis-services-create-model-portal.md) </span></span>  
  [<span data-ttu-id="d395b-137">Analysis Services 관리</span><span class="sxs-lookup"><span data-stu-id="d395b-137">Manage Analysis Services</span></span>](analysis-services-manage.md)  
