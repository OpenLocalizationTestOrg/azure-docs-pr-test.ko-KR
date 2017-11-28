---
title: "Azure SQL 데이터 웨어하우스 (SSIS)에 SQL Server에서 aaaLoad 데이터 | Microsoft Docs"
description: "다양 한 데이터를에서 SQL Server Integration Services (SSIS) 패키지 toomove 데이터 toocreate tooSQL 데이터 웨어하우스 원본 하는 방법을 보여 줍니다."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e2c252e9-0828-47c2-a808-e3bea46c134a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/30/2017
ms.author: cakarst;douglasl;barbkess
ms.openlocfilehash: bb28a08807a5b07832b85f2f074c2acf912c1dc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-ssis"></a><span data-ttu-id="d3a68-103">SQL Server에서 Azure SQL 데이터 웨어하우스로 데이터 로드(SSIS)</span><span class="sxs-lookup"><span data-stu-id="d3a68-103">Load data from SQL Server into Azure SQL Data Warehouse (SSIS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d3a68-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="d3a68-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="d3a68-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="d3a68-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="d3a68-106">bcp</span><span class="sxs-lookup"><span data-stu-id="d3a68-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="d3a68-107">Azure SQL 데이터 웨어하우스에 SQL Server에서 SQL Server Integration Services (SSIS) 패키지 tooload 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-107">Create a SQL Server Integration Services (SSIS) package tooload data from SQL Server into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d3a68-108">있습니다 수 필요에 따라 구조를 변경, 변환 및 hello SSIS 데이터 흐름을 통과할 때 hello 데이터를 정리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-108">You can optionally restructure, transform, and cleanse hello data as it passes through hello SSIS data flow.</span></span>

<span data-ttu-id="d3a68-109">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-109">In this tutorial, you will:</span></span>

* <span data-ttu-id="d3a68-110">Visual Studio에서 새 Integration Services 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-110">Create a new Integration Services project in Visual Studio.</span></span>
* <span data-ttu-id="d3a68-111">(원본)으로 SQL Server (대상)으로 SQL 데이터 웨어하우스를 비롯 한 toodata 원본에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-111">Connect toodata sources, including SQL Server (as a source) and SQL Data Warehouse (as a destination).</span></span>
* <span data-ttu-id="d3a68-112">Hello 대상으로 hello 소스에서 데이터를 로드 하는 SSIS 패키지를 디자인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-112">Design an SSIS package that loads data from hello source into hello destination.</span></span>
* <span data-ttu-id="d3a68-113">Hello SSIS 패키지 tooload hello 데이터를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-113">Run hello SSIS package tooload hello data.</span></span>

<span data-ttu-id="d3a68-114">이 자습서에서는 hello 데이터 원본으로 SQL Server를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-114">This tutorial uses SQL Server as hello data source.</span></span> <span data-ttu-id="d3a68-115">SQL Server는 온-프레미스 또는 Azure 가상 컴퓨터에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-115">SQL Server could be running on premises or in an Azure virtual machine.</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="d3a68-116">기본 개념</span><span class="sxs-lookup"><span data-stu-id="d3a68-116">Basic concepts</span></span>
<span data-ttu-id="d3a68-117">hello 패키지는 SSIS에서 작업의 hello 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-117">hello package is hello unit of work in SSIS.</span></span> <span data-ttu-id="d3a68-118">관련 패키지는 프로젝트로 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-118">Related packages are grouped in projects.</span></span> <span data-ttu-id="d3a68-119">Visual Studio에서 SQL Server Data Tools를 사용하여 프로젝트를 만들고 패키지를 디자인합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-119">You create projects and design packages in Visual Studio with SQL Server Data Tools.</span></span> <span data-ttu-id="d3a68-120">hello 디자인 프로세스는 시각적 프로세스를 끌어서 놓으면 구성 요소 hello 도구 상자 toohello 디자인 화면에서 이들을 연결 하 고 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-120">hello design process is a visual process in which you drag and drop components from hello Toolbox toohello design surface, connect them, and set their properties.</span></span> <span data-ttu-id="d3a68-121">패키지에서는 완료 된 후 배포할 수 있습니다 필요에 따라 포괄적인 관리, 모니터링 및 보안에 대 한 서버 tooSQL 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-121">After you finish your package, you can optionally deploy it tooSQL Server for comprehensive management, monitoring, and security.</span></span>

