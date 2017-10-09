---
title: "aaaMigrate 사용자 데이터 tooSQL 데이터 웨어하우스 | Microsoft Docs"
description: "솔루션 개발을 위한 사용자 데이터 tooAzure SQL 데이터 웨어하우스를 마이그레이션하기 위한 팁입니다."
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
ms.openlocfilehash: fe4c6b7e82094c59c45e06be6da225fee1b707ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data"></a><span data-ttu-id="beda8-103">데이터 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="beda8-103">Migrate Your Data</span></span>
<span data-ttu-id="beda8-104">다양한 도구를 사용하여 다양한 원본의 데이터를 SQL 데이터 웨어하우스로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-104">Data can be moved from different sources into your SQL Data Warehouse with a variety tools.</span></span>  <span data-ttu-id="beda8-105">ADF 복사, SSIS, 및 bcp 있을 수 있습니다 모두 사용 하는 tooachieve이이 목표입니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-105">ADF Copy, SSIS, and bcp can all be used tooachieve this goal.</span></span> <span data-ttu-id="beda8-106">그러나 hello 데이터 양이 증가 하면 hello 데이터 마이그레이션 프로세스를 단계로 세분화 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-106">However, as hello amount of data increases you should think about breaking down hello data migration process into steps.</span></span> <span data-ttu-id="beda8-107">이 통해 있습니다 hello 기회 toooptimize 성능 및 복원 력 tooensure 부드러운 데이터 마이그레이션에 대 한 각 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-107">This affords you hello opportunity toooptimize each step both for performance and for resilience tooensure a smooth data migration.</span></span>

<span data-ttu-id="beda8-108">먼저 ADF 복사, SSIS, 및 bcp의 hello 간단한 마이그레이션 시나리오에 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-108">This article first discusses hello simple migration scenarios of ADF Copy, SSIS, and bcp.</span></span> <span data-ttu-id="beda8-109">그런 다음 hello 마이그레이션 최적화 될 수 있습니다 어떻게를 자세하게 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-109">It then look a little deeper into how hello migration can be optimized.</span></span>

## <a name="azure-data-factory-adf-copy"></a><span data-ttu-id="beda8-110">Azure 데이터 팩터리(ADF) 복사본</span><span class="sxs-lookup"><span data-stu-id="beda8-110">Azure Data Factory (ADF) copy</span></span>
<span data-ttu-id="beda8-111">[ADF 복사본][ADF Copy]은 [Azure Data Factory][Azure Data Factory]의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-111">[ADF Copy][ADF Copy] is part of [Azure Data Factory][Azure Data Factory].</span></span> <span data-ttu-id="beda8-112">Azure blob 저장소에 또는 SQL 데이터 웨어하우스에 직접 tooremote 플랫 파일 보유 로컬 저장소에 있는 데이터 tooflat 파일 ADF 복사 tooexport를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-112">You can use ADF Copy tooexport your data tooflat files residing on local storage, tooremote flat files held in Azure blob storage or directly into SQL Data Warehouse.</span></span>

<span data-ttu-id="beda8-113">플랫 파일에 있는 데이터 시작 하 여 다음 tootransfer 먼저 경우 것 로드를 시작 하기 전에 tooAzure 저장소 blob에 SQL 데이터 웨어하우스 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-113">If your data starts in flat files, then you will first need tootransfer it tooAzure storage blob before initiating a load it into SQL Data Warehouse.</span></span> <span data-ttu-id="beda8-114">Azure blob 저장소로 hello 전송 속도가 toouse 선택할 수 있습니다 [ADF 복사] [ ADF Copy] SQL 데이터 웨어하우스로 다시 toopush hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-114">Once hello data is transferred into Azure blob storage you can choose toouse [ADF Copy][ADF Copy] again toopush hello data into SQL Data Warehouse.</span></span>

