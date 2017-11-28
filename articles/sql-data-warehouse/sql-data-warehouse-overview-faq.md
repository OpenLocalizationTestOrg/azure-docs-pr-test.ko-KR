---
title: "aaaAzure SQL 데이터 웨어하우스 질문과 대답 | Microsoft Docs"
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
ms.openlocfilehash: 09fd3f65d9507b09fcb8f477742c7d020add2755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a><span data-ttu-id="e6a64-103">SQL Data Warehouse에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="e6a64-103">SQL Data Warehouse Frequently asked questions</span></span>

## <a name="general"></a><span data-ttu-id="e6a64-104">일반</span><span class="sxs-lookup"><span data-stu-id="e6a64-104">General</span></span>

<span data-ttu-id="e6a64-105">Q.</span><span class="sxs-lookup"><span data-stu-id="e6a64-105">Q.</span></span> <span data-ttu-id="e6a64-106">SQL DW는 데이터 보안을 위해 어떤 기능을 제공하나요?</span><span class="sxs-lookup"><span data-stu-id="e6a64-106">What does SQL DW offer for data security?</span></span>

<span data-ttu-id="e6a64-107">A.</span><span class="sxs-lookup"><span data-stu-id="e6a64-107">A.</span></span> <span data-ttu-id="e6a64-108">SQL DW는 TDE 및 감사와 같이 데이터를 보호하기 위한 몇 가지 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a64-108">SQL DW offers several solutions for protecting data such as TDE and auditing.</span></span> <span data-ttu-id="e6a64-109">자세한 내용은 [보안]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6a64-109">For more information, see [Security].</span></span>

<span data-ttu-id="e6a64-110">Q.</span><span class="sxs-lookup"><span data-stu-id="e6a64-110">Q.</span></span> <span data-ttu-id="e6a64-111">SQL DW와 호환되는 법적 또는 비즈니스 표준은 어디에서 확인할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="e6a64-111">Where can I find out what legal or business standards is SQL DW compliant with?</span></span>

<span data-ttu-id="e6a64-112">A.</span><span class="sxs-lookup"><span data-stu-id="e6a64-112">A.</span></span> <span data-ttu-id="e6a64-113">Hello 방문 [Microsoft 준수] SOC 및 ISO와 같은 제품에 의해 다양 한 규정 준수 기능에 대 한 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a64-113">Visit hello [Microsoft Compliance] page for various compliance offerings by product such as SOC and ISO.</span></span> <span data-ttu-id="e6a64-114">먼저 규정 준수 제목으로 선택한 다음 확장 Azure의 hello 페이지 toosee hello 범위 내 Microsoft 클라우드 서비스 섹션 hello 오른쪽에 있는 Azure 서비스를 서비스는 규격입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a64-114">First choose by Compliance title, then expand Azure in hello Microsoft in-scope cloud services section on hello right side of hello page toosee what services are Azure services are compliant.</span></span>

<span data-ttu-id="e6a64-115">Q.</span><span class="sxs-lookup"><span data-stu-id="e6a64-115">Q.</span></span> <span data-ttu-id="e6a64-116">PowerBI를 연결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="e6a64-116">Can I connect PowerBI?</span></span>

<span data-ttu-id="e6a64-117">A.</span><span class="sxs-lookup"><span data-stu-id="e6a64-117">A.</span></span> <span data-ttu-id="e6a64-118">예!</span><span class="sxs-lookup"><span data-stu-id="e6a64-118">Yes!</span></span> <span data-ttu-id="e6a64-119">PowerBI는 SQL DW를 사용한 직접 쿼리를 지원하지만 많은 수의 사용자 또는 실시간 데이터용은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e6a64-119">Though PowerBI supports direct query with SQL DW, it’s not intended for large number of users or real-time data.</span></span> <span data-ttu-id="e6a64-120">PowerBI를 프로덕션용으로 사용하는 경우 Azure Analysis Services 또는 Analysis Services IaaS에서 PowerBI를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a64-120">For production use of PowerBI, we recommend using PowerBI on top of Azure Analysis Services or Analysis Service IaaS.</span></span> 

<span data-ttu-id="e6a64-121">Q.</span><span class="sxs-lookup"><span data-stu-id="e6a64-121">Q.</span></span> <span data-ttu-id="e6a64-122">SQL Data Warehouse 용량 제한은 얼마인가요?</span><span class="sxs-lookup"><span data-stu-id="e6a64-122">What are SQL Data Warehouse Capacity Limits?</span></span>

