---
title: "Azure SQL Data Warehouse에 대한 질문과 대답 | Microsoft Docs"
description: "이 문서에는 고객 및 개발자를 위한 Azure SQL Data Warehouse 관련 질문과 대답이 나와 있습니다."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 812CA525-3BF3-49DF-8DF3-FB4342464F4F
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 3/1/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 4c00710ecc0c91f8407eca81b78176075fcbd6ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a><span data-ttu-id="7b465-103">SQL Data Warehouse에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="7b465-103">SQL Data Warehouse Frequently asked questions</span></span>

## <a name="general"></a><span data-ttu-id="7b465-104">일반</span><span class="sxs-lookup"><span data-stu-id="7b465-104">General</span></span>

<span data-ttu-id="7b465-105">Q.</span><span class="sxs-lookup"><span data-stu-id="7b465-105">Q.</span></span> <span data-ttu-id="7b465-106">SQL DW는 데이터 보안을 위해 어떤 기능을 제공하나요?</span><span class="sxs-lookup"><span data-stu-id="7b465-106">What does SQL DW offer for data security?</span></span>

<span data-ttu-id="7b465-107">A.</span><span class="sxs-lookup"><span data-stu-id="7b465-107">A.</span></span> <span data-ttu-id="7b465-108">SQL DW는 TDE 및 감사와 같이 데이터를 보호하기 위한 몇 가지 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7b465-108">SQL DW offers several solutions for protecting data such as TDE and auditing.</span></span> <span data-ttu-id="7b465-109">자세한 내용은 [보안]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b465-109">For more information, see [Security].</span></span>

<span data-ttu-id="7b465-110">Q.</span><span class="sxs-lookup"><span data-stu-id="7b465-110">Q.</span></span> <span data-ttu-id="7b465-111">SQL DW와 호환되는 법적 또는 비즈니스 표준은 어디에서 확인할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7b465-111">Where can I find out what legal or business standards is SQL DW compliant with?</span></span>

<span data-ttu-id="7b465-112">A.</span><span class="sxs-lookup"><span data-stu-id="7b465-112">A.</span></span> <span data-ttu-id="7b465-113">SOC 및 ISO와 같은 제품에 대한 다양한 규정 준수 제안에 대해서는 [Microsoft 규정 준수] 페이지를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="7b465-113">Visit the [Microsoft Compliance] page for various compliance offerings by product such as SOC and ISO.</span></span> <span data-ttu-id="7b465-114">먼저 규정 준수 제목으로 선택하고, 페이지 오른쪽의 Microsoft 범위 내 클라우드 서비스 섹션에서 Azure를 확장하여 Azure 서비스와 호환되는 서비스를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7b465-114">First choose by Compliance title, then expand Azure in the Microsoft in-scope cloud services section on the right side of the page to see what services are Azure services are compliant.</span></span>

<span data-ttu-id="7b465-115">Q.</span><span class="sxs-lookup"><span data-stu-id="7b465-115">Q.</span></span> <span data-ttu-id="7b465-116">PowerBI를 연결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7b465-116">Can I connect PowerBI?</span></span>

<span data-ttu-id="7b465-117">A.</span><span class="sxs-lookup"><span data-stu-id="7b465-117">A.</span></span> <span data-ttu-id="7b465-118">예!</span><span class="sxs-lookup"><span data-stu-id="7b465-118">Yes!</span></span> <span data-ttu-id="7b465-119">PowerBI는 SQL DW를 사용한 직접 쿼리를 지원하지만 많은 수의 사용자 또는 실시간 데이터용은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7b465-119">Though PowerBI supports direct query with SQL DW, it’s not intended for large number of users or real-time data.</span></span> <span data-ttu-id="7b465-120">PowerBI를 프로덕션용으로 사용하는 경우 Azure Analysis Services 또는 Analysis Services IaaS에서 PowerBI를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7b465-120">For production use of PowerBI, we recommend using PowerBI on top of Azure Analysis Services or Analysis Service IaaS.</span></span> 

<span data-ttu-id="7b465-121">Q.</span><span class="sxs-lookup"><span data-stu-id="7b465-121">Q.</span></span> <span data-ttu-id="7b465-122">SQL Data Warehouse 용량 제한은 얼마인가요?</span><span class="sxs-lookup"><span data-stu-id="7b465-122">What are SQL Data Warehouse Capacity Limits?</span></span>

<span data-ttu-id="7b465-123">A.</span><span class="sxs-lookup"><span data-stu-id="7b465-123">A.</span></span> <span data-ttu-id="7b465-124">현재 [용량 제한] 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b465-124">See our current [capacity limits] page.</span></span> 

