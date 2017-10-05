---
title: "SQL Server에서 Azure SQL Data Warehouse로 데이터 로드(SSIS) | Microsoft Docs"
description: "SSIS(SQL Server Integration Services) 패키지를 만들어 다양한 데이터 원본에서 SQL 데이터 웨어하우스로 데이터를 이동하는 방법을 보여줍니다."
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
ms.openlocfilehash: 6c9cebdd715b6997d0633bc725a3945ba9e0c357
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-ssis"></a><span data-ttu-id="15ce6-103">SQL Server에서 Azure SQL 데이터 웨어하우스로 데이터 로드(SSIS)</span><span class="sxs-lookup"><span data-stu-id="15ce6-103">Load data from SQL Server into Azure SQL Data Warehouse (SSIS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="15ce6-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="15ce6-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="15ce6-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="15ce6-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="15ce6-106">bcp</span><span class="sxs-lookup"><span data-stu-id="15ce6-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="15ce6-107">SQL Server Integration Services(SSIS) 패키지를 사용하여 SQL Server에서 Azure SQL 데이터 웨어하우스로 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="15ce6-107">Create a SQL Server Integration Services (SSIS) package to load data from SQL Server into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="15ce6-108">또한 SSIS 데이터 흐름을 통과하는 데이터를 재구성, 변환 및 정리할 수 있습니다(선택 사항).</span><span class="sxs-lookup"><span data-stu-id="15ce6-108">You can optionally restructure, transform, and cleanse the data as it passes through the SSIS data flow.</span></span>

<span data-ttu-id="15ce6-109">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-109">In this tutorial, you will:</span></span>

* <span data-ttu-id="15ce6-110">Visual Studio에서 새 Integration Services 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-110">Create a new Integration Services project in Visual Studio.</span></span>
* <span data-ttu-id="15ce6-111">SQL Server(원본)를 비롯한 데이터 원본과 SQL 데이터 웨어하우스(대상)에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-111">Connect to data sources, including SQL Server (as a source) and SQL Data Warehouse (as a destination).</span></span>
* <span data-ttu-id="15ce6-112">원본에서 대상으로 데이터를 로드하는 SSIS 패키지를 디자인합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-112">Design an SSIS package that loads data from the source into the destination.</span></span>
* <span data-ttu-id="15ce6-113">SSIS 패키지를 실행하여 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-113">Run the SSIS package to load the data.</span></span>

<span data-ttu-id="15ce6-114">이 자습서는 데이터 원본으로 SQL Server를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-114">This tutorial uses SQL Server as the data source.</span></span> <span data-ttu-id="15ce6-115">SQL Server는 온-프레미스 또는 Azure 가상 컴퓨터에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-115">SQL Server could be running on premises or in an Azure virtual machine.</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="15ce6-116">기본 개념</span><span class="sxs-lookup"><span data-stu-id="15ce6-116">Basic concepts</span></span>
<span data-ttu-id="15ce6-117">패키지는 SSIS의 작업 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-117">The package is the unit of work in SSIS.</span></span> <span data-ttu-id="15ce6-118">관련 패키지는 프로젝트로 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-118">Related packages are grouped in projects.</span></span> <span data-ttu-id="15ce6-119">Visual Studio에서 SQL Server Data Tools를 사용하여 프로젝트를 만들고 패키지를 디자인합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-119">You create projects and design packages in Visual Studio with SQL Server Data Tools.</span></span> <span data-ttu-id="15ce6-120">디자인 프로세스는 도구 상자에서 디자인 화면으로 구성 요소를 끌어 놓고 서로 연결한 다음 속성을 설정하는 시각적 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-120">The design process is a visual process in which you drag and drop components from the Toolbox to the design surface, connect them, and set their properties.</span></span> <span data-ttu-id="15ce6-121">패키지를 마친 후에 포괄적 관리, 모니터링, 보안을 위해 SQL Server에 배포할 수 있습니다(선택 사항).</span><span class="sxs-lookup"><span data-stu-id="15ce6-121">After you finish your package, you can optionally deploy it to SQL Server for comprehensive management, monitoring, and security.</span></span>