<span data-ttu-id="e6a64-123">A.</span><span class="sxs-lookup"><span data-stu-id="e6a64-123">A.</span></span> <span data-ttu-id="e6a64-124">현재 [용량 제한] 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6a64-124">See our current [capacity limits] page.</span></span> 

<span data-ttu-id="e6a64-125">Q.</span><span class="sxs-lookup"><span data-stu-id="e6a64-125">Q.</span></span> <span data-ttu-id="e6a64-126">크기 조정/일시 중지/계속 작업이 너무 오래 걸리는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="e6a64-126">Why is my Scale/Pause/Resume taking so long?</span></span>

<span data-ttu-id="e6a64-127">A.</span><span class="sxs-lookup"><span data-stu-id="e6a64-127">A.</span></span> <span data-ttu-id="e6a64-128">다양 한 요인 계산 관리 작업에 대 한 hello 시간에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a64-128">A variety of factors can influence hello time for compute management operations.</span></span> <span data-ttu-id="e6a64-129">장기 실행 작업의 일반적인 경우는 트랜잭션 롤백입니다.</span><span class="sxs-lookup"><span data-stu-id="e6a64-129">A common case for  long running operations is transactional rollback.</span></span> <span data-ttu-id="e6a64-130">크기 조정 또는 일시 중지 작업이 시작되면 들어오는 모든 세션이 차단되고 쿼리가 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6a64-130">When a scale or pause operation is initiated, all incoming sessions are blocked and queries are drained.</span></span> <span data-ttu-id="e6a64-131">안정 된 상태가 주문 tooleave hello 시스템에서 작업을 시작할 수 있습니다 되기 전에 트랜잭션은 롤백할 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a64-131">In order tooleave hello system in a stable state, transactions must be rolled back before an operation can commence.</span></span> <span data-ttu-id="e6a64-132">더 많은 hello 수 및 트랜잭션 hello 로그 크기를 더 큰 hello, hello 시스템 tooa 안정적인 상태를 복원할 hello 긴 hello 작업이 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6a64-132">hello greater hello number and larger hello log size of transactions, hello longer hello operation will be stalled restoring hello system tooa stable state.</span></span>

## <a name="user-support"></a><span data-ttu-id="e6a64-133">사용자 지원</span><span class="sxs-lookup"><span data-stu-id="e6a64-133">User support</span></span>

<span data-ttu-id="e6a64-134">Q.</span><span class="sxs-lookup"><span data-stu-id="e6a64-134">Q.</span></span> <span data-ttu-id="e6a64-135">기능 요청이 있는 경우 어디에 제출하나요?</span><span class="sxs-lookup"><span data-stu-id="e6a64-135">I have a feature request, where do I submit it?</span></span>

<span data-ttu-id="e6a64-136">A.</span><span class="sxs-lookup"><span data-stu-id="e6a64-136">A.</span></span> <span data-ttu-id="e6a64-137">기능 요청이 있는 경우 [UserVoice] 페이지에 제출하세요.</span><span class="sxs-lookup"><span data-stu-id="e6a64-137">If you have a feature request, submit it on our [UserVoice] page</span></span>

<span data-ttu-id="e6a64-138">Q.</span><span class="sxs-lookup"><span data-stu-id="e6a64-138">Q.</span></span> <span data-ttu-id="e6a64-139">어떻게 하면 될까요?</span><span class="sxs-lookup"><span data-stu-id="e6a64-139">How can I do x?</span></span>

<span data-ttu-id="e6a64-140">A.</span><span class="sxs-lookup"><span data-stu-id="e6a64-140">A.</span></span> <span data-ttu-id="e6a64-141">SQL Data Warehouse를 사용하는 개발에 도움이 필요한 경우 [스택 오버플로] 페이지에서 질문할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a64-141">For help in developing with SQL Data Warehouse, you can ask questions on our [Stack Overflow] page.</span></span> 

<span data-ttu-id="e6a64-142">Q.</span><span class="sxs-lookup"><span data-stu-id="e6a64-142">Q.</span></span> <span data-ttu-id="e6a64-143">지원 티켓을 제출하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="e6a64-143">How do I submit a support ticket?</span></span>

