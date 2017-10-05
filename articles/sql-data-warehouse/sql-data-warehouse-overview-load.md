---
title: "Azure SQL Data Warehouse에 데이터 로드 | Microsoft Docs"
description: "SQL 데이터 웨어하우스에 데이터 로드를 위한 일반적인 시나리오에 대해 알아봅니다. 여기에는 PolyBase, Azure Blob 저장소, 플랫 파일 및 디스크 배송 사용이 포함됩니다. 타사 도구를 사용할 수도 있습니다."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 2253bf46-cf72-4de7-85ce-f267494d55fa
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: c4199a387f5cdbd477a5e348e48ba8e8b5900075
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="b650e-105">Azure SQL 데이터 웨어하우스에 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="b650e-105">Load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="b650e-106">SQL 데이터 웨어하우스로 데이터를 로드하기 위한 시나리오 옵션 및 권장 사항 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-106">A summary of the scenario options and recommendations for loading data into SQL Data Warehouse.</span></span>

<span data-ttu-id="b650e-107">데이터 로드에서 가장 어려운 부분은 일반적으로 로드할 데이터를 준비하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-107">The hardest part of loading data is usually preparing the data for the load.</span></span> <span data-ttu-id="b650e-108">Azure는 Azure Blob 저장소를 다양한 서비스에 대한 공용 데이터 저장소로 사용하고 Azure 서비스 간의 통신 및 데이터 이동을 오케스트레이션하는 데 Azure Data Factory를 사용하여 로드를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-108">Azure simplifies loading by using Azure blob storage as a common data store for many of the services, and using Azure Data Factory to orchestrate communication and data movement between the Azure services.</span></span> <span data-ttu-id="b650e-109">이러한 프로세스는 MPP(대규모 병렬 처리)를 사용하는 PolyBase 기술과 통합하여 Azure Blob 저장소에서 SQL 데이터 웨어하우스로 데이터를 병렬로 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-109">These processes are integrated with PolyBase technology which uses massively parallel processing (MPP) to load data in parallel from Azure blob storage into SQL Data Warehouse.</span></span> 

<span data-ttu-id="b650e-110">샘플 데이터베이스를 로드하는 자습서의 경우 [샘플 데이터베이스 로드][Load sample databases]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b650e-110">For tutorials that load sample databases, see [Load sample databases][Load sample databases].</span></span>

## <a name="load-from-azure-blob-storage"></a><span data-ttu-id="b650e-111">Azure Blob 저장소에서 로드</span><span class="sxs-lookup"><span data-stu-id="b650e-111">Load from Azure blob storage</span></span>
<span data-ttu-id="b650e-112">SQL 데이터 웨어하우스로 데이터를 가져오는 가장 빠른 방법은 PolyBase를 사용하여 Azure Blob 저장소에서 데이터를 로드하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-112">The fastest way to import data into SQL Data Warehouse is to use PolyBase to load data from Azure blob storage.</span></span> <span data-ttu-id="b650e-113">PolyBase는 SQL 데이터 웨어하우스의 MPP(대규모 병렬 처리) 디자인을 사용하여 Azure Blob 저장소에서 병렬로 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-113">PolyBase uses SQL Data Warehouse's massively parallel processing (MPP) design to load data in parallel from Azure blob storage.</span></span> <span data-ttu-id="b650e-114">PolyBase를 사용하려면 T-SQL 명령이나 Azure Data Factory 파이프라인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-114">To use PolyBase, you can use T-SQL commands or an Azure Data Factory pipeline.</span></span>

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="b650e-115">1. PolyBase 및 T-SQL 사용</span><span class="sxs-lookup"><span data-stu-id="b650e-115">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="b650e-116">로드 프로세스 요약:</span><span class="sxs-lookup"><span data-stu-id="b650e-116">Summary of loading process:</span></span>

