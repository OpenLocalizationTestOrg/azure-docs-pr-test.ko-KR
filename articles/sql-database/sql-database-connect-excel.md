---
title: "aaaConnect Excel tooSQL 데이터베이스 | Microsoft Docs"
description: "Hello 클라우드에서 tooconnect Microsoft Excel tooAzure SQL 데이터베이스 하는 방법에 대해 알아봅니다. 보고 및 데이터 탐색을 위해 Excel로 데이터를 가져옵니다."
services: sql-database
keywords: "연결 toosql excel, 데이터 tooexcel 가져오기"
documentationcenter: 
author: joseidz
manager: jhubbard
editor: 
ms.assetid: 906924bc-2707-48d3-bac6-397976a0409d
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: jhubbard
ms.openlocfilehash: 0048849432023145bd1009d45b6d9b64a9c7ac3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-tooan-azure-sql-database-and-create-a-report"></a><span data-ttu-id="aa64f-105">Excel tooan Azure SQL 데이터베이스 연결 및 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="aa64f-105">Connect Excel tooan Azure SQL database and create a report</span></span>

<span data-ttu-id="aa64f-106">Hello 클라우드에서 Excel tooa SQL 데이터베이스를 연결 하 고 데이터를 가져올 테이블 및 hello 데이터베이스의 값에 따라 차트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-106">Connect Excel tooa SQL database in hello cloud and import data and create tables and charts based on values in hello database.</span></span> <span data-ttu-id="aa64f-107">데이터베이스 테이블, Excel에서는 hello 연결을 설정 하는이 자습서에서는 Excel 용 데이터 및 hello 연결 정보를 저장 하는 hello 파일을 저장 한 다음 hello에서 피벗 차트를을 데이터베이스 값 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-107">In this tutorial you will set up hello connection between Excel and a database table, save hello file that stores data and hello connection information for Excel, and then create a pivot chart from hello database values.</span></span>

<span data-ttu-id="aa64f-108">시작하기 전에 Azure에서 SQL 데이터베이스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-108">You'll need a SQL database in Azure before you get started.</span></span> <span data-ttu-id="aa64f-109">하나 없다면 참조 [첫 번째 SQL 데이터베이스를 만듭니다.](sql-database-get-started-portal.md) tooget 데이터베이스 샘플 데이터로 설정 하 고 잠시 후에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-109">If you don't have one, see [Create your first SQL database](sql-database-get-started-portal.md) tooget a database with sample data up and running in a few minutes.</span></span> <span data-ttu-id="aa64f-110">이 문서에서는 해당 문서에서 샘플 데이터를 Excel에 가져오지만 고유의 데이터에서 비슷한 단계를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-110">In this article, you'll import sample data into Excel from that article, but you can follow similar steps with your own data.</span></span>