## <a name="options-for-loading-data-with-ssis"></a><span data-ttu-id="15ce6-122">SSIS를 이용하여 데이터 로드 시 선택 사항</span><span class="sxs-lookup"><span data-stu-id="15ce6-122">Options for loading data with SSIS</span></span>
<span data-ttu-id="15ce6-123">SSIS(SQL Server Integration Services)는 SQL 데이터 웨어하우스에 연결하고 데이터를 로드하는 다양한 옵션을 제공하는 유연한 도구 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-123">SQL Server Integration Services (SSIS) is a flexible set of tools that provides a variety of options for connecting to, and loading data into, SQL Data Warehouse.</span></span>

1. <span data-ttu-id="15ce6-124">ADO NET 대상을 사용하여 SQL 데이터 웨어하우스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-124">Use an ADO NET Destination to connect to SQL Data Warehouse.</span></span> <span data-ttu-id="15ce6-125">이 자습서는 구성 옵션이 가장 적은 ADO NET 대상을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-125">This tutorial uses an ADO NET Destination because it has the fewest configuration options.</span></span>
2. <span data-ttu-id="15ce6-126">OLE DB 대상을 사용하여 SQL 데이터 웨어하우스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-126">Use an OLE DB Destination to connect to SQL Data Warehouse.</span></span> <span data-ttu-id="15ce6-127">이 옵션은 ADO NET 대상보다 약간 뛰어난 성능을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-127">This option may provide slightly better performance than the ADO NET Destination.</span></span>
3. <span data-ttu-id="15ce6-128">Azure Blob 업로드 작업을 사용하여 Azure Blob 저장소의 데이터를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-128">Use the Azure Blob Upload Task to stage the data in Azure Blob Storage.</span></span> <span data-ttu-id="15ce6-129">그런 다음 SSIS 실행 SQL 작업을 사용하여 SQL 데이터 웨어하우스로 데이터를 로드하는 Polybase 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-129">Then use the SSIS Execute SQL task to launch a Polybase script that loads the data into SQL Data Warehouse.</span></span> <span data-ttu-id="15ce6-130">이 옵션은 여기에 나열된 세 가지 옵션에 대해 최고의 성능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-130">This option provides the best performance of the three options listed here.</span></span> <span data-ttu-id="15ce6-131">Azure Blob 업로드 작업을 가져오려면 [Azure용 Microsoft SQL Server 2016 Integration Services 기능 팩][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]을 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-131">To get the Azure Blob Upload task, download the [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure].</span></span> <span data-ttu-id="15ce6-132">Polybase에 대한 자세한 내용은 [PolyBase 가이드][PolyBase Guide]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15ce6-132">To learn more about Polybase, see [PolyBase Guide][PolyBase Guide].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="15ce6-133">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="15ce6-133">Before you start</span></span>
<span data-ttu-id="15ce6-134">이 자습서를 단계별로 실행하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-134">To step through this tutorial, you need:</span></span>