## <a name="options-for-loading-data-with-ssis"></a><span data-ttu-id="d3a68-122">SSIS를 이용하여 데이터 로드 시 선택 사항</span><span class="sxs-lookup"><span data-stu-id="d3a68-122">Options for loading data with SSIS</span></span>
<span data-ttu-id="d3a68-123">SSIS(SQL Server Integration Services)는 SQL 데이터 웨어하우스에 연결하고 데이터를 로드하는 다양한 옵션을 제공하는 유연한 도구 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-123">SQL Server Integration Services (SSIS) is a flexible set of tools that provides a variety of options for connecting to, and loading data into, SQL Data Warehouse.</span></span>

1. <span data-ttu-id="d3a68-124">ADO NET 대상 tooconnect tooSQL 데이터 웨어하우스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-124">Use an ADO NET Destination tooconnect tooSQL Data Warehouse.</span></span> <span data-ttu-id="d3a68-125">이 자습서에서는 가장 적은 구성 옵션 hello에 있기 때문에 ADO NET 대상을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-125">This tutorial uses an ADO NET Destination because it has hello fewest configuration options.</span></span>
2. <span data-ttu-id="d3a68-126">OLE DB Destination tooconnect tooSQL 데이터 웨어하우스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-126">Use an OLE DB Destination tooconnect tooSQL Data Warehouse.</span></span> <span data-ttu-id="d3a68-127">이 옵션에는 ADO NET 대상 hello 보다 약간 더 나은 성능을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-127">This option may provide slightly better performance than hello ADO NET Destination.</span></span>
3. <span data-ttu-id="d3a68-128">Azure Blob 저장소에 hello Azure Blob 업로드 태스크 toostage hello 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-128">Use hello Azure Blob Upload Task toostage hello data in Azure Blob Storage.</span></span> <span data-ttu-id="d3a68-129">Hello SSIS SQL 실행 태스크 toolaunch hello 데이터 SQL 데이터 웨어하우스를 로드 하는 Polybase 스크립트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-129">Then use hello SSIS Execute SQL task toolaunch a Polybase script that loads hello data into SQL Data Warehouse.</span></span> <span data-ttu-id="d3a68-130">이 옵션은 hello 여기에 나열 된 hello 세 가지 옵션 중 최상의 성능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-130">This option provides hello best performance of hello three options listed here.</span></span> <span data-ttu-id="d3a68-131">Azure Blob 업로드 태스크 tooget hello 다운로드 hello [Microsoft SQL Server 2016 Integration Services 기능 팩 azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-131">tooget hello Azure Blob Upload task, download hello [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure].</span></span> <span data-ttu-id="d3a68-132">Polybase에 대 한 자세한 toolearn 참조 [PolyBase 가이드][PolyBase Guide]합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-132">toolearn more about Polybase, see [PolyBase Guide][PolyBase Guide].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="d3a68-133">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="d3a68-133">Before you start</span></span>
<span data-ttu-id="d3a68-134">이 자습서를 통해 toostep를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-134">toostep through this tutorial, you need:</span></span>

