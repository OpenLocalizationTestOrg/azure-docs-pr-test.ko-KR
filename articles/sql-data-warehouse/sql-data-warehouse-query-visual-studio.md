---
title: "Azure SQL Data Warehouse - VSTS에 연결 | Microsoft Azure"
description: "Visual Studio를 사용하여 SQL 데이터 웨어하우스를 쿼리합니다."
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 1e44c6c3c47034a892753c69c5ef22a5eac18c0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-sql-data-warehouse-with-visual-studio-and-ssdt"></a><span data-ttu-id="ac8d3-103">Visual Studio 및 SSDT를 사용하여 SQL Data Warehouse에 연결</span><span class="sxs-lookup"><span data-stu-id="ac8d3-103">Connect to SQL Data Warehouse with Visual Studio and SSDT</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ac8d3-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="ac8d3-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="ac8d3-105">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="ac8d3-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="ac8d3-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ac8d3-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="ac8d3-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="ac8d3-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="ac8d3-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="ac8d3-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="ac8d3-109">Visual Studio를 사용하여 단 몇 분 만에 Azure SQL 데이터 웨어하우스를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-109">Use Visual Studio to query Azure SQL Data Warehouse in just a few minutes.</span></span> <span data-ttu-id="ac8d3-110">이 메서드는 Visual Studio에서 SQL Server 데이터 도구(SSDT) 확장을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-110">This method uses the SQL Server Data Tools (SSDT) extension in Visual Studio.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ac8d3-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ac8d3-111">Prerequisites</span></span>
<span data-ttu-id="ac8d3-112">이 자습서를 사용하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-112">To use this tutorial, you need:</span></span>

* <span data-ttu-id="ac8d3-113">기존 SQL 데이터 웨어하우스.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-113">An existing SQL data warehouse.</span></span> <span data-ttu-id="ac8d3-114">만들려면 [SQL Data Warehouse 만들기][Create a SQL Data Warehouse]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-114">To create one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="ac8d3-115">Visual Studio용 SSDT.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-115">SSDT for Visual Studio.</span></span> <span data-ttu-id="ac8d3-116">Visual Studio가 있는 경우 이미 소유하고 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-116">If you have Visual Studio, you probably already have this.</span></span> <span data-ttu-id="ac8d3-117">설치 지침 및 옵션은 [Visual Studio 및 SSDT 설치][Installing Visual Studio and SSDT]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-117">For installation instructions and options, see [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT].</span></span>
* <span data-ttu-id="ac8d3-118">정규화된 SQL 서버 이름.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-118">The fully qualified SQL server name.</span></span> <span data-ttu-id="ac8d3-119">이를 찾으려면 [SQL Data Warehouse에 연결][Connect to SQL Data Warehouse]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-119">To find this, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span></span>

## <a name="1-connect-to-your-sql-data-warehouse"></a><span data-ttu-id="ac8d3-120">1. SQL 데이터 웨어하우스에 연결</span><span class="sxs-lookup"><span data-stu-id="ac8d3-120">1. Connect to your SQL Data Warehouse</span></span>
1. <span data-ttu-id="ac8d3-121">Visual Studio 2013 또는 2015 열기</span><span class="sxs-lookup"><span data-stu-id="ac8d3-121">Open Visual Studio 2013 or 2015.</span></span>
2. <span data-ttu-id="ac8d3-122">SQL Server 개체 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-122">Open SQL Server Object Explorer.</span></span> <span data-ttu-id="ac8d3-123">그렇게 하려면 **보기** > **SQL Server 개체 탐색기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-123">To do this, select **View** > **SQL Server Object Explorer**.</span></span>
   
    ![SQL Server 개체 탐색기][1]
3. <span data-ttu-id="ac8d3-125">**SQL Server 추가** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-125">Click the **Add SQL Server** icon.</span></span>
   
    ![SQL Server 추가][2]
