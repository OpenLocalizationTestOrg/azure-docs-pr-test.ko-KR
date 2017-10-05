---
title: "Power BI Microsoft Azure로 SQL 데이터 웨어하우스 데이터 시각화"
description: "Power BI로 SQL 데이터 웨어하우스 데이터 시각화"
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: d7fb89d1-da1d-4788-a111-68d0e3fda799
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: a41393730143b14e91318a61858d989fff3786c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-data-with-power-bi"></a><span data-ttu-id="769f4-103">Power BI를 사용하여 데이터 시각화</span><span class="sxs-lookup"><span data-stu-id="769f4-103">Visualize data with Power BI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="769f4-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="769f4-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="769f4-105">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="769f4-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="769f4-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="769f4-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="769f4-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="769f4-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="769f4-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="769f4-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="769f4-109">이 자습서에서는 Power BI를 사용하여 SQL 데이터 웨어하우스에 연결하고 몇 가지 기본적인 시각화를 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-109">This tutorial shows you how to use Power BI to connect to SQL Data Warehouse and create a few basic visualizations.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="769f4-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="769f4-110">Prerequisites</span></span>
<span data-ttu-id="769f4-111">이 자습서를 단계별로 실행하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-111">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="769f4-112">AdventureWorksDW 데이터베이스로 미리 로드된 SQL 데이터 웨어하우스.</span><span class="sxs-lookup"><span data-stu-id="769f4-112">A SQL Data Warehouse pre-loaded with the AdventureWorksDW database.</span></span> <span data-ttu-id="769f4-113">프로비전하려면 [SQL Data Warehouse 만들기][Create a SQL Data Warehouse]를 참조하고 샘플 데이터 로드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-113">To provision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose to load the sample data.</span></span> <span data-ttu-id="769f4-114">데이터 웨어하우스는 있지만 샘플 데이터가 없는 경우 [샘플 데이터를 수동으로 로드][load sample data manually]할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-114">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-connect-to-your-database"></a><span data-ttu-id="769f4-115">1. 데이터베이스 연결</span><span class="sxs-lookup"><span data-stu-id="769f4-115">1. Connect to your database</span></span>
<span data-ttu-id="769f4-116">Power BI를 열고 AdventureWorksDW 데이터베이스에 연결하려면</span><span class="sxs-lookup"><span data-stu-id="769f4-116">To open Power BI and connect to your AdventureWorksDW database:</span></span>

