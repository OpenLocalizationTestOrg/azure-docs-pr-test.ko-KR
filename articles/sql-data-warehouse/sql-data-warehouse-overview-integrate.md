---
title: "SQL 데이터 웨어하우스에 aaaBuild 통합 솔루션 | Microsoft Docs"
description: "SQL 데이터 웨어하우스와 통합된 솔루션과 파트너 및 도구 "
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: e2dc8f3f-10e3-4589-a4e2-50c67dfcf67f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: c8a4202dd84305bea4e4c2faf0e4791d026e794f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a><span data-ttu-id="d43ca-103">SQL 데이터 웨어하우스와 함께 기타 서비스 활용</span><span class="sxs-lookup"><span data-stu-id="d43ca-103">Leverage other services with SQL Data Warehouse</span></span>
<span data-ttu-id="d43ca-104">또한 tooits 핵심 기능, SQL 데이터 웨어하우스 사용자 tooleverage 옆 Azure의 다른 서비스 hello 다양 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43ca-104">In addition tooits core functionality, SQL Data Warehouse enables users tooleverage many of hello other services in Azure alongside it.</span></span>  <span data-ttu-id="d43ca-105">특히, 우리 현재 단계를 수행 하 toodeeply hello 다음와 통합:</span><span class="sxs-lookup"><span data-stu-id="d43ca-105">Specifically, we have currently taken steps toodeeply integrate with hello following:</span></span>

* <span data-ttu-id="d43ca-106">Power BI</span><span class="sxs-lookup"><span data-stu-id="d43ca-106">Power BI</span></span>
* <span data-ttu-id="d43ca-107">Azure 데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="d43ca-107">Azure Data Factory</span></span>
* <span data-ttu-id="d43ca-108">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="d43ca-108">Azure Machine Learning</span></span>
* <span data-ttu-id="d43ca-109">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d43ca-109">Azure Stream Analytics</span></span>

<span data-ttu-id="d43ca-110">Hello Azure 에코 시스템에서 더 많은 서비스와 tooconnect을 노력 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d43ca-110">We are working tooconnect with more services across hello Azure ecosystem.</span></span>

## <a name="power-bi"></a><span data-ttu-id="d43ca-111">Power BI</span><span class="sxs-lookup"><span data-stu-id="d43ca-111">Power BI</span></span>
<span data-ttu-id="d43ca-112">Power BI 통합을 사용 하면 hello 동적 보고 데이터 웨어하우스의 SQL tooleverage hello 계산 능력 및 Power BI의 시각화가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d43ca-112">Power BI integration allows you tooleverage hello compute power of SQL Data Warehouse with hello dynamic reporting and visualization of Power BI.</span></span> <span data-ttu-id="d43ca-113">Power BI 통합에는 현재 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d43ca-113">Power BI integration currently includes:</span></span>

* <span data-ttu-id="d43ca-114">**직접 연결**: SQL 데이터 웨어하우스에 대해 논리적 푸시다운을 통한 보다 고급 연결.</span><span class="sxs-lookup"><span data-stu-id="d43ca-114">**Direct Connect**: A more advanced connection with logical pushdown against SQL Data Warehouse.</span></span>  <span data-ttu-id="d43ca-115">더 큰 규모를 더욱 빠르게 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="d43ca-115">This provides faster analysis on a larger scale.</span></span>
* <span data-ttu-id="d43ca-116">**Power BI에서 열기**: hello 'Power BI에서 열기' 단추 인스턴스 정보 tooPower BI, 더 원활한 연결 범위를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43ca-116">**Open in Power BI**: hello 'Open in Power BI' button passes instance information tooPower BI, allowing for a more seamless connection.</span></span>

