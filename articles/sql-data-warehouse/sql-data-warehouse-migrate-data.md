---
title: "SQL Data Warehouse로 데이터 마이그레이션| Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스로 데이터를 마이그레이션하기 위한 팁"
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: d78f954a-f54c-4aa4-9040-919bc6414887
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/29/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: dbdf1696cd169aa7e5e23f116027a1170347f4ea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="migrate-your-data"></a><span data-ttu-id="a9c89-103">데이터 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="a9c89-103">Migrate Your Data</span></span>
<span data-ttu-id="a9c89-104">다양한 도구를 사용하여 다양한 원본의 데이터를 SQL 데이터 웨어하우스로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-104">Data can be moved from different sources into your SQL Data Warehouse with a variety tools.</span></span>  <span data-ttu-id="a9c89-105">이 작업을 위해 ADF Copy, SSIS 및 bcp를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-105">ADF Copy, SSIS, and bcp can all be used to achieve this goal.</span></span> <span data-ttu-id="a9c89-106">그러나 데이터 크기가 증가하면 단계별로 데이터 마이그레이션 프로세스 세분화를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-106">However, as the amount of data increases you should think about breaking down the data migration process into steps.</span></span> <span data-ttu-id="a9c89-107">부드러운 데이터 마이그레이션이 되도록 성능 및 복원 모두를 위한 각 단계를 최적화하는 기회를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-107">This affords you the opportunity to optimize each step both for performance and for resilience to ensure a smooth data migration.</span></span>

<span data-ttu-id="a9c89-108">이 문서에서는 먼저 ADF Copy, SSIS 및 bcp의 간단한 마이그레이션 시나리오를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-108">This article first discusses the simple migration scenarios of ADF Copy, SSIS, and bcp.</span></span> <span data-ttu-id="a9c89-109">그런 다음 마이그레이션이 최적화되는 방법을 좀 더 깊게 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-109">It then look a little deeper into how the migration can be optimized.</span></span>

## <a name="azure-data-factory-adf-copy"></a><span data-ttu-id="a9c89-110">Azure 데이터 팩터리(ADF) 복사본</span><span class="sxs-lookup"><span data-stu-id="a9c89-110">Azure Data Factory (ADF) copy</span></span>
<span data-ttu-id="a9c89-111">[ADF 복사본][ADF Copy]은 [Azure Data Factory][Azure Data Factory]의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-111">[ADF Copy][ADF Copy] is part of [Azure Data Factory][Azure Data Factory].</span></span> <span data-ttu-id="a9c89-112">SQL 데이터 웨어하우스로 직접 또는 Azure blob 저장소에 있는 원격 플랫 파일, 로컬 저장소에 상주하는 플랫 파일로 데이터를 내보내는 데 ADF 복사본을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-112">You can use ADF Copy to export your data to flat files residing on local storage, to remote flat files held in Azure blob storage or directly into SQL Data Warehouse.</span></span>

<span data-ttu-id="a9c89-113">데이터가 플랫 파일에서 생성되는 경우 SQL Data Warehouse로 데이터 로드를 시작하기 전에 먼저 Azure Storage Blob에 데이터를 전송해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-113">If your data starts in flat files, then you will first need to transfer it to Azure storage blob before initiating a load it into SQL Data Warehouse.</span></span> <span data-ttu-id="a9c89-114">데이터가 Azure Blob Storage로 전송되면 [ADF 복사본][ADF Copy]을 다시 사용하도록 선택하여 SQL Data Warehouse로 데이터를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-114">Once the data is transferred into Azure blob storage you can choose to use [ADF Copy][ADF Copy] again to push the data into SQL Data Warehouse.</span></span>

