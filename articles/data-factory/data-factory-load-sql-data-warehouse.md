---
title: "SQL Data Warehouse로 데이터(TB) 로드 | Microsoft Docs"
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
ms.openlocfilehash: c29f1f01b660c4eb780e178a68036327fafa9ba6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a><span data-ttu-id="14e08-103">Data Factory를 통해 15분 내에 Azure SQL Data Warehouse에 1TB 로드</span><span class="sxs-lookup"><span data-stu-id="14e08-103">Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Data Factory</span></span>
<span data-ttu-id="14e08-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)는 거대한 양의 관계형 및 비관계형 데이터를 처리할 수 있는 클라우드 기반 규모 확장 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span>  <span data-ttu-id="14e08-105">대규모 병렬 처리(MPP) 아키텍처를 기반으로 하는 SQL Data Warehouse는 엔터프라이즈 데이터 웨어하우스 워크로드에 최적화됩니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-105">Built on massively parallel processing (MPP) architecture, SQL Data Warehouse is optimized for enterprise data warehouse workloads.</span></span>  <span data-ttu-id="14e08-106">저장소를 확장하고 개별적으로 계산할 수 있는 클라우드 탄력성을 유연하게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-106">It offers cloud elasticity with the flexibility to scale storage and compute independently.</span></span>

<span data-ttu-id="14e08-107">이제는 Azure SQL Data Warehouse를 시작하는 것이 **Azure Data Factory**를 사용하는 것보다 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-107">Getting started with Azure SQL Data Warehouse is now easier than ever using **Azure Data Factory**.</span></span>  <span data-ttu-id="14e08-108">Azure Data Factory는 완벽하게 관리되는 클라우드 기반 데이터 통합 서비스이며, SQL Data Warehouse를 기존 시스템에서 나온 데이터로 채우는 데 사용되므로 SQL Data Warehouse를 평가하고 분석 솔루션을 빌드하는 동안 소중한 시간을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-108">Azure Data Factory is a fully managed cloud-based data integration service, which can be used to populate a SQL Data Warehouse with the data from your existing system, and saving you valuable time while evaluating SQL Data Warehouse and building your analytics solutions.</span></span> <span data-ttu-id="14e08-109">Azure Data Factory를 사용하여 Azure SQL Data Warehouse로 데이터를 로드하는 방법의 주요 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-109">Here are the key benefits of loading data into Azure SQL Data Warehouse using Azure Data Factory:</span></span>

* <span data-ttu-id="14e08-110">**간편한 설정**: 스크립팅이 필요하지 않은 직관적인 5단계 마법사.</span><span class="sxs-lookup"><span data-stu-id="14e08-110">**Easy to set up**: 5-step intuitive wizard with no scripting required.</span></span>
* <span data-ttu-id="14e08-111">**다양한 데이터 저장소 지원**: 다양한 온-프레미스 및 클라우드 기반 데이터 저장소 집합에 대한 기본 제공 지원.</span><span class="sxs-lookup"><span data-stu-id="14e08-111">**Rich data store support**: built-in support for a rich set of on-premises and cloud-based data stores.</span></span>
* <span data-ttu-id="14e08-112">**보안 및 호환**: 데이터가 HTTPS 또는 ExpressRoute를 통해 전송되고 글로벌 서비스를 제공하므로 데이터가 지리적 경계를 벗어나지 않음</span><span class="sxs-lookup"><span data-stu-id="14e08-112">**Secure and compliant**: data is transferred over HTTPS or ExpressRoute, and global service presence ensures your data never leaves the geographical boundary</span></span>
* <span data-ttu-id="14e08-113">**PolyBase를 통해 제공되는 뛰어난 성능** – 데이터를 Azure SQL Data Warehouse로 이동하는 가장 효율적인 방법은 Polybase를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-113">**Unparalleled performance by using PolyBase** – Using Polybase is the most efficient way to move data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="14e08-114">스테이징 Blob 기능을 사용하면 Polybase가 기본적으로 지원하는 Azure Blob Storage를 제외한 모든 유형의 데이터 저장소에서 높은 로드 속도를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-114">Using the staging blob feature, you can achieve high load speeds from all types of data stores besides Azure Blob storage, which the Polybase supports by default.</span></span>