1. <span data-ttu-id="15ce6-135">**SSIS(SQL Server Integration Services)**.</span><span class="sxs-lookup"><span data-stu-id="15ce6-135">**SQL Server Integration Services (SSIS)**.</span></span> <span data-ttu-id="15ce6-136">SSIS는 SQL Server의 구성 요소이며 평가판 버전 또는 라이선스 버전의 SQL Server가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-136">SSIS is a component of SQL Server and requires an evaluation version or a licensed version of SQL Server.</span></span> <span data-ttu-id="15ce6-137">평가판 버전의 SQL Server 2016 Preview를 다운로드하려면 [SQL Server 평가][SQL Server Evaluations]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15ce6-137">To get an evaluation version of SQL Server 2016 Preview, see [SQL Server Evaluations][SQL Server Evaluations].</span></span>
2. <span data-ttu-id="15ce6-138">**Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="15ce6-138">**Visual Studio**.</span></span> <span data-ttu-id="15ce6-139">무료 Visual Studio Community Edition을 다운로드하려면 [Visual Studio Community][Visual Studio Community]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15ce6-139">To get the free Visual Studio Community Edition, see [Visual Studio Community][Visual Studio Community].</span></span>
3. <span data-ttu-id="15ce6-140">**Visual Studio용 SSDT(SQL Server Data Tools)**.</span><span class="sxs-lookup"><span data-stu-id="15ce6-140">**SQL Server Data Tools for Visual Studio (SSDT)**.</span></span> <span data-ttu-id="15ce6-141">Visual Studio용 SQL Server Data Tools를 다운로드하려면 [SSDT(SQL Server Data Tools) 다운로드][Download SQL Server Data Tools (SSDT)]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15ce6-141">To get SQL Server Data Tools for Visual Studio, see [Download SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].</span></span>
4. <span data-ttu-id="15ce6-142">**예제 데이터**.</span><span class="sxs-lookup"><span data-stu-id="15ce6-142">**Sample data**.</span></span> <span data-ttu-id="15ce6-143">이 자습서는 SQL 데이터 웨어하우스에 로드할 원본 데이터로 AdventureWorks 예제 데이터베이스의 SQL Server에 저장된 예제 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-143">This tutorial uses sample data stored in SQL Server in the AdventureWorks sample database as the source data to be loaded into SQL Data Warehouse.</span></span> <span data-ttu-id="15ce6-144">AdventureWorks 예제 데이터베이스를 다운로드하려면 [AdventureWorks 2014 예제 데이터베이스][AdventureWorks 2014 Sample Databases]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15ce6-144">To get the AdventureWorks sample database, see [AdventureWorks 2014 Sample Databases][AdventureWorks 2014 Sample Databases].</span></span>
5. <span data-ttu-id="15ce6-145">**SQL 데이터 웨어하우스 데이터베이스 및 사용 권한**.</span><span class="sxs-lookup"><span data-stu-id="15ce6-145">**A SQL Data Warehouse database and permissions**.</span></span> <span data-ttu-id="15ce6-146">이 자습서는 SQL 데이터 웨어하우스 인스턴스로 연결한 다음 여기로 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-146">This tutorial connects to a SQL Data Warehouse instance and loads data into it.</span></span> <span data-ttu-id="15ce6-147">테이블을 만들고 데이터를 로드할 수 있는 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-147">You have to have permissions to create a table and to load data.</span></span>
6. <span data-ttu-id="15ce6-148">**방화벽 규칙**.</span><span class="sxs-lookup"><span data-stu-id="15ce6-148">**A firewall rule**.</span></span> <span data-ttu-id="15ce6-149">SQL 데이터 웨어하우스로 데이터를 로드하기 전에 로컬 컴퓨터의 IP 주소를 사용하여 SQL 데이터 웨어하우스에 방화벽 규칙을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-149">You have to create a firewall rule on SQL Data Warehouse with the IP address of your local computer before you can upload data to the SQL Data Warehouse.</span></span>

## <a name="step-1-create-a-new-integration-services-project"></a><span data-ttu-id="15ce6-150">1단계: 새 Integration Services 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="15ce6-150">Step 1: Create a new Integration Services project</span></span>
1. <span data-ttu-id="15ce6-151">Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-151">Launch Visual Studio.</span></span>
2. <span data-ttu-id="15ce6-152">**파일** 메뉴에서 **새로 만들기 | 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-152">On the **File** menu, select **New | Project**.</span></span>
3. <span data-ttu-id="15ce6-153">**설치됨 | 템플릿 | 비즈니스 인텔리전스 | Integration Services** 프로젝트 형식으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-153">Navigate to the **Installed | Templates | Business Intelligence | Integration Services** project types.</span></span>
4. <span data-ttu-id="15ce6-154">**Integration Services 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-154">Select **Integration Services Project**.</span></span> <span data-ttu-id="15ce6-155">**이름** 및 **위치** 값을 입력한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-155">Provide values for **Name** and **Location**, and then select **OK**.</span></span>