<span data-ttu-id="e6a64-144">A.</span><span class="sxs-lookup"><span data-stu-id="e6a64-144">A.</span></span> <span data-ttu-id="e6a64-145">[지원 티켓]은 Azure Portal을 통해 정리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a64-145">[Support Tickets] can be filed through Azure portal.</span></span>

## <a name="sql-languagefeature-support"></a><span data-ttu-id="e6a64-146">SQL 언어/기능 지원</span><span class="sxs-lookup"><span data-stu-id="e6a64-146">SQL language/feature support</span></span> 

<span data-ttu-id="e6a64-147">Q.</span><span class="sxs-lookup"><span data-stu-id="e6a64-147">Q.</span></span> <span data-ttu-id="e6a64-148">SQL Data Warehouse는 어떤 데이터 형식을 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="e6a64-148">What datatypes does SQL Data Warehouse support?</span></span>

<span data-ttu-id="e6a64-149">A.</span><span class="sxs-lookup"><span data-stu-id="e6a64-149">A.</span></span> <span data-ttu-id="e6a64-150">SQL Data Warehouse [데이터 형식]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6a64-150">See SQL Data Warehouse [data types].</span></span>

<span data-ttu-id="e6a64-151">Q.</span><span class="sxs-lookup"><span data-stu-id="e6a64-151">Q.</span></span> <span data-ttu-id="e6a64-152">어떤 테이블 기능이 지원되나요?</span><span class="sxs-lookup"><span data-stu-id="e6a64-152">What table features do you support?</span></span>

<span data-ttu-id="e6a64-153">A.</span><span class="sxs-lookup"><span data-stu-id="e6a64-153">A.</span></span> <span data-ttu-id="e6a64-154">SQL Data Warehouse는 많은 기능을 지원하지만 일부 지원되지 않는 기능은 [지원되지 않는 테이블 기능]에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a64-154">While SQL Data Warehouse supports many features, some are not supported and are documented in [Unsupported Table Features].</span></span>

## <a name="tooling-and-administration"></a><span data-ttu-id="e6a64-155">도구 및 관리</span><span class="sxs-lookup"><span data-stu-id="e6a64-155">Tooling and administration</span></span>

<span data-ttu-id="e6a64-156">Q.</span><span class="sxs-lookup"><span data-stu-id="e6a64-156">Q.</span></span> <span data-ttu-id="e6a64-157">Visual Studio에서 데이터베이스 프로젝트가 지원되나요?</span><span class="sxs-lookup"><span data-stu-id="e6a64-157">Do you support Database projects in Visual Studio.</span></span>

<span data-ttu-id="e6a64-158">A.</span><span class="sxs-lookup"><span data-stu-id="e6a64-158">A.</span></span> <span data-ttu-id="e6a64-159">현재 Visual Studio에서는 SQL Data Warehouse용 데이터베이스 프로젝트가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a64-159">We currently do not support Database projects in Visual Studio for SQL Data Warehouse.</span></span> <span data-ttu-id="e6a64-160">Toocast 원하는 경우 투표 tooget이 기능을 통해 사용자 의견을 방문 [데이터베이스 프로젝트 기능 요청]합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a64-160">If you'd like toocast a vote tooget this feature, visit our User Voice [Database projects feature request].</span></span>

<span data-ttu-id="e6a64-161">Q.</span><span class="sxs-lookup"><span data-stu-id="e6a64-161">Q.</span></span> <span data-ttu-id="e6a64-162">SQL Data Warehouse는 REST API를 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="e6a64-162">Does SQL Data Warehouse support REST APIs?</span></span>

<span data-ttu-id="e6a64-163">A.</span><span class="sxs-lookup"><span data-stu-id="e6a64-163">A.</span></span> <span data-ttu-id="e6a64-164">예.</span><span class="sxs-lookup"><span data-stu-id="e6a64-164">Yes.</span></span> <span data-ttu-id="e6a64-165">SQL Database와 함께 사용할 수 있는 REST 기능 대부분을 SQL Data Warehouse에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a64-165">Most REST functionality that can be used with SQL Database is also available with SQL Data Warehouse.</span></span> <span data-ttu-id="e6a64-166">REST 설명서 페이지 또는 [MSDN]에서 이 API 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a64-166">You can find API information within REST documentation pages or [MSDN].</span></span>


