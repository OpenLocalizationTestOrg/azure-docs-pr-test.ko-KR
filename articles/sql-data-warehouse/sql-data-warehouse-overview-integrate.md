---
title: "SQL Data Warehouse와 통합된 솔루션 구축 | Microsoft Docs"
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
ms.openlocfilehash: d407c29f99fd7537590ec787febd84a9e3f4f353
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a><span data-ttu-id="aed65-103">SQL 데이터 웨어하우스와 함께 기타 서비스 활용</span><span class="sxs-lookup"><span data-stu-id="aed65-103">Leverage other services with SQL Data Warehouse</span></span>
<span data-ttu-id="aed65-104">사용자는 SQL 데이터 웨어하우스를 통해 핵심 기능 외에도, Azure에서 다양한 기타 서비스를 함께 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aed65-104">In addition to its core functionality, SQL Data Warehouse enables users to leverage many of the other services in Azure alongside it.</span></span>  <span data-ttu-id="aed65-105">특히 다음과 긴밀하게 통합하는 단계를 현재 진행했습니다.</span><span class="sxs-lookup"><span data-stu-id="aed65-105">Specifically, we have currently taken steps to deeply integrate with the following:</span></span>

* <span data-ttu-id="aed65-106">Power BI</span><span class="sxs-lookup"><span data-stu-id="aed65-106">Power BI</span></span>
* <span data-ttu-id="aed65-107">Azure 데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="aed65-107">Azure Data Factory</span></span>
* <span data-ttu-id="aed65-108">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="aed65-108">Azure Machine Learning</span></span>
* <span data-ttu-id="aed65-109">Azure 스트림 분석</span><span class="sxs-lookup"><span data-stu-id="aed65-109">Azure Stream Analytics</span></span>

<span data-ttu-id="aed65-110">Azure 에코시스템에서 더 많은 서비스가 연결되도록 노력하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aed65-110">We are working to connect with more services across the Azure ecosystem.</span></span>

## <a name="power-bi"></a><span data-ttu-id="aed65-111">Power BI</span><span class="sxs-lookup"><span data-stu-id="aed65-111">Power BI</span></span>
<span data-ttu-id="aed65-112">Power BI 통합을 통해 Power BI의 동적 보고 및 시각화와 더불어 SQL 데이터 웨어하우스의 계산 능력의 활용도를 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aed65-112">Power BI integration allows you to leverage the compute power of SQL Data Warehouse with the dynamic reporting and visualization of Power BI.</span></span> <span data-ttu-id="aed65-113">Power BI 통합에는 현재 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="aed65-113">Power BI integration currently includes:</span></span>

* <span data-ttu-id="aed65-114">**직접 연결**: SQL 데이터 웨어하우스에 대해 논리적 푸시다운을 통한 보다 고급 연결.</span><span class="sxs-lookup"><span data-stu-id="aed65-114">**Direct Connect**: A more advanced connection with logical pushdown against SQL Data Warehouse.</span></span>  <span data-ttu-id="aed65-115">더 큰 규모를 더욱 빠르게 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="aed65-115">This provides faster analysis on a larger scale.</span></span>
* <span data-ttu-id="aed65-116">**Power BI에서 열기**: 'Power BI에서 열기' 단추를 통해 인스턴스 정보를 Power BI에 전달하여 보다 원활한 연결이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="aed65-116">**Open in Power BI**: The 'Open in Power BI' button passes instance information to Power BI, allowing for a more seamless connection.</span></span>