1. <span data-ttu-id="d3a68-135">**SSIS(SQL Server Integration Services)**.</span><span class="sxs-lookup"><span data-stu-id="d3a68-135">**SQL Server Integration Services (SSIS)**.</span></span> <span data-ttu-id="d3a68-136">SSIS는 SQL Server의 구성 요소이며 평가판 버전 또는 라이선스 버전의 SQL Server가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-136">SSIS is a component of SQL Server and requires an evaluation version or a licensed version of SQL Server.</span></span> <span data-ttu-id="d3a68-137">평가 된 버전의 SQL Server 2016 Preview tooget 참조 [SQL Server 평가][SQL Server Evaluations]합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-137">tooget an evaluation version of SQL Server 2016 Preview, see [SQL Server Evaluations][SQL Server Evaluations].</span></span>
2. <span data-ttu-id="d3a68-138">**Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="d3a68-138">**Visual Studio**.</span></span> <span data-ttu-id="d3a68-139">tooget hello 무료 Visual Studio Community 버전을 참조 하십시오. [Visual Studio Community][Visual Studio Community]합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-139">tooget hello free Visual Studio Community Edition, see [Visual Studio Community][Visual Studio Community].</span></span>
3. <span data-ttu-id="d3a68-140">**Visual Studio용 SSDT(SQL Server Data Tools)**.</span><span class="sxs-lookup"><span data-stu-id="d3a68-140">**SQL Server Data Tools for Visual Studio (SSDT)**.</span></span> <span data-ttu-id="d3a68-141">Visual Studio 용 SQL Server Data Tools tooget 참조 [다운로드 SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)]합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-141">tooget SQL Server Data Tools for Visual Studio, see [Download SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].</span></span>
4. <span data-ttu-id="d3a68-142">**예제 데이터**.</span><span class="sxs-lookup"><span data-stu-id="d3a68-142">**Sample data**.</span></span> <span data-ttu-id="d3a68-143">이 자습서에서는 예제 데이터에 SQL 데이터 웨어하우스 로드 하는 원본 데이터 toobe hello 처럼 hello AdventureWorks 예제 데이터베이스의 SQL Server에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-143">This tutorial uses sample data stored in SQL Server in hello AdventureWorks sample database as hello source data toobe loaded into SQL Data Warehouse.</span></span> <span data-ttu-id="d3a68-144">tooget hello AdventureWorks 예제 데이터베이스 참조 [2014 샘플 데이터베이스 AdventureWorks][AdventureWorks 2014 Sample Databases]합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-144">tooget hello AdventureWorks sample database, see [AdventureWorks 2014 Sample Databases][AdventureWorks 2014 Sample Databases].</span></span>
5. <span data-ttu-id="d3a68-145">**SQL 데이터 웨어하우스 데이터베이스 및 사용 권한**.</span><span class="sxs-lookup"><span data-stu-id="d3a68-145">**A SQL Data Warehouse database and permissions**.</span></span> <span data-ttu-id="d3a68-146">이 자습서는 tooa SQL 데이터 웨어하우스 인스턴스를 연결 하 고 데이터를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-146">This tutorial connects tooa SQL Data Warehouse instance and loads data into it.</span></span> <span data-ttu-id="d3a68-147">Toohave 권한을 toocreate 테이블 및 tooload 데이터 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-147">You have toohave permissions toocreate a table and tooload data.</span></span>
6. <span data-ttu-id="d3a68-148">**방화벽 규칙**.</span><span class="sxs-lookup"><span data-stu-id="d3a68-148">**A firewall rule**.</span></span> <span data-ttu-id="d3a68-149">전에 실행 되어 toocreate 방화벽 규칙을 SQL 데이터 웨어하우스 로컬 컴퓨터의 hello IP 주소를 가진 데이터 toohello SQL 데이터 웨어하우스에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-149">You have toocreate a firewall rule on SQL Data Warehouse with hello IP address of your local computer before you can upload data toohello SQL Data Warehouse.</span></span>

## <a name="step-1-create-a-new-integration-services-project"></a><span data-ttu-id="d3a68-150">1단계: 새 Integration Services 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="d3a68-150">Step 1: Create a new Integration Services project</span></span>
1. <span data-ttu-id="d3a68-151">Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-151">Launch Visual Studio.</span></span>
2. <span data-ttu-id="d3a68-152">Hello에 **파일** 메뉴 선택 **새로 만들기 | 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-152">On hello **File** menu, select **New | Project**.</span></span>
3. <span data-ttu-id="d3a68-153">Toohello 이동 **설치 됨 | 템플릿 | Business Intelligence | Integration Services** 프로젝트 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-153">Navigate toohello **Installed | Templates | Business Intelligence | Integration Services** project types.</span></span>
4. <span data-ttu-id="d3a68-154">**Integration Services 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-154">Select **Integration Services Project**.</span></span> <span data-ttu-id="d3a68-155">**이름** 및 **위치** 값을 입력한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-155">Provide values for **Name** and **Location**, and then select **OK**.</span></span>

<span data-ttu-id="d3a68-156">Visual Studio가 열리고 새 SSIS(Integration Services) 프로젝트가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-156">Visual Studio opens and creates a new Integration Services (SSIS) project.</span></span> <span data-ttu-id="d3a68-157">그런 다음 Visual Studio는 hello 프로젝트에서 패키지에 대 한 hello 단일 새 SSIS (Package.dtsx) hello 디자이너를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-157">Then Visual Studio opens hello designer for hello single new SSIS package (Package.dtsx) in hello project.</span></span> <span data-ttu-id="d3a68-158">Hello 화면 영역을 따라 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-158">You see hello following screen areas:</span></span>

