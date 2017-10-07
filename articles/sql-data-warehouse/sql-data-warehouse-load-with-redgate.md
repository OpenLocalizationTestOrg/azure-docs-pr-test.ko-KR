---
title: "aaaUse Redgate tooload 데이터 tooyour Azure 데이터 웨어하우스 | Microsoft Docs"
description: "자세한 내용은 방법의 데이터 웨어하우징 시나리오에 대 한 데이터 플랫폼 Studio toouse Redgate 합니다."
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
ms.openlocfilehash: 6082390c07c8ffa73ebd8ab272ace00ba8bb1897
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a><span data-ttu-id="e9115-103">Redgate Data Platform Studio를 사용하여 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="e9115-103">Load data with Redgate Data Platform Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e9115-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="e9115-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)
> * [<span data-ttu-id="e9115-105">데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="e9115-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [<span data-ttu-id="e9115-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="e9115-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)
> * [<span data-ttu-id="e9115-107">BCP</span><span class="sxs-lookup"><span data-stu-id="e9115-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="e9115-108">이 자습서에서는 어떻게 toouse [Redgate의 데이터 플랫폼 Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DP) toomove 데이터는 온-프레미스 SQL Server tooAzure SQL 데이터 웨어하우스를에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-108">This tutorial shows you how toouse [Redgate's Data Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS) toomove data from an on-premises SQL Server tooAzure SQL Data Warehouse.</span></span> <span data-ttu-id="e9115-109">데이터 플랫폼 Studio hello 가장 적합 한 호환성 픽스를 적용 하 고 최적화, 아니므로 quickest hello 방식으로 tooget SQL 데이터 웨어하우스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-109">Data Platform Studio applies hello most appropriate compatibility fixes and optimizations, so it's hello quickest way tooget started with SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="e9115-110">[Redgate](http://www.red-gate.com)는 다양한 SQL Server 도구를 제공하는 오래된 Microsoft 파트너입니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-110">[Redgate](http://www.red-gate.com) is a long-time Microsoft partner that delivers various SQL Server tools.</span></span> <span data-ttu-id="e9115-111">Data Platform Studio의 이 기능은 상업 및 비상업적 용도 모두에서 무료로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-111">This feature in Data Platform Studio has been made available freely for both commercial and non-commercial use.</span></span>
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="e9115-112">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="e9115-112">Before you begin</span></span>
### <a name="create-or-identify-resources"></a><span data-ttu-id="e9115-113">리소스 만들기 또는 식별</span><span class="sxs-lookup"><span data-stu-id="e9115-113">Create or identify resources</span></span>
<span data-ttu-id="e9115-114">이 자습서를 시작 하기 전에 toohave가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-114">Before starting this tutorial, you need toohave:</span></span>

* <span data-ttu-id="e9115-115">**온-프레미스 SQL Server 데이터베이스**: tooimport tooSQL 데이터 웨어하우스 toocome 온-프레미스 SQL Server에서 필요한 데이터를 hello (버전 2008 r2 이상)입니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-115">**on-premises SQL Server Database**: hello data you want tooimport tooSQL Data Warehouse needs toocome from an on-premises SQL Server (version 2008R2 or above).</span></span> <span data-ttu-id="e9115-116">Data Platform Studio는 Azure SQL Database 또는 텍스트 파일에서 직접 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-116">Data Platform Studio cannot import data directly from an Azure SQL Database or from text files.</span></span>
* <span data-ttu-id="e9115-117">**Azure 저장소 계정**: 데이터 플랫폼 Studio SQL 데이터 웨어하우스에 로드 하기 전에 hello Azure Blob 저장소에는 데이터를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-117">**Azure Storage Account**: Data Platform Studio stages hello data in Azure Blob Storage before loading it into SQL Data Warehouse.</span></span> <span data-ttu-id="e9115-118">hello 저장소 계정 hello "클래식" 배포 모델 대신 hello "리소스 관리자" 배포 모델 (hello 기본값) 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-118">hello storage account must be using hello “Resource Manager” deployment model (hello default) rather than hello “Classic” deployment model.</span></span> <span data-ttu-id="e9115-119">저장소 계정이 없는 경우에 대해 배울 방법 tooCreate 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-119">If you don't have a storage account, learn how tooCreate a storage account.</span></span> 
* <span data-ttu-id="e9115-120">**SQL 데이터 웨어하우스**:이 자습서 hello 데이터 이동 온-프레미스 SQL Server 데이터 웨어하우스 tooSQL에서 toohave 필요는 온라인 데이터 웨어하우스 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-120">**SQL Data Warehouse**: This tutorial moves hello data from on-premises SQL Server tooSQL Data Warehouse, so you need toohave a data warehouse online.</span></span> <span data-ttu-id="e9115-121">데이터 웨어하우스 아직 없는 경우에 대해 배울 방법 tooCreate Azure SQL 데이터 웨어하우스 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-121">If you do not already have a data warehouse, learn how tooCreate an Azure SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="e9115-122">Hello 저장소 계정 및 데이터 웨어하우스 hello에에서 만들어집니다 hello 동일 하면 성능이 향상 됩니다 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-122">Performance is improved if hello storage account and hello data warehouse are created in hello same region.</span></span>
> 
> 

## <a name="step-1-sign-in-toodata-platform-studio-with-your-azure-account"></a><span data-ttu-id="e9115-123">1 단계: Azure 계정으로 tooData 플랫폼 Studio에 로그인</span><span class="sxs-lookup"><span data-stu-id="e9115-123">Step 1: Sign in tooData Platform Studio with your Azure account</span></span>
<span data-ttu-id="e9115-124">웹 브라우저를 열고 탐색 toohello [데이터 플랫폼 Studio](https://www.dataplatformstudio.com/) 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-124">Open your web browser and navigate toohello [Data Platform Studio](https://www.dataplatformstudio.com/) website.</span></span> <span data-ttu-id="e9115-125">동일한 Azure 계정 해당 하면 사용한 toocreate hello 저장소 계정 및 데이터 웨어하우스를 hello 하는으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-125">Sign in with hello same Azure account that you used toocreate hello storage account and data warehouse.</span></span> <span data-ttu-id="e9115-126">전자 메일 주소와 회사 또는 학교 계정 및 Microsoft 계정을 연결 된 경우에 tooyour 리소스에 액세스할 수 있는 있는지 toochoose hello 계정 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-126">If your email address is associated with both a work or school account and a Microsoft account, be sure toochoose hello account that has access tooyour resources.</span></span>

> [!NOTE]
> <span data-ttu-id="e9115-127">데이터 플랫폼 Studio를 사용 하 여 처음으로 이면 toogrant hello 응용 프로그램 사용 권한 toomanage Azure 리소스를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-127">If this is your first time using Data Platform Studio, you are asked toogrant hello application permission toomanage your Azure resources.</span></span>
> 
> 

## <a name="step-2-start-hello-import-wizard"></a><span data-ttu-id="e9115-128">2 단계: hello 가져오기 마법사 시작</span><span class="sxs-lookup"><span data-stu-id="e9115-128">Step 2: Start hello Import Wizard</span></span>
<span data-ttu-id="e9115-129">Hello DP 기본 화면에서 hello 가져오기 tooAzure SQL 데이터 웨어하우스 링크 toostart hello 가져오기 마법사를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-129">From hello DPS main screen, select hello Import tooAzure SQL Data Warehouse link toostart hello import wizard.</span></span>

![][1]

## <a name="step-3-install-hello-data-platform-studio-gateway"></a><span data-ttu-id="e9115-130">3 단계: hello 데이터 플랫폼 Studio 게이트웨이 설치</span><span class="sxs-lookup"><span data-stu-id="e9115-130">Step 3: Install hello Data Platform Studio Gateway</span></span>
<span data-ttu-id="e9115-131">tooconnect tooyour 온-프레미스 SQL Server 데이터베이스 tooinstall hello DP 게이트웨이가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-131">tooconnect tooyour on-premises SQL Server database, you need tooinstall hello DPS Gateway.</span></span> <span data-ttu-id="e9115-132">hello 게이트웨이 액세스 tooyour 온-프레미스 환경, hello 데이터를 추출 및 tooyour 저장소 계정에 업로드 제공 하는 클라이언트 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-132">hello gateway is a client agent that provides access tooyour on-premises environment, extracts hello data, and uploads it tooyour storage account.</span></span> <span data-ttu-id="e9115-133">데이터는 Redgate 서버를 통과하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-133">Your data never passes through Redgate’s servers.</span></span> <span data-ttu-id="e9115-134">tooinstall hello 게이트웨이:</span><span class="sxs-lookup"><span data-stu-id="e9115-134">tooinstall hello Gateway:</span></span>

1. <span data-ttu-id="e9115-135">Hello 클릭 **게이트웨이 만들기** 링크</span><span class="sxs-lookup"><span data-stu-id="e9115-135">Click hello **Create Gateway** link</span></span>
2. <span data-ttu-id="e9115-136">다운로드 및 사용 하 여 설치 hello 게이트웨이 hello 제공 된 설치 관리자</span><span class="sxs-lookup"><span data-stu-id="e9115-136">Download and install hello Gateway using hello provided installer</span></span>

![][2]

> [!NOTE]
> <span data-ttu-id="e9115-137">hello 게이트웨이 네트워크 액세스 toohello 원본 SQL Server 데이터베이스를 사용 하 여 컴퓨터에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-137">hello Gateway can be installed on any machine with network access toohello source SQL Server database.</span></span> <span data-ttu-id="e9115-138">Windows 인증을 사용 하 여 hello 현재 사용자의 hello 자격 증명 hello SQL Server 데이터베이스에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-138">It accesses hello SQL Server database using Windows authentication with hello credentials of hello current user.</span></span>
> 
> 

<span data-ttu-id="e9115-139">설치 되 면에 게이트웨이 상태 변경 내용을 tooConnected hello च े ं 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-139">Once installed, hello Gateway status changes tooConnected and you can select Next.</span></span>

## <a name="step-4-identify-hello-source-database"></a><span data-ttu-id="e9115-140">4 단계: hello 원본 데이터베이스를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-140">Step 4: Identify hello source database</span></span>
<span data-ttu-id="e9115-141">Hello에 *서버 이름 입력* hello 데이터베이스를 호스팅하는 hello 서버 이름을 입력 하 고 선택 하는 텍스트 상자 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-141">In hello *Enter Server Name* textbox, enter hello name of hello server that hosts your database and select **Next**.</span></span> <span data-ttu-id="e9115-142">그런 다음 hello 드롭 다운 메뉴에서의 tooimport 데이터 hello 데이터베이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-142">Then, from hello drop-down menu, select hello database you want tooimport data from.</span></span>

![][3]

<span data-ttu-id="e9115-143">DP은 tooimport 테이블에 대 한 hello 선택한 데이터베이스를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-143">DPS inspects hello selected database for tables tooimport.</span></span> <span data-ttu-id="e9115-144">기본적으로 DP hello 데이터베이스의 모든 hello 테이블을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-144">By default, DPS imports all hello tables in hello database.</span></span> <span data-ttu-id="e9115-145">선택할 수도 있고 모든 테이블에 연결 하는 hello를 확장 하 여 테이블을 선택 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-145">You can select or deselect tables by expanding hello All Tables link.</span></span> <span data-ttu-id="e9115-146">Hello 다음 단추 toomove 앞으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-146">Select hello Next button toomove forward.</span></span>

## <a name="step-5-choose-a-storage-account-toostage-hello-data"></a><span data-ttu-id="e9115-147">5 단계: 저장소 계정 toostage hello 데이터 선택</span><span class="sxs-lookup"><span data-stu-id="e9115-147">Step 5: Choose a storage account toostage hello data</span></span>
<span data-ttu-id="e9115-148">DP 위치 toostage hello 데이터에 대 한 라는 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-148">DPS prompts you for a location toostage hello data.</span></span> <span data-ttu-id="e9115-149">구독에서 기존 저장소 계정을 선택하고 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-149">Choose an existing storage account from your subscription and select **Next**.</span></span>

> [!NOTE]
> <span data-ttu-id="e9115-150">DP은 hello 선택한 저장소 계정에서에서 새 blob 컨테이너를 만들고 각 가져오기에 대 한 별도 폴더를 사용 하 여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-150">DPS will create a new blob container in hello chosen storage account and use a distinct folder for each import.</span></span>
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a><span data-ttu-id="e9115-151">6단계: 데이터 웨어하우스 선택</span><span class="sxs-lookup"><span data-stu-id="e9115-151">Step 6: Select a data warehouse</span></span>
<span data-ttu-id="e9115-152">다음으로, 온라인 선택 하면 [Azure SQL 데이터 웨어하우스](http://aka.ms/sqldw) tooimport hello 데이터를 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-152">Next, you select an online [Azure SQL Data Warehouse](http://aka.ms/sqldw) database tooimport hello data into.</span></span> <span data-ttu-id="e9115-153">Tooenter hello 자격 증명 tooconnect toohello 필요한 데이터베이스를 선택한 후 선택한 데이터베이스 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-153">Once you've selected your database, you need tooenter hello credentials tooconnect toohello database and select **Next**.</span></span>

![][5]

> [!NOTE]
> <span data-ttu-id="e9115-154">DP은 hello 데이터 웨어하우스로 hello 원본 데이터 테이블을 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-154">DPS merges hello source data tables into hello data warehouse.</span></span> <span data-ttu-id="e9115-155">DP 경우 hello 테이블 이름이 필요한 toooverwrite hello 데이터 웨어하우스에 있는 기존 테이블 경고 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-155">DPS warns you if hello table name requires it toooverwrite existing tables in hello data warehouse.</span></span> <span data-ttu-id="e9115-156">가져오기 전에 모든 기존 개체 삭제 틱 하 여 hello 데이터 웨어하우스의 모든 기존 개체를 선택적으로 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-156">You may optionally delete any existing objects in hello data warehouse by ticking Delete all existing objects before import.</span></span>
> 
> 

## <a name="step-7-import-hello-data"></a><span data-ttu-id="e9115-157">7 단계: hello 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="e9115-157">Step 7: Import hello data</span></span>
<span data-ttu-id="e9115-158">DP 싶다는 의사를 tooimport hello 데이터를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-158">DPS confirms that you would like tooimport hello data.</span></span> <span data-ttu-id="e9115-159">Hello 시작 가져오기 단추 toobegin hello 데이터 가져오기를 클릭 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-159">Simply click hello Start import button toobegin hello data import.</span></span>

![][6]

<span data-ttu-id="e9115-160">DP은 hello 추출 하 고 hello hello 온-프레미스 SQL Server 및 hello hello 가져오기 진행률이 SQL 데이터 웨어하우스로 데이터를 업로드 하는 중 진행 상황을 보여 주는 시각적으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-160">DPS displays a visualization that shows hello progress of extracting and uploading hello data from hello on-premises SQL Server and hello progress of hello import into SQL Data Warehouse.</span></span>

![][7]

<span data-ttu-id="e9115-161">Hello 가져오기가 완료 되 면 DP hello 데이터 가져오기에 대 한 요약 및의 hello 호환성 수정 수행 된 변경 내용 보고서를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-161">Once hello import is complete, DPS displays a summary of hello data import and a change report of hello compatibility fixes that have been performed.</span></span>

![][8]

## <a name="next-steps"></a><span data-ttu-id="e9115-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e9115-162">Next steps</span></span>
<span data-ttu-id="e9115-163">tooexplore SQL 데이터 웨어하우스 내에서 데이터 확인 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-163">tooexplore your data within SQL Data Warehouse, start by viewing:</span></span>

* <span data-ttu-id="e9115-164">[Azure SQL Data Warehouse 쿼리(Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span><span class="sxs-lookup"><span data-stu-id="e9115-164">[Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span></span>
* <span data-ttu-id="e9115-165">[Power BI를 사용하여 데이터 시각화][Visualize data with Power BI]</span><span class="sxs-lookup"><span data-stu-id="e9115-165">[Visualize data with Power BI][Visualize data with Power BI]</span></span>

<span data-ttu-id="e9115-166">toolearn Redgate의 데이터 플랫폼 Studio에 대 한 자세한:</span><span class="sxs-lookup"><span data-stu-id="e9115-166">toolearn more about Redgate’s Data Platform Studio:</span></span>

* [<span data-ttu-id="e9115-167">Hello DP 홈 페이지를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-167">Visit hello DPS homepage</span></span>](http://www.dataplatformstudio.com/)
* [<span data-ttu-id="e9115-168">Channel9에서 DPS 데모 보기</span><span class="sxs-lookup"><span data-stu-id="e9115-168">Watch a demo of DPS on Channel9</span></span>](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

<span data-ttu-id="e9115-169">다른 방법으로 toomigrate 및 부하의 개요에 대 한 SQL 데이터 웨어하우스에 데이터 참조:</span><span class="sxs-lookup"><span data-stu-id="e9115-169">For an overview of other ways toomigrate and load your data in SQL Data Warehouse see:</span></span>

* <span data-ttu-id="e9115-170">[사용자 솔루션 tooSQL 데이터 웨어하우스 마이그레이션][Migrate your solution tooSQL Data Warehouse]</span><span class="sxs-lookup"><span data-stu-id="e9115-170">[Migrate your solution tooSQL Data Warehouse][Migrate your solution tooSQL Data Warehouse]</span></span>
* [<span data-ttu-id="e9115-171">Azure SQL 데이터 웨어하우스에 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="e9115-171">Load data into Azure SQL Data Warehouse</span></span>](sql-data-warehouse-overview-load.md)

<span data-ttu-id="e9115-172">더 많은 개발 팁에 대 한 참조 hello [SQL 데이터 웨어하우스 개발 개요](sql-data-warehouse-overview-develop.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9115-172">For more development tips, see hello [SQL Data Warehouse development overview](sql-data-warehouse-overview-develop.md).</span></span>

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
[Migrate your solution tooSQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