<span data-ttu-id="d43ca-117">참조 [Power BI와 통합](sql-data-warehouse-integrate-power-bi.md) 또는 hello [Power BI 설명서](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43ca-117">See [Integrate with Power BI](sql-data-warehouse-integrate-power-bi.md) or hello [Power BI documentation](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) for more information.</span></span>

## <a name="azure-data-factory"></a><span data-ttu-id="d43ca-118">Azure 데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="d43ca-118">Azure Data Factory</span></span>
<span data-ttu-id="d43ca-119">Azure 데이터 팩터리 파이프라인 복잡 한 추출 로드 하는 관리 되는 플랫폼 toocreate를 사용자에 게 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43ca-119">Azure Data Factory gives users a managed platform toocreate complex Extract-Load pipelines.</span></span>  <span data-ttu-id="d43ca-120">Azure Data Factory와 SQL 데이터 웨어하우스 통합 hello 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d43ca-120">SQL Data Warehouse's integration with Azure Data Factory includes hello following:</span></span>

* <span data-ttu-id="d43ca-121">**저장 프로시저**: hello SQL 데이터 웨어하우스에서 저장된 프로시저 실행을 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43ca-121">**Stored Procedures**: Orchestrate hello execution of stored procedures on SQL Data Warehouse.</span></span>
* <span data-ttu-id="d43ca-122">**복사**: SQL 데이터 웨어하우스를 사용 하 여 ADF toomove 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="d43ca-122">**Copy**: Use ADF toomove data into SQL Data Warehouse.</span></span>  <span data-ttu-id="d43ca-123">이 작업 ADF의 표준 데이터 이동 메커니즘을 사용할 수 또는 hello에서 PolyBase에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43ca-123">This operation can use ADF's standard data movement mechanism or PolyBase under hello covers.</span></span> 

<span data-ttu-id="d43ca-124">참조 [Azure Data Factory와 통합](sql-data-warehouse-integrate-azure-data-factory.md) 또는 hello [Azure Data Factory 설명서](https://azure.microsoft.com/documentation/services/data-factory/) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43ca-124">See [Integrate with Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) or hello [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/) for more information.</span></span>

## <a name="azure-machine-learning"></a><span data-ttu-id="d43ca-125">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="d43ca-125">Azure Machine Learning</span></span>
<span data-ttu-id="d43ca-126">Azure 기계 학습 toocreate 다양 한 예측 도구를 활용 하는 복잡 한 모델 사용자가 수 있는 완전히 관리 되는 분석 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d43ca-126">Azure Machine Learning is a fully managed analytics service which allows users toocreate intricate models leveraging a large set of predictive tools.</span></span>  <span data-ttu-id="d43ca-127">SQL 데이터 웨어하우스 기능을 수행 하는 hello는 소스와 이러한 모델에 대 한 대상으로 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d43ca-127">SQL Data Warehouse is supported as both a source and destination for these models with hello following functionality:</span></span>

* <span data-ttu-id="d43ca-128">**데이터 읽기:** SQL 데이터 웨어하우스에 대해 T-SQL을 사용하는 규모에 따른 드라이브 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="d43ca-128">**Read Data:** Drive models at scale using T-SQL against SQL Data Warehouse.</span></span>
* <span data-ttu-id="d43ca-129">**데이터 쓰기:** 모든 모델에서 변경 내용을 커밋합니다 tooSQL 데이터 웨어하우스를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43ca-129">**Write Data:** Commit changes from any model back tooSQL Data Warehouse.</span></span>

<span data-ttu-id="d43ca-130">참조 [Azure 기계 학습와 통합](sql-data-warehouse-integrate-azure-machine-learning.md) 또는 hello [Azure 기계 학습 설명서](https://azure.microsoft.com/services/machine-learning/) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43ca-130">See [Integrate with Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) or hello [Azure Machine Learning documentation](https://azure.microsoft.com/services/machine-learning/) for more information.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="d43ca-131">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d43ca-131">Azure Stream Analytics</span></span>
<span data-ttu-id="d43ca-132">Azure 스트림 분석은 Azure 이벤트 허브에서 생성된 이벤트 데이터를 처리 및 사용하기 위한 복잡하고 완전히 관리되는 인프라입니다.</span><span class="sxs-lookup"><span data-stu-id="d43ca-132">Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.</span></span>  <span data-ttu-id="d43ca-133">SQL 데이터 웨어하우스 통합 데이터 toobe 효과적으로 처리 되 고 분석 더 많은 고급 깊은 사용 하도록 설정 하는 관계형 데이터와 함께 저장, 스트리밍에 대 한 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43ca-133">Integration with SQL Data Warehouse allows for streaming data toobe effectively processed and stored alongside relational data enabling deeper, more advanced analysis.</span></span>  

* <span data-ttu-id="d43ca-134">**작업 출력:** 송신 출력을 스트림 분석 작업 tooSQL 데이터 웨어하우스에 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43ca-134">**Job Output:** Send output from Stream Analytics jobs directly tooSQL Data Warehouse.</span></span>

<span data-ttu-id="d43ca-135">참조 [와 Azure 스트림 분석 통합](sql-data-warehouse-integrate-azure-stream-analytics.md) 또는 hello [Azure 스트림 분석 설명서](https://azure.microsoft.com/documentation/services/stream-analytics/) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d43ca-135">See [Integrate with Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) or hello [Azure Stream Analytics documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) for more information.</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop/

[Azure Data Factory]: sql-data-warehouse-integrate-azure-data-factory.md
[Azure Machine Learning]: sql-data-warehouse-integrate-azure-machine-learning.md
[Azure Stream Analytics]: sql-data-warehouse-integrate-azure-stream-analytics.md
[Power BI]: sql-data-warehouse-integrate-power-bi.md
[Partners]: sql-data-warehouse-partner-business-intelligence.md

<!--MSDN references-->

<!--Other Web references-->