1. <span data-ttu-id="769f4-117">[Azure Portal][Azure portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-117">Sign into the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="769f4-118">**SQL 데이터베이스** 를 클릭하고 AdventureWorks SQL 데이터 웨어하우스 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-118">Click **SQL databases** and choose your AdventureWorks SQL Data Warehouse database.</span></span>
   
    ![데이터베이스 찾기][1]
3. <span data-ttu-id="769f4-120">'Power BI에서 열기' 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-120">Click the 'Open in Power BI' button.</span></span>
   
    ![Power BI 단추][2]
4. <span data-ttu-id="769f4-122">이제 데이터베이스 웹 주소를 표시하는 SQL 데이터 웨어하우스 연결 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-122">You should now see the SQL Data Warehouse connection page displaying your database web address.</span></span> <span data-ttu-id="769f4-123">다음을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-123">Click next.</span></span>
   
    ![Power BI 연결][3]
5. <span data-ttu-id="769f4-125">Azure SQL 서버 사용자 이름과 암호를 입력하면 SQL 데이터 웨어하우스 데이터베이스에 완벽하게 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-125">Enter your Azure SQL server username and password and you will be fully connected to your SQL Data Warehouse database.</span></span>
   
    ![Power BI 로그인][4]
6. <span data-ttu-id="769f4-127">Power BI에 로그인하면 왼쪽 블레이드에서 AdventureWorksDW 데이터 집합을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-127">Once you have signed into Power BI, click the AdventureWorksDW dataset on the left blade.</span></span> <span data-ttu-id="769f4-128">그러면 데이터베이스가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-128">This will open the database.</span></span>
   
    ![Power BI AdventureWorksDW 열기][5]

## <a name="2-create-a-report"></a><span data-ttu-id="769f4-130">2. 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="769f4-130">2. Create a report</span></span>
<span data-ttu-id="769f4-131">이제 Power BI를 사용하여 AdventureWorksDW 샘플 데이터를 분석할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-131">You are now ready to use Power BI to analyze your AdventureWorksDW sample data.</span></span> <span data-ttu-id="769f4-132">분석을 수행하기 위해 AdventureWorksDW에는 AggregateSales라는 뷰가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-132">To perform the analysis, AdventureWorksDW has a view called AggregateSales.</span></span> <span data-ttu-id="769f4-133">이 뷰는 회사의 판매를 분석하기 위한 주요 메트릭 중 일부를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-133">This view contains a few of the key metrics for analyzing the sales of the company.</span></span>

1. <span data-ttu-id="769f4-134">우편 번호에 따라 판매액 지도를 만들려면 오른쪽 필드 창에서 AggregateSales 뷰를 클릭하여 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-134">To create a map of sales amount according to postal code, in the right-hand fields pane, click the AggregateSales view to expand it.</span></span> <span data-ttu-id="769f4-135">PostalCode 및 SalesAmount 열을 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-135">Click the PostalCode and SalesAmount columns to select them.</span></span>
   
    ![Power BI AggregateSales 선택][6]
   
    <span data-ttu-id="769f4-137">Power BI는 이를 지리적 데이터로 자동으로 인식하고 지도에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-137">Power BI automatically recognizes this is geographic data and put it in a map for you.</span></span>
   
    ![Power BI 맵][7]
2. <span data-ttu-id="769f4-139">이 단계에서는 고객 수익당 매출액을 보여주는 막대 그래프를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-139">This step creates a bar graph that shows amount of sales per customer income.</span></span> <span data-ttu-id="769f4-140">이 그래프를 만들려면 확장된 AggregateSales 보기로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-140">To create this go to the expanded AggregateSales view.</span></span> <span data-ttu-id="769f4-141">SalesAmount 필드를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-141">Click the SalesAmount field.</span></span> <span data-ttu-id="769f4-142">고객 수익 필드를 왼쪽으로 끌어 축에 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-142">Drag the Customer Income field to the left and drop it into Axis.</span></span>
   
    ![Power BI 축 선택][8]
   
    <span data-ttu-id="769f4-144">가로 막대형 차트를 왼쪽으로 이동했습니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-144">We moved the bar chart over the left.</span></span>
   
    ![Power BI 막대형][9]
3. <span data-ttu-id="769f4-146">이 단계에서는 주문 날짜당 판매 금액을 보여주는 꺽은선형 차트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-146">This step creates a line chart that shows sales amount per order date.</span></span> <span data-ttu-id="769f4-147">이 그래프를 만들려면 확장된 AggregateSales 보기로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-147">To create this go to the expanded AggregateSales view.</span></span> <span data-ttu-id="769f4-148">SalesAmount 및 OrderDate를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-148">Click SalesAmount and OrderDate.</span></span> <span data-ttu-id="769f4-149">시각화 열에서 왼쪽 차트 아이콘을 클릭합니다. 이 아이콘은 시각화에서 두 번째 열의 첫 번째 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-149">In the Visualizations column click the Line Chart icon; this is the first icon in the second line under visualizations.</span></span>
   
    ![Power BI 꺾은선형 차트 선택][10]
   
    <span data-ttu-id="769f4-151">이제 데이터를 다양한 시각화로 보여주는 보고서가 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-151">You now have a report that shows three different visualizations of the data.</span></span>
   
    ![Power BI 꺾은선형][11]

<span data-ttu-id="769f4-153">언제든지 **파일**을 클릭하고 **저장**을 선택하여 진행 상황을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-153">You can save your progress at any time by clicking **File** and selecting **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="769f4-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="769f4-154">Next steps</span></span>
<span data-ttu-id="769f4-155">이제 샘플 데이터로 [개발][develop], [로드][load] 또는 [마이그레이션][migrate]할 준비 시간을 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="769f4-155">Now that we've given you some time to warm up with the sample data, see how to [develop][develop], [load][load], or [migrate][migrate].</span></span> <span data-ttu-id="769f4-156">또는 [Power BI 웹 사이트][Power BI website]를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="769f4-156">Or take a look at the [Power BI website][Power BI website].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-find-database.png
[2]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-button.png
[3]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-connect-to-azure.png
[4]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-sign-in.png
[5]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-open-adventureworks.png
[6]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-aggregatesales.png
[7]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-map.png
[8]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-chooseaxis.png
[9]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-bar.png
[10]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-prepare-line.png
[11]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-line.png
[12]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-save.png

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[connecting to SQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