<span data-ttu-id="aed65-117">자세한 내용은 [Power BI와 통합](sql-data-warehouse-integrate-power-bi.md) 또는 [Power BI 설명서](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aed65-117">See [Integrate with Power BI](sql-data-warehouse-integrate-power-bi.md) or the [Power BI documentation](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) for more information.</span></span>

## <a name="azure-data-factory"></a><span data-ttu-id="aed65-118">Azure 데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="aed65-118">Azure Data Factory</span></span>
<span data-ttu-id="aed65-119">Azure 데이터 팩터리는 복잡한 추출-로드 파이프라인을 만들 수 있는 관리되는 플랫폼을 사용자에게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="aed65-119">Azure Data Factory gives users a managed platform to create complex Extract-Load pipelines.</span></span>  <span data-ttu-id="aed65-120">Azure 데이터 팩터리와 SQL 데이터 웨어하우스의 통합에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="aed65-120">SQL Data Warehouse's integration with Azure Data Factory includes the following:</span></span>

* <span data-ttu-id="aed65-121">**저장 프로시저**: SQL 데이터 웨어하우스에서 저장 프로시저의 실행을 오케스트레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="aed65-121">**Stored Procedures**: Orchestrate the execution of stored procedures on SQL Data Warehouse.</span></span>
* <span data-ttu-id="aed65-122">**복사**: ADF를 사용하여 SQL 데이터 웨어하우스로 데이터를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="aed65-122">**Copy**: Use ADF to move data into SQL Data Warehouse.</span></span>  <span data-ttu-id="aed65-123">이 작업에서는 백그라운드에서 ADF의 표준 데이터 이동 메커니즘 또는 PolyBase가 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aed65-123">This operation can use ADF's standard data movement mechanism or PolyBase under the covers.</span></span> 

<span data-ttu-id="aed65-124">자세한 내용은 [Azure Data Factory와 통합](sql-data-warehouse-integrate-azure-data-factory.md) 또는 [Azure Data Factory 설명서](https://azure.microsoft.com/documentation/services/data-factory/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aed65-124">See [Integrate with Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) or the [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/) for more information.</span></span>

## <a name="azure-machine-learning"></a><span data-ttu-id="aed65-125">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="aed65-125">Azure Machine Learning</span></span>
<span data-ttu-id="aed65-126">Azure 기계 학습은 사용자가 다양한 예측 도구를 활용하여 복잡한 모델을 만들 수 있는 완전히 관리되는 분석 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="aed65-126">Azure Machine Learning is a fully managed analytics service which allows users to create intricate models leveraging a large set of predictive tools.</span></span>  <span data-ttu-id="aed65-127">SQL 데이터 웨어하우스는 다음 기능을 포함하는 이러한 모델에 대한 소스 및 대상으로 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="aed65-127">SQL Data Warehouse is supported as both a source and destination for these models with the following functionality:</span></span>

* <span data-ttu-id="aed65-128">**데이터 읽기:** SQL 데이터 웨어하우스에 대해 T-SQL을 사용하는 규모에 따른 드라이브 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="aed65-128">**Read Data:** Drive models at scale using T-SQL against SQL Data Warehouse.</span></span>
* <span data-ttu-id="aed65-129">**데이터 쓰기:** 모델에서 SQL 데이터 웨어하우스로 변경 사항을 뒤로 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="aed65-129">**Write Data:** Commit changes from any model back to SQL Data Warehouse.</span></span>

<span data-ttu-id="aed65-130">자세한 내용은 [Azure Machine Learning과 통합](sql-data-warehouse-integrate-azure-machine-learning.md) 또는 [Azure Machine Learning 설명서](https://azure.microsoft.com/services/machine-learning/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aed65-130">See [Integrate with Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) or the [Azure Machine Learning documentation](https://azure.microsoft.com/services/machine-learning/) for more information.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="aed65-131">Azure 스트림 분석</span><span class="sxs-lookup"><span data-stu-id="aed65-131">Azure Stream Analytics</span></span>
<span data-ttu-id="aed65-132">Azure 스트림 분석은 Azure 이벤트 허브에서 생성된 이벤트 데이터를 처리 및 사용하기 위한 복잡하고 완전히 관리되는 인프라입니다.</span><span class="sxs-lookup"><span data-stu-id="aed65-132">Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.</span></span>  <span data-ttu-id="aed65-133">SQL 데이터 웨어하우스와 통합을 통해 스트리밍 데이터를 효과적으로 처리하고 관계형 데이터와 함께 저장하여 보다 심도있는 고급 분석이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="aed65-133">Integration with SQL Data Warehouse allows for streaming data to be effectively processed and stored alongside relational data enabling deeper, more advanced analysis.</span></span>  

* <span data-ttu-id="aed65-134">**작업 출력:** 스트림 분석 작업에서 SQL 데이터 웨어하우스로 출력을 직접 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="aed65-134">**Job Output:** Send output from Stream Analytics jobs directly to SQL Data Warehouse.</span></span>

<span data-ttu-id="aed65-135">자세한 내용은 [Azure Stream Analytics와 통합](sql-data-warehouse-integrate-azure-stream-analytics.md) 또는 [Azure Stream Analytics 설명서](https://azure.microsoft.com/documentation/services/stream-analytics/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aed65-135">See [Integrate with Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) or the [Azure Stream Analytics documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) for more information.</span></span>

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
