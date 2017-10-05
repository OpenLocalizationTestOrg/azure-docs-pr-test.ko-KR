---
title: "Redgate를 사용하여 Azure Data Warehouse에 데이터 로드 | Microsoft Docs"
description: "데이터 웨어하우징 시나리오에 대해 Redgate의 Data Platform Studio를 사용하는 방법을 알아봅니다."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 670aef98-31f7-4436-86c0-cc989a39fe7f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: a38b237d5bfc0450c1ca79b53a5784dbb9bf8602
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a><span data-ttu-id="086b6-103">Redgate Data Platform Studio를 사용하여 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="086b6-103">Load data with Redgate Data Platform Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="086b6-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="086b6-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)
> * [<span data-ttu-id="086b6-105">데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="086b6-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [<span data-ttu-id="086b6-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="086b6-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)
> * [<span data-ttu-id="086b6-107">BCP</span><span class="sxs-lookup"><span data-stu-id="086b6-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="086b6-108">이 자습서에서는 [Redgate의 DPS(Data Platform Studio)](http://www.red-gate.com/products/azure-development/data-platform-studio/)를 사용하여 온-프레미스 SQL Server에서 Azure SQL Data Warehouse로 데이터를 이동하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-108">This tutorial shows you how to use [Redgate's Data Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS) to move data from an on-premises SQL Server to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="086b6-109">Data Platform Studio는 가장 적합한 호환성 수정 및 최적화를 적용하므로 SQL Data Warehouse를 시작하는 가장 빠른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-109">Data Platform Studio applies the most appropriate compatibility fixes and optimizations, so it's the quickest way to get started with SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="086b6-110">[Redgate](http://www.red-gate.com)는 다양한 SQL Server 도구를 제공하는 오래된 Microsoft 파트너입니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-110">[Redgate](http://www.red-gate.com) is a long-time Microsoft partner that delivers various SQL Server tools.</span></span> <span data-ttu-id="086b6-111">Data Platform Studio의 이 기능은 상업 및 비상업적 용도 모두에서 무료로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-111">This feature in Data Platform Studio has been made available freely for both commercial and non-commercial use.</span></span>
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="086b6-112">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="086b6-112">Before you begin</span></span>
### <a name="create-or-identify-resources"></a><span data-ttu-id="086b6-113">리소스 만들기 또는 식별</span><span class="sxs-lookup"><span data-stu-id="086b6-113">Create or identify resources</span></span>
<span data-ttu-id="086b6-114">이 자습서를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-114">Before starting this tutorial, you need to have:</span></span>

* <span data-ttu-id="086b6-115">**온-프레미스 SQL Server Database**: SQL Data Warehouse로 가져올 데이터는 온-프레미스 SQL Server(버전 2008R2 이상)에서 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-115">**on-premises SQL Server Database**: The data you want to import to SQL Data Warehouse needs to come from an on-premises SQL Server (version 2008R2 or above).</span></span> <span data-ttu-id="086b6-116">Data Platform Studio는 Azure SQL Database 또는 텍스트 파일에서 직접 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-116">Data Platform Studio cannot import data directly from an Azure SQL Database or from text files.</span></span>
* <span data-ttu-id="086b6-117">**Azure Storage 계정**: Data Platform Studio는 SQL Data Warehouse에 데이터를 로드하기 전에 Azure Blob Storage에 데이터를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-117">**Azure Storage Account**: Data Platform Studio stages the data in Azure Blob Storage before loading it into SQL Data Warehouse.</span></span> <span data-ttu-id="086b6-118">저장소 계정으로는 "클래식" 배포 모델보다는 "Resource Manager" 배포 모델(기본값)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-118">The storage account must be using the “Resource Manager” deployment model (the default) rather than the “Classic” deployment model.</span></span> <span data-ttu-id="086b6-119">저장소 계정이 없을 경우 저장소 계정을 만드는 방법을 알아보세요</span><span class="sxs-lookup"><span data-stu-id="086b6-119">If you don't have a storage account, learn how to Create a storage account.</span></span> 
* <span data-ttu-id="086b6-120">**SQL Data Warehouse**: 이 자습서에서는 온-프레미스 SQL Server에서 SQL Data Warehouse로 데이터를 이동하므로 데이터 웨어하우스 온라인이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-120">**SQL Data Warehouse**: This tutorial moves the data from on-premises SQL Server to SQL Data Warehouse, so you need to have a data warehouse online.</span></span> <span data-ttu-id="086b6-121">데이터 웨어하우스가 아직 없는 경우 Azure SQL Data Warehouse를 만드는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="086b6-121">If you do not already have a data warehouse, learn how to Create an Azure SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="086b6-122">저장소 계정 및 데이터 웨어하우스를 동일한 지역에 만들면 성능이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-122">Performance is improved if the storage account and the data warehouse are created in the same region.</span></span>
> 
> 

## <a name="step-1-sign-in-to-data-platform-studio-with-your-azure-account"></a><span data-ttu-id="086b6-123">1단계: Azure 계정으로 Data Platform Studio에 로그인</span><span class="sxs-lookup"><span data-stu-id="086b6-123">Step 1: Sign in to Data Platform Studio with your Azure account</span></span>
<span data-ttu-id="086b6-124">웹 브라우저를 열고 [Data Platform Studio](https://www.dataplatformstudio.com/) 웹 사이트로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-124">Open your web browser and navigate to the [Data Platform Studio](https://www.dataplatformstudio.com/) website.</span></span> <span data-ttu-id="086b6-125">저장소 계정 및 데이터 웨어하우스를 만드는 데 사용했던 것과 동일한 Azure 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-125">Sign in with the same Azure account that you used to create the storage account and data warehouse.</span></span> <span data-ttu-id="086b6-126">전자 메일 주소가 회사 및 학교 계정 및 Microsoft 계정과 연결된 경우 리소스에 대한 액세스 권한이 있는 계정을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-126">If your email address is associated with both a work or school account and a Microsoft account, be sure to choose the account that has access to your resources.</span></span>

> [!NOTE]
> <span data-ttu-id="086b6-127">처음으로 Data Platform Studio를 사용하는 경우 Azure 리소스를 관리할 수 있는 응용 프로그램 권한을 부여하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-127">If this is your first time using Data Platform Studio, you are asked to grant the application permission to manage your Azure resources.</span></span>
> 
> 

## <a name="step-2-start-the-import-wizard"></a><span data-ttu-id="086b6-128">2단계: 가져오기 마법사 시작</span><span class="sxs-lookup"><span data-stu-id="086b6-128">Step 2: Start the Import Wizard</span></span>
<span data-ttu-id="086b6-129">DPS 주 화면에서 Azure SQL Data Warehouse로 가져오기 링크를 선택하여 가져오기 마법사를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-129">From the DPS main screen, select the Import to Azure SQL Data Warehouse link to start the import wizard.</span></span>

![][1]

## <a name="step-3-install-the-data-platform-studio-gateway"></a><span data-ttu-id="086b6-130">3단계: Data Platform Studio 게이트웨이 설치</span><span class="sxs-lookup"><span data-stu-id="086b6-130">Step 3: Install the Data Platform Studio Gateway</span></span>
<span data-ttu-id="086b6-131">온-프레미스 SQL Server 데이터베이스에 연결하려면 DPS 게이트웨이를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-131">To connect to your on-premises SQL Server database, you need to install the DPS Gateway.</span></span> <span data-ttu-id="086b6-132">게이트웨이는 온-프레미스 환경에 대한 액세스를 제공하고, 데이터를 추출하며, 이 데이터를 저장소 계정에 업로드하는 클라이언트 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-132">The gateway is a client agent that provides access to your on-premises environment, extracts the data, and uploads it to your storage account.</span></span> <span data-ttu-id="086b6-133">데이터는 Redgate 서버를 통과하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-133">Your data never passes through Redgate’s servers.</span></span> <span data-ttu-id="086b6-134">게이트웨이를 설치하려면:</span><span class="sxs-lookup"><span data-stu-id="086b6-134">To install the Gateway:</span></span>

1. <span data-ttu-id="086b6-135">**게이트웨이 만들기** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-135">Click the **Create Gateway** link</span></span>
2. <span data-ttu-id="086b6-136">제공된 설치 관리자를 사용하여 게이트웨이를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-136">Download and install the Gateway using the provided installer</span></span>

![][2]

> [!NOTE]
> <span data-ttu-id="086b6-137">게이트웨이는 원본 SQL Server 데이터베이스에 대한 네트워크 액세스 권한이 있는 모든 컴퓨터에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-137">The Gateway can be installed on any machine with network access to the source SQL Server database.</span></span> <span data-ttu-id="086b6-138">현재 사용자의 자격 증명으로 Windows 인증을 사용하여 SQL Server 데이터베이스에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-138">It accesses the SQL Server database using Windows authentication with the credentials of the current user.</span></span>
> 
> 

<span data-ttu-id="086b6-139">설치한 후에는 게이트웨이 상태가 연결됨으로 변경되고 다음을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-139">Once installed, the Gateway status changes to Connected and you can select Next.</span></span>

## <a name="step-4-identify-the-source-database"></a><span data-ttu-id="086b6-140">4단계: 원본 데이터베이스 식별</span><span class="sxs-lookup"><span data-stu-id="086b6-140">Step 4: Identify the source database</span></span>
<span data-ttu-id="086b6-141">*서버 이름 입력* 텍스트 상자에 데이터베이스를 호스트하는 서버 이름을 입력하고 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-141">In the *Enter Server Name* textbox, enter the name of the server that hosts your database and select **Next**.</span></span> <span data-ttu-id="086b6-142">그런 다음 드롭다운 메뉴에서 데이터를 가져올 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-142">Then, from the drop-down menu, select the database you want to import data from.</span></span>

![][3]

<span data-ttu-id="086b6-143">DPS가 선택한 데이터베이스에서 가져올 테이블을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-143">DPS inspects the selected database for tables to import.</span></span> <span data-ttu-id="086b6-144">기본적으로 DPS는 데이터베이스에 있는 모든 테이블을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-144">By default, DPS imports all the tables in the database.</span></span> <span data-ttu-id="086b6-145">모든 테이블 링크를 확장하여 테이블을 선택 또는 선택 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-145">You can select or deselect tables by expanding the All Tables link.</span></span> <span data-ttu-id="086b6-146">다음 단추를 선택하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-146">Select the Next button to move forward.</span></span>

## <a name="step-5-choose-a-storage-account-to-stage-the-data"></a><span data-ttu-id="086b6-147">5단계: 데이터를 준비할 저장소 계정 선택</span><span class="sxs-lookup"><span data-stu-id="086b6-147">Step 5: Choose a storage account to stage the data</span></span>
<span data-ttu-id="086b6-148">DPS는 데이터를 준비할 위치를 묻는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-148">DPS prompts you for a location to stage the data.</span></span> <span data-ttu-id="086b6-149">구독에서 기존 저장소 계정을 선택하고 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-149">Choose an existing storage account from your subscription and select **Next**.</span></span>

> [!NOTE]
> <span data-ttu-id="086b6-150">DPS가 선택한 저장소 계정에 새 Blob 컨테이너를 만들고 각 가져오기에 고유한 폴더를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-150">DPS will create a new blob container in the chosen storage account and use a distinct folder for each import.</span></span>
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a><span data-ttu-id="086b6-151">6단계: 데이터 웨어하우스 선택</span><span class="sxs-lookup"><span data-stu-id="086b6-151">Step 6: Select a data warehouse</span></span>
<span data-ttu-id="086b6-152">다음으로 데이터를 가져올 온라인 [Azure SQL Data Warehouse](http://aka.ms/sqldw) 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-152">Next, you select an online [Azure SQL Data Warehouse](http://aka.ms/sqldw) database to import the data into.</span></span> <span data-ttu-id="086b6-153">데이터베이스를 선택했으면 데이터베이스에 연결할 자격 증명을 입력하고 **다음**을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-153">Once you've selected your database, you need to enter the credentials to connect to the database and select **Next**.</span></span>

![][5]

> [!NOTE]
> <span data-ttu-id="086b6-154">DPS는 원본 데이터 테이블을 데이터 웨어하우스에 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-154">DPS merges the source data tables into the data warehouse.</span></span> <span data-ttu-id="086b6-155">DPS는 테이블 이름이 데이터 웨어하우스에 있는 기존 테이블을 덮어써야 하는 경우 이를 경고합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-155">DPS warns you if the table name requires it to overwrite existing tables in the data warehouse.</span></span> <span data-ttu-id="086b6-156">선택적으로 가져오기 전에 기존의 모든 개체 삭제를 선택하여 데이터 웨어하우스에서 기존 개체를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-156">You may optionally delete any existing objects in the data warehouse by ticking Delete all existing objects before import.</span></span>
> 
> 

## <a name="step-7-import-the-data"></a><span data-ttu-id="086b6-157">7단계: 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="086b6-157">Step 7: Import the data</span></span>
<span data-ttu-id="086b6-158">DPS는 데이터를 가져오려고 하는 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-158">DPS confirms that you would like to import the data.</span></span> <span data-ttu-id="086b6-159">가져오기 시작 단추를 클릭하면 데이터 가져오기가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-159">Simply click the Start import button to begin the data import.</span></span>

![][6]

<span data-ttu-id="086b6-160">DPS는 온-프레미스 SQL Server에서 데이터를 추출하고 업로드하는 진행 상황과 SQL Data Warehouse로 가져오는 진행 상황을 보여 주는 시각화를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-160">DPS displays a visualization that shows the progress of extracting and uploading the data from the on-premises SQL Server and the progress of the import into SQL Data Warehouse.</span></span>

![][7]

<span data-ttu-id="086b6-161">가져오기가 완료되면 DPS는 수행된 데이터 가져오기 및 호환성 수정의 변경 보고를 요약하여 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-161">Once the import is complete, DPS displays a summary of the data import and a change report of the compatibility fixes that have been performed.</span></span>

![][8]

## <a name="next-steps"></a><span data-ttu-id="086b6-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="086b6-162">Next steps</span></span>
<span data-ttu-id="086b6-163">SQL Data Warehouse 내에서 데이터를 탐색하려면 다음을 확인하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="086b6-163">To explore your data within SQL Data Warehouse, start by viewing:</span></span>

* <span data-ttu-id="086b6-164">[Azure SQL Data Warehouse 쿼리(Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span><span class="sxs-lookup"><span data-stu-id="086b6-164">[Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span></span>
* <span data-ttu-id="086b6-165">[Power BI를 사용하여 데이터 시각화][Visualize data with Power BI]</span><span class="sxs-lookup"><span data-stu-id="086b6-165">[Visualize data with Power BI][Visualize data with Power BI]</span></span>

<span data-ttu-id="086b6-166">Redgate의 Data Platform Studio에 대해 자세히 알아보려면:</span><span class="sxs-lookup"><span data-stu-id="086b6-166">To learn more about Redgate’s Data Platform Studio:</span></span>

* [<span data-ttu-id="086b6-167">DPS 홈 페이지 방문</span><span class="sxs-lookup"><span data-stu-id="086b6-167">Visit the DPS homepage</span></span>](http://www.dataplatformstudio.com/)
* [<span data-ttu-id="086b6-168">Channel9에서 DPS 데모 보기</span><span class="sxs-lookup"><span data-stu-id="086b6-168">Watch a demo of DPS on Channel9</span></span>](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

<span data-ttu-id="086b6-169">SQL Data Warehouse에서 데이터를 마이그레이션 및 로드하는 다른 방법에 대한 개요는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="086b6-169">For an overview of other ways to migrate and load your data in SQL Data Warehouse see:</span></span>

* <span data-ttu-id="086b6-170">[SQL Data Warehouse에 솔루션 마이그레이션][Migrate your solution to SQL Data Warehouse]</span><span class="sxs-lookup"><span data-stu-id="086b6-170">[Migrate your solution to SQL Data Warehouse][Migrate your solution to SQL Data Warehouse]</span></span>
* [<span data-ttu-id="086b6-171">Azure SQL 데이터 웨어하우스에 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="086b6-171">Load data into Azure SQL Data Warehouse</span></span>](sql-data-warehouse-overview-load.md)

<span data-ttu-id="086b6-172">더 많은 개발 팁은 [SQL Data Warehouse 개발 개요](sql-data-warehouse-overview-develop.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="086b6-172">For more development tips, see the [SQL Data Warehouse development overview](sql-data-warehouse-overview-develop.md).</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-redgate/2016-10-05_15-59-56.png
[2]: media/sql-data-warehouse-redgate/2016-10-05_11-16-07.png
[3]: media/sql-data-warehouse-redgate/2016-10-05_11-17-46.png
[4]: media/sql-data-warehouse-redgate/2016-10-05_11-20-41.png
[5]: media/sql-data-warehouse-redgate/2016-10-05_11-31-24.png
[6]: media/sql-data-warehouse-redgate/2016-10-05_11-32-20.png
[7]: media/sql-data-warehouse-redgate/2016-10-05_11-49-53.png
[8]: media/sql-data-warehouse-redgate/2016-10-05_12-57-10.png

<!--Article references-->
[Query Azure SQL Data Warehouse (Visual Studio)]: ./sql-data-warehouse-query-visual-studio.md
[Visualize data with Power BI]: ./sql-data-warehouse-get-started-visualize-with-power-bi.md
[Migrate your solution to SQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
