---
title: "aaaConnect tooAzure SQL 데이터 웨어하우스-VSTS | Microsoft Docs"
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
ms.openlocfilehash: 55eef4dff3e0647be5a735295bc89b43eb456079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-visual-studio-and-ssdt"></a><span data-ttu-id="fd397-103">Visual Studio와 SSDT를 사용 하 여 데이터 웨어하우스 tooSQL 연결</span><span class="sxs-lookup"><span data-stu-id="fd397-103">Connect tooSQL Data Warehouse with Visual Studio and SSDT</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fd397-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="fd397-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="fd397-105">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="fd397-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="fd397-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fd397-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="fd397-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="fd397-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="fd397-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="fd397-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="fd397-109">단 몇 분 후에 Visual Studio tooquery Azure SQL 데이터 웨어하우스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-109">Use Visual Studio tooquery Azure SQL Data Warehouse in just a few minutes.</span></span> <span data-ttu-id="fd397-110">이 메서드는 Visual Studio에서 hello SQL Server Data Tools (SSDT) 확장을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-110">This method uses hello SQL Server Data Tools (SSDT) extension in Visual Studio.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fd397-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fd397-111">Prerequisites</span></span>
<span data-ttu-id="fd397-112">toouse 해야이 자습서에서는:</span><span class="sxs-lookup"><span data-stu-id="fd397-112">toouse this tutorial, you need:</span></span>