<span data-ttu-id="a9c89-115">PolyBase는 데이터 로드를 위한 고성능 옵션도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-115">PolyBase also provides a high-performance option for loading the data.</span></span> <span data-ttu-id="a9c89-116">그러나 하나 대신 두 개의 도구를 사용하는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-116">However, that does mean using two tools instead of one.</span></span> <span data-ttu-id="a9c89-117">최상의 성능이 필요한 경우 PolyBase를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-117">If you need the best performance then use PolyBase.</span></span> <span data-ttu-id="a9c89-118">단일 도구 환경을 원하는 경우(및 데이터가 크지 않음) ADF가 답입니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-118">If you want a single tool experience (and the data is not massive) then ADF is your answer.</span></span>


> 
> 

<span data-ttu-id="a9c89-119">일부 훌륭한 [ADF 샘플][ADF samples]에 대한 다음 문서를 읽어 보세요.</span><span class="sxs-lookup"><span data-stu-id="a9c89-119">Head over to the following article for some great [ADF samples][ADF samples].</span></span>

## <a name="integration-services"></a><span data-ttu-id="a9c89-120">Integration Services</span><span class="sxs-lookup"><span data-stu-id="a9c89-120">Integration Services</span></span>
<span data-ttu-id="a9c89-121">Integration Services(SSIS)는 강력하고 유연한 변환 및 로드(ETL) 도구로, 복잡한 워크플로, 데이터 변환 및 여러 데이터 로드 옵션을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-121">Integration Services (SSIS) is a powerful and flexible Extract Transform and Load (ETL) tool that supports complex workflows, data transformation, and several data loading options.</span></span> <span data-ttu-id="a9c89-122">SSIS를 사용하여 광범위한 마이그레이션의 일부로 또는 Azure로 데이터를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-122">Use SSIS to simply transfer data to Azure or as part of a broader migration.</span></span>

> [!NOTE]
> <span data-ttu-id="a9c89-123">SSIS는 파일에 바이트 순서 표시가 없이 UTF-8로 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-123">SSIS can export to UTF-8 without the byte order mark in the file.</span></span> <span data-ttu-id="a9c89-124">구성하려면 먼저 파생된 열 구성 요소를 사용하여 데이터 흐름의 문자 데이터를 변환하고 65001 UTF-8 코드 페이지를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-124">To configure this you must first use the derived column component to convert the character data in the data flow to use the 65001 UTF-8 code page.</span></span> <span data-ttu-id="a9c89-125">열이 변환되면, 데이터를 플랫 파일 대상 어댑터에 작성하여 65001이 파일의 코드 페이지로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-125">Once the columns have been converted, write the data to the flat file destination adapter ensuring that 65001 has also been selected as the code page for the file.</span></span>
> 
> 

<span data-ttu-id="a9c89-126">SSIS는 SQL Server 배포에 연결한 것처럼 SQL 데이터 웨어하우스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-126">SSIS connects to SQL Data Warehouse just as it would connect to a SQL Server deployment.</span></span> <span data-ttu-id="a9c89-127">그러나 ADO.NET 연결 관리자를 사용하여 수를 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-127">However, your connections will need to be using an ADO.NET connection manager.</span></span> <span data-ttu-id="a9c89-128">또한 주의해서 "사용 가능한 경우 대량 삽입 사용" 설정을 구성하여 처리량을 최대화합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-128">You should also take care to configure the "Use bulk insert when available" setting to maximize throughput.</span></span> <span data-ttu-id="a9c89-129">이 속성에 대해 자세히 알아보려면 [ADO.NET 대상 어댑터][ADO.NET destination adapter] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9c89-129">Please refer to the [ADO.NET destination adapter][ADO.NET destination adapter] article to learn more about this property</span></span>

> [!NOTE]
> <span data-ttu-id="a9c89-130">OLEDB를 사용한 Azure SQL 데이터 웨어하우스 연결은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-130">Connecting to Azure SQL Data Warehouse by using OLEDB is not supported.</span></span>
> 
> 

