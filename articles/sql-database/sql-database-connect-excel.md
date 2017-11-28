---
title: "SQL Database에 Excel 연결 | Microsoft Docs"
description: "Microsoft Excel을 클라우드의 Azure SQL 데이터베이스에 연결하는 방법을 알아봅니다. 보고 및 데이터 탐색을 위해 Excel로 데이터를 가져옵니다."
services: sql-database
keywords: "SQL에 Excel 연결, Excel로 데이터 가져오기"
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
ms.openlocfilehash: 97344d7c0be38b3092a3224074d486b5bb984176
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-excel-to-an-azure-sql-database-and-create-a-report"></a><span data-ttu-id="0823a-105">Azure SQL 데이터베이스에 Excel 연결 및 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="0823a-105">Connect Excel to an Azure SQL database and create a report</span></span>

<span data-ttu-id="0823a-106">클라우드에서 SQL Database에 Excel을 연결하여 데이터를 가져오고 데이터베이스의 값을 기준으로 테이블 및 차트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-106">Connect Excel to a SQL database in the cloud and import data and create tables and charts based on values in the database.</span></span> <span data-ttu-id="0823a-107">이 자습서에서는 Excel과 데이터베이스 테이블 간의 연결을 설정하고 Excel에 대한 데이터 및 연결 정보가 있는 파일을 저장한 후 데이터베이스 값에서 피벗 차트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-107">In this tutorial you will set up the connection between Excel and a database table, save the file that stores data and the connection information for Excel, and then create a pivot chart from the database values.</span></span>

<span data-ttu-id="0823a-108">시작하기 전에 Azure에서 SQL 데이터베이스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-108">You'll need a SQL database in Azure before you get started.</span></span> <span data-ttu-id="0823a-109">SQL 데이터베이스가 없다면 [첫 번째 SQL 데이터베이스 만들기](sql-database-get-started-portal.md) 를 참조하여 몇 분 내에 샘플 데이터와 함께 실행되는 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-109">If you don't have one, see [Create your first SQL database](sql-database-get-started-portal.md) to get a database with sample data up and running in a few minutes.</span></span> <span data-ttu-id="0823a-110">이 문서에서는 해당 문서에서 샘플 데이터를 Excel에 가져오지만 고유의 데이터에서 비슷한 단계를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-110">In this article, you'll import sample data into Excel from that article, but you can follow similar steps with your own data.</span></span>