<span data-ttu-id="7b465-125">Q.</span><span class="sxs-lookup"><span data-stu-id="7b465-125">Q.</span></span> <span data-ttu-id="7b465-126">크기 조정/일시 중지/계속 작업이 너무 오래 걸리는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="7b465-126">Why is my Scale/Pause/Resume taking so long?</span></span>

<span data-ttu-id="7b465-127">A.</span><span class="sxs-lookup"><span data-stu-id="7b465-127">A.</span></span> <span data-ttu-id="7b465-128">다양한 요인이 계산 관리 작업 시간에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b465-128">A variety of factors can influence the time for compute management operations.</span></span> <span data-ttu-id="7b465-129">장기 실행 작업의 일반적인 경우는 트랜잭션 롤백입니다.</span><span class="sxs-lookup"><span data-stu-id="7b465-129">A common case for  long running operations is transactional rollback.</span></span> <span data-ttu-id="7b465-130">크기 조정 또는 일시 중지 작업이 시작되면 들어오는 모든 세션이 차단되고 쿼리가 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b465-130">When a scale or pause operation is initiated, all incoming sessions are blocked and queries are drained.</span></span> <span data-ttu-id="7b465-131">시스템을 안정된 상태로 유지하기 위해서는 작업을 시작하기 전에 트랜잭션을 롤백해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b465-131">In order to leave the system in a stable state, transactions must be rolled back before an operation can commence.</span></span> <span data-ttu-id="7b465-132">트랜잭션의 수가 많고 로그 크기가 클수록 시스템을 안정된 상태로 복원하기 위해 작업이 더 오래 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b465-132">The greater the number and larger the log size of transactions, the longer the operation will be stalled restoring the system to a stable state.</span></span>

## <a name="user-support"></a><span data-ttu-id="7b465-133">사용자 지원</span><span class="sxs-lookup"><span data-stu-id="7b465-133">User support</span></span>

<span data-ttu-id="7b465-134">Q.</span><span class="sxs-lookup"><span data-stu-id="7b465-134">Q.</span></span> <span data-ttu-id="7b465-135">기능 요청이 있는 경우 어디에 제출하나요?</span><span class="sxs-lookup"><span data-stu-id="7b465-135">I have a feature request, where do I submit it?</span></span>

<span data-ttu-id="7b465-136">A.</span><span class="sxs-lookup"><span data-stu-id="7b465-136">A.</span></span> <span data-ttu-id="7b465-137">기능 요청이 있는 경우 [UserVoice] 페이지에 제출하세요.</span><span class="sxs-lookup"><span data-stu-id="7b465-137">If you have a feature request, submit it on our [UserVoice] page</span></span>

<span data-ttu-id="7b465-138">Q.</span><span class="sxs-lookup"><span data-stu-id="7b465-138">Q.</span></span> <span data-ttu-id="7b465-139">어떻게 하면 될까요?</span><span class="sxs-lookup"><span data-stu-id="7b465-139">How can I do x?</span></span>

<span data-ttu-id="7b465-140">A.</span><span class="sxs-lookup"><span data-stu-id="7b465-140">A.</span></span> <span data-ttu-id="7b465-141">SQL Data Warehouse를 사용하는 개발에 도움이 필요한 경우 [스택 오버플로] 페이지에서 질문할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b465-141">For help in developing with SQL Data Warehouse, you can ask questions on our [Stack Overflow] page.</span></span> 

<span data-ttu-id="7b465-142">Q.</span><span class="sxs-lookup"><span data-stu-id="7b465-142">Q.</span></span> <span data-ttu-id="7b465-143">지원 티켓을 제출하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="7b465-143">How do I submit a support ticket?</span></span>

<span data-ttu-id="7b465-144">A.</span><span class="sxs-lookup"><span data-stu-id="7b465-144">A.</span></span> <span data-ttu-id="7b465-145">[지원 티켓]은 Azure Portal을 통해 정리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b465-145">[Support Tickets] can be filed through Azure portal.</span></span>

## <a name="sql-languagefeature-support"></a><span data-ttu-id="7b465-146">SQL 언어/기능 지원</span><span class="sxs-lookup"><span data-stu-id="7b465-146">SQL language/feature support</span></span> 

<span data-ttu-id="7b465-147">Q.</span><span class="sxs-lookup"><span data-stu-id="7b465-147">Q.</span></span> <span data-ttu-id="7b465-148">SQL Data Warehouse는 어떤 데이터 형식을 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="7b465-148">What datatypes does SQL Data Warehouse support?</span></span>

<span data-ttu-id="7b465-149">A.</span><span class="sxs-lookup"><span data-stu-id="7b465-149">A.</span></span> <span data-ttu-id="7b465-150">SQL Data Warehouse [데이터 형식]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b465-150">See SQL Data Warehouse [data types].</span></span>