<span data-ttu-id="a9c89-131">또한 제한 또는 네트워크 문제로 인해 패키지가 실패할 수 있는 가능성은 항상 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-131">In addition, there is always the possibility that a package might fail due to throttling or network issues.</span></span> <span data-ttu-id="a9c89-132">실패하기 전에 완료된 작업을 다시 실행하지 않고 실패 지점에서 재개할 수 있도록 패키지를 디자인합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-132">Design packages so they can be resumed at the point of failure, without redoing work that completed before the failure.</span></span>

<span data-ttu-id="a9c89-133">자세한 내용은 [SSIS 설명서][SSIS documentation]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9c89-133">For more information consult the [SSIS documentation][SSIS documentation].</span></span>

## <a name="bcp"></a><span data-ttu-id="a9c89-134">bcp</span><span class="sxs-lookup"><span data-stu-id="a9c89-134">bcp</span></span>
<span data-ttu-id="a9c89-135">bcp는 플랫 파일 데이터 가져오기 및 내보내기를 위해 설계된 명령줄 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-135">bcp is a command-line utility that is designed for flat file data import and export.</span></span> <span data-ttu-id="a9c89-136">일부 변환은 데이터를 내보내는 중에 수행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-136">Some transformation can take place during data export.</span></span> <span data-ttu-id="a9c89-137">수행하려면 간단한 변환은 쿼리를 사용하여 데이터를 선택하고 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-137">To perform simple transformations use a query to select and transform the data.</span></span> <span data-ttu-id="a9c89-138">내보낸 후 플랫 파일이 직접 대상 SQL 데이터 웨어하우스 데이터베이스로 로드될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-138">Once exported, the flat files can then be loaded directly into the target the SQL Data Warehouse database.</span></span>

> [!NOTE]
> <span data-ttu-id="a9c89-139">대개 원본 시스템의 보기에서 데이터 내보내기 중에 사용되는 변환을 캡슐화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-139">It is often a good idea to encapsulate the transformations used during data export in a view on the source system.</span></span> <span data-ttu-id="a9c89-140">이렇게 하면 논리가 유지되며 과정이 반복됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-140">This ensures that the logic is retained and the process is repeatable.</span></span>
> 
> 

<span data-ttu-id="a9c89-141">bcp의 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-141">Advantages of bcp are:</span></span>

* <span data-ttu-id="a9c89-142">단순성입니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-142">Simplicity.</span></span> <span data-ttu-id="a9c89-143">bcp 명령은 간단하게 작성되고 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-143">bcp commands are simple to build and execute</span></span>
* <span data-ttu-id="a9c89-144">다시 시작 가능한 로드 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-144">Re-startable load process.</span></span> <span data-ttu-id="a9c89-145">일단 내보내면, 임의의 횟수만큼 로드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-145">Once exported the load can be executed any number of times</span></span>

<span data-ttu-id="a9c89-146">bcp의 제한 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-146">Limitations of bcp are:</span></span>

* <span data-ttu-id="a9c89-147">bcp는 탭 형식의 플랫 파일에만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-147">bcp works with tabulated flat files only.</span></span> <span data-ttu-id="a9c89-148">xml 또는 JSON 등의 파일에서는 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-148">It does not work with files such as xml or JSON</span></span>
* <span data-ttu-id="a9c89-149">데이터 변환 기능은 내보내기 단계로만 제한되며 기본적으로 단순합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-149">Data transformation capabilities are limited to the export stage only and are simple in nature</span></span>
* <span data-ttu-id="a9c89-150">bcp는 인터넷을 통해 데이터를 로드할 때 강력한 것으로 조정되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-150">bcp has not been adapted to be robust when loading data over the internet.</span></span> <span data-ttu-id="a9c89-151">모든 네트워크 불안정으로 로드 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-151">Any network instability may cause a load error.</span></span>
* <span data-ttu-id="a9c89-152">bcp는 로드하기 전에 대상 데이터베이스에 표시되는 스키마를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-152">bcp relies on the schema being present in the target database prior to the load</span></span>

