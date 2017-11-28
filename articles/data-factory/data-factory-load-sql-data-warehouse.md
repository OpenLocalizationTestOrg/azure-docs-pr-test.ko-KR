---
title: "aaaLoad 테라바이트의 데이터를 SQL 데이터 웨어하우스에 | Microsoft Docs"
description: "Azure Data Factory를 통해 15분 내에 Azure SQL Data Warehouse에 1TB 데이터를 로드하는 방법을 보여 줍니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: a6c133c0-ced2-463c-86f0-a07b00c9e37f
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e63f60461b082b0e3979004cb631dbf4a6710de3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a><span data-ttu-id="28f94-103">Data Factory를 통해 15분 내에 Azure SQL Data Warehouse에 1TB 로드</span><span class="sxs-lookup"><span data-stu-id="28f94-103">Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Data Factory</span></span>
<span data-ttu-id="28f94-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)는 거대한 양의 관계형 및 비관계형 데이터를 처리할 수 있는 클라우드 기반 규모 확장 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span>  <span data-ttu-id="28f94-105">대규모 병렬 처리(MPP) 아키텍처를 기반으로 하는 SQL Data Warehouse는 엔터프라이즈 데이터 웨어하우스 워크로드에 최적화됩니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-105">Built on massively parallel processing (MPP) architecture, SQL Data Warehouse is optimized for enterprise data warehouse workloads.</span></span>  <span data-ttu-id="28f94-106">클라우드 탄력성 hello 유연성 tooscale 저장소와 독립적으로 계산 및 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-106">It offers cloud elasticity with hello flexibility tooscale storage and compute independently.</span></span>

<span data-ttu-id="28f94-107">이제는 Azure SQL Data Warehouse를 시작하는 것이 **Azure Data Factory**를 사용하는 것보다 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-107">Getting started with Azure SQL Data Warehouse is now easier than ever using **Azure Data Factory**.</span></span>  <span data-ttu-id="28f94-108">Azure 데이터 팩터리는 완전히 관리 되는 클라우드 기반 데이터 통합 서비스를 사용된 하면 중요 한 시간이 절약 SQL 데이터 웨어하우스를 평가 하 고 분석을 구축 하는 동안 hello 데이터 기존 컴퓨터에서 SQL 데이터 웨어하우스 toopopulate 될 수 있는 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-108">Azure Data Factory is a fully managed cloud-based data integration service, which can be used toopopulate a SQL Data Warehouse with hello data from your existing system, and saving you valuable time while evaluating SQL Data Warehouse and building your analytics solutions.</span></span> <span data-ttu-id="28f94-109">데이터를 Azure 데이터 팩터리를 사용 하 여 Azure SQL 데이터 웨어하우스 로드 hello 주요 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-109">Here are hello key benefits of loading data into Azure SQL Data Warehouse using Azure Data Factory:</span></span>

* <span data-ttu-id="28f94-110">**쉽게 tooset**: 스크립팅이 필요 없음와 5 단계 직관적인 마법사.</span><span class="sxs-lookup"><span data-stu-id="28f94-110">**Easy tooset up**: 5-step intuitive wizard with no scripting required.</span></span>
* <span data-ttu-id="28f94-111">**다양한 데이터 저장소 지원**: 다양한 온-프레미스 및 클라우드 기반 데이터 저장소 집합에 대한 기본 제공 지원.</span><span class="sxs-lookup"><span data-stu-id="28f94-111">**Rich data store support**: built-in support for a rich set of on-premises and cloud-based data stores.</span></span>
* <span data-ttu-id="28f94-112">**안전 하 고 규격**: 데이터는 HTTPS 또는 ExpressRoute를 통해 전송 되 고 글로벌 서비스의 현재 상태를 사용 하면 데이터 hello 지리적 경계를 벗어나지</span><span class="sxs-lookup"><span data-stu-id="28f94-112">**Secure and compliant**: data is transferred over HTTPS or ExpressRoute, and global service presence ensures your data never leaves hello geographical boundary</span></span>
* <span data-ttu-id="28f94-113">**PolyBase를 사용 하 여 최상의 성능** – Polybase를 사용 하는 hello 가장 효율적인 방식으로 toomove 데이터를 Azure SQL 데이터 웨어하우스에 합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-113">**Unparalleled performance by using PolyBase** – Using Polybase is hello most efficient way toomove data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="28f94-114">Blob 기능을 준비 하는 hello를 사용 하 여 모든 유형의 Azure Blob 저장소 외에도 기본적으로 Polybase 지원 hello는 데이터 저장소에서 높은 로드 속도 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-114">Using hello staging blob feature, you can achieve high load speeds from all types of data stores besides Azure Blob storage, which hello Polybase supports by default.</span></span>