<span data-ttu-id="7b465-151">Q.</span><span class="sxs-lookup"><span data-stu-id="7b465-151">Q.</span></span> <span data-ttu-id="7b465-152">어떤 테이블 기능이 지원되나요?</span><span class="sxs-lookup"><span data-stu-id="7b465-152">What table features do you support?</span></span>

<span data-ttu-id="7b465-153">A.</span><span class="sxs-lookup"><span data-stu-id="7b465-153">A.</span></span> <span data-ttu-id="7b465-154">SQL Data Warehouse는 많은 기능을 지원하지만 일부 지원되지 않는 기능은 [지원되지 않는 테이블 기능]에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b465-154">While SQL Data Warehouse supports many features, some are not supported and are documented in [Unsupported Table Features].</span></span>

## <a name="tooling-and-administration"></a><span data-ttu-id="7b465-155">도구 및 관리</span><span class="sxs-lookup"><span data-stu-id="7b465-155">Tooling and administration</span></span>

<span data-ttu-id="7b465-156">Q.</span><span class="sxs-lookup"><span data-stu-id="7b465-156">Q.</span></span> <span data-ttu-id="7b465-157">Visual Studio에서 데이터베이스 프로젝트가 지원되나요?</span><span class="sxs-lookup"><span data-stu-id="7b465-157">Do you support Database projects in Visual Studio.</span></span>

<span data-ttu-id="7b465-158">A.</span><span class="sxs-lookup"><span data-stu-id="7b465-158">A.</span></span> <span data-ttu-id="7b465-159">현재 Visual Studio에서는 SQL Data Warehouse용 데이터베이스 프로젝트가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b465-159">We currently do not support Database projects in Visual Studio for SQL Data Warehouse.</span></span> <span data-ttu-id="7b465-160">이 기능 제공 요청에 참여하려면 사용자 의견 [데이터베이스 프로젝트 기능 요청]을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="7b465-160">If you'd like to cast a vote to get this feature, visit our User Voice [Database projects feature request].</span></span>

<span data-ttu-id="7b465-161">Q.</span><span class="sxs-lookup"><span data-stu-id="7b465-161">Q.</span></span> <span data-ttu-id="7b465-162">SQL Data Warehouse는 REST API를 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="7b465-162">Does SQL Data Warehouse support REST APIs?</span></span>

<span data-ttu-id="7b465-163">A.</span><span class="sxs-lookup"><span data-stu-id="7b465-163">A.</span></span> <span data-ttu-id="7b465-164">예.</span><span class="sxs-lookup"><span data-stu-id="7b465-164">Yes.</span></span> <span data-ttu-id="7b465-165">SQL Database와 함께 사용할 수 있는 REST 기능 대부분을 SQL Data Warehouse에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b465-165">Most REST functionality that can be used with SQL Database is also available with SQL Data Warehouse.</span></span> <span data-ttu-id="7b465-166">REST 설명서 페이지 또는 [MSDN]에서 이 API 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b465-166">You can find API information within REST documentation pages or [MSDN].</span></span>


## <a name="loading"></a><span data-ttu-id="7b465-167">로드</span><span class="sxs-lookup"><span data-stu-id="7b465-167">Loading</span></span>

<span data-ttu-id="7b465-168">Q.</span><span class="sxs-lookup"><span data-stu-id="7b465-168">Q.</span></span> <span data-ttu-id="7b465-169">어떤 클라이언트 드라이버가 지원되나요?</span><span class="sxs-lookup"><span data-stu-id="7b465-169">What client drivers do you support?</span></span>

<span data-ttu-id="7b465-170">A.</span><span class="sxs-lookup"><span data-stu-id="7b465-170">A.</span></span> <span data-ttu-id="7b465-171">DW에 대한 드라이버 지원은 [연결 문자열] 페이지에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b465-171">Driver support for DW can be found on the [Connection Strings] page</span></span>

<span data-ttu-id="7b465-172">Q: SQL Data Warehouse를 사용하는 PolyBase는 어떤 파일 형식을 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="7b465-172">Q: What file formats are supported by PolyBase with SQL Data Warehouse?</span></span>

<span data-ttu-id="7b465-173">A: Orc, RC, Parquet 및 일반 구분 텍스트</span><span class="sxs-lookup"><span data-stu-id="7b465-173">A: Orc, RC, Parquet, and flat delimited text</span></span>

<span data-ttu-id="7b465-174">Q: PolyBase를 사용하여 SQL DW에서 어디로 연결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7b465-174">Q: What can I connect to from SQL DW using PolyBase?</span></span> 

<span data-ttu-id="7b465-175">A: [Azure Data Lake Store] 및 [Azure Storage Blob]</span><span class="sxs-lookup"><span data-stu-id="7b465-175">A: [Azure Data Lake Store] and [Azure Storage Blobs]</span></span>

