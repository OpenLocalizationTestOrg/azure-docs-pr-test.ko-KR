---
title: "SQL 데이터 웨어하우스에 Azure Data Factory aaaUse | Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 Azure 데이터 팩터리(ADF) 사용을 위한 팁"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 492de762-c7a2-4cdb-943f-3135230e94f1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d40a547830f9681504253d39ae3066800a955c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a><span data-ttu-id="4bbd9-103">SQL 데이터 웨어하우스와 함께 Azure 데이터 팩터리 사용</span><span class="sxs-lookup"><span data-stu-id="4bbd9-103">Use Azure Data Factory with SQL Data Warehouse</span></span>
<span data-ttu-id="4bbd9-104">Azure 데이터 팩터리를 통해 완전히 관리 되는 데이터의 전송을 hello 및 SQL 데이터 웨어하우스에서 저장된 프로시저의 실행 오케스트레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbd9-104">Azure Data Factory provides a fully managed method for orchestrating hello transfer of data and execution of stored procedures on SQL Data Warehouse.</span></span>  <span data-ttu-id="4bbd9-105">이렇게 하면 toomore 쉽게 설치 하 고 일정 복잡 한 변환 추출 및 로드 (ETL) 절차 SQL 데이터 웨어하우스에 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbd9-105">This will allow you toomore easily set-up and schedule complex Extract Transform and Load (ETL) procedures with SQL Data Warehouse.</span></span> <span data-ttu-id="4bbd9-106">Azure Data Factory의 자세한 개요를 참조 hello [Azure Data Factory 설명서][Azure Data Factory documentation]합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbd9-106">For a more complete overview of Azure Data Factory, see hello [Azure Data Factory documentation][Azure Data Factory documentation].</span></span>

## <a name="data-movement"></a><span data-ttu-id="4bbd9-107">데이터 이동</span><span class="sxs-lookup"><span data-stu-id="4bbd9-107">Data Movement</span></span>
<span data-ttu-id="4bbd9-108">Azure 데이터 팩터리는 온-프레미스 원본 및 다른 Azure 서비스 간의 데이터 이동을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bbd9-108">Azure Data Factory enables data movement between both on-premises sources and different Azure services.</span></span>  <span data-ttu-id="4bbd9-109">Azure Data Factory와 전반적인, 현재 통합 hello 다음 위치에서에서 데이터 이동을 tooand를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbd9-109">Overall, current integration with Azure Data Factory supports data movement tooand from hello following locations:</span></span>

* <span data-ttu-id="4bbd9-110">Azure Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="4bbd9-110">Azure blob storage</span></span>
* <span data-ttu-id="4bbd9-111">Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4bbd9-111">Azure SQL Database</span></span>
* <span data-ttu-id="4bbd9-112">온-프레미스 SQL Server</span><span class="sxs-lookup"><span data-stu-id="4bbd9-112">On-premises SQL Server</span></span>
* <span data-ttu-id="4bbd9-113">IaaS의 SQL Server</span><span class="sxs-lookup"><span data-stu-id="4bbd9-113">SQL Server on IaaS</span></span>

<span data-ttu-id="4bbd9-114">데이터를 tooset 활동을 복사 하는 방법에 대 한 내용은 [Azure 데이터 팩터리를 사용 하 여 데이터를 복사 합니다.][Copy data with Azure Data Factory]</span><span class="sxs-lookup"><span data-stu-id="4bbd9-114">For information on how tooset up a data copy activity see [Copy data with Azure Data Factory][Copy data with Azure Data Factory]</span></span>

## <a name="stored-procedures"></a><span data-ttu-id="4bbd9-115">저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="4bbd9-115">Stored Procedures</span></span>
 <span data-ttu-id="4bbd9-116">Hello에 동일한 방식으로 수 tooschedule 데이터 전송, Azure Data Factory 수 있는 저장된 프로시저의 사용된 tooorchestrate hello 실행 될도 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbd9-116">In hello same way it can be used tooschedule data transfer, Azure Data Factory can also be used tooorchestrate hello execution of stored procedures.</span></span>  <span data-ttu-id="4bbd9-117">이 통해 만든 더 복잡 한 파이프라인 toobe 있으며 Azure Data Factory 기능 tooleverage hello의 계산 능력 SQL 데이터 웨어하우스를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbd9-117">This allows more complex pipelines toobe created and extends Azure Data Factory's ability tooleverage hello computational power of SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bbd9-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4bbd9-118">Next steps</span></span>
<span data-ttu-id="4bbd9-119">통합 개요는 [SQL Data Warehouse 통합 개요][SQL Data Warehouse integration overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4bbd9-119">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>
<span data-ttu-id="4bbd9-120">더 많은 개발 팁은 [SQL Data Warehouse 개발 개요][SQL Data Warehouse development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4bbd9-120">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

