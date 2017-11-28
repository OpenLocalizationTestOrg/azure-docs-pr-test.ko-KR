---
title: "Power BI Microsoft Azure를 사용 하 여 SQL 데이터 웨어하우스 데이터 aaaVisualize"
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
ms.openlocfilehash: 0425cf5abe7bc001b2a41df4d09bf5f2e42527e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-data-with-power-bi"></a><span data-ttu-id="c9bee-103">Power BI를 사용하여 데이터 시각화</span><span class="sxs-lookup"><span data-stu-id="c9bee-103">Visualize data with Power BI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c9bee-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="c9bee-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="c9bee-105">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="c9bee-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="c9bee-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c9bee-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="c9bee-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="c9bee-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="c9bee-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="c9bee-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="c9bee-109">이 자습서에서는 어떻게 toouse Power BI tooconnect tooSQL 데이터 웨어하우스를 몇 가지 기본 시각화를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-109">This tutorial shows you how toouse Power BI tooconnect tooSQL Data Warehouse and create a few basic visualizations.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c9bee-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c9bee-110">Prerequisites</span></span>
<span data-ttu-id="c9bee-111">이 자습서를 통해 toostep를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-111">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="c9bee-112">SQL 데이터 웨어하우스 hello AdventureWorksDW 데이터베이스와 미리 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-112">A SQL Data Warehouse pre-loaded with hello AdventureWorksDW database.</span></span> <span data-ttu-id="c9bee-113">tooprovision이,이 참조 [SQL 데이터 웨어하우스를 만들] [ Create a SQL Data Warehouse] tooload hello 샘플 데이터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-113">tooprovision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose tooload hello sample data.</span></span> <span data-ttu-id="c9bee-114">데이터 웨어하우스는 있지만 샘플 데이터가 없는 경우 [샘플 데이터를 수동으로 로드][load sample data manually]할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-114">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-connect-tooyour-database"></a><span data-ttu-id="c9bee-115">1. Tooyour 데이터베이스 연결</span><span class="sxs-lookup"><span data-stu-id="c9bee-115">1. Connect tooyour database</span></span>
<span data-ttu-id="c9bee-116">Power BI tooopen tooyour AdventureWorksDW 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-116">tooopen Power BI and connect tooyour AdventureWorksDW database:</span></span>