## <a name="loading"></a><span data-ttu-id="e6a64-167">로드</span><span class="sxs-lookup"><span data-stu-id="e6a64-167">Loading</span></span>

<span data-ttu-id="e6a64-168">Q.</span><span class="sxs-lookup"><span data-stu-id="e6a64-168">Q.</span></span> <span data-ttu-id="e6a64-169">어떤 클라이언트 드라이버가 지원되나요?</span><span class="sxs-lookup"><span data-stu-id="e6a64-169">What client drivers do you support?</span></span>

<span data-ttu-id="e6a64-170">A.</span><span class="sxs-lookup"><span data-stu-id="e6a64-170">A.</span></span> <span data-ttu-id="e6a64-171">Hello에 DW에 대 한 드라이버 지원이 있습니다 [연결 문자열] 페이지</span><span class="sxs-lookup"><span data-stu-id="e6a64-171">Driver support for DW can be found on hello [Connection Strings] page</span></span>

<span data-ttu-id="e6a64-172">Q: SQL Data Warehouse를 사용하는 PolyBase는 어떤 파일 형식을 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="e6a64-172">Q: What file formats are supported by PolyBase with SQL Data Warehouse?</span></span>

<span data-ttu-id="e6a64-173">A: Orc, RC, Parquet 및 일반 구분 텍스트</span><span class="sxs-lookup"><span data-stu-id="e6a64-173">A: Orc, RC, Parquet, and flat delimited text</span></span>

<span data-ttu-id="e6a64-174">Q: 수 toofrom SQL DW PolyBase를 사용 하 여 연결 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="e6a64-174">Q: What can I connect toofrom SQL DW using PolyBase?</span></span> 

<span data-ttu-id="e6a64-175">A: [Azure Data Lake Store] 및 [Azure Storage Blob]</span><span class="sxs-lookup"><span data-stu-id="e6a64-175">A: [Azure Data Lake Store] and [Azure Storage Blobs]</span></span>

<span data-ttu-id="e6a64-176">Q: 연결 하는 저장소 Blob 또는 ADLS tooAzure 때 가능한 계산 푸시 다운을 인가요?</span><span class="sxs-lookup"><span data-stu-id="e6a64-176">Q: Is computation pushdown possible  when connecting tooAzure Storage Blobs or ADLS?</span></span> 

<span data-ttu-id="e6a64-177">A: 아니요, SQL DW PolyBase는만 hello 저장소 구성 요소 상호 작용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6a64-177">A: No, SQL DW PolyBase only interacts hello storage components.</span></span> 

<span data-ttu-id="e6a64-178">Q: tooHDI를 연결할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="e6a64-178">Q: Can I connect tooHDI?</span></span>

<span data-ttu-id="e6a64-179">A: HDI ADLS 또는 WASB hello HDFS 계층 기호로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a64-179">A: HDI can use either ADLS or WASB as hello HDFS layer.</span></span> <span data-ttu-id="e6a64-180">둘 중 하나를 HDFS 계층으로 사용하는 경우 해당 데이터를 SQL DW에 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a64-180">If you have either as your HDFS layer, then you can load that data into SQL DW.</span></span> <span data-ttu-id="e6a64-181">그러나 푸시 다운 계산 toohello HDI 인스턴스를 생성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e6a64-181">However, you cannot generate pushdown computation toohello HDI instance.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e6a64-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e6a64-182">Next steps</span></span>
<span data-ttu-id="e6a64-183">SQL Data Warehouse 전반에 대한 자세한 내용은 [개요] 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6a64-183">For more information on SQL Data Warehouse as a whole, see our [Overview] page.</span></span>


<!-- Article references -->
[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[연결 문자열]: ./sql-data-warehouse-connection-strings.md
[스택 오버플로]: http://stackoverflow.com/questions/tagged/azure-sqldw
[지원 티켓]: ./sql-data-warehouse-get-started-create-support-ticket.md
[보안]: ./sql-data-warehouse-overview-manage-security.md
[Microsoft 준수]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings
[용량 제한]: ./sql-data-warehouse-service-capacity-limits.md
[데이터 형식]: ./sql-data-warehouse-tables-data-types.md
[지원되지 않는 테이블 기능]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md
[Azure Storage Blob]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[데이터베이스 프로젝트 기능 요청]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu
[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx
[개요]: ./sql-data-warehouse-overview-faq.md