<span data-ttu-id="beda8-115">PolyBase는 또한 hello 데이터 로드에 대 한 성능 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-115">PolyBase also provides a high-performance option for loading hello data.</span></span> <span data-ttu-id="beda8-116">그러나 하나 대신 두 개의 도구를 사용하는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-116">However, that does mean using two tools instead of one.</span></span> <span data-ttu-id="beda8-117">경우 최상의 성능을 얻으려면 hello 필요 PolyBase를 사용 하십시오.</span><span class="sxs-lookup"><span data-stu-id="beda8-117">If you need hello best performance then use PolyBase.</span></span> <span data-ttu-id="beda8-118">단일 도구 환경을 원하는 (및 hello 데이터가 massive있지 않습니다) 하는 경우 ADF 답변이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-118">If you want a single tool experience (and hello data is not massive) then ADF is your answer.</span></span>


> 
> 

<span data-ttu-id="beda8-119">다음 문서에 대 한 몇 가지 훌륭한 toohello 통해 헤드 [ADF 샘플][ADF samples]합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-119">Head over toohello following article for some great [ADF samples][ADF samples].</span></span>

## <a name="integration-services"></a><span data-ttu-id="beda8-120">Integration Services</span><span class="sxs-lookup"><span data-stu-id="beda8-120">Integration Services</span></span>
<span data-ttu-id="beda8-121">Integration Services(SSIS)는 강력하고 유연한 변환 및 로드(ETL) 도구로, 복잡한 워크플로, 데이터 변환 및 여러 데이터 로드 옵션을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-121">Integration Services (SSIS) is a powerful and flexible Extract Transform and Load (ETL) tool that supports complex workflows, data transformation, and several data loading options.</span></span> <span data-ttu-id="beda8-122">SSIS toosimply 전송 데이터 tooAzure를 사용 하 여 또는 광범위 한 마이그레이션의 일환으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-122">Use SSIS toosimply transfer data tooAzure or as part of a broader migration.</span></span>

> [!NOTE]
> <span data-ttu-id="beda8-123">SSIS는 tooUTF-8 hello 바이트 순서 표시가 hello 파일에 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-123">SSIS can export tooUTF-8 without hello byte order mark in hello file.</span></span> <span data-ttu-id="beda8-124">열 구성 요소 tooconvert hello 문자 데이터에서 파생 된 hello를 먼저 사용 해야이 tooconfigure hello 데이터 흐름 toouse hello 65001 utf-8 코드 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-124">tooconfigure this you must first use hello derived column component tooconvert hello character data in hello data flow toouse hello 65001 UTF-8 code page.</span></span> <span data-ttu-id="beda8-125">Hello 열으로 변환 되 면 hello 데이터 toohello 플랫 파일 대상 어댑터가 보장 65001 hello 파일에 대 한 코드 페이지 hello로 선택도 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-125">Once hello columns have been converted, write hello data toohello flat file destination adapter ensuring that 65001 has also been selected as hello code page for hello file.</span></span>
> 
> 

<span data-ttu-id="beda8-126">SSIS는 tooa SQL Server 배포에 연결 됩니다. 것 처럼 tooSQL 데이터 웨어하우스에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-126">SSIS connects tooSQL Data Warehouse just as it would connect tooa SQL Server deployment.</span></span> <span data-ttu-id="beda8-127">그러나 연결 toobe ADO.NET 연결 관리자를 사용 하 여 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-127">However, your connections will need toobe using an ADO.NET connection manager.</span></span> <span data-ttu-id="beda8-128">또한 주의 해야 tooconfigure hello "사용 가능한 경우 대량 삽입 사용" toomaximize 처리량 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-128">You should also take care tooconfigure hello "Use bulk insert when available" setting toomaximize throughput.</span></span> <span data-ttu-id="beda8-129">Toohello를 참조 하십시오 [ADO.NET 대상 어댑터] [ ADO.NET destination adapter] 이 속성에 대 한 문서 toolearn</span><span class="sxs-lookup"><span data-stu-id="beda8-129">Please refer toohello [ADO.NET destination adapter][ADO.NET destination adapter] article toolearn more about this property</span></span>

> [!NOTE]
> <span data-ttu-id="beda8-130">SQL 데이터 웨어하우스 tooAzure OLEDB를 사용 하 여 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-130">Connecting tooAzure SQL Data Warehouse by using OLEDB is not supported.</span></span>
> 
> 