<span data-ttu-id="aa64f-111">또한 Excel의 사본이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-111">You'll also need a copy of Excel.</span></span> <span data-ttu-id="aa64f-112">이 문서는 [Microsoft Excel 2016](https://products.office.com/)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-112">This article uses [Microsoft Excel 2016](https://products.office.com/).</span></span>

## <a name="connect-excel-tooa-sql-database-and-create-an-odc-file"></a><span data-ttu-id="aa64f-113">Excel tooa SQL 데이터베이스를 연결 하 고 odc 파일을 만들</span><span class="sxs-lookup"><span data-stu-id="aa64f-113">Connect Excel tooa SQL database and create an odc file</span></span>
1. <span data-ttu-id="aa64f-114">tooconnect Excel tooSQL 데이터베이스 Excel을 열고 새 통합 문서를 만들거나 기존 Excel 통합 문서를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-114">tooconnect Excel tooSQL database, open Excel and then create a new workbook or open an existing Excel workbook.</span></span>
2. <span data-ttu-id="aa64f-115">Hello hello 페이지 위쪽에 hello 메뉴 모음에서 클릭 **데이터**, 클릭 **기타 원본**, 클릭 하 고 **SQL Server에서**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-115">In hello menu bar at hello top of hello page click **Data**, click **From Other Sources**, and then click **From SQL Server**.</span></span>
   
   ![데이터 원본 선택: Excel tooSQL 데이터베이스를 연결 합니다.](./media/sql-database-connect-excel/excel_data_source.png)
   
   <span data-ttu-id="aa64f-117">hello 데이터 연결 마법사가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-117">hello Data Connection Wizard opens.</span></span>
3. <span data-ttu-id="aa64f-118">Hello에 **tooDatabase 서버 연결** 대화 상자에서 SQL 데이터베이스 유형 hello **서버 이름** tooconnect tooin hello 양식 표시할 <*servername* > **. database.windows.net**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-118">In hello **Connect tooDatabase Server** dialog box, type hello SQL Database **Server name** you want tooconnect tooin hello form <*servername*>**.database.windows.net**.</span></span> <span data-ttu-id="aa64f-119">예를 들어 **adworkserver.database.windows.net**입니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-119">For example, **adworkserver.database.windows.net**.</span></span>
4. <span data-ttu-id="aa64f-120">아래 **로그온 자격 증명**, 클릭 **다음 사용자 이름 및 암호 사용 하 여 hello**, 형식 hello **사용자 이름** 및 **암호** 에 설정 SQL 데이터베이스 서버를 만들 때 hello 및 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-120">Under **Log on credentials**, click **Use hello following User Name and Password**, type hello **User Name** and **Password** you set up for hello SQL Database server when you created it, and then click **Next**.</span></span>
   
   ![Hello 서버 이름 및 로그인 자격 증명을 입력 합니다.](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > <span data-ttu-id="aa64f-122">네트워크 환경에 따라 수 tooconnect 수 또는 hello SQL 데이터베이스 서버에 클라이언트 IP 주소의 트래픽을 허용 하지 않으면 hello 연결 손실 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-122">Depending on your network environment, you may not be able tooconnect or you may lose hello connection if hello SQL Database server doesn't allow traffic from your client IP address.</span></span> <span data-ttu-id="aa64f-123">Toohello 이동 [Azure 포털](https://portal.azure.com/)SQL 서버, 서버 클릭 하 여, 방화벽 설정에서 클릭을 클라이언트 IP 주소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-123">Go toohello [Azure portal](https://portal.azure.com/), click SQL servers, click your server, click firewall under settings and add your client IP address.</span></span> <span data-ttu-id="aa64f-124">참조 [tooconfigure 방화벽 설정을 어떻게](sql-database-configure-firewall-settings.md) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-124">See [How tooconfigure firewall settings](sql-database-configure-firewall-settings.md) for details.</span></span>
   > 
   > 
5. <span data-ttu-id="aa64f-125">Hello에 **데이터베이스 및 테이블 선택** 대화 상자에서 선택 hello 데이터베이스 toowork와 hello 목록에서 선택 하 고 hello 테이블이 나 뷰를 toowork 원하는 클릭 합니다 (선택한 **vGetAllCategories**), 한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-125">In hello **Select Database and Table** dialog, select hello database you want toowork with from hello list, and then click hello tables or views you want toowork with (we chose **vGetAllCategories**), and then click **Next**.</span></span>
   
    ![데이터베이스 및 테이블 선택](./media/sql-database-connect-excel/select-database-and-table.png)
   
    <span data-ttu-id="aa64f-127">hello **데이터 연결 파일 저장 및 마침** Excel에서 사용 하는 hello Office 데이터베이스 연결 (*.odc) 파일에 대 한 정보를 입력할 수 있는 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-127">hello **Save Data Connection File and Finish** dialog box opens, where you provide information about hello Office database connection (*.odc) file that Excel uses.</span></span> <span data-ttu-id="aa64f-128">Hello 기본값 그대로 두고 하거나 선택 항목을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-128">You can leave hello defaults or customize your selections.</span></span>
6. <span data-ttu-id="aa64f-129">참고 hello 하지만 hello 기본값을 그대로 두면 **파일 이름** 특히 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-129">You can leave hello defaults, but note hello **File Name** in particular.</span></span> <span data-ttu-id="aa64f-130">A **설명**, **이름**, 및 **검색 키워드** 도와주 고, 다른 사용자가 연결 하려는 기억 tooand hello 연결을 찾을 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-130">A **Description**, a **Friendly Name**, and **Search Keywords** help you and other users remember what you're connecting tooand find hello connection.</span></span> <span data-ttu-id="aa64f-131">클릭 **항상 시도 toouse이 파일 toorefresh 데이터** tooit를 연결 하 고 클릭 하는 경우 업데이트할 수 있습니다 hello odc 파일에 저장 된 연결 정보를 원하는 경우 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-131">Click **Always attempt toouse this file toorefresh data** if you want connection information stored in hello odc file so it can update when you connect tooit, and then click **Finish**.</span></span>
   
    ![odc 파일 저장](./media/sql-database-connect-excel/save-odc-file.png)
   
    <span data-ttu-id="aa64f-133">hello **데이터를 가져올** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-133">hello **Import data** dialog box appears.</span></span>

## <a name="import-hello-data-into-excel-and-create-a-pivot-chart"></a><span data-ttu-id="aa64f-134">Excel로 hello 데이터 가져오기 및 피벗 차트 만들기</span><span class="sxs-lookup"><span data-stu-id="aa64f-134">Import hello data into Excel and create a pivot chart</span></span>
<span data-ttu-id="aa64f-135">Hello 연결 및 데이터 및 연결 정보로 만든된 hello 파일 설정 했으므로 tooimport hello 데이터를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-135">Now that you've established hello connection and created hello file with data and connection information, you're reading tooimport hello data.</span></span>

1. <span data-ttu-id="aa64f-136">Hello에 **데이터 가져오기** 대화 상자에서 hello 워크시트에서 데이터를 제공할 원하는 hello 옵션을 클릭 한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-136">In hello **Import Data** dialog, click hello option you want for presenting your data in hello worksheet and then click **OK**.</span></span> <span data-ttu-id="aa64f-137">**PivotChart**를 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-137">We chose **PivotChart**.</span></span> <span data-ttu-id="aa64f-138">Toocreate 선택할 수도 있습니다는 **새 워크시트** 또는 너무**이 데이터 tooa 데이터 모델 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-138">You can also choose toocreate a **New worksheet** or too**Add this data tooa Data Model**.</span></span> <span data-ttu-id="aa64f-139">데이터 모델에 대한 자세한 내용은 [Excel에서 데이터 모델 만들기](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aa64f-139">For more information on Data Models, see [Create a data model in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span></span> <span data-ttu-id="aa64f-140">클릭 **속성** hello 이전 단계와 toochoose 새로 고침 옵션을 hello 데이터에서 만든 hello odc 파일에 대 한 tooexplore 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-140">Click **Properties** tooexplore information about hello odc file you created in hello previous step and toochoose options for refreshing hello data.</span></span>
   
    ![Excel에서 데이터에 대 한 hello 형식 선택](./media/sql-database-connect-excel/import-data.png)
   
    <span data-ttu-id="aa64f-142">이제 hello 워크시트에 빈 피벗 테이블 및 차트입니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-142">hello worksheet now has an empty pivot table and chart.</span></span>
2. <span data-ttu-id="aa64f-143">아래 **피벗 테이블 필드**, tooview 원하는 필드를 hello 모든 hello에 대 한 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-143">Under **PivotTable Fields**, select all hello check-boxes for hello fields you want tooview.</span></span>
   
    ![데이터베이스 보고서를 구성합니다.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> <span data-ttu-id="aa64f-145">다른 Excel 통합 문서 및 워크시트 toohello 데이터베이스 tooconnect 원하는 클릭 **데이터**, 클릭 **연결**, 클릭 **추가**, 만든 hello 연결을 선택 hello 목록에서 **열려**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-145">If you want tooconnect other Excel workbooks and worksheets toohello database, click **Data**, click **Connections**, click **Add**, choose hello connection you created from hello list, and then click **Open**.</span></span>
> <span data-ttu-id="aa64f-146">![다른 통합 문서에서 연결 열기](./media/sql-database-connect-excel/open-from-another-workbook.png)</span><span class="sxs-lookup"><span data-stu-id="aa64f-146">![Open a connection from another workbook](./media/sql-database-connect-excel/open-from-another-workbook.png)</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="aa64f-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aa64f-147">Next steps</span></span>
* <span data-ttu-id="aa64f-148">너무 방법에 대해 알아봅니다[tooSQL 데이터베이스 SQL Server Management Studio를 사용 하 여 연결](sql-database-connect-query-ssms.md) 고급 쿼리 및 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-148">Learn how too[Connect tooSQL Database with SQL Server Management Studio](sql-database-connect-query-ssms.md) for advanced querying and analysis.</span></span>
* <span data-ttu-id="aa64f-149">Hello 이점에 대 한 자세한 내용은 [탄력적 풀](sql-database-elastic-pool.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-149">Learn about hello benefits of [elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="aa64f-150">너무 방법에 대해 알아봅니다[tooSQL 데이터베이스 hello 백 엔드에 연결 하는 웹 응용 프로그램 만들기](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa64f-150">Learn how too[create a web application that connects tooSQL Database on hello back-end](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span>

