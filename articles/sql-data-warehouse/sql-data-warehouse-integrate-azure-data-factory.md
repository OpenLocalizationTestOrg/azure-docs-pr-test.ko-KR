---
title: "SQL Data Warehouse와 함께 Azure Data Factory 사용 | Microsoft Docs"
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
ms.openlocfilehash: 7cd113f4a92635bc68253c2beb165ad1f0c96569
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a><span data-ttu-id="1dd90-103">SQL 데이터 웨어하우스와 함께 Azure 데이터 팩터리 사용</span><span class="sxs-lookup"><span data-stu-id="1dd90-103">Use Azure Data Factory with SQL Data Warehouse</span></span>
<span data-ttu-id="1dd90-104">Azure 데이터 팩터리는 데이터를 전송 및 SQL 데이터 웨어하우스에 대한 저장 프로시저의 실행 조율을 위한 완전한 관리 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd90-104">Azure Data Factory provides a fully managed method for orchestrating the transfer of data and execution of stored procedures on SQL Data Warehouse.</span></span>  <span data-ttu-id="1dd90-105">이렇게 하면 복잡한 ETL(Extract Transform and Load) 프로시저를 SQL 데이터 웨어하우스와 함께 보다 쉽게 설정하고 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd90-105">This will allow you to more easily set-up and schedule complex Extract Transform and Load (ETL) procedures with SQL Data Warehouse.</span></span> <span data-ttu-id="1dd90-106">Azure Data Factory의 전체 개요는 [Azure Data Factory 설명서][Azure Data Factory documentation]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1dd90-106">For a more complete overview of Azure Data Factory, see the [Azure Data Factory documentation][Azure Data Factory documentation].</span></span>

## <a name="data-movement"></a><span data-ttu-id="1dd90-107">데이터 이동</span><span class="sxs-lookup"><span data-stu-id="1dd90-107">Data Movement</span></span>
<span data-ttu-id="1dd90-108">Azure 데이터 팩터리는 온-프레미스 원본 및 다른 Azure 서비스 간의 데이터 이동을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd90-108">Azure Data Factory enables data movement between both on-premises sources and different Azure services.</span></span>  <span data-ttu-id="1dd90-109">Azure 데이터 팩터리와의 전반적인 현재 통합은 다음 위치에서의/으로의 데이터 이동을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd90-109">Overall, current integration with Azure Data Factory supports data movement to and from the following locations:</span></span>

* <span data-ttu-id="1dd90-110">Azure Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="1dd90-110">Azure blob storage</span></span>
* <span data-ttu-id="1dd90-111">Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="1dd90-111">Azure SQL Database</span></span>
* <span data-ttu-id="1dd90-112">온-프레미스 SQL Server</span><span class="sxs-lookup"><span data-stu-id="1dd90-112">On-premises SQL Server</span></span>
* <span data-ttu-id="1dd90-113">IaaS의 SQL Server</span><span class="sxs-lookup"><span data-stu-id="1dd90-113">SQL Server on IaaS</span></span>

<span data-ttu-id="1dd90-114">데이터 복사 활동을 설정하는 방법에 대한 정보는 [Azure Data Factory를 사용하여 데이터 복사][Copy data with Azure Data Factory]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1dd90-114">For information on how to set up a data copy activity see [Copy data with Azure Data Factory][Copy data with Azure Data Factory]</span></span>

## <a name="stored-procedures"></a><span data-ttu-id="1dd90-115">저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="1dd90-115">Stored Procedures</span></span>
 <span data-ttu-id="1dd90-116">데이터 전송을 예약하는 데 사용할 수 있는 동일한 방법으로 Azure 데이터 팩터리는 저장 프로시저의 실행을 오케스트레이션하는 데도 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd90-116">In the same way it can be used to schedule data transfer, Azure Data Factory can also be used to orchestrate the execution of stored procedures.</span></span>  <span data-ttu-id="1dd90-117">이렇게 하면 더 복잡한 파이프라인을 만들 수 있으며 Azure 데이터 팩터리 기능을 확장하여 SQL 데이터 웨어하우스의 컴퓨팅 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd90-117">This allows more complex pipelines to be created and extends Azure Data Factory's ability to leverage the computational power of SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1dd90-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1dd90-118">Next steps</span></span>
<span data-ttu-id="1dd90-119">통합 개요는 [SQL Data Warehouse 통합 개요][SQL Data Warehouse integration overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1dd90-119">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>
<span data-ttu-id="1dd90-120">더 많은 개발 팁은 [SQL Data Warehouse 개발 개요][SQL Data Warehouse development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1dd90-120">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