<span data-ttu-id="beda8-131">또한 항상 hello 가능성은 패키지가 실패할 수 있는 toothrottling 또는 네트워크 문제 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-131">In addition, there is always hello possibility that a package might fail due toothrottling or network issues.</span></span> <span data-ttu-id="beda8-132">Hello 오류 발생 시점에 관계 없이 재개할 수 있도록 디자인 패키지 hello 오류 전에 완료 하는 작업을 다시 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-132">Design packages so they can be resumed at hello point of failure, without redoing work that completed before hello failure.</span></span>

<span data-ttu-id="beda8-133">자세한 내용은 참조 hello [SSIS 설명서][SSIS documentation]합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-133">For more information consult hello [SSIS documentation][SSIS documentation].</span></span>

## <a name="bcp"></a><span data-ttu-id="beda8-134">bcp</span><span class="sxs-lookup"><span data-stu-id="beda8-134">bcp</span></span>
<span data-ttu-id="beda8-135">bcp는 플랫 파일 데이터 가져오기 및 내보내기를 위해 설계된 명령줄 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-135">bcp is a command-line utility that is designed for flat file data import and export.</span></span> <span data-ttu-id="beda8-136">일부 변환은 데이터를 내보내는 중에 수행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-136">Some transformation can take place during data export.</span></span> <span data-ttu-id="beda8-137">tooperform 단순 쿼리 tooselect를 사용 하 여 변환과 hello 데이터를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-137">tooperform simple transformations use a query tooselect and transform hello data.</span></span> <span data-ttu-id="beda8-138">내보낸 후 hello 플랫 파일 hello 대상 hello SQL 데이터 웨어하우스 데이터베이스에 직접 로드 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-138">Once exported, hello flat files can then be loaded directly into hello target hello SQL Data Warehouse database.</span></span>

> [!NOTE]
> <span data-ttu-id="beda8-139">Hello 원본 시스템에서 보기에서 내보낼 데이터 중에 사용 되는 변환 하는 것이 좋습니다 tooencapsulate hello 방식은 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-139">It is often a good idea tooencapsulate hello transformations used during data export in a view on hello source system.</span></span> <span data-ttu-id="beda8-140">이렇게 하면 hello 논리 유지 되는 있고 hello 프로세스를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-140">This ensures that hello logic is retained and hello process is repeatable.</span></span>
> 
> 

<span data-ttu-id="beda8-141">bcp의 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-141">Advantages of bcp are:</span></span>

* <span data-ttu-id="beda8-142">단순성입니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-142">Simplicity.</span></span> <span data-ttu-id="beda8-143">bcp 명령을 간단한 toobuild는 및 실행</span><span class="sxs-lookup"><span data-stu-id="beda8-143">bcp commands are simple toobuild and execute</span></span>
* <span data-ttu-id="beda8-144">다시 시작 가능한 로드 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-144">Re-startable load process.</span></span> <span data-ttu-id="beda8-145">한 번 내보낸된 hello 로드 될 수 있습니다에 여러 번 실행</span><span class="sxs-lookup"><span data-stu-id="beda8-145">Once exported hello load can be executed any number of times</span></span>

<span data-ttu-id="beda8-146">bcp의 제한 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-146">Limitations of bcp are:</span></span>

* <span data-ttu-id="beda8-147">bcp는 탭 형식의 플랫 파일에만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-147">bcp works with tabulated flat files only.</span></span> <span data-ttu-id="beda8-148">xml 또는 JSON 등의 파일에서는 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-148">It does not work with files such as xml or JSON</span></span>
* <span data-ttu-id="beda8-149">데이터 변환 기능 제한 toohello 내보내기 단계만 되며 기본적에서으로 단순한</span><span class="sxs-lookup"><span data-stu-id="beda8-149">Data transformation capabilities are limited toohello export stage only and are simple in nature</span></span>
* <span data-ttu-id="beda8-150">bcp를 통해 데이터를 로드 하는 인터넷 hello 때 강력한 조정된 toobe 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-150">bcp has not been adapted toobe robust when loading data over hello internet.</span></span> <span data-ttu-id="beda8-151">모든 네트워크 불안정으로 로드 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-151">Any network instability may cause a load error.</span></span>
* <span data-ttu-id="beda8-152">bcp은 hello 대상 데이터베이스 이전 toohello 부하에 없는 hello 스키마 사용</span><span class="sxs-lookup"><span data-stu-id="beda8-152">bcp relies on hello schema being present in hello target database prior toohello load</span></span>