<span data-ttu-id="28f94-115">이 문서에서는 어떻게 toouse 데이터 팩터리 복사 마법사 tooload 1TB 데이터를 Azure SQL 데이터 웨어하우스에 Azure Blob 저장소에서 넘는 1.2 g b p s 처리량에 15 분 미만입니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-115">This article shows you how toouse Data Factory Copy Wizard tooload 1-TB data from Azure Blob Storage into Azure SQL Data Warehouse in under 15 minutes, at over 1.2 GBps throughput.</span></span>

<span data-ttu-id="28f94-116">이 문서는 hello 복사 마법사를 사용 하 여 Azure SQL 데이터 웨어하우스로 데이터를 이동 하기 위한 단계별 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-116">This article provides step-by-step instructions for moving data into Azure SQL Data Warehouse by using hello Copy Wizard.</span></span>

> [!NOTE]
>  <span data-ttu-id="28f94-117">참조의 일반 정보 기능에 대 한 데이터 팩터리의/Azure SQL 데이터 웨어하우스 로부터 데이터를 이동, [Azure 데이터 팩터리를 사용 하 여 Azure SQL 데이터 웨어하우스 로부터 데이터 tooand 이동](data-factory-azure-sql-data-warehouse-connector.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="28f94-117">For general information about capabilities of Data Factory in moving data to/from Azure SQL Data Warehouse, see [Move data tooand from Azure SQL Data Warehouse using Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) article.</span></span>
>
> <span data-ttu-id="28f94-118">Azure Portal, Visual Studio, PowerShell 등을 사용하여 파이프라인을 빌드할 수도 있습니다. 참조 [자습서: Azure Blob tooAzure SQL 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 간략 한 설명이 hello 복사 작업을 사용 하 여 Azure Data Factory에 대 한 단계별 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-118">You can also build pipelines using Azure portal, Visual Studio, PowerShell, etc. See [Tutorial: Copy data from Azure Blob tooAzure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a quick walkthrough with step-by-step instructions for using hello Copy Activity in Azure Data Factory.</span></span>  
>
>

## <a name="prerequisites"></a><span data-ttu-id="28f94-119">필수 조건</span><span class="sxs-lookup"><span data-stu-id="28f94-119">Prerequisites</span></span>
* <span data-ttu-id="28f94-120">Azure Blob Storage: 이 실험에서는 Azure Blob Storage(GRS)를 사용하여 TPC-H 테스트 데이터 집합을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-120">Azure Blob Storage: this experiment uses Azure Blob Storage (GRS) for storing TPC-H testing dataset.</span></span>  <span data-ttu-id="28f94-121">Azure 저장소 계정이 없는 경우에 대해 배울 [어떻게 toocreate 저장소 계정](../storage/common/storage-create-storage-account.md#create-a-storage-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-121">If you do not have an Azure storage account, learn [how toocreate a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="28f94-122">[TPC H](http://www.tpc.org/tpch/) 데이터: 하겠습니다 toouse TPC H hello 테스트 데이터 집합으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-122">[TPC-H](http://www.tpc.org/tpch/) data: we are going toouse TPC-H as hello testing dataset.</span></span>  <span data-ttu-id="28f94-123">toodo 해야 하는, toouse `dbgen` TPC H 도구 키트에서 데 사용할 수 있는 hello 데이터 집합을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-123">toodo that, you need toouse `dbgen` from TPC-H toolkit, which helps you generate hello dataset.</span></span>  <span data-ttu-id="28f94-124">소스 코드를 다운로드 하거나 `dbgen` 에서 [TPC 도구](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) , 직접 또는 다운로드 hello 컴파일된 이진에서 컴파일 및 [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools)합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-124">You can either download source code for `dbgen` from [TPC Tools](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) and compile it yourself, or download hello compiled binary from [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span></span>  <span data-ttu-id="28f94-125">Hello 다음과 같이 실행된 dbgen.exe toogenerate 1TB 플랫 파일에 대 한 명령을 `lineitem` 10 개의 파일을 통해 확산 테이블:</span><span class="sxs-lookup"><span data-stu-id="28f94-125">Run dbgen.exe with hello following commands toogenerate 1 TB flat file for `lineitem` table spread across 10 files:</span></span>

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * <span data-ttu-id="28f94-126">…</span><span class="sxs-lookup"><span data-stu-id="28f94-126">…</span></span>
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    <span data-ttu-id="28f94-127">이제 복사 hello 파일 tooAzure Blob를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-127">Now copy hello generated files tooAzure Blob.</span></span>  <span data-ttu-id="28f94-128">너무 참조[Azure 데이터 팩터리를 사용 하 여 온-프레미스 파일 시스템에서 데이터 tooand 이동](data-factory-onprem-file-system-connector.md) 방법에 대 한 toodo 하는 ADF 사본을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-128">Refer too[Move data tooand from an on-premises file system by using Azure Data Factory](data-factory-onprem-file-system-connector.md) for how toodo that using ADF Copy.</span></span>    
* <span data-ttu-id="28f94-129">Azure SQL Data Warehouse: 이 실험에서는 6,000개 DWU를 사용하여 만들어진 Azure SQL Data Warehouse로 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-129">Azure SQL Data Warehouse: this experiment loads data into Azure SQL Data Warehouse created with 6,000 DWUs</span></span>

    <span data-ttu-id="28f94-130">너무 참조[Azure SQL 데이터 웨어하우스를 만들](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) 에 대 한 자세한 지침은 어떻게 toocreate SQL 데이터 웨어하우스 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="28f94-130">Refer too[Create an Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) for detailed instructions on how toocreate a SQL Data Warehouse database.</span></span>  <span data-ttu-id="28f94-131">tooget hello 최상의 가능한 로드 성능을 Polybase를 사용 하 여 SQL 데이터 웨어하우스로 최대 6000 Dwu hello 성능 설정에 허용 된 데이터 웨어하우스 단위 (Dwu) 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-131">tooget hello best possible load performance into SQL Data Warehouse using Polybase, we choose maximum number of Data Warehouse Units (DWUs) allowed in hello Performance setting, which is 6,000 DWUs.</span></span>

  > [!NOTE]
  > <span data-ttu-id="28f94-132">Azure Blob를 로드할 때 로드 성능을 하는 hello 데이터는 SQL 데이터 웨어하우스 hello에 구성한 Dwu 정비례 toohello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-132">When loading from Azure Blob, hello data loading performance is directly proportional toohello number of DWUs you configure on hello SQL Data Warehouse:</span></span>
  >
  > <span data-ttu-id="28f94-133">1TB를 1,000 DWU SQL Data Warehouse에 로드하는 데는 87분(~200MBps 처리량)이 걸리고, 1TB를 2,000 DWU SQL Data Warehouse에 로드하는 데는 46분(~380MBps 처리량)이 걸리고, 1TB를 6,000 DWU SQL Data Warehouse에 로드하는 데는 14분(~1.2GBps 처리량)이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-133">Loading 1 TB into 1,000 DWU SQL Data Warehouse takes 87 minutes (~200 MBps throughput) Loading 1 TB into 2,000 DWU SQL Data Warehouse takes 46 minutes (~380 MBps throughput) Loading 1 TB into 6,000 DWU SQL Data Warehouse takes 14 minutes (~1.2 GBps throughput)</span></span>
  >
  >

    <span data-ttu-id="28f94-134">toocreate 6000 Dwu로 SQL 데이터 웨어하우스 hello 성능 슬라이더 모든 hello 방식으로 toohello 오른쪽 이동:</span><span class="sxs-lookup"><span data-stu-id="28f94-134">toocreate a SQL Data Warehouse with 6,000 DWUs, move hello Performance slider all hello way toohello right:</span></span>

    ![성능 슬라이더](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    <span data-ttu-id="28f94-136">6,000 DWU를 포함하도록 구성되지 않은 기존 데이터베이스의 경우 Azure Portal을 사용하여 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-136">For an existing database that is not configured with 6,000 DWUs, you can scale it up using Azure portal.</span></span>  <span data-ttu-id="28f94-137">Azure 포털에서 toohello 데이터베이스를 이동 하 고는 **배율** hello 단추 **개요** 패널 hello 다음 이미지에에서 표시 된:</span><span class="sxs-lookup"><span data-stu-id="28f94-137">Navigate toohello database in Azure portal, and there is a **Scale** button in hello **Overview** panel shown in hello following image:</span></span>

    ![크기 조정 단추](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    <span data-ttu-id="28f94-139">Hello 클릭 **배율** 단추 tooopen hello 다음 패널 hello 슬라이더 toohello 최대 값을 이동 하 고 클릭 **저장** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-139">Click hello **Scale** button tooopen hello following panel, move hello slider toohello maximum value, and click **Save** button.</span></span>

    ![크기 조정 대화 상자](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    <span data-ttu-id="28f94-141">이 실험에서는 `xlargerc` 리소스 클래스를 사용하여 Azure SQL Data Warehouse로 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-141">This experiment loads data into Azure SQL Data Warehouse using `xlargerc` resource class.</span></span>

    <span data-ttu-id="28f94-142">최상의 가능한 처리량 tooachieve 복사가 필요한 너무 속한 SQL 데이터 웨어하우스 사용자를 사용 하 여 수행 toobe`xlargerc` 리소스 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-142">tooachieve best possible throughput, copy needs toobe performed using a SQL Data Warehouse user belonging too`xlargerc` resource class.</span></span>  <span data-ttu-id="28f94-143">자세한 방법을 toodo를 따르면 [사용자 리소스 클래스 예제 변경](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example)합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-143">Learn how toodo that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>  
* <span data-ttu-id="28f94-144">DDL 문 다음 hello를 실행 하 여 Azure SQL 데이터 웨어하우스 데이터베이스에서 대상 테이블 스키마를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-144">Create destination table schema in Azure SQL Data Warehouse database, by running hello following DDL statement:</span></span>

    ```SQL  
    CREATE TABLE [dbo].[lineitem]
    (
        [L_ORDERKEY] [bigint] NOT NULL,
        [L_PARTKEY] [bigint] NOT NULL,
        [L_SUPPKEY] [bigint] NOT NULL,
        [L_LINENUMBER] [int] NOT NULL,
        [L_QUANTITY] [decimal](15, 2) NULL,
        [L_EXTENDEDPRICE] [decimal](15, 2) NULL,
        [L_DISCOUNT] [decimal](15, 2) NULL,
        [L_TAX] [decimal](15, 2) NULL,
        [L_RETURNFLAG] [char](1) NULL,
        [L_LINESTATUS] [char](1) NULL,
        [L_SHIPDATE] [date] NULL,
        [L_COMMITDATE] [date] NULL,
        [L_RECEIPTDATE] [date] NULL,
        [L_SHIPINSTRUCT] [char](25) NULL,
        [L_SHIPMODE] [char](10) NULL,
        [L_COMMENT] [varchar](44) NULL
    )
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    ```
<span data-ttu-id="28f94-145">Hello 필수 구성 요소 단계를 완료 하는 이제 hello 복사 마법사를 사용 하 여 준비 tooconfigure hello 복사 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-145">With hello prerequisite steps completed, we are now ready tooconfigure hello copy activity using hello Copy Wizard.</span></span>

## <a name="launch-copy-wizard"></a><span data-ttu-id="28f94-146">복사 마법사 시작</span><span class="sxs-lookup"><span data-stu-id="28f94-146">Launch Copy Wizard</span></span>
1. <span data-ttu-id="28f94-147">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-147">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="28f94-148">클릭 **+ 새로 만들기** hello 왼쪽 위 모퉁이에서 클릭 **인텔리전스 + 분석**를 클릭 하 고 **Data Factory**합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-148">Click **+ NEW** from hello top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="28f94-149">Hello에 **새 데이터 팩터리** 블레이드:</span><span class="sxs-lookup"><span data-stu-id="28f94-149">In hello **New data factory** blade:</span></span>

   1. <span data-ttu-id="28f94-150">입력 **LoadIntoSQLDWDataFactory** hello에 대 한 **이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-150">Enter **LoadIntoSQLDWDataFactory** for hello **name**.</span></span>
       <span data-ttu-id="28f94-151">hello Azure 데이터 팩터리의 hello 이름을 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-151">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="28f94-152">Hello 오류가 나타나면: **"LoadIntoSQLDWDataFactory" 데이터 팩터리 이름을 사용할 수 없으면**을 hello hello 데이터 팩터리의 이름입니다 (예를 들어 yournameLoadIntoSQLDWDataFactory)을 변경 하 고 다시 만들어 보십시오.</span><span class="sxs-lookup"><span data-stu-id="28f94-152">If you receive hello error: **Data factory name “LoadIntoSQLDWDataFactory” is not available**, change hello name of hello data factory (for example, yournameLoadIntoSQLDWDataFactory) and try creating again.</span></span> <span data-ttu-id="28f94-153">데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="28f94-153">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
   2. <span data-ttu-id="28f94-154">Azure **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-154">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="28f94-155">리소스 그룹에 대 한 단계를 수행 하는 hello 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-155">For Resource Group, do one of hello following steps:</span></span>
      1. <span data-ttu-id="28f94-156">선택 **기존 항목 사용** tooselect 기존 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-156">Select **Use existing** tooselect an existing resource group.</span></span>
      2. <span data-ttu-id="28f94-157">선택 **새로 만들기** tooenter 리소스 그룹에 대 한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-157">Select **Create new** tooenter a name for a resource group.</span></span>
   4. <span data-ttu-id="28f94-158">선택 된 **위치** hello 데이터 팩토리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-158">Select a **location** for hello data factory.</span></span>
   5. <span data-ttu-id="28f94-159">선택 **Pin toodashboard** hello hello 블레이드 맨 아래에 있는 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-159">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>  
   6. <span data-ttu-id="28f94-160">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-160">Click **Create**.</span></span>
4. <span data-ttu-id="28f94-161">Hello 참조 hello 만들기가 완료 되 면 **Data Factory** hello 다음 이미지와 같이 블레이드:</span><span class="sxs-lookup"><span data-stu-id="28f94-161">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image:</span></span>

   ![데이터 팩터리 홈페이지](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. <span data-ttu-id="28f94-163">Hello Data Factory 홈 페이지에서 클릭 hello **데이터 복사** toolaunch 타일 **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-163">On hello Data Factory home page, click hello **Copy data** tile toolaunch **Copy Wizard**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="28f94-164">해당 hello 웹 브라우저에서 "권한 부여..." 걸려 표시 되 면 사용 안 함/취소 **제 3 자 쿠키를 차단 및 사이트 데이터** 설정 (또는)에 사용 가능한 상태로 유지 하 고 예외를 만들 **login.microsoftonline.com**및 hello 마법사를 다시 시작 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="28f94-164">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a><span data-ttu-id="28f94-165">1단계: 데이터 로드 일정 구성</span><span class="sxs-lookup"><span data-stu-id="28f94-165">Step 1: Configure data loading schedule</span></span>
<span data-ttu-id="28f94-166">hello 첫 번째 단계는 tooconfigure hello 데이터 로드 작업 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-166">hello first step is tooconfigure hello data loading schedule.</span></span>  

<span data-ttu-id="28f94-167">Hello에 **속성** 페이지:</span><span class="sxs-lookup"><span data-stu-id="28f94-167">In hello **Properties** page:</span></span>

1. <span data-ttu-id="28f94-168">**작업 이름**으로 **CopyFromBlobToAzureSqlDataWarehouse**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-168">Enter **CopyFromBlobToAzureSqlDataWarehouse** for **Task name**</span></span>
2. <span data-ttu-id="28f94-169">**지금 한 번 실행** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-169">Select **Run once now** option.</span></span>   
3. <span data-ttu-id="28f94-170">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-170">Click **Next**.</span></span>  

    ![복사 마법사 - 속성 페이지](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a><span data-ttu-id="28f94-172">2단계: 원본 구성</span><span class="sxs-lookup"><span data-stu-id="28f94-172">Step 2: Configure source</span></span>
<span data-ttu-id="28f94-173">이 섹션에서는 단계 tooconfigure hello 소스 hello: 1TB TPC hello Azure Blob에 포함 된-H 품목 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-173">This section shows you hello steps tooconfigure hello source: Azure Blob containing hello 1-TB TPC-H line item files.</span></span>

1. <span data-ttu-id="28f94-174">선택 hello **Azure Blob 저장소** hello 데이터를 저장 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-174">Select hello **Azure Blob Storage** as hello data store and click **Next**.</span></span>

    ![복사 마법사 - 원본 페이지 선택](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. <span data-ttu-id="28f94-176">Hello Azure Blob 저장소 계정에 대 한 hello 연결 정보를 입력 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-176">Fill in hello connection information for hello Azure Blob storage account, and click **Next**.</span></span>

    ![복사 마법사 - 원본 연결 정보](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. <span data-ttu-id="28f94-178">Hello 선택 **폴더** hello TPC H 줄이 포함 된 파일 항목을 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-178">Choose hello **folder** containing hello TPC-H line item files and click **Next**.</span></span>

    ![복사 마법사 - 입력 폴더 선택](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. <span data-ttu-id="28f94-180">클릭 하면 **다음**, hello 파일 형식 설정은 자동으로 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-180">Upon clicking **Next**, hello file format settings are detected automatically.</span></span>  <span data-ttu-id="28f94-181">Toomake 해당 열 구분 기호 인지를 확인 합니다. ' | hello 기본 쉼표',' 대신 '.</span><span class="sxs-lookup"><span data-stu-id="28f94-181">Check toomake sure that column delimiter is ‘|’ instead of hello default comma ‘,’.</span></span>  <span data-ttu-id="28f94-182">클릭 **다음** hello 데이터를 미리 본 후입니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-182">Click **Next** after you have previewed hello data.</span></span>

    ![복사 마법사 - 파일 형식 설정](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a><span data-ttu-id="28f94-184">3단계: 대상 구성</span><span class="sxs-lookup"><span data-stu-id="28f94-184">Step 3: Configure destination</span></span>
<span data-ttu-id="28f94-185">이 섹션에서는 어떻게 tooconfigure hello 대상: `lineitem` hello Azure SQL 데이터 웨어하우스 데이터베이스의 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-185">This section shows you how tooconfigure hello destination: `lineitem` table in hello Azure SQL Data Warehouse database.</span></span>

1. <span data-ttu-id="28f94-186">선택 **Azure SQL 데이터 웨어하우스** hello 대상으로 저장 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-186">Choose **Azure SQL Data Warehouse** as hello destination store and click **Next**.</span></span>

    ![복사 마법사 - 대상 데이터 저장소 선택](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. <span data-ttu-id="28f94-188">Azure SQL 데이터 웨어하우스에 대 한 hello 연결 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-188">Fill in hello connection information for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="28f94-189">Hello 역할의 구성원 인 hello 사용자를 지정 했는지 확인 `xlargerc` (hello 참조 **필수 구성 요소** 자세한 지침에 대 한 섹션)를 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-189">Make sure you specify hello user that is a member of hello role `xlargerc` (see hello **prerequisites** section for detailed instructions), and click **Next**.</span></span>

    ![복사 마법사 - 대상 연결 정보](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. <span data-ttu-id="28f94-191">Hello 대상 테이블을 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-191">Choose hello destination table and click **Next**.</span></span>

    ![복사 마법사 - 테이블 매핑 페이지](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. <span data-ttu-id="28f94-193">스키마 매핑 페이지에서 "열 매핑 적용" 옵션을 선택 취소하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-193">In Schema mapping page, leave "Apply column mapping" option unchecked and click **Next**.</span></span>

## <a name="step-4-performance-settings"></a><span data-ttu-id="28f94-194">4단계: 성능 설정</span><span class="sxs-lookup"><span data-stu-id="28f94-194">Step 4: Performance settings</span></span>

<span data-ttu-id="28f94-195">**Polybase 허용**은 기본적으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-195">**Allow polybase** is checked by default.</span></span>  <span data-ttu-id="28f94-196">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-196">Click **Next**.</span></span>

![복사 마법사 - 스키마 매핑 페이지](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a><span data-ttu-id="28f94-198">5단계: 로드 결과 배포 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="28f94-198">Step 5: Deploy and monitor load results</span></span>
1. <span data-ttu-id="28f94-199">클릭 **마침** 단추 toodeploy 합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-199">Click **Finish** button toodeploy.</span></span>

    ![복사 마법사 - 요약 페이지](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. <span data-ttu-id="28f94-201">Hello 배포가 완료 된 후 클릭 `Click here toomonitor copy pipeline` toomonitor hello 복사 진행을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-201">After hello deployment is complete, click `Click here toomonitor copy pipeline` toomonitor hello copy run progress.</span></span> <span data-ttu-id="28f94-202">Hello에서 만든 선택 hello 복사 파이프라인 **활동 창** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-202">Select hello copy pipeline you created in hello **Activity Windows** list.</span></span>

    ![복사 마법사 - 요약 페이지](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    <span data-ttu-id="28f94-204">Hello에서 세부 정보를 실행 하는 hello 복사본을 볼 수 **활동 Window 탐색기** 소스에서 읽고 쓸 대상, 기간 및 실행 하는 hello에 대 한 평균 처리량 hello에 hello 데이터 볼륨을 포함 하 여 hello 오른쪽 패널에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-204">You can view hello copy run details in hello **Activity Window Explorer** in hello right panel, including hello data volume read from source and written into destination, duration, and hello average throughput for hello run.</span></span>

    <span data-ttu-id="28f94-205">다음 스크린 샷, Azure Blob 저장소에서 SQL 데이터 웨어하우스로 1TB를 복사 하는 hello에서 볼 수 있듯이 효과적으로 1.22 g b p s 처리량을 달성 하는 14 분 소요!</span><span class="sxs-lookup"><span data-stu-id="28f94-205">As you can see from hello following screen shot, copying 1 TB from Azure Blob Storage into SQL Data Warehouse took 14 minutes, effectively achieving 1.22 GBps throughput!</span></span>

    ![복사 마법사 - 성공 대화 상자](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a><span data-ttu-id="28f94-207">모범 사례</span><span class="sxs-lookup"><span data-stu-id="28f94-207">Best practices</span></span>
<span data-ttu-id="28f94-208">Azure SQL Data Warehouse 데이터베이스 실행에 대한 몇 가지 모범 사례는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-208">Here are a few best practices for running your Azure SQL Data Warehouse database:</span></span>

* <span data-ttu-id="28f94-209">클러스터형 COLUMNSTORE 인덱스로 로드될 경우 더 큰 리소스 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-209">Use a larger resource class when loading into a CLUSTERED COLUMNSTORE INDEX.</span></span>
* <span data-ttu-id="28f94-210">더 효율적으로 조인하려면 기본 라운드 로빈 배포가 아닌 열 선택에 의한 해시 배포를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-210">For more efficient joins, consider using hash distribution by a select column instead of default round robin distribution.</span></span>
* <span data-ttu-id="28f94-211">로드 속도를 높이려면 임시 데이터에 힙을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-211">For faster load speeds, consider using heap for transient data.</span></span>
* <span data-ttu-id="28f94-212">Azure SQL Data Warehouse 로드를 완료한 후 통계를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-212">Create statistics after you finish loading Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="28f94-213">자세한 내용은 [Azure SQL Data Warehouse에 대한 모범 사례](../sql-data-warehouse/sql-data-warehouse-best-practices.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="28f94-213">See [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28f94-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="28f94-214">Next steps</span></span>
* <span data-ttu-id="28f94-215">[데이터 팩터리 복사 마법사](data-factory-copy-wizard.md) -이 문서에서는 hello 복사 마법사에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-215">[Data Factory Copy Wizard](data-factory-copy-wizard.md) - This article provides details about hello Copy Wizard.</span></span>
* <span data-ttu-id="28f94-216">[복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) -hello 참조 성능 측정 및 조정 가이드가이 문서를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="28f94-216">[Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) - This article contains hello reference performance measurements and tuning guide.</span></span>