<span data-ttu-id="a9c89-153">자세한 내용은 [bcp를 사용하여 SQL Data Warehouse로 데이터 로드][Use bcp to load data into SQL Data Warehouse]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9c89-153">For more information, see [Use bcp to load data into SQL Data Warehouse][Use bcp to load data into SQL Data Warehouse].</span></span>

## <a name="optimizing-data-migration"></a><span data-ttu-id="a9c89-154">데이터 마이그레이션 최적화</span><span class="sxs-lookup"><span data-stu-id="a9c89-154">Optimizing data migration</span></span>
<span data-ttu-id="a9c89-155">불연속 세 단계로 SQLDW 데이터 마이그레이션 프로세스를 효과적으로 나눌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-155">A SQLDW data migration process can be effectively broken down into three discrete steps:</span></span>

1. <span data-ttu-id="a9c89-156">원본 데이터의 내보내기</span><span class="sxs-lookup"><span data-stu-id="a9c89-156">Export of source data</span></span>
2. <span data-ttu-id="a9c89-157">Azure에 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="a9c89-157">Transfer of data to Azure</span></span>
3. <span data-ttu-id="a9c89-158">대상 SQLDW 데이터베이스로 로드</span><span class="sxs-lookup"><span data-stu-id="a9c89-158">Load into the target SQLDW database</span></span>

<span data-ttu-id="a9c89-159">단계마다 성능을 최대화하는 강력하고 다시 시작 가능하며 복원력 있는 마이그레이션 프로세스를 만들도록 각 단계를 개별적으로 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-159">Each step can be individually optimized to create a robust, re-startable and resilient migration process that maximizes performance at each step.</span></span>

## <a name="optimizing-data-load"></a><span data-ttu-id="a9c89-160">데이터 로드 최적화</span><span class="sxs-lookup"><span data-stu-id="a9c89-160">Optimizing data load</span></span>
<span data-ttu-id="a9c89-161">잠시 반대 순서로 살펴보면 데이터를 로드하는 가장 빠른 방법은 PolyBase를 통해서입니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-161">Looking at these in reverse order for a moment; the fastest way to load data is via PolyBase.</span></span> <span data-ttu-id="a9c89-162">PolyBase 로드 프로세스를 최적화하는 경우 이전 단계에서 필수 구성 요소를 충족해야 하므로, 이 작업은 미리 숙지해 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-162">Optimizing for a PolyBase load process places prerequisites on the preceding steps so it's best to understand this upfront.</span></span> <span data-ttu-id="a9c89-163">아래에 이 계정과 키의 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-163">They are:</span></span>

1. <span data-ttu-id="a9c89-164">데이터 파일의 인코딩</span><span class="sxs-lookup"><span data-stu-id="a9c89-164">Encoding of data files</span></span>
2. <span data-ttu-id="a9c89-165">데이터 파일의 형식</span><span class="sxs-lookup"><span data-stu-id="a9c89-165">Format of data files</span></span>
3. <span data-ttu-id="a9c89-166">데이터 파일의 위치</span><span class="sxs-lookup"><span data-stu-id="a9c89-166">Location of data files</span></span>

### <a name="encoding"></a><span data-ttu-id="a9c89-167">인코딩</span><span class="sxs-lookup"><span data-stu-id="a9c89-167">Encoding</span></span>
<span data-ttu-id="a9c89-168">PolyBase를 사용하려면 데이터 파일이 UTF-8 또는 UTF-16FE여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-168">PolyBase requires data files to be UTF-8 or UTF-16FE.</span></span> 



### <a name="format-of-data-files"></a><span data-ttu-id="a9c89-169">데이터 파일의 형식</span><span class="sxs-lookup"><span data-stu-id="a9c89-169">Format of data files</span></span>
<span data-ttu-id="a9c89-170">PolyBase는 \n 또는 새 줄의 고정된 행 종결자를 규정합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-170">PolyBase mandates a fixed row terminator of \n or newline.</span></span> <span data-ttu-id="a9c89-171">데이터 파일은 이 표준을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-171">Your data files must conform to this standard.</span></span> <span data-ttu-id="a9c89-172">문자열 또는 열 종결자에 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-172">There aren't any restrictions on string or column terminators.</span></span>