<span data-ttu-id="beda8-153">자세한 내용은 참조 [bcp tooload 데이터를 사용 하 여 SQL 데이터 웨어하우스로][Use bcp tooload data into SQL Data Warehouse]합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-153">For more information, see [Use bcp tooload data into SQL Data Warehouse][Use bcp tooload data into SQL Data Warehouse].</span></span>

## <a name="optimizing-data-migration"></a><span data-ttu-id="beda8-154">데이터 마이그레이션 최적화</span><span class="sxs-lookup"><span data-stu-id="beda8-154">Optimizing data migration</span></span>
<span data-ttu-id="beda8-155">불연속 세 단계로 SQLDW 데이터 마이그레이션 프로세스를 효과적으로 나눌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-155">A SQLDW data migration process can be effectively broken down into three discrete steps:</span></span>

1. <span data-ttu-id="beda8-156">원본 데이터의 내보내기</span><span class="sxs-lookup"><span data-stu-id="beda8-156">Export of source data</span></span>
2. <span data-ttu-id="beda8-157">데이터 tooAzure 전송</span><span class="sxs-lookup"><span data-stu-id="beda8-157">Transfer of data tooAzure</span></span>
3. <span data-ttu-id="beda8-158">Hello 대상 SQLDW 데이터베이스에 로드</span><span class="sxs-lookup"><span data-stu-id="beda8-158">Load into hello target SQLDW database</span></span>

<span data-ttu-id="beda8-159">각 단계에는 개별적으로 최적화 된 toocreate 각 단계에서 성능을 최대화 하는 강력 하 고 복원 력 있는 사이트를 다시 시작할 마이그레이션 프로세스 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-159">Each step can be individually optimized toocreate a robust, re-startable and resilient migration process that maximizes performance at each step.</span></span>

## <a name="optimizing-data-load"></a><span data-ttu-id="beda8-160">데이터 로드 최적화</span><span class="sxs-lookup"><span data-stu-id="beda8-160">Optimizing data load</span></span>
<span data-ttu-id="beda8-161">잠시;에 대 한 반대 순서로 이러한를 살펴보면 hello 가장 빠른 방법은 tooload 데이터 PolyBase 통하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-161">Looking at these in reverse order for a moment; hello fastest way tooload data is via PolyBase.</span></span> <span data-ttu-id="beda8-162">PolyBase 로드 프로세스에 대 한 최적화 하면 필수 구성 요소에 이전 단계 최상의 toounderstand 되기 때문이 hello 업 프런트 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-162">Optimizing for a PolyBase load process places prerequisites on hello preceding steps so it's best toounderstand this upfront.</span></span> <span data-ttu-id="beda8-163">아래에 이 계정과 키의 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-163">They are:</span></span>

1. <span data-ttu-id="beda8-164">데이터 파일의 인코딩</span><span class="sxs-lookup"><span data-stu-id="beda8-164">Encoding of data files</span></span>
2. <span data-ttu-id="beda8-165">데이터 파일의 형식</span><span class="sxs-lookup"><span data-stu-id="beda8-165">Format of data files</span></span>
3. <span data-ttu-id="beda8-166">데이터 파일의 위치</span><span class="sxs-lookup"><span data-stu-id="beda8-166">Location of data files</span></span>

### <a name="encoding"></a><span data-ttu-id="beda8-167">인코딩</span><span class="sxs-lookup"><span data-stu-id="beda8-167">Encoding</span></span>
<span data-ttu-id="beda8-168">PolyBase는 데이터 파일 toobe utf-8 또는 u t F-16FE 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-168">PolyBase requires data files toobe UTF-8 or UTF-16FE.</span></span> 



### <a name="format-of-data-files"></a><span data-ttu-id="beda8-169">데이터 파일의 형식</span><span class="sxs-lookup"><span data-stu-id="beda8-169">Format of data files</span></span>
<span data-ttu-id="beda8-170">PolyBase는 \n 또는 새 줄의 고정된 행 종결자를 규정합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-170">PolyBase mandates a fixed row terminator of \n or newline.</span></span> <span data-ttu-id="beda8-171">데이터 파일 toothis 표준을 준수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-171">Your data files must conform toothis standard.</span></span> <span data-ttu-id="beda8-172">문자열 또는 열 종결자에 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-172">There aren't any restrictions on string or column terminators.</span></span>