* <span data-ttu-id="d3a68-159">Hello 왼쪽에 hello **도구 상자** SSIS 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-159">On hello left, hello **Toolbox** of SSIS components.</span></span>
* <span data-ttu-id="d3a68-160">Hello 중간 hello 디자인 화면에서 여러 탭으로 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-160">In hello middle, hello design surface, with multiple tabs.</span></span> <span data-ttu-id="d3a68-161">일반적으로 사용 하면 최소한 hello **제어 흐름** 및 hello **데이터 흐름** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-161">You typically use at least hello **Control Flow** and hello **Data Flow** tabs.</span></span>
* <span data-ttu-id="d3a68-162">오른쪽 hello에 hello **솔루션 탐색기** 및 hello **속성** 창.</span><span class="sxs-lookup"><span data-stu-id="d3a68-162">On hello right, hello **Solution Explorer** and hello **Properties** panes.</span></span>
  
    ![][01]

## <a name="step-2-create-hello-basic-data-flow"></a><span data-ttu-id="d3a68-163">2 단계: hello 기본 데이터 흐름 만들기</span><span class="sxs-lookup"><span data-stu-id="d3a68-163">Step 2: Create hello basic data flow</span></span>
1. <span data-ttu-id="d3a68-164">Hello 도구 상자 toohello hello 디자인 화면 가운데의에서 데이터 흐름 태스크를 끌어 옵니다 (hello에 **제어 흐름** 탭).</span><span class="sxs-lookup"><span data-stu-id="d3a68-164">Drag a Data Flow Task from hello Toolbox toohello center of hello design surface (on hello **Control Flow** tab).</span></span>
   
    ![][02]
2. <span data-ttu-id="d3a68-165">Hello 데이터 흐름 태스크 tooswitch toohello 데이터 흐름 탭을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-165">Double-click hello Data Flow Task tooswitch toohello Data Flow tab.</span></span>
3. <span data-ttu-id="d3a68-166">Hello 도구 상자에에서 hello 기타 원본 목록에서 ADO.NET 원본 toohello 디자인 화면으로를 끕니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-166">From hello Other Sources list in hello Toolbox, drag an ADO.NET Source toohello design surface.</span></span> <span data-ttu-id="d3a68-167">Hello 원본 어댑터 선택 된 상태를 해당 이름을 변경할 너무**SQL Server 원본** hello에 **속성** 창.</span><span class="sxs-lookup"><span data-stu-id="d3a68-167">With hello source adapter still selected, change its name too**SQL Server source** in hello **Properties** pane.</span></span>
4. <span data-ttu-id="d3a68-168">Hello 도구 상자에에서 hello 기타 대상 목록에서 hello ADO.NET 소스에서 ADO.NET 대상 toohello 디자인 화면으로를 끕니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-168">From hello Other Destinations list in hello Toolbox, drag an ADO.NET Destination toohello design surface under hello ADO.NET Source.</span></span> <span data-ttu-id="d3a68-169">Hello 대상 어댑터를 선택한 상태를 해당 이름을 변경할 너무**SQL DW 대상** hello에 **속성** 창.</span><span class="sxs-lookup"><span data-stu-id="d3a68-169">With hello destination adapter still selected, change its name too**SQL DW destination** in hello **Properties** pane.</span></span>
   
    ![][09]

## <a name="step-3-configure-hello-source-adapter"></a><span data-ttu-id="d3a68-170">3 단계: hello 원본 어댑터 구성</span><span class="sxs-lookup"><span data-stu-id="d3a68-170">Step 3: Configure hello source adapter</span></span>
1. <span data-ttu-id="d3a68-171">Hello 원본 어댑터 tooopen hello를 두 번 클릭 **ADO.NET 원본 편집기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-171">Double-click hello source adapter tooopen hello **ADO.NET Source Editor**.</span></span>
   
    ![][03]