<span data-ttu-id="14e08-115">이 문서에서는 Data Factory 복사 마법사를 사용하여 Azure Blob Storage에서 나온 1TB 데이터를 15분 내에 1.2GBps 이상의 처리량 속도로 Azure SQL Data Warehouse로 로드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-115">This article shows you how to use Data Factory Copy Wizard to load 1-TB data from Azure Blob Storage into Azure SQL Data Warehouse in under 15 minutes, at over 1.2 GBps throughput.</span></span>

<span data-ttu-id="14e08-116">또한 복사 마법사를 사용하여 Azure SQL Data Warehouse로 데이터를 이동하기 위한 단계별 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-116">This article provides step-by-step instructions for moving data into Azure SQL Data Warehouse by using the Copy Wizard.</span></span>

> [!NOTE]
>  <span data-ttu-id="14e08-117">Azure SQL Data Warehouse 간에 데이터를 이동하는 Data Factory 기능에 대한 일반적인 내용은 [Azure Data Factory를 사용하여 Azure SQL Data Warehouse 간 데이터 이동](data-factory-azure-sql-data-warehouse-connector.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14e08-117">For general information about capabilities of Data Factory in moving data to/from Azure SQL Data Warehouse, see [Move data to and from Azure SQL Data Warehouse using Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) article.</span></span>
>
> <span data-ttu-id="14e08-118">Azure Portal, Visual Studio, PowerShell 등을 사용하여 파이프라인을 빌드할 수도 있습니다. Azure 데이터 팩터리에서 복사 작업을 사용하는 단계별 지침이 있는 빠른 연습은 [자습서: Azure Blob에서 Azure SQL 데이터베이스에 데이터 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14e08-118">You can also build pipelines using Azure portal, Visual Studio, PowerShell, etc. See [Tutorial: Copy data from Azure Blob to Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a quick walkthrough with step-by-step instructions for using the Copy Activity in Azure Data Factory.</span></span>  
>
>

## <a name="prerequisites"></a><span data-ttu-id="14e08-119">필수 조건</span><span class="sxs-lookup"><span data-stu-id="14e08-119">Prerequisites</span></span>
* <span data-ttu-id="14e08-120">Azure Blob Storage: 이 실험에서는 Azure Blob Storage(GRS)를 사용하여 TPC-H 테스트 데이터 집합을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-120">Azure Blob Storage: this experiment uses Azure Blob Storage (GRS) for storing TPC-H testing dataset.</span></span>  <span data-ttu-id="14e08-121">Azure Storage 계정이 없을 경우 [저장소 계정을 만드는 방법](../storage/common/storage-create-storage-account.md#create-a-storage-account)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14e08-121">If you do not have an Azure storage account, learn [how to create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="14e08-122">[TPC-H](http://www.tpc.org/tpch/) 데이터: 테스트 집합으로는 TPC-H를 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-122">[TPC-H](http://www.tpc.org/tpch/) data: we are going to use TPC-H as the testing dataset.</span></span>  <span data-ttu-id="14e08-123">이렇게 하려면 데이터 집합을 생성하도록 도와주는 TPC-H 도구 키트의 `dbgen`을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-123">To do that, you need to use `dbgen` from TPC-H toolkit, which helps you generate the dataset.</span></span>  <span data-ttu-id="14e08-124">[TPC 도구](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp)에서 `dbgen`에 대한 원본 코드를 다운로드하여 직접 컴파일하거나, [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools)에서 컴파일된 이진 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-124">You can either download source code for `dbgen` from [TPC Tools](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) and compile it yourself, or download the compiled binary from [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span></span>  <span data-ttu-id="14e08-125">dbgen.exe를 다음 명령과 함께 실행하여 10개 파일에 분산되어 있는 `lineitem` 표에 대한 1TB의 플랫 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-125">Run dbgen.exe with the following commands to generate 1 TB flat file for `lineitem` table spread across 10 files:</span></span>

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * <span data-ttu-id="14e08-126">…</span><span class="sxs-lookup"><span data-stu-id="14e08-126">…</span></span>
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    <span data-ttu-id="14e08-127">이제 생성된 파일을 Azure Blob에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-127">Now copy the generated files to Azure Blob.</span></span>  <span data-ttu-id="14e08-128">ADF 복사를 사용하여 이 작업을 하는 방법에 대한 자세한 내용은 [Azure Data Factory를 사용하여 온-프레미스 파일 시스템 간 데이터 이동](data-factory-onprem-file-system-connector.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14e08-128">Refer to [Move data to and from an on-premises file system by using Azure Data Factory](data-factory-onprem-file-system-connector.md) for how to do that using ADF Copy.</span></span>    
* <span data-ttu-id="14e08-129">Azure SQL Data Warehouse: 이 실험에서는 6,000개 DWU를 사용하여 만들어진 Azure SQL Data Warehouse로 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-129">Azure SQL Data Warehouse: this experiment loads data into Azure SQL Data Warehouse created with 6,000 DWUs</span></span>

    <span data-ttu-id="14e08-130">SQL Data Warehouse 데이터베이스를 만드는 방법에 대한 자세한 내용은 [Azure SQL Data Warehouse 만들기](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14e08-130">Refer to [Create an Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) for detailed instructions on how to create a SQL Data Warehouse database.</span></span>  <span data-ttu-id="14e08-131">Polybase를 사용하여 SQL Data Warehouse에 대한 최상의 로드 성능을 얻기 위해 성능 설정에서 허용되는 최대 DWU(데이터 웨어하우스 단위) 수(6,000 DWU)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-131">To get the best possible load performance into SQL Data Warehouse using Polybase, we choose maximum number of Data Warehouse Units (DWUs) allowed in the Performance setting, which is 6,000 DWUs.</span></span>

  > [!NOTE]
  > <span data-ttu-id="14e08-132">Azure Blob에서 로드할 때 데이터 로드 성능은 SQL Data Warehouse에서 구성하는 DWU 수에 정비례합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-132">When loading from Azure Blob, the data loading performance is directly proportional to the number of DWUs you configure on the SQL Data Warehouse:</span></span>
  >
  > <span data-ttu-id="14e08-133">1TB를 1,000 DWU SQL Data Warehouse에 로드하는 데는 87분(~200MBps 처리량)이 걸리고, 1TB를 2,000 DWU SQL Data Warehouse에 로드하는 데는 46분(~380MBps 처리량)이 걸리고, 1TB를 6,000 DWU SQL Data Warehouse에 로드하는 데는 14분(~1.2GBps 처리량)이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-133">Loading 1 TB into 1,000 DWU SQL Data Warehouse takes 87 minutes (~200 MBps throughput) Loading 1 TB into 2,000 DWU SQL Data Warehouse takes 46 minutes (~380 MBps throughput) Loading 1 TB into 6,000 DWU SQL Data Warehouse takes 14 minutes (~1.2 GBps throughput)</span></span>
  >
  >

    <span data-ttu-id="14e08-134">6,000 DWU가 포함된 SQL Data Warehouse를 만들려면 성능 슬라이더를 완전히 오른쪽으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-134">To create a SQL Data Warehouse with 6,000 DWUs, move the Performance slider all the way to the right:</span></span>

    ![성능 슬라이더](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    <span data-ttu-id="14e08-136">6,000 DWU를 포함하도록 구성되지 않은 기존 데이터베이스의 경우 Azure Portal을 사용하여 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-136">For an existing database that is not configured with 6,000 DWUs, you can scale it up using Azure portal.</span></span>  <span data-ttu-id="14e08-137">Azure Portal에서 데이터베이스로 이동하면 다음 이미지에 표시된 **개요** 패널에 **크기 조정** 단추가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-137">Navigate to the database in Azure portal, and there is a **Scale** button in the **Overview** panel shown in the following image:</span></span>

    ![크기 조정 단추](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    <span data-ttu-id="14e08-139">**크기 조정** 단추를 클릭하여 다음 패널을 열고, 슬라이더를 최대값으로 이동하고 나서, **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-139">Click the **Scale** button to open the following panel, move the slider to the maximum value, and click **Save** button.</span></span>

    ![크기 조정 대화 상자](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    <span data-ttu-id="14e08-141">이 실험에서는 `xlargerc` 리소스 클래스를 사용하여 Azure SQL Data Warehouse로 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-141">This experiment loads data into Azure SQL Data Warehouse using `xlargerc` resource class.</span></span>

    <span data-ttu-id="14e08-142">최상의 처리량을 얻으려면 `xlargerc` 리소스 클래스에 속한 SQL Data Warehouse 사용자를 사용하여 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-142">To achieve best possible throughput, copy needs to be performed using a SQL Data Warehouse user belonging to `xlargerc` resource class.</span></span>  <span data-ttu-id="14e08-143">[사용자 리소스 클래스 변경 예제](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example)에 따라 이 작업을 하는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="14e08-143">Learn how to do that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>  
* <span data-ttu-id="14e08-144">다음 DDL 문을 실행하여 Azure SQL Data Warehouse 데이터베이스에서 대상 테이블 스키마를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-144">Create destination table schema in Azure SQL Data Warehouse database, by running the following DDL statement:</span></span>

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
<span data-ttu-id="14e08-145">필수 구성 요소 단계가 완료되면 이제 복사 마법사를 사용하여 복사 활동을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-145">With the prerequisite steps completed, we are now ready to configure the copy activity using the Copy Wizard.</span></span>

## <a name="launch-copy-wizard"></a><span data-ttu-id="14e08-146">복사 마법사 시작</span><span class="sxs-lookup"><span data-stu-id="14e08-146">Launch Copy Wizard</span></span>
1. <span data-ttu-id="14e08-147">[Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-147">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="14e08-148">왼쪽 위 모서리에서 **+ 새로 만들기**를 클릭하고 **인텔리전스 + 분석**을 클릭하고 **Data Factory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-148">Click **+ NEW** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="14e08-149">**새 데이터 팩터리** 블레이드에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-149">In the **New data factory** blade:</span></span>

   1. <span data-ttu-id="14e08-150">**이름**으로 **LoadIntoSQLDWDataFactory**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-150">Enter **LoadIntoSQLDWDataFactory** for the **name**.</span></span>
       <span data-ttu-id="14e08-151">Azure Data Factory 이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-151">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="14e08-152">**Data Factory 이름 “LoadIntoSQLDWDataFactory”를 사용할 수 없습니다.**오류가 표시되는 경우 Data Factory 이름을 변경하고(예: yournameLoadIntoSQLDWDataFactory) 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-152">If you receive the error: **Data factory name “LoadIntoSQLDWDataFactory” is not available**, change the name of the data factory (for example, yournameLoadIntoSQLDWDataFactory) and try creating again.</span></span> <span data-ttu-id="14e08-153">데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14e08-153">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
   2. <span data-ttu-id="14e08-154">Azure **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-154">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="14e08-155">리소스 그룹에 대해 다음 단계 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-155">For Resource Group, do one of the following steps:</span></span>
      1. <span data-ttu-id="14e08-156">**기존 항목 사용**을 선택하고 기존 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-156">Select **Use existing** to select an existing resource group.</span></span>
      2. <span data-ttu-id="14e08-157">**새로 만들기**를 선택하고 리소스 그룹의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-157">Select **Create new** to enter a name for a resource group.</span></span>
   4. <span data-ttu-id="14e08-158">Data Factory의 **위치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-158">Select a **location** for the data factory.</span></span>
   5. <span data-ttu-id="14e08-159">블레이드 하단에서 **대시보드에 고정** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-159">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>  
   6. <span data-ttu-id="14e08-160">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-160">Click **Create**.</span></span>
4. <span data-ttu-id="14e08-161">만들기가 완료되면 다음 이미지와 같이 **Data Factory** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-161">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span></span>

   ![데이터 팩터리 홈페이지](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. <span data-ttu-id="14e08-163">데이터 팩터리 홈 페이지에서 **데이터 복사** 타일을 클릭하여 **복사 마법사**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-163">On the Data Factory home page, click the **Copy data** tile to launch **Copy Wizard**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="14e08-164">웹 브라우저가 "권한 부여..." 상태로 중지된 것을 확인하면 **타사 쿠키 및 사이트 데이터 차단** 설정을 사용 안 함/선택 취소하고 (또는) 계속 사용하지 않습니다. 그리고 **login.microsoftonline.com**에 대한 예외를 만든 다음 마법사를 다시 시작해봅니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-164">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a><span data-ttu-id="14e08-165">1단계: 데이터 로드 일정 구성</span><span class="sxs-lookup"><span data-stu-id="14e08-165">Step 1: Configure data loading schedule</span></span>
<span data-ttu-id="14e08-166">첫 번째 단계에서는 데이터 로드 일정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-166">The first step is to configure the data loading schedule.</span></span>  

<span data-ttu-id="14e08-167">**속성** 페이지에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-167">In the **Properties** page:</span></span>

1. <span data-ttu-id="14e08-168">**작업 이름**으로 **CopyFromBlobToAzureSqlDataWarehouse**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-168">Enter **CopyFromBlobToAzureSqlDataWarehouse** for **Task name**</span></span>
2. <span data-ttu-id="14e08-169">**지금 한 번 실행** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-169">Select **Run once now** option.</span></span>   
3. <span data-ttu-id="14e08-170">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-170">Click **Next**.</span></span>  

    ![복사 마법사 - 속성 페이지](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a><span data-ttu-id="14e08-172">2단계: 원본 구성</span><span class="sxs-lookup"><span data-stu-id="14e08-172">Step 2: Configure source</span></span>
<span data-ttu-id="14e08-173">이 섹션에서는 1TB TPC-H 라인 항목 파일이 포함된 원본: Azure Blob을 구성하는 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-173">This section shows you the steps to configure the source: Azure Blob containing the 1-TB TPC-H line item files.</span></span>

1. <span data-ttu-id="14e08-174">데이터 저장소로 **Azure Blob Storage**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-174">Select the **Azure Blob Storage** as the data store and click **Next**.</span></span>

    ![복사 마법사 - 원본 페이지 선택](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. <span data-ttu-id="14e08-176">Azure Blob Storage 계정의 연결 정보를 입력하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-176">Fill in the connection information for the Azure Blob storage account, and click **Next**.</span></span>

    ![복사 마법사 - 원본 연결 정보](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. <span data-ttu-id="14e08-178">TPC-H 라인 항목 파일이 포함된 **폴더**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-178">Choose the **folder** containing the TPC-H line item files and click **Next**.</span></span>

    ![복사 마법사 - 입력 폴더 선택](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. <span data-ttu-id="14e08-180">**다음**을 클릭하면 파일 형식 설정이 자동으로 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-180">Upon clicking **Next**, the file format settings are detected automatically.</span></span>  <span data-ttu-id="14e08-181">열 구분 기호가 기본 쉼표 ‘,’가 아닌 ‘|’인지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="14e08-181">Check to make sure that column delimiter is ‘|’ instead of the default comma ‘,’.</span></span>  <span data-ttu-id="14e08-182">데이터를 미리 본 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-182">Click **Next** after you have previewed the data.</span></span>

    ![복사 마법사 - 파일 형식 설정](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a><span data-ttu-id="14e08-184">3단계: 대상 구성</span><span class="sxs-lookup"><span data-stu-id="14e08-184">Step 3: Configure destination</span></span>
<span data-ttu-id="14e08-185">이 섹션에서는 대상: Azure SQL Data Warehouse 데이터베이스의 `lineitem` 테이블을 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-185">This section shows you how to configure the destination: `lineitem` table in the Azure SQL Data Warehouse database.</span></span>

1. <span data-ttu-id="14e08-186">대상 저장소로 **Azure SQL Data Warehouse**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-186">Choose **Azure SQL Data Warehouse** as the destination store and click **Next**.</span></span>

    ![복사 마법사 - 대상 데이터 저장소 선택](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. <span data-ttu-id="14e08-188">Azure SQL Data Warehouse의 연결 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-188">Fill in the connection information for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="14e08-189">`xlargerc` 역할(자세한 내용은 **필수 구성 요소** 섹션 참조)의 구성원인 사용자를 지정하는지 확인하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-189">Make sure you specify the user that is a member of the role `xlargerc` (see the **prerequisites** section for detailed instructions), and click **Next**.</span></span>

    ![복사 마법사 - 대상 연결 정보](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. <span data-ttu-id="14e08-191">대상 테이블을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-191">Choose the destination table and click **Next**.</span></span>

    ![복사 마법사 - 테이블 매핑 페이지](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. <span data-ttu-id="14e08-193">스키마 매핑 페이지에서 "열 매핑 적용" 옵션을 선택 취소하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-193">In Schema mapping page, leave "Apply column mapping" option unchecked and click **Next**.</span></span>

## <a name="step-4-performance-settings"></a><span data-ttu-id="14e08-194">4단계: 성능 설정</span><span class="sxs-lookup"><span data-stu-id="14e08-194">Step 4: Performance settings</span></span>

<span data-ttu-id="14e08-195">**Polybase 허용**은 기본적으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-195">**Allow polybase** is checked by default.</span></span>  <span data-ttu-id="14e08-196">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-196">Click **Next**.</span></span>

![복사 마법사 - 스키마 매핑 페이지](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a><span data-ttu-id="14e08-198">5단계: 로드 결과 배포 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="14e08-198">Step 5: Deploy and monitor load results</span></span>
1. <span data-ttu-id="14e08-199">**마침** 단추를 클릭하여 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-199">Click **Finish** button to deploy.</span></span>

    ![복사 마법사 - 요약 페이지](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. <span data-ttu-id="14e08-201">배포가 완료된 후 `Click here to monitor copy pipeline`을 클릭하여 복사 실행 진행률을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-201">After the deployment is complete, click `Click here to monitor copy pipeline` to monitor the copy run progress.</span></span> <span data-ttu-id="14e08-202">**Activity Windows**(활동 기간) 목록에서 직접 만든 복사 파이프라인을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-202">Select the copy pipeline you created in the **Activity Windows** list.</span></span>

    ![복사 마법사 - 요약 페이지](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    <span data-ttu-id="14e08-204">오른쪽 패널의 **Activity Window Explorer**(활동 기간 탐색기)에서는 원본에서 읽고 대상에 쓴 데이터 볼륨, 기간, 평균 실행 처리량을 비롯한 복사 실행 세부 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-204">You can view the copy run details in the **Activity Window Explorer** in the right panel, including the data volume read from source and written into destination, duration, and the average throughput for the run.</span></span>

    <span data-ttu-id="14e08-205">다음 스크린샷처럼 Azure Blob Storage에서 SQL Data Warehouse로 1TB를 복사하는 데는 14분이 걸려서 실제로 1.22GBps 처리량을 얻었습니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-205">As you can see from the following screen shot, copying 1 TB from Azure Blob Storage into SQL Data Warehouse took 14 minutes, effectively achieving 1.22 GBps throughput!</span></span>

    ![복사 마법사 - 성공 대화 상자](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a><span data-ttu-id="14e08-207">모범 사례</span><span class="sxs-lookup"><span data-stu-id="14e08-207">Best practices</span></span>
<span data-ttu-id="14e08-208">Azure SQL Data Warehouse 데이터베이스 실행에 대한 몇 가지 모범 사례는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-208">Here are a few best practices for running your Azure SQL Data Warehouse database:</span></span>

* <span data-ttu-id="14e08-209">클러스터형 COLUMNSTORE 인덱스로 로드될 경우 더 큰 리소스 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-209">Use a larger resource class when loading into a CLUSTERED COLUMNSTORE INDEX.</span></span>
* <span data-ttu-id="14e08-210">더 효율적으로 조인하려면 기본 라운드 로빈 배포가 아닌 열 선택에 의한 해시 배포를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-210">For more efficient joins, consider using hash distribution by a select column instead of default round robin distribution.</span></span>
* <span data-ttu-id="14e08-211">로드 속도를 높이려면 임시 데이터에 힙을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-211">For faster load speeds, consider using heap for transient data.</span></span>
* <span data-ttu-id="14e08-212">Azure SQL Data Warehouse 로드를 완료한 후 통계를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-212">Create statistics after you finish loading Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="14e08-213">자세한 내용은 [Azure SQL Data Warehouse에 대한 모범 사례](../sql-data-warehouse/sql-data-warehouse-best-practices.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14e08-213">See [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14e08-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="14e08-214">Next steps</span></span>
* <span data-ttu-id="14e08-215">[Data Factory 복사 마법사](data-factory-copy-wizard.md) - 이 문서에서는 복사 마법사에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-215">[Data Factory Copy Wizard](data-factory-copy-wizard.md) - This article provides details about the Copy Wizard.</span></span>
* <span data-ttu-id="14e08-216">[복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md) - 이 문서에는 참조 성능 측정값과 조정 가이드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="14e08-216">[Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) - This article contains the reference performance measurements and tuning guide.</span></span>