<span data-ttu-id="a9c89-173">PolyBase에서 외부 테이블의 일부로 파일에서 모든 열을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-173">You will have to define every column in the file as part of your external table in PolyBase.</span></span> <span data-ttu-id="a9c89-174">내보낸 모든 열이 필요하고 해당 형식은 필요한 표준을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-174">Make sure that all exported columns are required and that the types conform to the required standards.</span></span>

<span data-ttu-id="a9c89-175">지원되는 데이터 형식은 [스키마 마이그레이션] 문서를 다시 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9c89-175">Please refer back to the [migrate your schema] article for detail on supported data types.</span></span>

### <a name="location-of-data-files"></a><span data-ttu-id="a9c89-176">데이터 파일의 위치</span><span class="sxs-lookup"><span data-stu-id="a9c89-176">Location of data files</span></span>
<span data-ttu-id="a9c89-177">SQL 데이터 웨어하우스는 PolyBase를 사용하여 Azure blob 저장소에 데이터를 독점적으로 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-177">SQL Data Warehouse uses PolyBase to load data from Azure Blob Storage exclusively.</span></span> <span data-ttu-id="a9c89-178">따라서 데이터가 먼저 blob 저장소로 전송되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-178">Consequently, the data must have been first transferred into blob storage.</span></span>

## <a name="optimizing-data-transfer"></a><span data-ttu-id="a9c89-179">데이터 전송 최적화</span><span class="sxs-lookup"><span data-stu-id="a9c89-179">Optimizing data transfer</span></span>
<span data-ttu-id="a9c89-180">데이터 마이그레이션의 느린 부분 중 하나는 Azure에 데이터를 전송하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-180">One of the slowest parts of data migration is the transfer of the data to Azure.</span></span> <span data-ttu-id="a9c89-181">네트워크 대역폭 문제가 발생할 수 뿐만 아니라 네트워크 안정성 진행률 심각하게 방해가 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-181">Not only can network bandwidth be an issue but also network reliability can seriously hamper progress.</span></span> <span data-ttu-id="a9c89-182">기본적으로 데이터를 Azure로 마이그레이션하는 전송 오류 발생 가능성 합리적으로 가능성이 있으므로 인터넷을 통해 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-182">By default migrating data to Azure is over the internet so the chances of transfer errors occurring are reasonably likely.</span></span> <span data-ttu-id="a9c89-183">그러나 이러한 오류는 데이터를 전부 또는 일부를 다시 보내어야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-183">However, these errors may require data to be re-sent either in whole or in part.</span></span>

<span data-ttu-id="a9c89-184">다행히 속도 및 이 프로세스의 복원력을 향상시키는 여러 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-184">Fortunately you have several options to improve the speed and resilience of this process:</span></span>

### <a name="expressrouteexpressroute"></a><span data-ttu-id="a9c89-185">[ExpressRoute][ExpressRoute]</span><span class="sxs-lookup"><span data-stu-id="a9c89-185">[ExpressRoute][ExpressRoute]</span></span>
<span data-ttu-id="a9c89-186">[ExpressRoute][ExpressRoute]를 사용하여 전송의 속도를 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-186">You may want to consider using [ExpressRoute][ExpressRoute] to speed up the transfer.</span></span> <span data-ttu-id="a9c89-187">[ExpressRoute][ExpressRoute]는 Azure에 대한 개인 연결을 설정하므로 공용 인터넷을 통해 연결되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-187">[ExpressRoute][ExpressRoute] provides you with an established private connection to Azure so the connection does not go over the public internet.</span></span> <span data-ttu-id="a9c89-188">이 단계는 필수 단계는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-188">This is by no means a mandatory step.</span></span> <span data-ttu-id="a9c89-189">그러나 온-프레미스 또는 공동 배치 위치에서 데이터를 Azure로 푸시하는 경우, 처리량이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-189">However, it will improve throughput when pushing data to Azure from an on-premises or co-location facility.</span></span>