2. <span data-ttu-id="d3a68-172">Hello에 **연결 관리자** hello 탭 **ADO.NET 원본 편집기**, hello 클릭 **새로** 단추 다음 toohello **ADO.NET 연결 관리자**목록 tooopen hello **ADO.NET 연결 관리자 구성** 대화 상자 및이 자습서에서는 데이터를 로드 하는 hello SQL Server 데이터베이스에 대 한 연결 설정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-172">On hello **Connection Manager** tab of hello **ADO.NET Source Editor**, click hello **New** button next toohello **ADO.NET connection manager** list tooopen hello **Configure ADO.NET Connection Manager** dialog box and create connection settings for hello SQL Server database from which this tutorial loads data.</span></span>
   
    ![][04]
3. <span data-ttu-id="d3a68-173">Hello에 **ADO.NET 연결 관리자 구성** 대화 상자를 클릭 hello **새로 만들기** 단추 tooopen hello **연결 관리자** 대화 상자 하 고 새 데이터 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-173">In hello **Configure ADO.NET Connection Manager** dialog box, click hello **New** button tooopen hello **Connection Manager** dialog box and create a new data connection.</span></span>
   
    ![][05]
4. <span data-ttu-id="d3a68-174">Hello에 **연결 관리자** 대화 상자에서 다음 작업 hello 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-174">In hello **Connection Manager** dialog box, do hello following things.</span></span>
   
   1. <span data-ttu-id="d3a68-175">에 대 한 **공급자**, 선택 hello SqlClient 데이터 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-175">For **Provider**, select hello SqlClient Data Provider.</span></span>
   2. <span data-ttu-id="d3a68-176">에 대 한 **서버 이름**, hello SQL Server 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-176">For **Server name**, enter hello SQL Server name.</span></span>
   3. <span data-ttu-id="d3a68-177">Hello에 **toohello 서버 로그온** 섹션을 선택 하거나 인증 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-177">In hello **Log on toohello server** section, select or enter authentication information.</span></span>
   4. <span data-ttu-id="d3a68-178">Hello에 **연결 tooa 데이터베이스** 섹션 hello AdventureWorks 예제 데이터베이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-178">In hello **Connect tooa database** section, select hello AdventureWorks sample database.</span></span>
   5. <span data-ttu-id="d3a68-179">**연결 테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-179">Click **Test Connection**.</span></span>
      
       ![][06]
   6. <span data-ttu-id="d3a68-180">Hello 연결 테스트의 hello 결과 보고 하는 hello 대화 상자에서 클릭 **확인** tooreturn toohello **연결 관리자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="d3a68-180">In hello dialog box that reports hello results of hello connection test, click **OK** tooreturn toohello **Connection Manager** dialog box.</span></span>
   7. <span data-ttu-id="d3a68-181">Hello에 **연결 관리자** 대화 상자를 클릭 **확인** tooreturn toohello **ADO.NET 연결 관리자 구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="d3a68-181">In hello **Connection Manager** dialog box, click **OK** tooreturn toohello **Configure ADO.NET Connection Manager** dialog box.</span></span>
5. <span data-ttu-id="d3a68-182">Hello에 **ADO.NET 연결 관리자 구성** 대화 상자를 클릭 **확인** tooreturn toohello **ADO.NET 원본 편집기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-182">In hello **Configure ADO.NET Connection Manager** dialog box, click **OK** tooreturn toohello **ADO.NET Source Editor**.</span></span>
6. <span data-ttu-id="d3a68-183">Hello에 **ADO.NET 원본 편집기**, hello에 **hello 뷰나 hello 테이블의 이름을** 목록, 선택 hello **Sales.SalesOrderDetail** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-183">In hello **ADO.NET Source Editor**, in hello **Name of hello table or hello view** list, select hello **Sales.SalesOrderDetail** table.</span></span>
   
    ![][07]
7. <span data-ttu-id="d3a68-184">클릭 **미리 보기** toosee hello hello의 hello 원본 테이블에에서 데이터의 처음 200 행 **쿼리 결과 미리 보기** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="d3a68-184">Click **Preview** toosee hello first 200 rows of data in hello source table in hello **Preview Query Results** dialog box.</span></span>
   
    ![][08]
8. <span data-ttu-id="d3a68-185">Hello에 **쿼리 결과 미리 보기** 대화 상자를 클릭 **닫기** tooreturn toohello **ADO.NET 원본 편집기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-185">In hello **Preview Query Results** dialog box, click **Close** tooreturn toohello **ADO.NET Source Editor**.</span></span>
9. <span data-ttu-id="d3a68-186">Hello에 **ADO.NET 원본 편집기**, 클릭 **확인** toofinish hello 데이터 원본을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-186">In hello **ADO.NET Source Editor**, click **OK** toofinish configuring hello data source.</span></span>