<span data-ttu-id="15ce6-156">Visual Studio가 열리고 새 SSIS(Integration Services) 프로젝트가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-156">Visual Studio opens and creates a new Integration Services (SSIS) project.</span></span> <span data-ttu-id="15ce6-157">그런 다음 Visual Studio의 프로젝트에 새 SSIS 패키지(Package.dtsx)의 디자이너가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-157">Then Visual Studio opens the designer for the single new SSIS package (Package.dtsx) in the project.</span></span> <span data-ttu-id="15ce6-158">다음과 같은 화면 영역이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-158">You see the following screen areas:</span></span>

* <span data-ttu-id="15ce6-159">왼쪽은 SSIS 구성 요소의 **도구 상자** 입니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-159">On the left, the **Toolbox** of SSIS components.</span></span>
* <span data-ttu-id="15ce6-160">가운데는 여러 탭이 포함된 디자인 화면입니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-160">In the middle, the design surface, with multiple tabs.</span></span> <span data-ttu-id="15ce6-161">최소한 **제어 흐름**과 **데이터 흐름** 탭을 사용하는 경우가 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-161">You typically use at least the **Control Flow** and the **Data Flow** tabs.</span></span>
* <span data-ttu-id="15ce6-162">오른쪽은 **솔루션 탐색기**와 **속성** 창입니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-162">On the right, the **Solution Explorer** and the **Properties** panes.</span></span>
  
    ![][01]

## <a name="step-2-create-the-basic-data-flow"></a><span data-ttu-id="15ce6-163">2단계: 기본 데이터 흐름 만들기</span><span class="sxs-lookup"><span data-stu-id="15ce6-163">Step 2: Create the basic data flow</span></span>
1. <span data-ttu-id="15ce6-164">도구 상자의 데이터 흐름 작업을 ( **제어 흐름** 탭의) 디자인 화면으로 끌어 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-164">Drag a Data Flow Task from the Toolbox to the center of the design surface (on the **Control Flow** tab).</span></span>
   
    ![][02]
2. <span data-ttu-id="15ce6-165">데이터 흐름 작업을 두 번 클릭하여 데이터 흐름 탭으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-165">Double-click the Data Flow Task to switch to the Data Flow tab.</span></span>
3. <span data-ttu-id="15ce6-166">도구 상자의 기타 원본 목록에서 ADO.NET 원본을 디자인 화면으로 끌어 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-166">From the Other Sources list in the Toolbox, drag an ADO.NET Source to the design surface.</span></span> <span data-ttu-id="15ce6-167">아직 원본 어댑터가 선택된 상태에서 **속성** 창에서 이름을 **SQL Server 원본**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-167">With the source adapter still selected, change its name to **SQL Server source** in the **Properties** pane.</span></span>
4. <span data-ttu-id="15ce6-168">도구 상자의 기타 대상 목록에서 ADO.NET 대상을 ADO.NET 원본의 디자인 화면으로 끌어 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-168">From the Other Destinations list in the Toolbox, drag an ADO.NET Destination to the design surface under the ADO.NET Source.</span></span> <span data-ttu-id="15ce6-169">아직 대상 어댑터가 선택된 상태에서 **속성** 창에서 이름을 **SQL DW 대상**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-169">With the destination adapter still selected, change its name to **SQL DW destination** in the **Properties** pane.</span></span>
   
    ![][09]