1. <span data-ttu-id="c9bee-117">Hello에 로그인 [Azure 포털][Azure portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-117">Sign into hello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="c9bee-118">**SQL 데이터베이스** 를 클릭하고 AdventureWorks SQL 데이터 웨어하우스 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-118">Click **SQL databases** and choose your AdventureWorks SQL Data Warehouse database.</span></span>
   
    ![데이터베이스 찾기][1]
3. <span data-ttu-id="c9bee-120">Hello 'Power BI에서 열기' 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-120">Click hello 'Open in Power BI' button.</span></span>
   
    ![Power BI 단추][2]
4. <span data-ttu-id="c9bee-122">이제 데이터베이스 웹 주소를 표시 하는 hello SQL 데이터 웨어하우스 연결 페이지를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-122">You should now see hello SQL Data Warehouse connection page displaying your database web address.</span></span> <span data-ttu-id="c9bee-123">다음을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-123">Click next.</span></span>
   
    ![Power BI 연결][3]
5. <span data-ttu-id="c9bee-125">Azure SQL server 사용자 이름 및 암호를 입력 하 고 완전히 연결 된 tooyour SQL 데이터 웨어하우스 데이터베이스 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-125">Enter your Azure SQL server username and password and you will be fully connected tooyour SQL Data Warehouse database.</span></span>
   
    ![Power BI 로그인][4]
6. <span data-ttu-id="c9bee-127">Power BI에 로그인 하면 hello 왼쪽 블레이드에서 hello AdventureWorksDW 데이터 집합을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-127">Once you have signed into Power BI, click hello AdventureWorksDW dataset on hello left blade.</span></span> <span data-ttu-id="c9bee-128">Hello 데이터베이스를 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-128">This will open hello database.</span></span>
   
    ![Power BI AdventureWorksDW 열기][5]

## <a name="2-create-a-report"></a><span data-ttu-id="c9bee-130">2. 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="c9bee-130">2. Create a report</span></span>
<span data-ttu-id="c9bee-131">사용자는 이제 준비 toouse Power BI tooanalyze AdventureWorksDW 예제 데이터.</span><span class="sxs-lookup"><span data-stu-id="c9bee-131">You are now ready toouse Power BI tooanalyze your AdventureWorksDW sample data.</span></span> <span data-ttu-id="c9bee-132">tooperform hello 분석 AdventureWorksDW에 AggregateSales 라는 보기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-132">tooperform hello analysis, AdventureWorksDW has a view called AggregateSales.</span></span> <span data-ttu-id="c9bee-133">이 보기에는 hello 회사의 hello 판매를 분석 하는 것에 대 한 주요 메트릭 hello 중 몇 가지 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-133">This view contains a few of hello key metrics for analyzing hello sales of hello company.</span></span>

1. <span data-ttu-id="c9bee-134">toocreate hello 오른쪽 필드 창에서 toopostal 코드에 따라 판매 금액의 맵을 클릭 hello AggregateSales 보기 tooexpand 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-134">toocreate a map of sales amount according toopostal code, in hello right-hand fields pane, click hello AggregateSales view tooexpand it.</span></span> <span data-ttu-id="c9bee-135">Hello PostalCode 및 SalesAmount 열 tooselect 클릭으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-135">Click hello PostalCode and SalesAmount columns tooselect them.</span></span>
   
    ![Power BI AggregateSales 선택][6]
   
    <span data-ttu-id="c9bee-137">Power BI는 이를 지리적 데이터로 자동으로 인식하고 지도에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-137">Power BI automatically recognizes this is geographic data and put it in a map for you.</span></span>
   
    ![Power BI 맵][7]
2. <span data-ttu-id="c9bee-139">이 단계에서는 고객 수익당 매출액을 보여주는 막대 그래프를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-139">This step creates a bar graph that shows amount of sales per customer income.</span></span> <span data-ttu-id="c9bee-140">toocreate이 이동 toohello AggregateSales 보기를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-140">toocreate this go toohello expanded AggregateSales view.</span></span> <span data-ttu-id="c9bee-141">Hello SalesAmount 필드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-141">Click hello SalesAmount field.</span></span> <span data-ttu-id="c9bee-142">Hello 고객의 소득을 필드 toohello 왼쪽 끌어서 축에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-142">Drag hello Customer Income field toohello left and drop it into Axis.</span></span>
   
    ![Power BI 축 선택][8]
   
    <span data-ttu-id="c9bee-144">Hello 가로 막대형 차트 hello 왼쪽 위로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-144">We moved hello bar chart over hello left.</span></span>
   
    ![Power BI 막대형][9]
3. <span data-ttu-id="c9bee-146">이 단계에서는 주문 날짜당 판매 금액을 보여주는 꺽은선형 차트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-146">This step creates a line chart that shows sales amount per order date.</span></span> <span data-ttu-id="c9bee-147">toocreate이 이동 toohello AggregateSales 보기를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-147">toocreate this go toohello expanded AggregateSales view.</span></span> <span data-ttu-id="c9bee-148">SalesAmount 및 OrderDate를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-148">Click SalesAmount and OrderDate.</span></span> <span data-ttu-id="c9bee-149">Hello 시각화 열에서 hello 꺾은선형 차트 아이콘;를 클릭 합니다. hello 시각화에서 두 번째 줄에 hello 첫 번째 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-149">In hello Visualizations column click hello Line Chart icon; this is hello first icon in hello second line under visualizations.</span></span>
   
    ![Power BI 꺾은선형 차트 선택][10]
   
    <span data-ttu-id="c9bee-151">Hello 데이터의 세 가지 각기 다른 시각화를 표시 하는 보고서를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-151">You now have a report that shows three different visualizations of hello data.</span></span>
   
    ![Power BI 꺾은선형][11]

<span data-ttu-id="c9bee-153">언제든지 **파일**을 클릭하고 **저장**을 선택하여 진행 상황을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-153">You can save your progress at any time by clicking **File** and selecting **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9bee-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c9bee-154">Next steps</span></span>
<span data-ttu-id="c9bee-155">지금 म 부여한 하면 일부 시간 toowarm hello 샘플 데이터로 하는 방법을 너무 참조[개발][develop], [로드][load], 또는 [ 마이그레이션][migrate]합니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-155">Now that we've given you some time toowarm up with hello sample data, see how too[develop][develop], [load][load], or [migrate][migrate].</span></span> <span data-ttu-id="c9bee-156">Hello 살펴보세요 또는 [Power BI 웹사이트][Power BI website]합니다.</span><span class="sxs-lookup"><span data-stu-id="c9bee-156">Or take a look at hello [Power BI website][Power BI website].</span></span>

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
[connecting tooSQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