## <a name="step-4-connect-hello-source-adapter-toohello-destination-adapter"></a><span data-ttu-id="d3a68-187">4 단계: hello 원본 어댑터 toohello 대상 어댑터에 연결</span><span class="sxs-lookup"><span data-stu-id="d3a68-187">Step 4: Connect hello source adapter toohello destination adapter</span></span>
1. <span data-ttu-id="d3a68-188">Hello 원본 어댑터 hello 디자인 화면에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-188">Select hello source adapter on hello design surface.</span></span>
2. <span data-ttu-id="d3a68-189">Hello 원본 어댑터에서 확장 된 hello 파란색 화살표를 선택 해을 제자리에 될 때까지 toohello 대상 편집기 끕니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-189">Select hello blue arrow that extends from hello source adapter and drag it toohello destination editor until it snaps into place.</span></span>
   
    ![][10]
   
    <span data-ttu-id="d3a68-190">일반적인 SSIS 패키지는에서 다양 한 hello SSIS 도구 상자 hello 소스 및 대상 toorestructure hello, 변환 사이에서 다른 구성 요소를 사용 하 여 한 hello SSIS 데이터 흐름을 통과할 때 데이터를 정리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-190">In a typical SSIS package, you use a number of other components from hello SSIS Toolbox in between hello source and hello destination toorestructure, transform, and cleanse your data as it passes through hello SSIS data flow.</span></span> <span data-ttu-id="d3a68-191">tookeep에서는 연결 하는 가능한 한 단순한 것이 예제에서는 hello 원본 직접 toohello 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-191">tookeep this example as simple as possible, we’re connecting hello source directly toohello destination.</span></span>

## <a name="step-5-configure-hello-destination-adapter"></a><span data-ttu-id="d3a68-192">5 단계: hello 대상 어댑터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-192">Step 5: Configure hello destination adapter</span></span>
1. <span data-ttu-id="d3a68-193">Hello 대상 어댑터 tooopen hello를 두 번 클릭 **ADO.NET 대상 편집기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-193">Double-click hello destination adapter tooopen hello **ADO.NET Destination Editor**.</span></span>
   
    ![][11]
2. <span data-ttu-id="d3a68-194">Hello에 **연결 관리자** hello 탭 **ADO.NET 대상 편집기**, hello 클릭 **새로** 단추 다음 toohello **연결 관리자**목록 tooopen hello **ADO.NET 연결 관리자 구성** 대화 상자 및이 자습서는 데이터를 로드 하는 hello Azure SQL 데이터 웨어하우스 데이터베이스에 대 한 연결 설정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-194">On hello **Connection Manager** tab of hello **ADO.NET Destination Editor**, click hello **New** button next toohello **Connection manager** list tooopen hello **Configure ADO.NET Connection Manager** dialog box and create connection settings for hello Azure SQL Data Warehouse database into which this tutorial loads data.</span></span>
3. <span data-ttu-id="d3a68-195">Hello에 **ADO.NET 연결 관리자 구성** 대화 상자를 클릭 hello **새로 만들기** 단추 tooopen hello **연결 관리자** 대화 상자 하 고 새 데이터 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-195">In hello **Configure ADO.NET Connection Manager** dialog box, click hello **New** button tooopen hello **Connection Manager** dialog box and create a new data connection.</span></span>
4. <span data-ttu-id="d3a68-196">Hello에 **연결 관리자** 대화 상자에서 다음 작업 hello 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-196">In hello **Connection Manager** dialog box, do hello following things.</span></span>
   1. <span data-ttu-id="d3a68-197">에 대 한 **공급자**, 선택 hello SqlClient 데이터 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-197">For **Provider**, select hello SqlClient Data Provider.</span></span>
   2. <span data-ttu-id="d3a68-198">에 대 한 **서버 이름**, hello SQL 데이터 웨어하우스 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-198">For **Server name**, enter hello SQL Data Warehouse name.</span></span>
   3. <span data-ttu-id="d3a68-199">Hello에 **toohello 서버 로그온** 섹션에서 **사용 하 여 SQL Server 인증** 인증 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-199">In hello **Log on toohello server** section, select **Use SQL Server authentication** and enter authentication information.</span></span>
   4. <span data-ttu-id="d3a68-200">Hello에 **연결 tooa 데이터베이스** 섹션에서 기존 SQL 데이터 웨어하우스 데이터베이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-200">In hello **Connect tooa database** section, select an existing SQL Data Warehouse database.</span></span>
   5. <span data-ttu-id="d3a68-201">**연결 테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-201">Click **Test Connection**.</span></span>
   6. <span data-ttu-id="d3a68-202">Hello 연결 테스트의 hello 결과 보고 하는 hello 대화 상자에서 클릭 **확인** tooreturn toohello **연결 관리자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="d3a68-202">In hello dialog box that reports hello results of hello connection test, click **OK** tooreturn toohello **Connection Manager** dialog box.</span></span>
   7. <span data-ttu-id="d3a68-203">Hello에 **연결 관리자** 대화 상자를 클릭 **확인** tooreturn toohello **ADO.NET 연결 관리자 구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="d3a68-203">In hello **Connection Manager** dialog box, click **OK** tooreturn toohello **Configure ADO.NET Connection Manager** dialog box.</span></span>