## <a name="step-3-configure-the-source-adapter"></a><span data-ttu-id="15ce6-170">3단계: 원본 어댑터 구성</span><span class="sxs-lookup"><span data-stu-id="15ce6-170">Step 3: Configure the source adapter</span></span>
1. <span data-ttu-id="15ce6-171">원본 어댑터를 두 번 클릭하여 **ADO.NET 원본 편집기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-171">Double-click the source adapter to open the **ADO.NET Source Editor**.</span></span>
   
    ![][03]
2. <span data-ttu-id="15ce6-172">**ADO.NET 원본 편집기**의 **연결 관리자** 탭에서 **ADO.NET 연결 관리자** 목록 옆에 있는 **새로 만들기** 단추를 클릭하여 **ADO.NET 연결 관리자 구성** 대화 상자를 열고 이 자습서에서 데이터를 로드하는 원본 SQL Server 데이터베이스의 연결 설정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-172">On the **Connection Manager** tab of the **ADO.NET Source Editor**, click the **New** button next to the **ADO.NET connection manager** list to open the **Configure ADO.NET Connection Manager** dialog box and create connection settings for the SQL Server database from which this tutorial loads data.</span></span>
   
    ![][04]
3. <span data-ttu-id="15ce6-173">**ADO.NET 연결 관리자 구성** 대화 상자에서 **새로 만들기** 단추를 클릭하여 **연결 관리자** 대화 상자를 열고 새 데이터 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-173">In the **Configure ADO.NET Connection Manager** dialog box, click the **New** button to open the **Connection Manager** dialog box and create a new data connection.</span></span>
   
    ![][05]
4. <span data-ttu-id="15ce6-174">**연결 관리자** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-174">In the **Connection Manager** dialog box, do the following things.</span></span>
   
   1. <span data-ttu-id="15ce6-175">**공급자**에 대해 SqlClient 데이터 공급자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-175">For **Provider**, select the SqlClient Data Provider.</span></span>
   2. <span data-ttu-id="15ce6-176">**서버 이름**에 SQL Server 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-176">For **Server name**, enter the SQL Server name.</span></span>
   3. <span data-ttu-id="15ce6-177">**서버에 로그온** 섹션에서 인증 정보를 선택하거나 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-177">In the **Log on to the server** section, select or enter authentication information.</span></span>
   4. <span data-ttu-id="15ce6-178">**데이터베이스에 연결** 섹션에서 AdventureWorks 예제 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-178">In the **Connect to a database** section, select the AdventureWorks sample database.</span></span>
   5. <span data-ttu-id="15ce6-179">**연결 테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-179">Click **Test Connection**.</span></span>
      
       ![][06]
   6. <span data-ttu-id="15ce6-180">연결 테스트 결과를 보고하는 대화 상자에서 **확인**을 클릭하여 **연결 관리자** 대화 상자로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-180">In the dialog box that reports the results of the connection test, click **OK** to return to the **Connection Manager** dialog box.</span></span>
   7. <span data-ttu-id="15ce6-181">**연결 관리자** 대화 상자에서 **확인**을 클릭하여 **ADO.NET 연결 관리자 구성** 대화 상자로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-181">In the **Connection Manager** dialog box, click **OK** to return to the **Configure ADO.NET Connection Manager** dialog box.</span></span>
5. <span data-ttu-id="15ce6-182">**ADO.NET 연결 관리자 구성** 대화 상자에서 **확인**을 클릭하여 **ADO.NET 원본 편집기**로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-182">In the **Configure ADO.NET Connection Manager** dialog box, click **OK** to return to the **ADO.NET Source Editor**.</span></span>
6. <span data-ttu-id="15ce6-183">**ADO.NET 원본 편집기**의 **테이블 또는 뷰 이름** 목록에서 **Sales.SalesOrderDetail** 테이블을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-183">In the **ADO.NET Source Editor**, in the **Name of the table or the view** list, select the **Sales.SalesOrderDetail** table.</span></span>
   
    ![][07]