<span data-ttu-id="beda8-173">나면 toodefine 모든 열 hello 파일에 PolyBase에서 외부 테이블의 일부분으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-173">You will have toodefine every column in hello file as part of your external table in PolyBase.</span></span> <span data-ttu-id="beda8-174">내보낸된 모든 열은 필요 하며 필요한 toohello 표준 hello 형식을 따르는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-174">Make sure that all exported columns are required and that hello types conform toohello required standards.</span></span>

<span data-ttu-id="beda8-175">다시 toohello 참조 하십시오. [스키마 마이그레이션] 지원 되는 데이터 형식에 대 한 세부 정보에 대 한 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-175">Please refer back toohello [migrate your schema] article for detail on supported data types.</span></span>

### <a name="location-of-data-files"></a><span data-ttu-id="beda8-176">데이터 파일의 위치</span><span class="sxs-lookup"><span data-stu-id="beda8-176">Location of data files</span></span>
<span data-ttu-id="beda8-177">SQL 데이터 웨어하우스는 Azure Blob 저장소에서 PolyBase tooload 데이터를 단독으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-177">SQL Data Warehouse uses PolyBase tooload data from Azure Blob Storage exclusively.</span></span> <span data-ttu-id="beda8-178">따라서 hello 데이터 해야 먼저 전송 된 blob 저장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-178">Consequently, hello data must have been first transferred into blob storage.</span></span>

## <a name="optimizing-data-transfer"></a><span data-ttu-id="beda8-179">데이터 전송 최적화</span><span class="sxs-lookup"><span data-stu-id="beda8-179">Optimizing data transfer</span></span>
<span data-ttu-id="beda8-180">데이터 마이그레이션의 hello 느린 부분 중 하나에 hello 데이터 tooAzure hello 전송입니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-180">One of hello slowest parts of data migration is hello transfer of hello data tooAzure.</span></span> <span data-ttu-id="beda8-181">네트워크 대역폭 문제가 발생할 수 뿐만 아니라 네트워크 안정성 진행률 심각하게 방해가 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-181">Not only can network bandwidth be an issue but also network reliability can seriously hamper progress.</span></span> <span data-ttu-id="beda8-182">기본적으로 마이그레이션 데이터 tooAzure 인터넷 가능성이 합리적으로 발생 하는 전송 오류 가능성을 지금 hello hello 끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-182">By default migrating data tooAzure is over hello internet so hello chances of transfer errors occurring are reasonably likely.</span></span> <span data-ttu-id="beda8-183">그러나 이러한 오류는 일부 또는 전부에서를 다시 보낼 데이터 toobe가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-183">However, these errors may require data toobe re-sent either in whole or in part.</span></span>

<span data-ttu-id="beda8-184">다행히 몇 가지 옵션 tooimprove hello 속도 및이 프로세스의 복구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-184">Fortunately you have several options tooimprove hello speed and resilience of this process:</span></span>

### <a name="expressrouteexpressroute"></a><span data-ttu-id="beda8-185">[ExpressRoute][ExpressRoute]</span><span class="sxs-lookup"><span data-stu-id="beda8-185">[ExpressRoute][ExpressRoute]</span></span>
<span data-ttu-id="beda8-186">Tooconsider 사용 하 여 원하는 수 [ExpressRoute] [ ExpressRoute] toospeed hello 전송 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-186">You may want tooconsider using [ExpressRoute][ExpressRoute] toospeed up hello transfer.</span></span> <span data-ttu-id="beda8-187">[ExpressRoute] [ ExpressRoute] 개인 설정 된 연결 tooAzure는 hello 연결을 통해 전달 되지 않습니다 하므로 hello 공용 인터넷을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-187">[ExpressRoute][ExpressRoute] provides you with an established private connection tooAzure so hello connection does not go over hello public internet.</span></span> <span data-ttu-id="beda8-188">이 단계는 필수 단계는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-188">This is by no means a mandatory step.</span></span> <span data-ttu-id="beda8-189">그러나 온-프레미스에서 데이터 tooAzure 푸시할 때 처리량이 향상 될 것 또는 공동 배치 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-189">However, it will improve throughput when pushing data tooAzure from an on-premises or co-location facility.</span></span>