* <span data-ttu-id="fd397-113">기존 SQL 데이터 웨어하우스.</span><span class="sxs-lookup"><span data-stu-id="fd397-113">An existing SQL data warehouse.</span></span> <span data-ttu-id="fd397-114">하나의 toocreate 참조 [SQL 데이터 웨어하우스를 만들][Create a SQL Data Warehouse]합니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-114">toocreate one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="fd397-115">Visual Studio용 SSDT.</span><span class="sxs-lookup"><span data-stu-id="fd397-115">SSDT for Visual Studio.</span></span> <span data-ttu-id="fd397-116">Visual Studio가 있는 경우 이미 소유하고 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-116">If you have Visual Studio, you probably already have this.</span></span> <span data-ttu-id="fd397-117">설치 지침 및 옵션은 [Visual Studio 및 SSDT 설치][Installing Visual Studio and SSDT]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fd397-117">For installation instructions and options, see [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT].</span></span>
* <span data-ttu-id="fd397-118">hello 정규화 된 SQL server 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-118">hello fully qualified SQL server name.</span></span> <span data-ttu-id="fd397-119">toofind이,이 참조 [tooSQL 데이터 웨어하우스 연결][Connect tooSQL Data Warehouse]합니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-119">toofind this, see [Connect tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span></span>

## <a name="1-connect-tooyour-sql-data-warehouse"></a><span data-ttu-id="fd397-120">1. SQL 데이터 웨어하우스 tooyour 연결</span><span class="sxs-lookup"><span data-stu-id="fd397-120">1. Connect tooyour SQL Data Warehouse</span></span>
1. <span data-ttu-id="fd397-121">Visual Studio 2013 또는 2015 열기</span><span class="sxs-lookup"><span data-stu-id="fd397-121">Open Visual Studio 2013 or 2015.</span></span>
2. <span data-ttu-id="fd397-122">SQL Server 개체 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-122">Open SQL Server Object Explorer.</span></span> <span data-ttu-id="fd397-123">toodo이,이 선택 **보기** > **SQL Server 개체 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-123">toodo this, select **View** > **SQL Server Object Explorer**.</span></span>
   
    ![SQL Server 개체 탐색기][1]
3. <span data-ttu-id="fd397-125">Hello 클릭 **SQL Server 추가** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-125">Click hello **Add SQL Server** icon.</span></span>
   
    ![SQL Server 추가][2]
4. <span data-ttu-id="fd397-127">Hello 연결 tooServer 창의 hello 필드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-127">Fill in hello fields in hello Connect tooServer window.</span></span>
   
    ![TooServer 연결][3]
   
   * <span data-ttu-id="fd397-129">**서버 이름**.</span><span class="sxs-lookup"><span data-stu-id="fd397-129">**Server name**.</span></span> <span data-ttu-id="fd397-130">Hello 입력 **서버 이름** 앞에서 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-130">Enter hello **server name** previously identified.</span></span>
   * <span data-ttu-id="fd397-131">**인증**.</span><span class="sxs-lookup"><span data-stu-id="fd397-131">**Authentication**.</span></span> <span data-ttu-id="fd397-132">**SQL Server 인증** 또는 **Active Directory 통합 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-132">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="fd397-133">**사용자 이름** 및 **암호**.</span><span class="sxs-lookup"><span data-stu-id="fd397-133">**User Name** and **Password**.</span></span> <span data-ttu-id="fd397-134">위에서 SQL Server 인증을 선택한 경우 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-134">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="fd397-135">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-135">Click **Connect**.</span></span>
5. <span data-ttu-id="fd397-136">tooexplore, Azure SQL 서버를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-136">tooexplore, expand your Azure SQL server.</span></span> <span data-ttu-id="fd397-137">Hello 서버와 관련 된 hello 데이터베이스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-137">You can view hello databases associated with hello server.</span></span> <span data-ttu-id="fd397-138">예제 데이터베이스 AdventureWorksDW toosee hello 테이블을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-138">Expand AdventureWorksDW toosee hello tables in your sample database.</span></span>
   
    ![AdventureWorksDW 탐색하기][4]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="fd397-140">2. 샘플 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="fd397-140">2. Run a sample query</span></span>
<span data-ttu-id="fd397-141">연결에 대 한 설정 된 tooyour 데이터베이스를 수행한 했으므로 쿼리를 작성해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-141">Now that a connection has been established tooyour database, let's write a query.</span></span>

1. <span data-ttu-id="fd397-142">SQL Server 개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-142">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="fd397-143">**새 쿼리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-143">Select **New Query**.</span></span> <span data-ttu-id="fd397-144">새 쿼리 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-144">A new query window opens.</span></span>
   
    ![새 쿼리][5]
3. <span data-ttu-id="fd397-146">이 t s q L 쿼리 hello 쿼리 창에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-146">Copy this TSQL query into hello query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="fd397-147">Hello 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-147">Run hello query.</span></span> <span data-ttu-id="fd397-148">toodo hello 녹색 화살표를 클릭 하거나 바로 가기 다음 hello를 사용 하 여이: `CTRL` + `SHIFT` + `E`합니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-148">toodo this, click hello green arrow or use hello following shortcut: `CTRL`+`SHIFT`+`E`.</span></span>
   
    ![쿼리 실행][6]
5. <span data-ttu-id="fd397-150">Hello 쿼리 결과 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-150">Look at hello query results.</span></span> <span data-ttu-id="fd397-151">이 예제에서는 hello FactInternetSales 테이블 60398 행에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-151">In this example, hello FactInternetSales table has 60398 rows.</span></span>
   
    ![쿼리 결과][7]

## <a name="next-steps"></a><span data-ttu-id="fd397-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fd397-153">Next steps</span></span>
<span data-ttu-id="fd397-154">연결 하 고 쿼리할 수, 하 고 나면 [PowerBI 사용 하 여 hello 데이터 시각화][visualizing hello data with PowerBI]합니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-154">Now that you can connect and query, try [visualizing hello data with PowerBI][visualizing hello data with PowerBI].</span></span>

<span data-ttu-id="fd397-155">Azure Active Directory 인증을 위한 환경 참조 tooconfigure [tooSQL 데이터 웨어하우스를 인증][Authenticate tooSQL Data Warehouse]합니다.</span><span class="sxs-lookup"><span data-stu-id="fd397-155">tooconfigure your environment for Azure Active Directory authentication, see [Authenticate tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

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
