---
title: "aaaConnect tooAzure SQL 데이터 웨어하우스-SSMS | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스 SQL Server Management Studio (SSMS) tooconnect tooand 쿼리를 사용 합니다."
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
ms.openlocfilehash: bcbaf7139d2e5183b388b8d58c015cf5ad726722
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sql-server-management-studio-ssms"></a><span data-ttu-id="03efd-103">TooSQL 데이터 웨어하우스 SQL Server Management Studio (SSMS)와 연결</span><span class="sxs-lookup"><span data-stu-id="03efd-103">Connect tooSQL Data Warehouse with SQL Server Management Studio (SSMS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="03efd-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="03efd-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="03efd-105">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="03efd-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="03efd-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="03efd-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="03efd-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="03efd-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="03efd-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="03efd-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="03efd-109">Azure SQL 데이터 웨어하우스 SQL Server Management Studio (SSMS) tooconnect tooand 쿼리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-109">Use SQL Server Management Studio (SSMS) tooconnect tooand query Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="03efd-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="03efd-110">Prerequisites</span></span>
<span data-ttu-id="03efd-111">toouse 해야이 자습서에서는:</span><span class="sxs-lookup"><span data-stu-id="03efd-111">toouse this tutorial, you need:</span></span>

* <span data-ttu-id="03efd-112">기존 SQL 데이터 웨어하우스.</span><span class="sxs-lookup"><span data-stu-id="03efd-112">An existing SQL data warehouse.</span></span> <span data-ttu-id="03efd-113">하나의 toocreate 참조 [SQL 데이터 웨어하우스를 만들][Create a SQL Data Warehouse]합니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-113">toocreate one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="03efd-114">SSMS(SQL Server Management Studio) 설치됨.</span><span class="sxs-lookup"><span data-stu-id="03efd-114">SQL Server Management Studio (SSMS) installed.</span></span> <span data-ttu-id="03efd-115">아직 없는 경우 무료로 [SSMS를 설치][Install SSMS]합니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-115">[Install SSMS][Install SSMS] for free if you don't already have it.</span></span>
* <span data-ttu-id="03efd-116">hello 정규화 된 SQL server 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-116">hello fully qualified SQL server name.</span></span> <span data-ttu-id="03efd-117">toofind이,이 참조 [tooSQL 데이터 웨어하우스 연결][Connect tooSQL Data Warehouse]합니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-117">toofind this, see [Connect tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span></span>

## <a name="1-connect-tooyour-sql-data-warehouse"></a><span data-ttu-id="03efd-118">1. SQL 데이터 웨어하우스 tooyour 연결</span><span class="sxs-lookup"><span data-stu-id="03efd-118">1. Connect tooyour SQL Data Warehouse</span></span>
1. <span data-ttu-id="03efd-119">SSMS를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-119">Open SSMS.</span></span>
2. <span data-ttu-id="03efd-120">개체 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-120">Open Object Explorer.</span></span> <span data-ttu-id="03efd-121">toodo이,이 선택 **파일** > **개체 탐색기 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-121">toodo this, select **File** > **Connect Object Explorer**.</span></span>
   
    ![SQL Server 개체 탐색기][1]
3. <span data-ttu-id="03efd-123">Hello 연결 tooServer 창의 hello 필드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-123">Fill in hello fields in hello Connect tooServer window.</span></span>
   
    ![TooServer 연결][2]
   
   * <span data-ttu-id="03efd-125">**서버 이름**.</span><span class="sxs-lookup"><span data-stu-id="03efd-125">**Server name**.</span></span> <span data-ttu-id="03efd-126">Hello 입력 **서버 이름** 앞에서 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-126">Enter hello **server name** previously identified.</span></span>
   * <span data-ttu-id="03efd-127">**인증**.</span><span class="sxs-lookup"><span data-stu-id="03efd-127">**Authentication**.</span></span> <span data-ttu-id="03efd-128">**SQL Server 인증** 또는 **Active Directory 통합 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-128">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="03efd-129">**사용자 이름** 및 **암호**.</span><span class="sxs-lookup"><span data-stu-id="03efd-129">**User Name** and **Password**.</span></span> <span data-ttu-id="03efd-130">위에서 SQL Server 인증을 선택한 경우 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-130">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="03efd-131">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-131">Click **Connect**.</span></span>
4. <span data-ttu-id="03efd-132">tooexplore, Azure SQL 서버를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-132">tooexplore, expand your Azure SQL server.</span></span> <span data-ttu-id="03efd-133">Hello 서버와 관련 된 hello 데이터베이스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-133">You can view hello databases associated with hello server.</span></span> <span data-ttu-id="03efd-134">예제 데이터베이스 AdventureWorksDW toosee hello 테이블을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-134">Expand AdventureWorksDW toosee hello tables in your sample database.</span></span>
   
    ![AdventureWorksDW 탐색하기][3]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="03efd-136">2. 샘플 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="03efd-136">2. Run a sample query</span></span>
<span data-ttu-id="03efd-137">연결에 대 한 설정 된 tooyour 데이터베이스를 수행한 했으므로 쿼리를 작성해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-137">Now that a connection has been established tooyour database, let's write a query.</span></span>

1. <span data-ttu-id="03efd-138">SQL Server 개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-138">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="03efd-139">**새 쿼리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-139">Select **New Query**.</span></span> <span data-ttu-id="03efd-140">새 쿼리 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-140">A new query window opens.</span></span>
   
    ![새 쿼리][4]
3. <span data-ttu-id="03efd-142">이 t s q L 쿼리 hello 쿼리 창에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-142">Copy this TSQL query into hello query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="03efd-143">Hello 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-143">Run hello query.</span></span> <span data-ttu-id="03efd-144">toodo이를 클릭 하이 여 `Execute` 사용 하 여 hello 다음 바로 가기 또는: `F5`합니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-144">toodo this, click `Execute` or use hello following shortcut: `F5`.</span></span>
   
    ![쿼리 실행][5]
5. <span data-ttu-id="03efd-146">Hello 쿼리 결과 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-146">Look at hello query results.</span></span> <span data-ttu-id="03efd-147">이 예제에서는 hello FactInternetSales 테이블 60398 행에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-147">In this example, hello FactInternetSales table has 60398 rows.</span></span>
   
    ![쿼리 결과][6]

## <a name="next-steps"></a><span data-ttu-id="03efd-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="03efd-149">Next steps</span></span>
<span data-ttu-id="03efd-150">연결 하 고 쿼리할 수, 하 고 나면 [PowerBI 사용 하 여 hello 데이터 시각화][visualizing hello data with PowerBI]합니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-150">Now that you can connect and query, try [visualizing hello data with PowerBI][visualizing hello data with PowerBI].</span></span>

<span data-ttu-id="03efd-151">Azure Active Directory 인증을 위한 환경 참조 tooconfigure [tooSQL 데이터 웨어하우스를 인증][Authenticate tooSQL Data Warehouse]합니다.</span><span class="sxs-lookup"><span data-stu-id="03efd-151">tooconfigure your environment for Azure Active Directory authentication, see [Authenticate tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

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
