---
title: "aaaLoad 데이터를 Azure SQL 데이터 웨어하우스에 | Microsoft Docs"
description: "SQL 데이터 웨어하우스를 로드 하는 데이터에 대 한 hello 일반적인 시나리오에 알아봅니다. 여기에는 PolyBase, Azure Blob 저장소, 플랫 파일 및 디스크 배송 사용이 포함됩니다. 타사 도구를 사용할 수도 있습니다."
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
ms.openlocfilehash: d1a5063f484e9bd95f854e27a4baed512148aad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="d745a-105">Azure SQL 데이터 웨어하우스에 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="d745a-105">Load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="d745a-106">Hello 시나리오 옵션 및 SQL 데이터 웨어하우스로 데이터를 로드 하기 위한 권장 사항을 요약 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-106">A summary of hello scenario options and recommendations for loading data into SQL Data Warehouse.</span></span>

<span data-ttu-id="d745a-107">hello 부하에 대 한 데이터를 로드 하의 가장 어려운 일부 hello hello 데이터 준비 중 일반적으로입니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-107">hello hardest part of loading data is usually preparing hello data for hello load.</span></span> <span data-ttu-id="d745a-108">Azure 데이터 팩터리를 사용 하 여 사이의 통신 및 데이터 이동 tooorchestrate hello Azure 서비스를 azure hello 서비스의 대부분에 대 한 일반 데이터 저장소로 Azure blob 저장소를 사용 하 여 로드 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-108">Azure simplifies loading by using Azure blob storage as a common data store for many of hello services, and using Azure Data Factory tooorchestrate communication and data movement between hello Azure services.</span></span> <span data-ttu-id="d745a-109">이러한 프로세스는 Azure blob 저장소에서 동시에 (MPP) tooload 데이터를 SQL 데이터 웨어하우스에 방대한 병렬 처리를 사용 하 여 PolyBase 기술을와 통합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-109">These processes are integrated with PolyBase technology which uses massively parallel processing (MPP) tooload data in parallel from Azure blob storage into SQL Data Warehouse.</span></span> 

<span data-ttu-id="d745a-110">샘플 데이터베이스를 로드하는 자습서의 경우 [샘플 데이터베이스 로드][Load sample databases]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d745a-110">For tutorials that load sample databases, see [Load sample databases][Load sample databases].</span></span>

## <a name="load-from-azure-blob-storage"></a><span data-ttu-id="d745a-111">Azure Blob 저장소에서 로드</span><span class="sxs-lookup"><span data-stu-id="d745a-111">Load from Azure blob storage</span></span>
<span data-ttu-id="d745a-112">SQL 데이터 웨어하우스로 hello 가장 빠른 방법은 tooimport 데이터 toouse PolyBase tooload 데이터 Azure blob 저장소의 경우</span><span class="sxs-lookup"><span data-stu-id="d745a-112">hello fastest way tooimport data into SQL Data Warehouse is toouse PolyBase tooload data from Azure blob storage.</span></span> <span data-ttu-id="d745a-113">PolyBase 사용 하 여 SQL 데이터 웨어하우스의는 방대한 병렬 Azure blob 저장소에서 동시에 (MPP) 디자인 tooload 데이터를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-113">PolyBase uses SQL Data Warehouse's massively parallel processing (MPP) design tooload data in parallel from Azure blob storage.</span></span> <span data-ttu-id="d745a-114">PolyBase toouse T-SQL 명령이 나 Azure 데이터 팩터리 파이프라인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-114">toouse PolyBase, you can use T-SQL commands or an Azure Data Factory pipeline.</span></span>

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="d745a-115">1. PolyBase 및 T-SQL 사용</span><span class="sxs-lookup"><span data-stu-id="d745a-115">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="d745a-116">로드 프로세스 요약:</span><span class="sxs-lookup"><span data-stu-id="d745a-116">Summary of loading process:</span></span>