<span data-ttu-id="7b465-176">Q: Azure Storage Blob 또는 ADLS에 연결할 때 계산 푸시다운이 가능한가요?</span><span class="sxs-lookup"><span data-stu-id="7b465-176">Q: Is computation pushdown possible  when connecting to Azure Storage Blobs or ADLS?</span></span> 

<span data-ttu-id="7b465-177">A: 아니요. SQL DW PolyBase는 저장소 구성 요소와만 상호 작용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b465-177">A: No, SQL DW PolyBase only interacts the storage components.</span></span> 

<span data-ttu-id="7b465-178">Q: HDI에 연결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7b465-178">Q: Can I connect to HDI?</span></span>

<span data-ttu-id="7b465-179">A: HDI는 HDFS 계층으로 ADLS 또는 WASB를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b465-179">A: HDI can use either ADLS or WASB as the HDFS layer.</span></span> <span data-ttu-id="7b465-180">둘 중 하나를 HDFS 계층으로 사용하는 경우 해당 데이터를 SQL DW에 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b465-180">If you have either as your HDFS layer, then you can load that data into SQL DW.</span></span> <span data-ttu-id="7b465-181">그러나 HDI 인스턴스로의 푸시다운 계산을 생성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b465-181">However, you cannot generate pushdown computation to the HDI instance.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7b465-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7b465-182">Next steps</span></span>
<span data-ttu-id="7b465-183">SQL Data Warehouse 전반에 대한 자세한 내용은 [개요] 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b465-183">For more information on SQL Data Warehouse as a whole, see our [Overview] page.</span></span>


<!-- Article references -->
<span data-ttu-id="7b465-184">[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse</span><span class="sxs-lookup"><span data-stu-id="7b465-184">[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse</span></span>
<span data-ttu-id="7b465-185">[연결 문자열]: ./sql-data-warehouse-connection-strings.md</span><span class="sxs-lookup"><span data-stu-id="7b465-185">[Connection Strings]: ./sql-data-warehouse-connection-strings.md</span></span>
<span data-ttu-id="7b465-186">[스택 오버플로]: http://stackoverflow.com/questions/tagged/azure-sqldw</span><span class="sxs-lookup"><span data-stu-id="7b465-186">[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw</span></span>
<span data-ttu-id="7b465-187">[지원 티켓]: ./sql-data-warehouse-get-started-create-support-ticket.md</span><span class="sxs-lookup"><span data-stu-id="7b465-187">[Support Tickets]: ./sql-data-warehouse-get-started-create-support-ticket.md</span></span>
<span data-ttu-id="7b465-188">[보안]: ./sql-data-warehouse-overview-manage-security.md</span><span class="sxs-lookup"><span data-stu-id="7b465-188">[Security]: ./sql-data-warehouse-overview-manage-security.md</span></span>
<span data-ttu-id="7b465-189">[Microsoft 규정 준수]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings</span><span class="sxs-lookup"><span data-stu-id="7b465-189">[Microsoft Compliance]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings</span></span>
<span data-ttu-id="7b465-190">[용량 제한]: ./sql-data-warehouse-service-capacity-limits.md</span><span class="sxs-lookup"><span data-stu-id="7b465-190">[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md</span></span>
<span data-ttu-id="7b465-191">[데이터 형식]: ./sql-data-warehouse-tables-data-types.md</span><span class="sxs-lookup"><span data-stu-id="7b465-191">[data types]: ./sql-data-warehouse-tables-data-types.md</span></span>
<span data-ttu-id="7b465-192">[지원되지 않는 테이블 기능]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features</span><span class="sxs-lookup"><span data-stu-id="7b465-192">[Unsupported Table Features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features</span></span>
<span data-ttu-id="7b465-193">[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md</span><span class="sxs-lookup"><span data-stu-id="7b465-193">[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md</span></span>
<span data-ttu-id="7b465-194">[Azure Storage Blob]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md</span><span class="sxs-lookup"><span data-stu-id="7b465-194">[Azure Storage Blobs]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md</span></span>
<span data-ttu-id="7b465-195">[데이터베이스 프로젝트 기능 요청]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu</span><span class="sxs-lookup"><span data-stu-id="7b465-195">[Database projects feature request]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu</span></span>
<span data-ttu-id="7b465-196">[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx</span><span class="sxs-lookup"><span data-stu-id="7b465-196">[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx</span></span>
<span data-ttu-id="7b465-197">[개요]: ./sql-data-warehouse-overview-faq.md</span><span class="sxs-lookup"><span data-stu-id="7b465-197">[Overview]: ./sql-data-warehouse-overview-faq.md</span></span>