<span data-ttu-id="0823a-111">또한 Excel의 사본이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-111">You'll also need a copy of Excel.</span></span> <span data-ttu-id="0823a-112">이 문서는 [Microsoft Excel 2016](https://products.office.com/)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-112">This article uses [Microsoft Excel 2016](https://products.office.com/).</span></span>

## <a name="connect-excel-to-a-sql-database-and-create-an-odc-file"></a><span data-ttu-id="0823a-113">SQL 데이터베이스에 Excel 연결 및 odc 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="0823a-113">Connect Excel to a SQL database and create an odc file</span></span>
1. <span data-ttu-id="0823a-114">Excel을 SQL 데이터베이스에 연결하려면 Excel을 연 다음 새 통합 문서를 만들거나 기존 Excel 통합 문서를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-114">To connect Excel to SQL database, open Excel and then create a new workbook or open an existing Excel workbook.</span></span>
2. <span data-ttu-id="0823a-115">페이지 위쪽에 있는 메뉴 모음에서 **데이터**, **기타 원본에서** 및 **SQL Server에서**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-115">In the menu bar at the top of the page click **Data**, click **From Other Sources**, and then click **From SQL Server**.</span></span>
   
   ![데이터 원본 선택: SQL 데이터베이스에 Excel을 연결합니다.](./media/sql-database-connect-excel/excel_data_source.png)
   
   <span data-ttu-id="0823a-117">데이터 연결 마법사가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-117">The Data Connection Wizard opens.</span></span>
3. <span data-ttu-id="0823a-118">**데이터베이스 서버에 연결** 대화 상자에서 <*servername*>**.database.windows.net** 형식에서 연결하려는 SQL Database **서버 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-118">In the **Connect to Database Server** dialog box, type the SQL Database **Server name** you want to connect to in the form <*servername*>**.database.windows.net**.</span></span> <span data-ttu-id="0823a-119">예를 들어 **adworkserver.database.windows.net**입니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-119">For example, **adworkserver.database.windows.net**.</span></span>
4. <span data-ttu-id="0823a-120">**로그온 자격 증명**에서 **다음 사용자 이름 및 암호 사용**을 클릭하고 SQL Database 서버를 만들 때 설정한 **사용자 이름** 및 **암호**를 입력한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-120">Under **Log on credentials**, click **Use the following User Name and Password**, type the **User Name** and **Password** you set up for the SQL Database server when you created it, and then click **Next**.</span></span>
   
   ![서버 이름 및 로그인 자격 증명 입력](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > <span data-ttu-id="0823a-122">네트워크 환경에 따라 SQL 데이터베이스 서버에서 클라이언트 IP 주소에서 트래픽을 허용하지 않는 경우 연결할 수 없거나 연결이 끊길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-122">Depending on your network environment, you may not be able to connect or you may lose the connection if the SQL Database server doesn't allow traffic from your client IP address.</span></span> <span data-ttu-id="0823a-123">[Azure 포털](https://portal.azure.com/)로 이동하고 SQL Server를 클릭하고 서버를 클릭하며 설정 아래에서 방화벽을 클릭하고 클라이언트 IP 주소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-123">Go to the [Azure portal](https://portal.azure.com/), click SQL servers, click your server, click firewall under settings and add your client IP address.</span></span> <span data-ttu-id="0823a-124">자세한 내용은 [방화벽 설정 구성 방법](sql-database-configure-firewall-settings.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0823a-124">See [How to configure firewall settings](sql-database-configure-firewall-settings.md) for details.</span></span>
   > 
   > 
5. <span data-ttu-id="0823a-125">**데이터베이스 및 테이블 선택** 대화 상자에서 목록에서 작업할 데이터베이스를 선택한 후 작업할 테이블 또는 뷰(**vGetAllCategories** 선택)를 클릭한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-125">In the **Select Database and Table** dialog, select the database you want to work with from the list, and then click the tables or views you want to work with (we chose **vGetAllCategories**), and then click **Next**.</span></span>
   
    ![데이터베이스 및 테이블 선택](./media/sql-database-connect-excel/select-database-and-table.png)
   
    <span data-ttu-id="0823a-127">**데이터 연결 파일 저장 및 마침** 대화 상자가 열리고 여기에 Excel에서 사용하는 Office 데이터베이스 연결(*.odc) 파일에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-127">The **Save Data Connection File and Finish** dialog box opens, where you provide information about the Office database connection (*.odc) file that Excel uses.</span></span> <span data-ttu-id="0823a-128">기본값을 그대로 두거나 선택 항목을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-128">You can leave the defaults or customize your selections.</span></span>
6. <span data-ttu-id="0823a-129">기본값을 그대로 두지만 특히 **파일 이름** 은 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-129">You can leave the defaults, but note the **File Name** in particular.</span></span> <span data-ttu-id="0823a-130">**설명**, **친숙한 이름** 및 **검색 키워드**를 통해 사용자는 연결할 대상을 기억하고 연결을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-130">A **Description**, a **Friendly Name**, and **Search Keywords** help you and other users remember what you're connecting to and find the connection.</span></span> <span data-ttu-id="0823a-131">odc 파일에 저장된 연결 정보를 원하는 경우 **항상 이 파일을 사용하여 데이터 새로 고침**을 클릭하여 연결할 때 업데이트할 수 있도록 한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-131">Click **Always attempt to use this file to refresh data** if you want connection information stored in the odc file so it can update when you connect to it, and then click **Finish**.</span></span>
   
    ![odc 파일 저장](./media/sql-database-connect-excel/save-odc-file.png)
   
    <span data-ttu-id="0823a-133">**데이터 가져오기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-133">The **Import data** dialog box appears.</span></span>

## <a name="import-the-data-into-excel-and-create-a-pivot-chart"></a><span data-ttu-id="0823a-134">Excel로 데이터 가져오기 및 피벗 차트 만들기</span><span class="sxs-lookup"><span data-stu-id="0823a-134">Import the data into Excel and create a pivot chart</span></span>
<span data-ttu-id="0823a-135">이제 연결을 설정했고 데이터 및 연결 정보로 파일을 만들었으며 데이터를 가져올 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-135">Now that you've established the connection and created the file with data and connection information, you're reading to import the data.</span></span>

1. <span data-ttu-id="0823a-136">**데이터 가져오기** 대화 상자에서 워크시트의 데이터를 표시하기 위해 원하는 옵션을 클릭한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-136">In the **Import Data** dialog, click the option you want for presenting your data in the worksheet and then click **OK**.</span></span> <span data-ttu-id="0823a-137">**PivotChart**를 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-137">We chose **PivotChart**.</span></span> <span data-ttu-id="0823a-138">또한 **새 워크시트**를 만들거나 **이 데이터를 데이터 모델에 추가하도록** 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-138">You can also choose to create a **New worksheet** or to **Add this data to a Data Model**.</span></span> <span data-ttu-id="0823a-139">데이터 모델에 대한 자세한 내용은 [Excel에서 데이터 모델 만들기](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0823a-139">For more information on Data Models, see [Create a data model in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span></span> <span data-ttu-id="0823a-140">**속성** 을 클릭하여 이전 단계에서 만든 odc 파일에 대한 정보를 탐색하고 데이터를 새로 고치는 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-140">Click **Properties** to explore information about the odc file you created in the previous step and to choose options for refreshing the data.</span></span>
   
    ![Excel에서 데이터에 대한 형식 선택](./media/sql-database-connect-excel/import-data.png)
   
    <span data-ttu-id="0823a-142">이제 워크시트에는 빈 피벗 테이블 및 차트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-142">The worksheet now has an empty pivot table and chart.</span></span>
2. <span data-ttu-id="0823a-143">**PivotTable 필드**아래에서 보려는 필드에 대한 모든 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-143">Under **PivotTable Fields**, select all the check-boxes for the fields you want to view.</span></span>
   
    ![데이터베이스 보고서를 구성합니다.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> <span data-ttu-id="0823a-145">다른 Excel 통합 문서 및 워크시트를 데이터베이스에 연결하려면 **데이터**, **연결**, **추가**를 차례로 클릭하고 목록에서 만든 연결을 선택한 후 **열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0823a-145">If you want to connect other Excel workbooks and worksheets to the database, click **Data**, click **Connections**, click **Add**, choose the connection you created from the list, and then click **Open**.</span></span>
> <span data-ttu-id="0823a-146">![다른 통합 문서에서 연결 열기](./media/sql-database-connect-excel/open-from-another-workbook.png)</span><span class="sxs-lookup"><span data-stu-id="0823a-146">![Open a connection from another workbook](./media/sql-database-connect-excel/open-from-another-workbook.png)</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0823a-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0823a-147">Next steps</span></span>
* <span data-ttu-id="0823a-148">고급 쿼리 및 분석을 위해 [SQL Server Management Studio를 사용하여 SQL 데이터베이스에 연결](sql-database-connect-query-ssms.md) 하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="0823a-148">Learn how to [Connect to SQL Database with SQL Server Management Studio](sql-database-connect-query-ssms.md) for advanced querying and analysis.</span></span>
* <span data-ttu-id="0823a-149">[탄력적 풀](sql-database-elastic-pool.md)의 이점에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="0823a-149">Learn about the benefits of [elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="0823a-150">[백 엔드에서 SQL 데이터베이스에 연결할 웹 응용 프로그램을 만드는](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md)방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="0823a-150">Learn how to [create a web application that connects to SQL Database on the back-end](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span>

