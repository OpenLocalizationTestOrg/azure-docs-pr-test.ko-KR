---
title: "Azure SQL Data Warehouse에 연결 - SSMS | Microsoft Docs"
description: "SSMS(SQL Server Management Studio)를 사용하여 Azure SQL Data Warehouse에 연결하고 쿼리합니다."
services: sql-data-warehouse
documentationcenter: 
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 299e50b3-e68a-471c-8aee-b0b9874781bd
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 207fb9fd861c66039fbde89681aed3df3a2f4021
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-sql-data-warehouse-with-sql-server-management-studio-ssms"></a><span data-ttu-id="32b4a-103">SSM(SQL Server Management Studio)를 사용하여 SQL Data Warehouse에 연결</span><span class="sxs-lookup"><span data-stu-id="32b4a-103">Connect to SQL Data Warehouse with SQL Server Management Studio (SSMS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="32b4a-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="32b4a-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="32b4a-105">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="32b4a-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="32b4a-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="32b4a-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="32b4a-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="32b4a-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="32b4a-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="32b4a-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="32b4a-109">SSMS(SQL Server Management Studio)를 사용하여 Azure SQL Data Warehouse에 연결하고 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="32b4a-109">Use SQL Server Management Studio (SSMS) to connect to and query Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="32b4a-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="32b4a-110">Prerequisites</span></span>
<span data-ttu-id="32b4a-111">이 자습서를 사용하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="32b4a-111">To use this tutorial, you need:</span></span>

* <span data-ttu-id="32b4a-112">기존 SQL 데이터 웨어하우스.</span><span class="sxs-lookup"><span data-stu-id="32b4a-112">An existing SQL data warehouse.</span></span> <span data-ttu-id="32b4a-113">만들려면 [SQL Data Warehouse 만들기][Create a SQL Data Warehouse]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32b4a-113">To create one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="32b4a-114">SSMS(SQL Server Management Studio) 설치됨.</span><span class="sxs-lookup"><span data-stu-id="32b4a-114">SQL Server Management Studio (SSMS) installed.</span></span> <span data-ttu-id="32b4a-115">아직 없는 경우 무료로 [SSMS를 설치][Install SSMS]합니다.</span><span class="sxs-lookup"><span data-stu-id="32b4a-115">[Install SSMS][Install SSMS] for free if you don't already have it.</span></span>
* <span data-ttu-id="32b4a-116">정규화된 SQL 서버 이름.</span><span class="sxs-lookup"><span data-stu-id="32b4a-116">The fully qualified SQL server name.</span></span> <span data-ttu-id="32b4a-117">이를 찾으려면 [SQL Data Warehouse에 연결][Connect to SQL Data Warehouse]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32b4a-117">To find this, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span></span>

## <a name="1-connect-to-your-sql-data-warehouse"></a><span data-ttu-id="32b4a-118">1. SQL 데이터 웨어하우스에 연결</span><span class="sxs-lookup"><span data-stu-id="32b4a-118">1. Connect to your SQL Data Warehouse</span></span>
1. <span data-ttu-id="32b4a-119">SSMS를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="32b4a-119">Open SSMS.</span></span>
2. <span data-ttu-id="32b4a-120">개체 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="32b4a-120">Open Object Explorer.</span></span> <span data-ttu-id="32b4a-121">이를 수행하려면 **파일** > **개체 탐색기 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32b4a-121">To do this, select **File** > **Connect Object Explorer**.</span></span>
   
    ![SQL Server 개체 탐색기][1]