7. <span data-ttu-id="15ce6-184">원본 테이블의 첫 번째 200개 데이터 행을 **쿼리 결과 미리 보기** 대화 상자로 보려면 **미리 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-184">Click **Preview** to see the first 200 rows of data in the source table in the **Preview Query Results** dialog box.</span></span>
   
    ![][08]
8. <span data-ttu-id="15ce6-185">**쿼리 결과 미리 보기** 대화 상자에서 **닫기**를 클릭하여 **ADO.NET 원본 편집기**로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-185">In the **Preview Query Results** dialog box, click **Close** to return to the **ADO.NET Source Editor**.</span></span>
9. <span data-ttu-id="15ce6-186">**ADO.NET 원본 편집기**에서 **확인**을 클릭하여 데이터 원본 구성을 마칩니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-186">In the **ADO.NET Source Editor**, click **OK** to finish configuring the data source.</span></span>

## <a name="step-4-connect-the-source-adapter-to-the-destination-adapter"></a><span data-ttu-id="15ce6-187">4단계: 대상 어댑터에 원본 어댑터 연결</span><span class="sxs-lookup"><span data-stu-id="15ce6-187">Step 4: Connect the source adapter to the destination adapter</span></span>
1. <span data-ttu-id="15ce6-188">디자인 화면에서 원본 어댑터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-188">Select the source adapter on the design surface.</span></span>
2. <span data-ttu-id="15ce6-189">원본 어댑터에서 나오는 파란색 화살표를 선택하고 대상 편집기에 맞춰질 때까지 끌어 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-189">Select the blue arrow that extends from the source adapter and drag it to the destination editor until it snaps into place.</span></span>
   
    ![][10]
   
    <span data-ttu-id="15ce6-190">일반 SSIS 패키지에서는 원본과 대상 간 SSIS 도구 상자의 다양한 구성 요소를 사용하여 SSIS 데이터 흐름을 통과하는 데이터를 재구성, 변환, 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-190">In a typical SSIS package, you use a number of other components from the SSIS Toolbox in between the source and the destination to restructure, transform, and cleanse your data as it passes through the SSIS data flow.</span></span> <span data-ttu-id="15ce6-191">이 예제는 가능한 간단히 유지하기 위해 원본을 대상에 직접 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-191">To keep this example as simple as possible, we’re connecting the source directly to the destination.</span></span>

## <a name="step-5-configure-the-destination-adapter"></a><span data-ttu-id="15ce6-192">5단계: 대상 어댑터 구성</span><span class="sxs-lookup"><span data-stu-id="15ce6-192">Step 5: Configure the destination adapter</span></span>
1. <span data-ttu-id="15ce6-193">대상 어댑터를 두 번 클릭하여 **ADO.NET 대상 편집기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-193">Double-click the destination adapter to open the **ADO.NET Destination Editor**.</span></span>
   
    ![][11]