<span data-ttu-id="beda8-190">사용의 이점 hello [ExpressRoute] [ ExpressRoute] 됩니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-190">hello benefits of using [ExpressRoute][ExpressRoute] are:</span></span>

1. <span data-ttu-id="beda8-191">향상된 안정성</span><span class="sxs-lookup"><span data-stu-id="beda8-191">Increased reliability</span></span>
2. <span data-ttu-id="beda8-192">더 빨라진 네트워크 속도</span><span class="sxs-lookup"><span data-stu-id="beda8-192">Faster network speed</span></span>
3. <span data-ttu-id="beda8-193">줄어든 네트워크 대기 시간</span><span class="sxs-lookup"><span data-stu-id="beda8-193">Lower network latency</span></span>
4. <span data-ttu-id="beda8-194">강화된 네트워크 보안</span><span class="sxs-lookup"><span data-stu-id="beda8-194">higher network security</span></span>

<span data-ttu-id="beda8-195">[ExpressRoute] [ ExpressRoute] 마이그레이션 뿐 아니라 hello;은 다양 한 시나리오에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-195">[ExpressRoute][ExpressRoute] is beneficial for a number of scenarios; not just hello migration.</span></span>

<span data-ttu-id="beda8-196">관심이 있나요?</span><span class="sxs-lookup"><span data-stu-id="beda8-196">Interested?</span></span> <span data-ttu-id="beda8-197">자세한 내용 및 하십시오 가격 책정에 대 한 방문 hello [express 경로 설명서][ExpressRoute documentation]합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-197">For more information and pricing please visit hello [ExpressRoute documentation][ExpressRoute documentation].</span></span>

### <a name="azure-import-and-export-service"></a><span data-ttu-id="beda8-198">Azure 가져오기 및 내보내기 서비스</span><span class="sxs-lookup"><span data-stu-id="beda8-198">Azure Import and Export Service</span></span>
<span data-ttu-id="beda8-199">hello Azure 가져오기 / 내보내기 서비스는 큰 (g B + +) toomassive (t B + +) 전송에 데이터를 Azure로 설계 된 데이터 전송 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-199">hello Azure Import and Export Service is a data transfer process designed for large (GB++) toomassive (TB++) transfers of data into Azure.</span></span> <span data-ttu-id="beda8-200">데이터 toodisks를 작성 하 고 tooan Azure 데이터 센터에 배송 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-200">It involves writing your data toodisks and shipping them tooan Azure data center.</span></span> <span data-ttu-id="beda8-201">다음 사용자 대신 Azure 저장소 Blob에 hello 디스크 내용이 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-201">hello disk contents will then be loaded into Azure Storage Blobs on your behalf.</span></span>

<span data-ttu-id="beda8-202">높은 수준의 hello 가져오기 내보내기 프로세스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-202">A high-level view of hello import export process is as follows:</span></span>

1. <span data-ttu-id="beda8-203">Azure Blob 저장소 컨테이너 tooreceive hello 데이터 구성</span><span class="sxs-lookup"><span data-stu-id="beda8-203">Configure an Azure Blob Storage container tooreceive hello data</span></span>
2. <span data-ttu-id="beda8-204">데이터 toolocal 저장소 내보내기</span><span class="sxs-lookup"><span data-stu-id="beda8-204">Export your data toolocal storage</span></span>
3. <span data-ttu-id="beda8-205">Hello 데이터 too3.5 인치 SATA II/III 하드 디스크 드라이브 hello [Azure 가져오기/내보내기 도구]를 사용 하 여 복사</span><span class="sxs-lookup"><span data-stu-id="beda8-205">Copy hello data too3.5 inch SATA II/III hard disk drives using hello [Azure Import/Export Tool]</span></span>
4. <span data-ttu-id="beda8-206">Hello Azure 가져오기 및 내보내기 서비스 제공 hello [Azure 가져오기/내보내기 도구]에서 생성 된 hello 저널 파일을 사용 하 여 가져오기 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="beda8-206">Create an Import Job using hello Azure Import and Export Service providing hello journal files produced by hello [Azure Import/Export Tool]</span></span>
5. <span data-ttu-id="beda8-207">지정한 Azure 데이터 센터 hello 디스크 제공</span><span class="sxs-lookup"><span data-stu-id="beda8-207">Ship hello disks your nominated Azure data center</span></span>
6. <span data-ttu-id="beda8-208">데이터는 전송 된 tooyour Azure Blob 저장소 컨테이너</span><span class="sxs-lookup"><span data-stu-id="beda8-208">Your data is transferred tooyour Azure Blob Storage container</span></span>
7. <span data-ttu-id="beda8-209">PolyBase를 사용 하 여 SQLDW hello 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="beda8-209">Load hello data into SQLDW using PolyBase</span></span>