3. <span data-ttu-id="32b4a-123">서버 창에 연결에서 필드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="32b4a-123">Fill in the fields in the Connect to Server window.</span></span>
   
    ![서버에 연결][2]
   
   * <span data-ttu-id="32b4a-125">**서버 이름**.</span><span class="sxs-lookup"><span data-stu-id="32b4a-125">**Server name**.</span></span> <span data-ttu-id="32b4a-126">이전에 식별한 **서버 이름** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="32b4a-126">Enter the **server name** previously identified.</span></span>
   * <span data-ttu-id="32b4a-127">**인증**.</span><span class="sxs-lookup"><span data-stu-id="32b4a-127">**Authentication**.</span></span> <span data-ttu-id="32b4a-128">**SQL Server 인증** 또는 **Active Directory 통합 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32b4a-128">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="32b4a-129">**사용자 이름** 및 **암호**.</span><span class="sxs-lookup"><span data-stu-id="32b4a-129">**User Name** and **Password**.</span></span> <span data-ttu-id="32b4a-130">위에서 SQL Server 인증을 선택한 경우 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="32b4a-130">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="32b4a-131">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32b4a-131">Click **Connect**.</span></span>
4. <span data-ttu-id="32b4a-132">탐색하려면 SQL Azure Server를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="32b4a-132">To explore, expand your Azure SQL server.</span></span> <span data-ttu-id="32b4a-133">서버와 연결된 데이터베이스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32b4a-133">You can view the databases associated with the server.</span></span> <span data-ttu-id="32b4a-134">AdventureWorksDW를 확장하여 샘플 데이터베이스의 테이블을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="32b4a-134">Expand AdventureWorksDW to see the tables in your sample database.</span></span>
   
    ![AdventureWorksDW 탐색하기][3]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="32b4a-136">2. 샘플 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="32b4a-136">2. Run a sample query</span></span>
<span data-ttu-id="32b4a-137">데이터베이스에 대한 연결을 설정했으므로 쿼리를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="32b4a-137">Now that a connection has been established to your database, let's write a query.</span></span>

1. <span data-ttu-id="32b4a-138">SQL Server 개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32b4a-138">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="32b4a-139">**새 쿼리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32b4a-139">Select **New Query**.</span></span> <span data-ttu-id="32b4a-140">새 쿼리 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="32b4a-140">A new query window opens.</span></span>
   
    ![새 쿼리][4]
3. <span data-ttu-id="32b4a-142">이 TSQL 쿼리를 쿼리 창에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="32b4a-142">Copy this TSQL query into the query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="32b4a-143">쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="32b4a-143">Run the query.</span></span> <span data-ttu-id="32b4a-144">이렇게 하려면 `Execute`를 클릭하거나 다음 바로 가기(`F5`)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="32b4a-144">To do this, click `Execute` or use the following shortcut: `F5`.</span></span>
   
    ![쿼리 실행][5]
5. <span data-ttu-id="32b4a-146">쿼리 결과를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="32b4a-146">Look at the query results.</span></span> <span data-ttu-id="32b4a-147">이 예에서 FactInternetSales 테이블에는 60398 행이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32b4a-147">In this example, the FactInternetSales table has 60398 rows.</span></span>
   
    ![쿼리 결과][6]

## <a name="next-steps"></a><span data-ttu-id="32b4a-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="32b4a-149">Next steps</span></span>
<span data-ttu-id="32b4a-150">이제 연결 및 쿼리할 수 있으므로 [PowerBI로 데이터 시각화][visualizing the data with PowerBI]를 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="32b4a-150">Now that you can connect and query, try [visualizing the data with PowerBI][visualizing the data with PowerBI].</span></span>

<span data-ttu-id="32b4a-151">Azure Active Directory 인증을 위한 환경을 구성하려면 [SQL Data Warehouse에 대한 인증][Authenticate to SQL Data Warehouse]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32b4a-151">To configure your environment for Azure Active Directory authentication, see [Authenticate to SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect to SQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate to SQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing the data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

<!--Other-->
[Azure portal]: https://portal.azure.com
[Install SSMS]: https://msdn.microsoft.com/en-US/library/hh213248.aspx


<!--Image references-->

[1]: media/sql-data-warehouse-query-ssms/connect-object-explorer.png
[2]: media/sql-data-warehouse-query-ssms/connect-object-explorer1.png
[3]: media/sql-data-warehouse-query-ssms/explore-tables.png
[4]: media/sql-data-warehouse-query-ssms/new-query.png
[5]: media/sql-data-warehouse-query-ssms/execute-query.png
[6]: media/sql-data-warehouse-query-ssms/results.png