2. <span data-ttu-id="15ce6-194">**ADO.NET 원본 편집기**의 **연결 관리자** 탭에서 **연결 관리자** 목록 옆에 있는 **새로 만들기** 단추를 클릭하여 **ADO.NET 연결 관리자 구성** 대화 상자를 열고 이 자습서에서 데이터를 로드하는 대상 Azure SQL Data Warehouse 데이터베이스의 연결 설정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-194">On the **Connection Manager** tab of the **ADO.NET Destination Editor**, click the **New** button next to the **Connection manager** list to open the **Configure ADO.NET Connection Manager** dialog box and create connection settings for the Azure SQL Data Warehouse database into which this tutorial loads data.</span></span>
3. <span data-ttu-id="15ce6-195">**ADO.NET 연결 관리자 구성** 대화 상자에서 **새로 만들기** 단추를 클릭하여 **연결 관리자** 대화 상자를 열고 새 데이터 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-195">In the **Configure ADO.NET Connection Manager** dialog box, click the **New** button to open the **Connection Manager** dialog box and create a new data connection.</span></span>
4. <span data-ttu-id="15ce6-196">**연결 관리자** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-196">In the **Connection Manager** dialog box, do the following things.</span></span>
   1. <span data-ttu-id="15ce6-197">**공급자**에 대해 SqlClient 데이터 공급자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-197">For **Provider**, select the SqlClient Data Provider.</span></span>
   2. <span data-ttu-id="15ce6-198">**서버 이름**에 SQL 데이터 웨어하우스 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-198">For **Server name**, enter the SQL Data Warehouse name.</span></span>
   3. <span data-ttu-id="15ce6-199">**서버에 로그온** 섹션에서 **SQL Server 인증 사용**을 선택하고 인증 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-199">In the **Log on to the server** section, select **Use SQL Server authentication** and enter authentication information.</span></span>
   4. <span data-ttu-id="15ce6-200">**데이터베이스에 연결** 섹션에서 기존 SQL 데이터 웨어하우스 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-200">In the **Connect to a database** section, select an existing SQL Data Warehouse database.</span></span>
   5. <span data-ttu-id="15ce6-201">**연결 테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-201">Click **Test Connection**.</span></span>
   6. <span data-ttu-id="15ce6-202">연결 테스트 결과를 보고하는 대화 상자에서 **확인**을 클릭하여 **연결 관리자** 대화 상자로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-202">In the dialog box that reports the results of the connection test, click **OK** to return to the **Connection Manager** dialog box.</span></span>
   7. <span data-ttu-id="15ce6-203">**연결 관리자** 대화 상자에서 **확인**을 클릭하여 **ADO.NET 연결 관리자 구성** 대화 상자로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-203">In the **Connection Manager** dialog box, click **OK** to return to the **Configure ADO.NET Connection Manager** dialog box.</span></span>
5. <span data-ttu-id="15ce6-204">**ADO.NET 연결 관리자 구성** 대화 상자에서 **확인**을 클릭하여 **ADO.NET 대상 편집기**로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-204">In the **Configure ADO.NET Connection Manager** dialog box, click **OK** to return to the **ADO.NET Destination Editor**.</span></span>
6. <span data-ttu-id="15ce6-205">**ADO.NET 대상 편집기**에서 **테이블 또는 뷰 사용** 목록 옆에 있는 **새로 만들기**를 클릭하여 **테이블 만들기** 대화 상자를 열고 원본 테이블과 일치하는 열 목록이 포함된 새 대상 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-205">In the **ADO.NET Destination Editor**, click **New** next to the **Use a table or view** list to open the **Create Table** dialog box to create a new destination table with a column list that matches the source table.</span></span>
   
    ![][12a]