### <a name="azcopyazcopy-utility"></a><span data-ttu-id="beda8-210">[AZCopy][AZCopy] 유틸리티</span><span class="sxs-lookup"><span data-stu-id="beda8-210">[AZCopy][AZCopy] utility</span></span>
<span data-ttu-id="beda8-211">hello [AZCopy][AZCopy] 유틸리티는 Azure 저장소 Blob으로 전송 하 여 데이터를 가져오는 데 좋은 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-211">hello [AZCopy][AZCopy] utility is a great tool for getting your data transferred into Azure Storage Blobs.</span></span> <span data-ttu-id="beda8-212">작은 (MB + +) toovery 큰 (g B + +) 데이터 전송을 위해 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-212">It is designed for small (MB++) toovery large (GB++) data transfers.</span></span> <span data-ttu-id="beda8-213">[AZCopy] 되었습니다 복원 처리량이 좋은 디자인 된 tooprovide hello 데이터 전송 단계에 대 한 최선의 선택은 데이터 tooAzure 등을 전송 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="beda8-213">[AZCopy] has also been designed tooprovide good resilient throughput when transferring data tooAzure and so is a great choice for hello data transfer step.</span></span> <span data-ttu-id="beda8-214">한 번 전송 hello 데이터 PolyBase를 사용 하 여 SQL 데이터 웨어하우스로 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-214">Once transferred you can load hello data using PolyBase into SQL Data Warehouse.</span></span> <span data-ttu-id="beda8-215">또한 "프로세스 실행" 작업을 사용하여 SSIS 패키지로 AZCopy를 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-215">You can also incorporate AZCopy into your SSIS packages using an "Execute Process" task.</span></span>

<span data-ttu-id="beda8-216">toouse AZCopy 먼저 toodownload 필요 하 고 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-216">toouse AZCopy you will first need toodownload and install it.</span></span> <span data-ttu-id="beda8-217">[프로덕션 버전][production version] 및 [미리 보기 버전][preview version]을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-217">There is a [production version][production version] and a [preview version][preview version] available.</span></span>

<span data-ttu-id="beda8-218">tooupload 해야 하나 hello 같은 명령을 아래 파일 시스템에서 파일:</span><span class="sxs-lookup"><span data-stu-id="beda8-218">tooupload a file from your file system you will need a command like hello one below:</span></span>

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="beda8-219">이 프로세스는 대략적으로 다음과 같이 요약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-219">A high-level process summary could be:</span></span>

1. <span data-ttu-id="beda8-220">Azure 저장소 blob 컨테이너 tooreceive hello 데이터 구성</span><span class="sxs-lookup"><span data-stu-id="beda8-220">Configure an Azure storage blob container tooreceive hello data</span></span>
2. <span data-ttu-id="beda8-221">데이터 toolocal 저장소 내보내기</span><span class="sxs-lookup"><span data-stu-id="beda8-221">Export your data toolocal storage</span></span>
3. <span data-ttu-id="beda8-222">AZCopy hello Azure Blob 저장소 컨테이너의 데이터</span><span class="sxs-lookup"><span data-stu-id="beda8-222">AZCopy your data in hello Azure Blob Storage container</span></span>
4. <span data-ttu-id="beda8-223">PolyBase를 사용 하 여 SQL 데이터 웨어하우스 hello 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="beda8-223">Load hello data into SQL Data Warehouse using PolyBase</span></span>

<span data-ttu-id="beda8-224">사용 가능한 전체 설명서는 [AZCopy][AZCopy]입니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-224">Full documentation available: [AZCopy][AZCopy].</span></span>