4. <span data-ttu-id="ac8d3-127">서버 창에 연결에서 필드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-127">Fill in the fields in the Connect to Server window.</span></span>
   
    ![서버에 연결][3]
   
   * <span data-ttu-id="ac8d3-129">**서버 이름**.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-129">**Server name**.</span></span> <span data-ttu-id="ac8d3-130">이전에 식별한 **서버 이름** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-130">Enter the **server name** previously identified.</span></span>
   * <span data-ttu-id="ac8d3-131">**인증**.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-131">**Authentication**.</span></span> <span data-ttu-id="ac8d3-132">**SQL Server 인증** 또는 **Active Directory 통합 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-132">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="ac8d3-133">**사용자 이름** 및 **암호**.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-133">**User Name** and **Password**.</span></span> <span data-ttu-id="ac8d3-134">위에서 SQL Server 인증을 선택한 경우 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-134">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="ac8d3-135">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-135">Click **Connect**.</span></span>
5. <span data-ttu-id="ac8d3-136">탐색하려면 SQL Azure Server를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-136">To explore, expand your Azure SQL server.</span></span> <span data-ttu-id="ac8d3-137">서버와 연결된 데이터베이스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-137">You can view the databases associated with the server.</span></span> <span data-ttu-id="ac8d3-138">AdventureWorksDW를 확장하여 샘플 데이터베이스의 테이블을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-138">Expand AdventureWorksDW to see the tables in your sample database.</span></span>
   
    ![AdventureWorksDW 탐색하기][4]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="ac8d3-140">2. 샘플 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="ac8d3-140">2. Run a sample query</span></span>
<span data-ttu-id="ac8d3-141">데이터베이스에 대한 연결을 설정했으므로 쿼리를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-141">Now that a connection has been established to your database, let's write a query.</span></span>

1. <span data-ttu-id="ac8d3-142">SQL Server 개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-142">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="ac8d3-143">**새 쿼리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-143">Select **New Query**.</span></span> <span data-ttu-id="ac8d3-144">새 쿼리 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-144">A new query window opens.</span></span>
   
    ![새 쿼리][5]
3. <span data-ttu-id="ac8d3-146">이 TSQL 쿼리를 쿼리 창에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-146">Copy this TSQL query into the query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="ac8d3-147">쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-147">Run the query.</span></span> <span data-ttu-id="ac8d3-148">이렇게 하려면 녹색 화살표를 클릭하거나 다음 바로 가기를 사용합니다. `CTRL`+`SHIFT`+`E`</span><span class="sxs-lookup"><span data-stu-id="ac8d3-148">To do this, click the green arrow or use the following shortcut: `CTRL`+`SHIFT`+`E`.</span></span>
   
    ![쿼리 실행][6]
5. <span data-ttu-id="ac8d3-150">쿼리 결과를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-150">Look at the query results.</span></span> <span data-ttu-id="ac8d3-151">이 예에서 FactInternetSales 테이블에는 60398 행이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-151">In this example, the FactInternetSales table has 60398 rows.</span></span>
   
    ![쿼리 결과][7]

## <a name="next-steps"></a><span data-ttu-id="ac8d3-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ac8d3-153">Next steps</span></span>
<span data-ttu-id="ac8d3-154">이제 연결 및 쿼리할 수 있으므로 [PowerBI로 데이터 시각화][visualizing the data with PowerBI]를 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-154">Now that you can connect and query, try [visualizing the data with PowerBI][visualizing the data with PowerBI].</span></span>

<span data-ttu-id="ac8d3-155">Azure Active Directory 인증을 위한 환경을 구성하려면 [SQL Data Warehouse에 대한 인증][Authenticate to SQL Data Warehouse]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac8d3-155">To configure your environment for Azure Active Directory authentication, see [Authenticate to SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect to SQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate to SQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing the data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: media/sql-data-warehouse-query-visual-studio/query-results.png