<span data-ttu-id="a9c89-190">[ExpressRoute][ExpressRoute] 사용의 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-190">The benefits of using [ExpressRoute][ExpressRoute] are:</span></span>

1. <span data-ttu-id="a9c89-191">향상된 안정성</span><span class="sxs-lookup"><span data-stu-id="a9c89-191">Increased reliability</span></span>
2. <span data-ttu-id="a9c89-192">더 빨라진 네트워크 속도</span><span class="sxs-lookup"><span data-stu-id="a9c89-192">Faster network speed</span></span>
3. <span data-ttu-id="a9c89-193">줄어든 네트워크 대기 시간</span><span class="sxs-lookup"><span data-stu-id="a9c89-193">Lower network latency</span></span>
4. <span data-ttu-id="a9c89-194">강화된 네트워크 보안</span><span class="sxs-lookup"><span data-stu-id="a9c89-194">higher network security</span></span>

<span data-ttu-id="a9c89-195">[ExpressRoute][ExpressRoute]는 마이그레이션뿐만이 아니라 다양한 시나리오에 대해 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-195">[ExpressRoute][ExpressRoute] is beneficial for a number of scenarios; not just the migration.</span></span>

<span data-ttu-id="a9c89-196">관심이 있나요?</span><span class="sxs-lookup"><span data-stu-id="a9c89-196">Interested?</span></span> <span data-ttu-id="a9c89-197">자세한 내용 및 가격은 [ExpressRoute 설명서][ExpressRoute documentation]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9c89-197">For more information and pricing please visit the [ExpressRoute documentation][ExpressRoute documentation].</span></span>

### <a name="azure-import-and-export-service"></a><span data-ttu-id="a9c89-198">Azure 가져오기 및 내보내기 서비스</span><span class="sxs-lookup"><span data-stu-id="a9c89-198">Azure Import and Export Service</span></span>
<span data-ttu-id="a9c89-199">Azure 가져오기 및 내보내기 서비스는 큰(GB++) 데이터에서 대용량(TB++) 데이터까지 Azure로 전송하기 위해 설계된 데이터 전송 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-199">The Azure Import and Export Service is a data transfer process designed for large (GB++) to massive (TB++) transfers of data into Azure.</span></span> <span data-ttu-id="a9c89-200">디스크에 데이터 작성 및 Azure 데이터 센터에 배송이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-200">It involves writing your data to disks and shipping them to an Azure data center.</span></span> <span data-ttu-id="a9c89-201">사용자를 대신해 Azure Storage Blob에 디스크 콘텐츠가 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-201">The disk contents will then be loaded into Azure Storage Blobs on your behalf.</span></span>

<span data-ttu-id="a9c89-202">아래에는 가져오기/내보내기 프로세스가 대략적으로 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-202">A high-level view of the import export process is as follows:</span></span>

1. <span data-ttu-id="a9c89-203">데이터를 수신하도록 Azure Blob 저장소 컨테이너를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-203">Configure an Azure Blob Storage container to receive the data</span></span>
2. <span data-ttu-id="a9c89-204">로컬 저장소로 데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="a9c89-204">Export your data to local storage</span></span>
3. <span data-ttu-id="a9c89-205">[Azure 가져오기/내보내기 도구]를 사용하여 3.5 인치 SATA II/III 하드 디스크 드라이브에 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="a9c89-205">Copy the data to 3.5 inch SATA II/III hard disk drives using the [Azure Import/Export Tool]</span></span>
4. <span data-ttu-id="a9c89-206">[Azure 가져오기/내보내기 도구]에서 생성된 저널 파일을 제공하는 Azure 가져오기 및 내보내기 서비스를 사용하여 가져오기 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="a9c89-206">Create an Import Job using the Azure Import and Export Service providing the journal files produced by the [Azure Import/Export Tool]</span></span>
5. <span data-ttu-id="a9c89-207">지정된 Azure 데이터 센터로 디스크 배송</span><span class="sxs-lookup"><span data-stu-id="a9c89-207">Ship the disks your nominated Azure data center</span></span>
6. <span data-ttu-id="a9c89-208">Azure Blob 저장소 컨테이너로 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="a9c89-208">Your data is transferred to your Azure Blob Storage container</span></span>
7. <span data-ttu-id="a9c89-209">PolyBase를 사용하여 SQLDW로 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="a9c89-209">Load the data into SQLDW using PolyBase</span></span>