## <a name="optimizing-data-export"></a><span data-ttu-id="beda8-225">데이터 내보내기 최적화</span><span class="sxs-lookup"><span data-stu-id="beda8-225">Optimizing data export</span></span>
<span data-ttu-id="beda8-226">또한 hello 내보내기 PolyBase에서으로 배치 toohello 요구 사항을 준수 하는지 tooensuring hello 데이터 tooimprove hello 프로세스의 추가 toooptimize hello 내보내기 또한 검색 수입니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-226">In addition tooensuring that hello export conforms toohello requirements laid out by PolyBase you can also seek toooptimize hello export of hello data tooimprove hello process further.</span></span>



### <a name="data-compression"></a><span data-ttu-id="beda8-227">데이터 압축</span><span class="sxs-lookup"><span data-stu-id="beda8-227">Data compression</span></span>
<span data-ttu-id="beda8-228">PolyBase는 gzip 압축된 데이터를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-228">PolyBase can read gzip compressed data.</span></span> <span data-ttu-id="beda8-229">Toocompress 수 있다면 데이터 toogzip 파일 하면 hello hello 네트워크를 통해 반영 하는 데이터 양을 최소화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-229">If you are able toocompress your data toogzip files then you will minimize hello amount of data being pushed over hello network.</span></span>

### <a name="multiple-files"></a><span data-ttu-id="beda8-230">여러 파일</span><span class="sxs-lookup"><span data-stu-id="beda8-230">Multiple files</span></span>
<span data-ttu-id="beda8-231">Tooimprove 속도 내보낼 수 뿐만 아니라 여러 파일로 큰 테이블 분할 사용 하 여 전송할 re-startability를 하 고 hello hello 데이터 hello Azure blob 저장소에 한 번의 전체 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-231">Breaking up large tables into several files not only helps tooimprove export speed, it also helps with transfer re-startability, and hello overall manageability of hello data once in hello Azure blob storage.</span></span> <span data-ttu-id="beda8-232">PolyBase의 많은 유용한 기능이 됩니다 폴더 내의 모든 hello 파일 읽기를 한 테이블으로 처리 하는 hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-232">One of hello many nice features of PolyBase is that it will read all hello files inside a folder and treat it as one table.</span></span> <span data-ttu-id="beda8-233">따라서 자체 폴더 내에 있는 각 테이블에 대 한 것이 좋습니다 tooisolate hello 파일 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-233">It is therefore a good idea tooisolate hello files for each table into its own folder.</span></span>

<span data-ttu-id="beda8-234">또한 PolyBase는 "재귀적 폴더 이동"이라는 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-234">PolyBase also supports a feature known as "recursive folder traversal".</span></span> <span data-ttu-id="beda8-235">이 기능을 사용할 수 toofurther 내보낸된 데이터 tooimprove의 hello 조직 데이터 관리를 향상 합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-235">You can use this feature toofurther enhance hello organization of your exported data tooimprove your data management.</span></span>

<span data-ttu-id="beda8-236">PolyBase 사용 하 여 데이터 로드에 대 한 더 toolearn 참조 [SQL 데이터 웨어하우스를 사용 하 여 PolyBase tooload 데이터][Use PolyBase tooload data into SQL Data Warehouse]합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-236">toolearn more about loading data with PolyBase, see [Use PolyBase tooload data into SQL Data Warehouse][Use PolyBase tooload data into SQL Data Warehouse].</span></span>

## <a name="next-steps"></a><span data-ttu-id="beda8-237">다음 단계</span><span class="sxs-lookup"><span data-stu-id="beda8-237">Next steps</span></span>
<span data-ttu-id="beda8-238">마이그레이션에 대 한 자세한 내용은 [사용자 솔루션 tooSQL 데이터 웨어하우스 마이그레이션][Migrate your solution tooSQL Data Warehouse]합니다.</span><span class="sxs-lookup"><span data-stu-id="beda8-238">For more about migration, see [Migrate your solution tooSQL Data Warehouse][Migrate your solution tooSQL Data Warehouse].</span></span>
<span data-ttu-id="beda8-239">더 많은 개발 팁은 [개발 개요][development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="beda8-239">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution tooSQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp tooload data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase tooload data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