1. <span data-ttu-id="d745a-117">데이터 tooAzure blob 저장소 또는 Azure 데이터 레이크 저장소를 이동 하 고 텍스트 파일에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-117">Move your data tooAzure blob storage or Azure Data Lake Store and store it in text files.</span></span>
2. <span data-ttu-id="d745a-118">SQL 데이터 웨어하우스 toodefine hello 위치와 hello 데이터의 형식에 외부 개체를 구성</span><span class="sxs-lookup"><span data-stu-id="d745a-118">Configure external objects in SQL Data Warehouse toodefine hello location and format of hello data</span></span>
3. <span data-ttu-id="d745a-119">새 데이터베이스 테이블에 병렬로 T-SQL 명령 tooload hello 데이터를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-119">Run a T-SQL command tooload hello data in parallel into a new database table.</span></span>

<!-- 5. Schedule and run a loading job. --> 

<span data-ttu-id="d745a-120">자습서를 참조 하십시오. [Azure blob 저장소 tooSQL 데이터 웨어하우스 (PolyBase)에서 데이터를 로드할][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-120">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

### <a name="2-use-azure-data-factory"></a><span data-ttu-id="d745a-121">2. Azure Data Factory 사용</span><span class="sxs-lookup"><span data-stu-id="d745a-121">2. Use Azure Data Factory</span></span>
<span data-ttu-id="d745a-122">더 간단한 방법은 toouse PolyBase, SQL 데이터 웨어하우스로 PolyBase tooload 데이터 Azure blob 저장소를 사용 하는 Azure 데이터 팩터리 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-122">For a simpler way toouse PolyBase, you can create an Azure Data Factory pipeline that uses PolyBase tooload data from Azure blob storage into SQL Data Warehouse.</span></span> <span data-ttu-id="d745a-123">Toodefine hello T-SQL 개체 필요 하지 않으므로 빠른 tooconfigure입니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-123">This is fast tooconfigure since you don't need toodefine hello T-SQL objects.</span></span> <span data-ttu-id="d745a-124">Tooquery hello 외부 데이터를 가져오지 않고 해야 할 경우 T-SQL을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-124">If you need tooquery hello external data without importing it, use T-SQL.</span></span> 

<span data-ttu-id="d745a-125">로드 프로세스 요약:</span><span class="sxs-lookup"><span data-stu-id="d745a-125">Summary of loading process:</span></span>

1. <span data-ttu-id="d745a-126">사용자가 데이터 tooAzure blob 저장소를 이동 하 고 텍스트 파일에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-126">Move your data tooAzure blob storage and store it in text files.</span></span> <span data-ttu-id="d745a-127">Azure Data Factory는 현재 PolyBase와의 ADLS 연결을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-127">Azure Data Factory does not currently support ADLS connectivity with PolyBase).</span></span>
2. <span data-ttu-id="d745a-128">Azure 데이터 팩터리 파이프라인 tooingest hello 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-128">Create an Azure Data Factory pipeline tooingest hello data.</span></span> <span data-ttu-id="d745a-129">Hello PolyBase 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-129">Use hello PolyBase option.</span></span>
4. <span data-ttu-id="d745a-130">예약 하 고 hello 파이프라인을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-130">Schedule and run hello pipeline.</span></span>