### <a name="azcopyazcopy-utility"></a><span data-ttu-id="a9c89-210">[AZCopy][AZCopy] 유틸리티</span><span class="sxs-lookup"><span data-stu-id="a9c89-210">[AZCopy][AZCopy] utility</span></span>
<span data-ttu-id="a9c89-211">[AZCopy][AZCopy] 유틸리티는 Azure 저장소 Blob으로 데이터를 전송하기 위한 훌륭한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-211">The [AZCopy][AZCopy] utility is a great tool for getting your data transferred into Azure Storage Blobs.</span></span> <span data-ttu-id="a9c89-212">작은 데이터 전송(MB++)에서부터 매우 큰 데이터 전송(GB++)까지 설계되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-212">It is designed for small (MB++) to very large (GB++) data transfers.</span></span> <span data-ttu-id="a9c89-213">[AZCopy] 도 좋은 복원력 있는 처리량 등 Azure에 데이터를 전송 하는 경우에 데이터 전송 단계에 대한 훌륭한 선택이 제공하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-213">[AZCopy] has also been designed to provide good resilient throughput when transferring data to Azure and so is a great choice for the data transfer step.</span></span> <span data-ttu-id="a9c89-214">한 번 전송되면, PolyBase를 사용하여 SQL 데이터 웨어하우스로 데이터를 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-214">Once transferred you can load the data using PolyBase into SQL Data Warehouse.</span></span> <span data-ttu-id="a9c89-215">또한 "프로세스 실행" 작업을 사용하여 SSIS 패키지로 AZCopy를 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-215">You can also incorporate AZCopy into your SSIS packages using an "Execute Process" task.</span></span>

<span data-ttu-id="a9c89-216">AZCopy를 사용하려면 먼저 다운로드하고 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-216">To use AZCopy you will first need to download and install it.</span></span> <span data-ttu-id="a9c89-217">[프로덕션 버전][production version] 및 [미리 보기 버전][preview version]을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-217">There is a [production version][production version] and a [preview version][preview version] available.</span></span>

<span data-ttu-id="a9c89-218">파일 시스템에서 파일을 업로드하려면 아래와 같은 명령이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-218">To upload a file from your file system you will need a command like the one below:</span></span>

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="a9c89-219">이 프로세스는 대략적으로 다음과 같이 요약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-219">A high-level process summary could be:</span></span>

1. <span data-ttu-id="a9c89-220">데이터를 수신하도록 Azure 저장소 Blob 컨테이너 구성</span><span class="sxs-lookup"><span data-stu-id="a9c89-220">Configure an Azure storage blob container to receive the data</span></span>
2. <span data-ttu-id="a9c89-221">로컬 저장소로 데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="a9c89-221">Export your data to local storage</span></span>
3. <span data-ttu-id="a9c89-222">Azure Blob 저장소 컨테이너의 데이터 AZCopy</span><span class="sxs-lookup"><span data-stu-id="a9c89-222">AZCopy your data in the Azure Blob Storage container</span></span>
4. <span data-ttu-id="a9c89-223">PolyBase를 사용하여 SQL 데이터 웨어하우스로 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="a9c89-223">Load the data into SQL Data Warehouse using PolyBase</span></span>