7. <span data-ttu-id="15ce6-206">**테이블 만들기** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-206">In the **Create Table** dialog box, do the following things.</span></span>
   
   1. <span data-ttu-id="15ce6-207">대상 테이블의 이름을 **SalesOrderDetail**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-207">Change the name of the destination table to **SalesOrderDetail**.</span></span>
   2. <span data-ttu-id="15ce6-208">**rowguid** 열을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-208">Remove the **rowguid** column.</span></span> <span data-ttu-id="15ce6-209">SQL 데이터 웨어하우스에는 **uniqueidentifier** 데이터 형식이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-209">The **uniqueidentifier** data type is not supported in SQL Data Warehouse.</span></span>
   3. <span data-ttu-id="15ce6-210">**LineTotal** 열의 데이터 형식을 **money**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-210">Change the data type of the **LineTotal** column to **money**.</span></span> <span data-ttu-id="15ce6-211">SQL 데이터 웨어하우스에는 **decimal** 데이터 형식이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-211">The **decimal** data type is not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="15ce6-212">지원되는 데이터 형식에 대한 자세한 내용은 [테이블 만들기(Azure SQL Data Warehouse, 병렬 데이터 웨어하우스)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15ce6-212">For info about supported data types, see [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].</span></span>
      
       ![][12b]
   4. <span data-ttu-id="15ce6-213">**확인**을 클릭하여 테이블을 만들고 **ADO.NET 대상 편집기**로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-213">Click **OK** to create the table and return to the **ADO.NET Destination Editor**.</span></span>
8. <span data-ttu-id="15ce6-214">**ADO.NET 대상 편집기**에서 **매핑** 탭을 선택하여 원본의 열이 대상의 열과 어떻게 매핑되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-214">In the **ADO.NET Destination Editor**, select the **Mappings** tab to see how columns in the source are mapped to columns in the destination.</span></span>
   
    ![][13]
9. <span data-ttu-id="15ce6-215">**확인** 을 클릭하여 데이터 원본 구성을 마칩니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-215">Click **OK** to finish configuring the data source.</span></span>

## <a name="step-6-run-the-package-to-load-the-data"></a><span data-ttu-id="15ce6-216">6단계: 패키지를 실행하여 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="15ce6-216">Step 6: Run the package to load the data</span></span>
<span data-ttu-id="15ce6-217">도구 모음의 **시작** 단추를 클릭하거나 **디버그** 메뉴의 **실행** 옵션 중 하나를 선택하여 패키지를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-217">Run the package by clicking the **Start** button on the toolbar or by selecting one of the **Run** options on the **Debug** menu.</span></span>

<span data-ttu-id="15ce6-218">패키지가 실행되기 시작하면 작업을 나타내는 노란색 회전 바퀴와 지금까지 처리된 행 수가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-218">As the package begins to run, you see yellow spinning wheels to indicate activity as well as the number of rows processed so far.</span></span>

![][14]

<span data-ttu-id="15ce6-219">패키지에서 실행을 완료하면 성공을 나타내는 녹색 확인 표시와 원본에서 대상으로 로드된 총 데이터 행 수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-219">When the package has finished running, you see green check marks to indicate success as well as the total number of rows of data loaded from the source to the destination.</span></span>

![][15]

<span data-ttu-id="15ce6-220">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-220">Congratulations!</span></span> <span data-ttu-id="15ce6-221">SQL Server Integration Services를 사용하여 Azure SQL 데이터 웨어하우스로 데이터를 성공적으로 로드했습니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-221">You’ve successfully used SQL Server Integration Services to load data into Azure SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15ce6-222">다음 단계</span><span class="sxs-lookup"><span data-stu-id="15ce6-222">Next steps</span></span>
* <span data-ttu-id="15ce6-223">SSIS 데이터 흐름에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="15ce6-223">Learn more about the SSIS data flow.</span></span> <span data-ttu-id="15ce6-224">[데이터 흐름][Data Flow]에서 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-224">Start here: [Data Flow][Data Flow].</span></span>
* <span data-ttu-id="15ce6-225">디자인 환경에서 바로 패키지를 디버그하고 문제를 해결하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="15ce6-225">Learn how to debug and troubleshoot your packages right in the design environment.</span></span> <span data-ttu-id="15ce6-226">[패키지 개발용 문제 해결 도구][Troubleshooting Tools for Package Development]에서 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-226">Start here: [Troubleshooting Tools for Package Development][Troubleshooting Tools for Package Development].</span></span>
* <span data-ttu-id="15ce6-227">SSIS 프로젝트와 패키지를 Integration Services 서버 또는 다른 저장소 위치에 배포하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="15ce6-227">Learn how to deploy your SSIS projects and packages to Integration Services Server or to another storage location.</span></span> <span data-ttu-id="15ce6-228">[프로젝트 및 패키지 배포][Deployment of Projects and Packages]에서 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ce6-228">Start here: [Deployment of Projects and Packages][Deployment of Projects and Packages].</span></span>

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