<span data-ttu-id="d745a-131">자습서를 참조 하십시오. [Azure blob 저장소 tooSQL 데이터 웨어하우스 (Azure 데이터 팩터리)에서 데이터를 로드할][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-131">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].</span></span>

## <a name="load-from-sql-server"></a><span data-ttu-id="d745a-132">SQL Server에서 로드</span><span class="sxs-lookup"><span data-stu-id="d745a-132">Load from SQL Server</span></span>
<span data-ttu-id="d745a-133">tooload 데이터 tooSQL SQL Server Integration Services (SSIS)를 사용할 수는 데이터 웨어하우스를에서 플랫 파일을 전송 하거나 디스크 tooMicrosoft를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-133">tooload data from SQL Server tooSQL Data Warehouse you can use Integration Services (SSIS), transfer flat files, or ship disks tooMicrosoft.</span></span> <span data-ttu-id="d745a-134">다른 프로세스와 링크 tootutorials 로드 hello에 대 한 요약 toosee 계속 읽어 보십시오.</span><span class="sxs-lookup"><span data-stu-id="d745a-134">Read on toosee a summary of hello different loading processes and links tootutorials.</span></span>

<span data-ttu-id="d745a-135">데이터 웨어하우스 SQL Server tooSQL에서 전체 데이터 마이그레이션을 tooplan 참조 hello [마이그레이션 개요][Migration overview]합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-135">tooplan a full data migration from SQL Server tooSQL Data Warehouse, see hello [Migration overview][Migration overview].</span></span> 

### <a name="use-integration-services-ssis"></a><span data-ttu-id="d745a-136">Integration Services(SSIS) 사용</span><span class="sxs-lookup"><span data-stu-id="d745a-136">Use Integration Services (SSIS)</span></span>
<span data-ttu-id="d745a-137">SQL Server에 Integration Services (SSIS) 패키지 tooload을 이미 사용 중인 경우에 hello 소스 및 hello 대상으로 SQL 데이터 웨어하우스 사용자 패키지 toouse SQL Server를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-137">If you are already using Integration Services (SSIS) packages tooload into SQL Server, you can update your packages toouse SQL Server as hello source and SQL Data Warehouse as hello destination.</span></span> <span data-ttu-id="d745a-138">이 신속 하 게 하 고 쉽게 toodo 시도 하지 않는 toomigrate 사용자 로드에 적합 한 선택 인지 hello 클라우드에서 이미 toouse 데이터를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-138">This is quick and easy toodo, and is a good choice if you are not trying toomigrate your loading process toouse data already in hello cloud.</span></span> <span data-ttu-id="d745a-139">hello 단점은 hello 부하 PolyBase를 사용 하 여이 SSIS 병렬로 hello 부하를 수행 하지 않으므로 보다 느리다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-139">hello tradeoff is hello load will be slower than using PolyBase because this SSIS does not perform hello load in parallel.</span></span>

<span data-ttu-id="d745a-140">로드 프로세스 요약:</span><span class="sxs-lookup"><span data-stu-id="d745a-140">Summary of loading process:</span></span>

1. <span data-ttu-id="d745a-141">Hello 원본에 대 한 Integration Services 패키지 toopoint toohello SQL Server 인스턴스 및 hello 대상에 대 한 hello SQL 데이터 웨어하우스 데이터베이스를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-141">Revise your Integration Services package toopoint toohello SQL Server instance for hello source and hello SQL Data Warehouse database for hello destination.</span></span>
2. <span data-ttu-id="d745a-142">없는 아직 없는 경우 프로그램 스키마 tooSQL 데이터 웨어하우스를 마이그레이션하십시오.</span><span class="sxs-lookup"><span data-stu-id="d745a-142">Migrate your schema tooSQL Data Warehouse, if it is not there already.</span></span>
3. <span data-ttu-id="d745a-143">SQL 데이터 웨어하우스에서 지 원하는 hello 데이터 형식만 사용 하는 경우 패키지에 hello 매핑을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-143">Change hello mapping in your packages use only hello data types that are supported by SQL Data Warehouse.</span></span>
4. <span data-ttu-id="d745a-144">예약 하 고 hello 패키지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-144">Schedule and run hello package.</span></span>

<span data-ttu-id="d745a-145">자습서를 참조 하십시오. [SQL Server tooAzure SQL 데이터 웨어하우스 (SSIS)에서 데이터를 로드할][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-145">For a tutorial, see [Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].</span></span>

### <a name="use-azcopy-recommended-for--10-tb-data"></a><span data-ttu-id="d745a-146">AZCopy 사용(10TB 미만의 데이터에 권장)</span><span class="sxs-lookup"><span data-stu-id="d745a-146">Use AZCopy (recommended for < 10 TB data)</span></span>
<span data-ttu-id="d745a-147">데이터 크기 < 10TB 인 경우 SQL Server tooflat 파일에서 hello 데이터를 내보낼, hello 파일 tooAzure blob 저장소에 복사한 다음 PolyBase tooload hello 데이터를 사용 하 여 SQL 데이터 웨어하우스로</span><span class="sxs-lookup"><span data-stu-id="d745a-147">If your data size is < 10 TB, you can export hello data from SQL Server tooflat files, copy hello files tooAzure blob storage, and then use PolyBase tooload hello data into SQL Data Warehouse</span></span>

<span data-ttu-id="d745a-148">로드 프로세스 요약:</span><span class="sxs-lookup"><span data-stu-id="d745a-148">Summary of loading process:</span></span>

1. <span data-ttu-id="d745a-149">SQL Server tooflat 파일에서 hello bcp 명령줄 유틸리티 tooexport 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-149">Use hello bcp command-line utility tooexport data from SQL Server tooflat files.</span></span>
2. <span data-ttu-id="d745a-150">Hello AZCopy 명령줄 유틸리티 toocopy 플랫 파일 tooAzure blob 저장소에서 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-150">Use hello AZCopy command-line utility toocopy data from flat files tooAzure blob storage.</span></span>
3. <span data-ttu-id="d745a-151">SQL 데이터 웨어하우스로 tooload PolyBase를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-151">Use PolyBase tooload into SQL Data Warehouse.</span></span>

<span data-ttu-id="d745a-152">자습서를 참조 하십시오. [Azure blob 저장소 tooSQL 데이터 웨어하우스 (PolyBase)에서 데이터를 로드할][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-152">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

### <a name="use-bcp"></a><span data-ttu-id="d745a-153">bcp 사용</span><span class="sxs-lookup"><span data-stu-id="d745a-153">Use bcp</span></span>
<span data-ttu-id="d745a-154">적은 양의 데이터가 있는 경우 bcp tooload Azure SQL 데이터 웨어하우스에 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-154">If you have a small amount of data you can use bcp tooload directly into Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="d745a-155">로드 프로세스 요약:</span><span class="sxs-lookup"><span data-stu-id="d745a-155">Summary of loading process:</span></span>

1. <span data-ttu-id="d745a-156">SQL Server tooflat 파일에서 hello bcp 명령줄 유틸리티 tooexport 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-156">Use hello bcp command-line utility tooexport data from SQL Server tooflat files.</span></span>
2. <span data-ttu-id="d745a-157">Bcp tooload 데이터 범위를 플랫 파일을 tooSQL 데이터 웨어하우스에 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-157">Use bcp tooload data from flat files directly tooSQL Data Warehouse.</span></span>

<span data-ttu-id="d745a-158">자습서를 참조 하십시오. [SQL Server tooAzure SQL 데이터 웨어하우스 (bcp)에서 데이터를 로드할][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-158">For a tutorial, see [Load data from SQL Server tooAzure SQL Data Warehouse (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].</span></span>

### <a name="use-importexport-recommended-for--10-tb-data"></a><span data-ttu-id="d745a-159">가져오기/내보내기 사용(10TB를 초과하는 데이터에 권장)</span><span class="sxs-lookup"><span data-stu-id="d745a-159">Use Import/Export (recommended for > 10 TB data)</span></span>
<span data-ttu-id="d745a-160">데이터 크기가 > 10TB toomove를 원하는 경우 해당 tooAzure, 권장 서비스를 전달 합니다.이 디스크를 사용 하는 [가져오기/내보내기][Import/Export]합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-160">If your data size is > 10 TB and you want toomove it tooAzure, we recommend that you use our disk shipping service [Import/Export][Import/Export].</span></span> 

<span data-ttu-id="d745a-161">로드 프로세스 요약</span><span class="sxs-lookup"><span data-stu-id="d745a-161">Summary of loading process</span></span>

1. <span data-ttu-id="d745a-162">SQL Server tooflat 파일을 전송한 디스크에서 hello bcp 명령줄 유틸리티 tooexport 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-162">Use hello bcp command-line utility tooexport data from SQL Server tooflat files on transferrable disks.</span></span>
2. <span data-ttu-id="d745a-163">Hello 디스크 tooMicrosoft 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-163">Ship hello disks tooMicrosoft.</span></span>
3. <span data-ttu-id="d745a-164">Microsoft은 SQL 데이터 웨어하우스 hello 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="d745a-164">Microsoft loads hello data into SQL Data Warehouse</span></span>

## <a name="load-from-hdinsight"></a><span data-ttu-id="d745a-165">HDInsight에서 로드</span><span class="sxs-lookup"><span data-stu-id="d745a-165">Load from HDInsight</span></span>
<span data-ttu-id="d745a-166">SQL 데이터 웨어하우스는 PolyBase 통해 HDInsight에서 데이터 로드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-166">SQL Data Warehouse supports loading data from HDInsight via PolyBase.</span></span> <span data-ttu-id="d745a-167">hello 프로세스-PolyBase tooconnect tooHDInsight tooload 데이터를 사용 하 여 Azure Blob 저장소에서 데이터를 로드 동일 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-167">hello process is hello same as loading data from Azure Blob Storage - using PolyBase tooconnect tooHDInsight tooload data.</span></span> 

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="d745a-168">1. PolyBase 및 T-SQL 사용</span><span class="sxs-lookup"><span data-stu-id="d745a-168">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="d745a-169">로드 프로세스 요약:</span><span class="sxs-lookup"><span data-stu-id="d745a-169">Summary of loading process:</span></span>

1. <span data-ttu-id="d745a-170">데이터 tooHDInsight 이동 하 고 텍스트 파일에 저장 ORC, Parquet 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-170">Move your data tooHDInsight and store it in text files, ORC or Parquet format.</span></span>
2. <span data-ttu-id="d745a-171">SQL 데이터 웨어하우스 toodefine hello 위치 및 hello 데이터 형식의 외부 개체를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-171">Configure external objects in SQL Data Warehouse toodefine hello location and format of hello data.</span></span>
3. <span data-ttu-id="d745a-172">새 데이터베이스 테이블에 병렬로 T-SQL 명령 tooload hello 데이터를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-172">Run a T-SQL command tooload hello data in parallel into a new database table.</span></span>

<span data-ttu-id="d745a-173">자습서를 참조 하십시오. [Azure blob 저장소 tooSQL 데이터 웨어하우스 (PolyBase)에서 데이터를 로드할][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-173">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

## <a name="recommendations"></a><span data-ttu-id="d745a-174">권장 사항</span><span class="sxs-lookup"><span data-stu-id="d745a-174">Recommendations</span></span>
<span data-ttu-id="d745a-175">상당수의 파트너에게는 로드 솔루션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-175">Many of our partners have loading solutions.</span></span> <span data-ttu-id="d745a-176">자세한 내용을 보려면 toofind 목록을 보려면 우리의 [솔루션 파트너][solution partners]합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-176">toofind out more, see a list of our [solution partners][solution partners].</span></span> 

<span data-ttu-id="d745a-177">데이터-관계형 원본에서 가져온 고로 SQL 데이터 웨어하우스 있습니다 tooload tootransform 필요 합니다 행과 열 로드 하기 전에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-177">If your data is coming from a non-relational source and you want tooload it into SQL Data Warehouse you will need tootransform it into rows and columns before you load it.</span></span> <span data-ttu-id="d745a-178">hello 변환 된 데이터는 데이터베이스에 저장 된 toobe 필요 하지 않습니다, 그리고 텍스트 파일에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-178">hello transformed data doesn't need toobe stored in a database, it can be stored in text files.</span></span>

<span data-ttu-id="d745a-179">새로 로드한 데이터에 대한 통계를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-179">Create statistics on newly loaded data.</span></span> <span data-ttu-id="d745a-180">Azure SQL 데이터 웨어하우스는 자동 만들기 또는 통계 자동 업데이트를 아직 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="d745a-181">순서 tooget hello 최상의 성능을 얻으려면 쿼리에서 것이 중요 toocreate 통계 hello 후 모든 테이블의 모든 열에 먼저 로드 또는 모든 변경이 hello 데이터에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-181">In order tooget hello best performance from your queries, it's important toocreate statistics on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="d745a-182">자세한 내용은 [통계][Statistics]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d745a-182">For details, see [Statistics][Statistics].</span></span>

## <a name="next-steps"></a><span data-ttu-id="d745a-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d745a-183">Next steps</span></span>
<span data-ttu-id="d745a-184">더 많은 개발 팁에 대 한 참조 hello [개발 개요][development overview]합니다.</span><span class="sxs-lookup"><span data-stu-id="d745a-184">For more development tips, see hello [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server tooAzure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