5. <span data-ttu-id="d3a68-204">Hello에 **ADO.NET 연결 관리자 구성** 대화 상자를 클릭 **확인** tooreturn toohello **ADO.NET 대상 편집기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-204">In hello **Configure ADO.NET Connection Manager** dialog box, click **OK** tooreturn toohello **ADO.NET Destination Editor**.</span></span>
6. <span data-ttu-id="d3a68-205">Hello에 **ADO.NET 대상 편집기**, 클릭 **새로** 다음 toohello **테이블 또는 뷰를 사용 하 여** 목록 tooopen hello **Create Table** 대화 상자 toocreate hello 원본 테이블을 일치 하는 열 목록과 함께 새 대상 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-205">In hello **ADO.NET Destination Editor**, click **New** next toohello **Use a table or view** list tooopen hello **Create Table** dialog box toocreate a new destination table with a column list that matches hello source table.</span></span>
   
    ![][12a]
7. <span data-ttu-id="d3a68-206">Hello에 **Create Table** 대화 상자에서 다음 작업 hello 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-206">In hello **Create Table** dialog box, do hello following things.</span></span>
   
   1. <span data-ttu-id="d3a68-207">Hello 대상 테이블의 이름을 hello도 변경**SalesOrderDetail**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-207">Change hello name of hello destination table too**SalesOrderDetail**.</span></span>
   2. <span data-ttu-id="d3a68-208">Hello 제거 **rowguid** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-208">Remove hello **rowguid** column.</span></span> <span data-ttu-id="d3a68-209">hello **uniqueidentifier** SQL 데이터 웨어하우스에 데이터 형식이 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-209">hello **uniqueidentifier** data type is not supported in SQL Data Warehouse.</span></span>
   3. <span data-ttu-id="d3a68-210">Hello 변수의 hello 데이터 형식을 변경 **LineTotal** 열 너무**money**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-210">Change hello data type of hello **LineTotal** column too**money**.</span></span> <span data-ttu-id="d3a68-211">hello **10 진수** SQL 데이터 웨어하우스에 데이터 형식이 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-211">hello **decimal** data type is not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="d3a68-212">지원되는 데이터 형식에 대한 자세한 내용은 [테이블 만들기(Azure SQL Data Warehouse, 병렬 데이터 웨어하우스)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3a68-212">For info about supported data types, see [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].</span></span>
      
       ![][12b]
   4. <span data-ttu-id="d3a68-213">클릭 **확인** toocreate hello 테이블 및 반환 toohello **ADO.NET 대상 편집기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-213">Click **OK** toocreate hello table and return toohello **ADO.NET Destination Editor**.</span></span>
8. <span data-ttu-id="d3a68-214">Hello에 **ADO.NET 대상 편집기**선택, hello **매핑** toosee 탭 어떻게 hello 원본의 열에에서 매핑된 toocolumns hello 대상에 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-214">In hello **ADO.NET Destination Editor**, select hello **Mappings** tab toosee how columns in hello source are mapped toocolumns in hello destination.</span></span>
   
    ![][13]
9. <span data-ttu-id="d3a68-215">클릭 **확인** toofinish hello 데이터 원본을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-215">Click **OK** toofinish configuring hello data source.</span></span>

## <a name="step-6-run-hello-package-tooload-hello-data"></a><span data-ttu-id="d3a68-216">6 단계: 실행 hello 패키지 tooload hello 데이터</span><span class="sxs-lookup"><span data-stu-id="d3a68-216">Step 6: Run hello package tooload hello data</span></span>
<span data-ttu-id="d3a68-217">Hello를 클릭 하 여 패키지 실행된 hello **시작** hello 도구 모음이 나 hello 중 하나를 선택 하 여 단추 **실행** hello에 옵션 **디버그** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="d3a68-217">Run hello package by clicking hello **Start** button on hello toolbar or by selecting one of hello **Run** options on hello **Debug** menu.</span></span>

<span data-ttu-id="d3a68-218">Hello 패키지 시작 toorun 때 노란색 회전 바퀴 tooindicate 활동 뿐 아니라 hello 지금까지 처리 된 행 수는 것이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-218">As hello package begins toorun, you see yellow spinning wheels tooindicate activity as well as hello number of rows processed so far.</span></span>

![][14]

<span data-ttu-id="d3a68-219">Hello 패키지 실행이 완료 되었을 때 있습니다 녹색 확인 표시가 tooindicate 성공으로 볼 hello hello 소스 toohello 대상에서 로드 한 데이터의 행의 총 수입니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-219">When hello package has finished running, you see green check marks tooindicate success as well as hello total number of rows of data loaded from hello source toohello destination.</span></span>

![][15]

<span data-ttu-id="d3a68-220">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-220">Congratulations!</span></span> <span data-ttu-id="d3a68-221">성공적으로 Azure SQL 데이터 웨어하우스에 SQL Server Integration Services tooload 데이터를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-221">You’ve successfully used SQL Server Integration Services tooload data into Azure SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3a68-222">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d3a68-222">Next steps</span></span>
* <span data-ttu-id="d3a68-223">Hello SSIS 데이터 흐름에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="d3a68-223">Learn more about hello SSIS data flow.</span></span> <span data-ttu-id="d3a68-224">[데이터 흐름][Data Flow]에서 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-224">Start here: [Data Flow][Data Flow].</span></span>
* <span data-ttu-id="d3a68-225">자세한 내용은 어떻게 toodebug 고 hello 디자인 환경에서 패키지 권한은 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-225">Learn how toodebug and troubleshoot your packages right in hello design environment.</span></span> <span data-ttu-id="d3a68-226">[패키지 개발용 문제 해결 도구][Troubleshooting Tools for Package Development]에서 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-226">Start here: [Troubleshooting Tools for Package Development][Troubleshooting Tools for Package Development].</span></span>
* <span data-ttu-id="d3a68-227">방법을 배웁니다 toodeploy SSIS 프로젝트를 패키지 tooIntegration 서비스 서버 또는 tooanother 저장소 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-227">Learn how toodeploy your SSIS projects and packages tooIntegration Services Server or tooanother storage location.</span></span> <span data-ttu-id="d3a68-228">[프로젝트 및 패키지 배포][Deployment of Projects and Packages]에서 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3a68-228">Start here: [Deployment of Projects and Packages][Deployment of Projects and Packages].</span></span>

<!-- Image references -->
[01]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-designer-01.png
[02]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-data-flow-task-02.png
[03]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-03.png
[04]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-manager-04.png
[05]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-05.png
[06]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/test-connection-06.png
[07]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-07.png
[08]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/preview-data-08.png
[09]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/source-destination-09.png
[10]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/connect-source-destination-10.png
[11]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-destination-11.png
[12a]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-before-12a.png
[12b]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-after-12b.png
[13]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/column-mapping-13.png
[14]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-running-14.png
[15]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: https://msdn.microsoft.com/library/mt143171.aspx
[Download SQL Server Data Tools (SSDT)]: https://msdn.microsoft.com/library/mt204009.aspx
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: https://msdn.microsoft.com/library/mt203953.aspx
[Data Flow]: https://msdn.microsoft.com/library/ms140080.aspx
[Troubleshooting Tools for Package Development]: https://msdn.microsoft.com/library/ms137625.aspx
[Deployment of Projects and Packages]: https://msdn.microsoft.com/library/hh213290.aspx

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[SQL Server Evaluations]: https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016
[Visual Studio Community]: https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://msftdbprodsamples.codeplex.com/releases/view/125550