1. <span data-ttu-id="b650e-117">Azure Blob Storage 또는 Azure Data Lake Store로 데이터를 이동하고 텍스트 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-117">Move your data to Azure blob storage or Azure Data Lake Store and store it in text files.</span></span>
2. <span data-ttu-id="b650e-118">SQL 데이터 웨어하우스의 외부 개체를 데이터의 위치 및 형식을 정의하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-118">Configure external objects in SQL Data Warehouse to define the location and format of the data</span></span>
3. <span data-ttu-id="b650e-119">새 데이터베이스 테이블에 병렬로 데이터를 로드하기 위해 T-SQL 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-119">Run a T-SQL command to load the data in parallel into a new database table.</span></span>

<!-- 5. Schedule and run a loading job. --> 

<span data-ttu-id="b650e-120">자습서의 경우 [Azure Blob Storage에서 SQL Data Warehouse로 데이터 로드(PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b650e-120">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

### <a name="2-use-azure-data-factory"></a><span data-ttu-id="b650e-121">2. Azure Data Factory 사용</span><span class="sxs-lookup"><span data-stu-id="b650e-121">2. Use Azure Data Factory</span></span>
<span data-ttu-id="b650e-122">PolyBase를 사용하는 더 간단한 방법으로, PolyBase를 사용하여 Azure Blob 저장소에서 SQL 데이터 웨어하우스로 데이터를 로드하는 Azure Data Factory 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-122">For a simpler way to use PolyBase, you can create an Azure Data Factory pipeline that uses PolyBase to load data from Azure blob storage into SQL Data Warehouse.</span></span> <span data-ttu-id="b650e-123">이 방법은 T-SQL 개체를 정의할 필요가 없으므로 구성이 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-123">This is fast to configure since you don't need to define the T-SQL objects.</span></span> <span data-ttu-id="b650e-124">외부 데이터를 가져오지 않고 쿼리를 해야 하는 경우 T-SQL을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-124">If you need to query the external data without importing it, use T-SQL.</span></span> 

<span data-ttu-id="b650e-125">로드 프로세스 요약:</span><span class="sxs-lookup"><span data-stu-id="b650e-125">Summary of loading process:</span></span>

1. <span data-ttu-id="b650e-126">Azure Blob 저장소로 데이터를 이동하고 텍스트 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-126">Move your data to Azure blob storage and store it in text files.</span></span> <span data-ttu-id="b650e-127">Azure Data Factory는 현재 PolyBase와의 ADLS 연결을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-127">Azure Data Factory does not currently support ADLS connectivity with PolyBase).</span></span>
2. <span data-ttu-id="b650e-128">데이터를 수집할 Azure Data Factory 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-128">Create an Azure Data Factory pipeline to ingest the data.</span></span> <span data-ttu-id="b650e-129">PolyBase 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-129">Use the PolyBase option.</span></span>
4. <span data-ttu-id="b650e-130">파이프라인을 예약 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-130">Schedule and run the pipeline.</span></span>

<span data-ttu-id="b650e-131">자습서의 경우 [Azure Blob Storage에서 SQL Data Warehouse로 데이터 로드(Azure Data Factory)][Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b650e-131">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)].</span></span>

## <a name="load-from-sql-server"></a><span data-ttu-id="b650e-132">SQL Server에서 로드</span><span class="sxs-lookup"><span data-stu-id="b650e-132">Load from SQL Server</span></span>
<span data-ttu-id="b650e-133">Integration Services(SSIS)를 사용하거나, 플랫 파일을 전송하거나, Microsoft로 디스크를 배송하여 SQL Server에서 SQL 데이터 웨어하우스로 데이터를 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-133">To load data from SQL Server to SQL Data Warehouse you can use Integration Services (SSIS), transfer flat files, or ship disks to Microsoft.</span></span> <span data-ttu-id="b650e-134">다른 로드 프로세스 요약 및 자습서에 대한 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b650e-134">Read on to see a summary of the different loading processes and links to tutorials.</span></span>

<span data-ttu-id="b650e-135">SQL Server에서 SQL Data Warehouse로 전체 데이터 마이그레이션을 계획하려면 [마이그레이션 개요][Migration overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b650e-135">To plan a full data migration from SQL Server to SQL Data Warehouse, see the [Migration overview][Migration overview].</span></span> 

### <a name="use-integration-services-ssis"></a><span data-ttu-id="b650e-136">Integration Services(SSIS) 사용</span><span class="sxs-lookup"><span data-stu-id="b650e-136">Use Integration Services (SSIS)</span></span>
<span data-ttu-id="b650e-137">이미 Integration Services(SSIS) 패키지를 사용하여 SQL Server에 로드하고 있다면 패키지를 업데이트하여 SQL Server를 원본으로, SQL 데이터 웨어하우스를 대상으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-137">If you are already using Integration Services (SSIS) packages to load into SQL Server, you can update your packages to use SQL Server as the source and SQL Data Warehouse as the destination.</span></span> <span data-ttu-id="b650e-138">이 방법은 빠르고 수행하기 쉬우며, 클라우드에서 데이터를 사용하기 위한 로드 프로세스 마이그레이션을 아직 시도하지 않은 경우에 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-138">This is quick and easy to do, and is a good choice if you are not trying to migrate your loading process to use data already in the cloud.</span></span> <span data-ttu-id="b650e-139">단점은 이 SSIS는 병렬 로드를 수행하지 않으므로 PolyBase를 사용하는 것보다 속도가 느릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-139">The tradeoff is the load will be slower than using PolyBase because this SSIS does not perform the load in parallel.</span></span>

<span data-ttu-id="b650e-140">로드 프로세스 요약:</span><span class="sxs-lookup"><span data-stu-id="b650e-140">Summary of loading process:</span></span>

1. <span data-ttu-id="b650e-141">원본용으로 SQL Server 인스턴스를 가리키고 대상용으로 SQL 데이터 웨어하우스 데이터베이스를 가리키도록 Integration Services 패키지를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-141">Revise your Integration Services package to point to the SQL Server instance for the source and the SQL Data Warehouse database for the destination.</span></span>
2. <span data-ttu-id="b650e-142">SQL 데이터 웨어하우스에 아직 스키마가 없는 경우 스키마를 SQL 데이터 웨어하우스로 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-142">Migrate your schema to SQL Data Warehouse, if it is not there already.</span></span>
3. <span data-ttu-id="b650e-143">SQL 데이터 웨어하우스에서 지원되는 데이터 형식만 사용하도록 패키지의 매핑을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-143">Change the mapping in your packages use only the data types that are supported by SQL Data Warehouse.</span></span>
4. <span data-ttu-id="b650e-144">패키지를 예약 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-144">Schedule and run the package.</span></span>

<span data-ttu-id="b650e-145">자습서의 경우 [SQL Server에서 Azure SQL Data Warehouse로 데이터 로드(SSIS)][Load data from SQL Server to Azure SQL Data Warehouse (SSIS)]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b650e-145">For a tutorial, see [Load data from SQL Server to Azure SQL Data Warehouse (SSIS)][Load data from SQL Server to Azure SQL Data Warehouse (SSIS)].</span></span>

### <a name="use-azcopy-recommended-for--10-tb-data"></a><span data-ttu-id="b650e-146">AZCopy 사용(10TB 미만의 데이터에 권장)</span><span class="sxs-lookup"><span data-stu-id="b650e-146">Use AZCopy (recommended for < 10 TB data)</span></span>
<span data-ttu-id="b650e-147">데이터 크기가 10TB 미만일 경우 SQL Server에서 플랫 파일로 데이터를 내보내고 Azure Blob 저장소에 파일을 복사한 다음 PolyBase를 사용하여 SQL 데이터 웨어하우스로 데이터를 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-147">If your data size is < 10 TB, you can export the data from SQL Server to flat files, copy the files to Azure blob storage, and then use PolyBase to load the data into SQL Data Warehouse</span></span>

<span data-ttu-id="b650e-148">로드 프로세스 요약:</span><span class="sxs-lookup"><span data-stu-id="b650e-148">Summary of loading process:</span></span>

1. <span data-ttu-id="b650e-149">bcp 명령줄 유틸리티를 사용하여 SQL Server에서 플랫 파일로 데이터를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-149">Use the bcp command-line utility to export data from SQL Server to flat files.</span></span>
2. <span data-ttu-id="b650e-150">AZCopy 명령줄 유틸리티를 사용하여 플랫 파일에서 Azure Blob 저장소로 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-150">Use the AZCopy command-line utility to copy data from flat files to Azure blob storage.</span></span>
3. <span data-ttu-id="b650e-151">PolyBase를 사용하여 SQL 데이터 웨어하우스로 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-151">Use PolyBase to load into SQL Data Warehouse.</span></span>

<span data-ttu-id="b650e-152">자습서의 경우 [Azure Blob Storage에서 SQL Data Warehouse로 데이터 로드(PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b650e-152">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

### <a name="use-bcp"></a><span data-ttu-id="b650e-153">bcp 사용</span><span class="sxs-lookup"><span data-stu-id="b650e-153">Use bcp</span></span>
<span data-ttu-id="b650e-154">데이터의 양이 적을 경우 bcp를 사용하여 Azure SQL 데이터 웨어하우스에 직접 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-154">If you have a small amount of data you can use bcp to load directly into Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="b650e-155">로드 프로세스 요약:</span><span class="sxs-lookup"><span data-stu-id="b650e-155">Summary of loading process:</span></span>

1. <span data-ttu-id="b650e-156">bcp 명령줄 유틸리티를 사용하여 SQL Server에서 플랫 파일로 데이터를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-156">Use the bcp command-line utility to export data from SQL Server to flat files.</span></span>
2. <span data-ttu-id="b650e-157">bcp를 사용하여 플랫 파일에서 SQL 데이터 웨어하우스로 데이터를 직접 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-157">Use bcp to load data from flat files directly to SQL Data Warehouse.</span></span>

<span data-ttu-id="b650e-158">자습서의 경우 [SQL Server에서 Azure SQL Data Warehouse로 데이터 로드(bcp)][Load data from SQL Server to Azure SQL Data Warehouse (bcp)]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b650e-158">For a tutorial, see [Load data from SQL Server to Azure SQL Data Warehouse (bcp)][Load data from SQL Server to Azure SQL Data Warehouse (bcp)].</span></span>

### <a name="use-importexport-recommended-for--10-tb-data"></a><span data-ttu-id="b650e-159">가져오기/내보내기 사용(10TB를 초과하는 데이터에 권장)</span><span class="sxs-lookup"><span data-stu-id="b650e-159">Use Import/Export (recommended for > 10 TB data)</span></span>
<span data-ttu-id="b650e-160">10TB를 초과하는 크기의 데이터를 Azure로 이동하려는 경우 디스크 전달 서비스인 [Import/Export][Import/Export]를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-160">If your data size is > 10 TB and you want to move it to Azure, we recommend that you use our disk shipping service [Import/Export][Import/Export].</span></span> 

<span data-ttu-id="b650e-161">로드 프로세스 요약</span><span class="sxs-lookup"><span data-stu-id="b650e-161">Summary of loading process</span></span>

1. <span data-ttu-id="b650e-162">bcp 명령줄 유틸리티를 사용하여 SQL Server에서 전송 가능한 디스크에 있는 플랫 파일로 데이터를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-162">Use the bcp command-line utility to export data from SQL Server to flat files on transferrable disks.</span></span>
2. <span data-ttu-id="b650e-163">Microsoft에 디스크를 배송합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-163">Ship the disks to Microsoft.</span></span>
3. <span data-ttu-id="b650e-164">Microsoft는 SQL 데이터 웨어하우스에 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-164">Microsoft loads the data into SQL Data Warehouse</span></span>

## <a name="load-from-hdinsight"></a><span data-ttu-id="b650e-165">HDInsight에서 로드</span><span class="sxs-lookup"><span data-stu-id="b650e-165">Load from HDInsight</span></span>
<span data-ttu-id="b650e-166">SQL 데이터 웨어하우스는 PolyBase 통해 HDInsight에서 데이터 로드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-166">SQL Data Warehouse supports loading data from HDInsight via PolyBase.</span></span> <span data-ttu-id="b650e-167">프로세스는 Azure Blob 저장소에서 데이터를 로드할 때와 같이 PolyBase를 사용하여 HDInsight에 연결하여 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-167">The process is the same as loading data from Azure Blob Storage - using PolyBase to connect to HDInsight to load data.</span></span> 

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="b650e-168">1. PolyBase 및 T-SQL 사용</span><span class="sxs-lookup"><span data-stu-id="b650e-168">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="b650e-169">로드 프로세스 요약:</span><span class="sxs-lookup"><span data-stu-id="b650e-169">Summary of loading process:</span></span>

1. <span data-ttu-id="b650e-170">HDInsight로 데이터를 이동하고 ORC 또는 Parquet 형식으로 텍스트 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-170">Move your data to HDInsight and store it in text files, ORC or Parquet format.</span></span>
2. <span data-ttu-id="b650e-171">SQL 데이터 웨어하우스의 외부 개체를 데이터의 위치 및 형식을 정의하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-171">Configure external objects in SQL Data Warehouse to define the location and format of the data.</span></span>
3. <span data-ttu-id="b650e-172">새 데이터베이스 테이블에 병렬로 데이터를 로드하기 위해 T-SQL 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-172">Run a T-SQL command to load the data in parallel into a new database table.</span></span>

<span data-ttu-id="b650e-173">자습서의 경우 [Azure Blob Storage에서 SQL Data Warehouse로 데이터 로드(PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b650e-173">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

## <a name="recommendations"></a><span data-ttu-id="b650e-174">추천</span><span class="sxs-lookup"><span data-stu-id="b650e-174">Recommendations</span></span>
<span data-ttu-id="b650e-175">상당수의 파트너에게는 로드 솔루션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-175">Many of our partners have loading solutions.</span></span> <span data-ttu-id="b650e-176">자세한 내용을 알아보려면 [솔루션 파트너][solution partners] 목록을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b650e-176">To find out more, see a list of our [solution partners][solution partners].</span></span> 

<span data-ttu-id="b650e-177">비관계형 원본에서 가져온 데이터를 SQL 데이터 웨어하우스로 로드하려는 경우 로드하기 전에 데이터를 행과 열로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-177">If your data is coming from a non-relational source and you want to load it into SQL Data Warehouse you will need to transform it into rows and columns before you load it.</span></span> <span data-ttu-id="b650e-178">변환된 데이터는 데이터베이스에 저장할 필요 없이 텍스트 파일에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-178">The transformed data doesn't need to be stored in a database, it can be stored in text files.</span></span>

<span data-ttu-id="b650e-179">새로 로드한 데이터에 대한 통계를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-179">Create statistics on newly loaded data.</span></span> <span data-ttu-id="b650e-180">Azure SQL 데이터 웨어하우스는 자동 만들기 또는 통계 자동 업데이트를 아직 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="b650e-181">쿼리에서 최상의 성능을 얻으려면, 데이터를 처음 로드하거나 데이터에 상당한 변화가 발생한 후에 모든 테이블의 모든 열에서 통계가 만들어지는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="b650e-181">In order to get the best performance from your queries, it's important to create statistics on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="b650e-182">자세한 내용은 [통계][Statistics]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b650e-182">For details, see [Statistics][Statistics].</span></span>

## <a name="next-steps"></a><span data-ttu-id="b650e-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b650e-183">Next steps</span></span>
<span data-ttu-id="b650e-184">더 많은 개발 팁은 [개발 개요][development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b650e-184">For more development tips, see the [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage to SQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server to Azure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server to Azure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server to Azure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