<span data-ttu-id="a9c89-224">사용 가능한 전체 설명서는 [AZCopy][AZCopy]입니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-224">Full documentation available: [AZCopy][AZCopy].</span></span>

## <a name="optimizing-data-export"></a><span data-ttu-id="a9c89-225">데이터 내보내기 최적화</span><span class="sxs-lookup"><span data-stu-id="a9c89-225">Optimizing data export</span></span>
<span data-ttu-id="a9c89-226">내보내기가 PolyBase에서 설계한 배치 요구 사항에 맞는지 확인하는 것 외에도 데이터 내보내기를 최적화하여 프로세스가 더 향상되도록 시도할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-226">In addition to ensuring that the export conforms to the requirements laid out by PolyBase you can also seek to optimize the export of the data to improve the process further.</span></span>



### <a name="data-compression"></a><span data-ttu-id="a9c89-227">데이터 압축</span><span class="sxs-lookup"><span data-stu-id="a9c89-227">Data compression</span></span>
<span data-ttu-id="a9c89-228">PolyBase는 gzip 압축된 데이터를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-228">PolyBase can read gzip compressed data.</span></span> <span data-ttu-id="a9c89-229">gzip 파일로 데이터를 압축할 수 있는 경우 네트워크를 통해 푸시되는 데이터의 양을 최소화합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-229">If you are able to compress your data to gzip files then you will minimize the amount of data being pushed over the network.</span></span>

### <a name="multiple-files"></a><span data-ttu-id="a9c89-230">여러 파일</span><span class="sxs-lookup"><span data-stu-id="a9c89-230">Multiple files</span></span>
<span data-ttu-id="a9c89-231">대형 테이블을 여러 파일로 분할하면 내보내기 속도를 향상시킬 수 뿐만 아니라 전송을 다시 시작 및 Azure blob 저장소에서의 전반적인 데이터 관리 효율성에도 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-231">Breaking up large tables into several files not only helps to improve export speed, it also helps with transfer re-startability, and the overall manageability of the data once in the Azure blob storage.</span></span> <span data-ttu-id="a9c89-232">PolyBase의 여러 유용한 기능 중 하나는 폴더 내 모든 파일을 읽고 하나의 테이블로 처리된다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-232">One of the many nice features of PolyBase is that it will read all the files inside a folder and treat it as one table.</span></span> <span data-ttu-id="a9c89-233">따라서 각 테이블의 파일을 자체 폴더로 격리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-233">It is therefore a good idea to isolate the files for each table into its own folder.</span></span>

<span data-ttu-id="a9c89-234">또한 PolyBase는 "재귀적 폴더 이동"이라는 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-234">PolyBase also supports a feature known as "recursive folder traversal".</span></span> <span data-ttu-id="a9c89-235">내보낸 데이터의 조직의 데이터 관리를 개선하도록 이 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9c89-235">You can use this feature to further enhance the organization of your exported data to improve your data management.</span></span>

<span data-ttu-id="a9c89-236">PolyBase 사용한 데이터 로드에 대해 자세히 알려면 [PolyBase를 사용하여 SQL Data Warehouse로 데이터 로드][Use PolyBase to load data into SQL Data Warehouse]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9c89-236">To learn more about loading data with PolyBase, see [Use PolyBase to load data into SQL Data Warehouse][Use PolyBase to load data into SQL Data Warehouse].</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9c89-237">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a9c89-237">Next steps</span></span>
<span data-ttu-id="a9c89-238">마이그레이션에 대한 자세한 내용은 [SQL Data Warehouse로 솔루션 마이그레이션][Migrate your solution to SQL Data Warehouse]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9c89-238">For more about migration, see [Migrate your solution to SQL Data Warehouse][Migrate your solution to SQL Data Warehouse].</span></span>
<span data-ttu-id="a9c89-239">더 많은 개발 팁은 [개발 개요][development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9c89-239">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution to SQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp to load data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase to load data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
