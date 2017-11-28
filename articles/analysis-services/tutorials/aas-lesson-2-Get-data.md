---
<span data-ttu-id="6ff59-101">제목: aaa "2 Azure Analysis Services 자습서 단원: 데이터 가져오기 | Microsoft Docs "설명: 방식에서 데이터 가져오기 및 tooget hello Azure Analysis Services tutorial 프로젝트에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-101">title: aaa"Azure Analysis Services tutorial lesson 2: Get data | Microsoft Docs" description: Describes how tooget and import data in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="6ff59-102">서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '</span><span class="sxs-lookup"><span data-stu-id="6ff59-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="6ff59-103">ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="6ff59-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---

# <a name="lesson-2-get-data"></a><span data-ttu-id="6ff59-104">단원 2: 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="6ff59-104">Lesson 2: Get data</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="6ff59-105">이 단원에서는 데이터 가져오기 SSDT tooconnect toohello AdventureWorksDW2014 예제 데이터베이스, 데이터 선택, 미리 보기 및 필터를 사용 하 여 한 다음 모델 작업 영역으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-105">In this lesson, you use Get Data in SSDT tooconnect toohello AdventureWorksDW2014 sample database, select data, preview and filter, and then import into your model workspace.</span></span>  
  
<span data-ttu-id="6ff59-106">데이터 가져오기를 사용하여 Azure SQL Database, Oracle, Sybase, OData Feed, Teradata, 파일 등 다양한 원본에서 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-106">By using Get Data, you can import data from a wide variety of sources: Azure SQL Database, Oracle, Sybase, OData Feed, Teradata, files and more.</span></span> <span data-ttu-id="6ff59-107">파워 쿼리 M 수식을 사용하여 데이터를 쿼리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-107">Data can also be queried using a Power Query M formula expression.</span></span>
  
<span data-ttu-id="6ff59-108">이 단원에서는 시간 toocomplete 예상: **10 분**</span><span class="sxs-lookup"><span data-stu-id="6ff59-108">Estimated time toocomplete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="6ff59-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6ff59-109">Prerequisites</span></span>  
<span data-ttu-id="6ff59-110">이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="6ff59-111">이 단원에서는 hello 작업을 수행 하기 전에 완료 해야 hello 이전 단원: [1 단원: 새 테이블 형식 모델 프로젝트 만들기](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-111">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 1: Create a new tabular model project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
## <a name="create-a-connection"></a><span data-ttu-id="6ff59-112">연결 만들기</span><span class="sxs-lookup"><span data-stu-id="6ff59-112">Create a connection</span></span>  
  
#### <a name="toocreate-a-connection-toohello-adventureworksdw2014-database"></a><span data-ttu-id="6ff59-113">toocreate 연결 toohello AdventureWorksDW2014 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="6ff59-113">toocreate a connection toohello AdventureWorksDW2014 database</span></span>  
  
1.  <span data-ttu-id="6ff59-114">테이블 형식 모델 탐색기에서 **데이터 원본** > **데이터 원본에서 가져오기**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-114">In Tabular Model Explorer, right-click **Data Sources** > **Import from Data Source**.</span></span>  
  
    <span data-ttu-id="6ff59-115">데이터 가져오기에서 연결 tooa 데이터 소스를 안내해 주는 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-115">This launches Get Data, which guides you through connecting tooa data source.</span></span> <span data-ttu-id="6ff59-116">테이블 형식 모델 탐색기에 표시 되지 않는 경우 **솔루션 탐색기**를 두 번 클릭 **Model.bim** hello 디자이너에서 tooopen hello 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-116">If you don't see Tabular Model Explorer, in **Solution Explorer**, double-click **Model.bim** tooopen hello model in hello designer.</span></span> 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  <span data-ttu-id="6ff59-118">데이터 가져오기에서 **데이터베이스** > **SQL Server 데이터베이스** > **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-118">In Get Data, click **Database** > **SQL Server Database** > **Connect**.</span></span>  
  
3.  <span data-ttu-id="6ff59-119">Hello에 **SQL Server 데이터베이스** 대화에 **서버**, hello AdventureWorksDW2014 데이터베이스를 설치한 hello 서버 hello 이름을 입력 하 고 클릭 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-119">In hello **SQL Server Database** dialog, in **Server**, type hello name of hello server where you installed hello AdventureWorksDW2014 database, and then click **Connect**.</span></span>  

4.  <span data-ttu-id="6ff59-120">메시지가 표시 되 면 Analysis Services를 가져오고 데이터를 처리할 때 tooconnect toohello 데이터 원본을 사용 하 여 toospecify hello 자격 증명이 필요 tooenter 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-120">When prompted tooenter credentials, you need toospecify hello credentials Analysis Services uses tooconnect toohello data source when importing and processing data.</span></span> <span data-ttu-id="6ff59-121">**가장 모드**에서 **계정 가장**을 선택한 다음 자격 증명을 입력하고 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-121">In **Impersonation Mode**, select **Impersonate Account**, then enter credentials, and then click **Connect**.</span></span> <span data-ttu-id="6ff59-122">계정을 사용 하면 hello 암호 만료 되지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-122">It's recommended you use an account where hello password doesn't expire.</span></span>

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > <span data-ttu-id="6ff59-124">Windows 사용자 계정 및 암호를 사용 하 여 hello 연결 tooa 데이터 원본의 가장 안전한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-124">Using a Windows user account and password provides hello most secure method of connecting tooa data source.</span></span>
  
5.  <span data-ttu-id="6ff59-125">탐색 창의 hello 선택 **AdventureWorksDW2014** 데이터베이스를 선택한 다음 클릭 **확인**합니다. Hello 연결 toohello 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-125">In Navigator, select hello **AdventureWorksDW2014** database, and then click **OK**.This creates hello connection toohello database.</span></span> 
  
6.  <span data-ttu-id="6ff59-126">탐색 창에서 선택 hello 다음 표는 hello에 대 한 확인란: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**,  **DimProductCategory**, **DimProductSubcategory**, 및 **FactInternetSales**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-126">In Navigator, select hello check box for hello following tables: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales**.</span></span>  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
<span data-ttu-id="6ff59-128">확인을 클릭하면 쿼리 편집기가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-128">After you click OK, Query Editor opens.</span></span> <span data-ttu-id="6ff59-129">Hello 다음 섹션에서 원하는 tooimport hello 데이터만 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-129">In hello next section, you select only hello data you want tooimport.</span></span>

  
## <a name="filter-hello-table-data"></a><span data-ttu-id="6ff59-130">Hello 테이블 데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="6ff59-130">Filter hello table data</span></span>  
<span data-ttu-id="6ff59-131">Hello AdventureWorksDW2014 예제 데이터베이스의 테이블에는 모델에 필요한 tooinclude 없는 데이터를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-131">Tables in hello AdventureWorksDW2014 sample database have data that isn't necessary tooinclude in your model.</span></span> <span data-ttu-id="6ff59-132">가능 하면 원하는 toofilter hello 모델에 사용 되는 불필요 한 데이터 toosave 메모리 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-132">When possible, you want toofilter out unnecessary data toosave in-memory space used by hello model.</span></span> <span data-ttu-id="6ff59-133">하지 가져온 hello 작업 영역 데이터베이스 또는 hello model 데이터베이스에 배포 된 후 되므로 일부 hello 테이블의에서 열을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-133">You filter out some of hello columns from tables so they're not imported into hello workspace database, or hello model database after it has been deployed.</span></span> 
  
#### <a name="toofilter-hello-table-data-before-importing"></a><span data-ttu-id="6ff59-134">toofilter hello 테이블 데이터를 가져오기 전에</span><span class="sxs-lookup"><span data-stu-id="6ff59-134">toofilter hello table data before importing</span></span>  
  
1.  <span data-ttu-id="6ff59-135">쿼리 편집기에서 선택 hello **DimCustomer** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-135">In Query Editor, select hello **DimCustomer** table.</span></span> <span data-ttu-id="6ff59-136">Hello 데이터 원본 (AdventureWorksDWQ2014 샘플 데이터베이스)에 hello DimCustomer 테이블의 뷰가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-136">A view of hello DimCustomer table at hello datasource (your AdventureWorksDWQ2014 sample database) appears.</span></span> 
  
2.  <span data-ttu-id="6ff59-137">**SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**을 다중 선택(Ctrl + 클릭)한 후 마우스 오른쪽 단추를 클릭한 후 **열 제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-137">Multi-select (Ctrl + click) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, then right-click, and then click **Remove Columns**.</span></span> 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    <span data-ttu-id="6ff59-139">없기 때문에 이러한 열에 대 한 hello 값 관련 tooInternet 판매 분석 아닌 없습니다 필요 tooimport 이러한 열입니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-139">Since hello values for these columns are not relevant tooInternet sales analysis, there is no need tooimport these columns.</span></span> <span data-ttu-id="6ff59-140">불필요한 열을 제거하여 모델을 더 작고 효율적으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-140">Eliminating unnecessary columns makes your model smaller and more efficient.</span></span>  
  
4.  <span data-ttu-id="6ff59-141">Hello 남아 있는 각 테이블의 열을 다음 hello를 제거 하 여 테이블을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-141">Filter hello remaining tables by removing hello following columns in each table:</span></span>  
    
    <span data-ttu-id="6ff59-142">**DimDate**</span><span class="sxs-lookup"><span data-stu-id="6ff59-142">**DimDate**</span></span>
    
      |<span data-ttu-id="6ff59-143">열</span><span class="sxs-lookup"><span data-stu-id="6ff59-143">Column</span></span>|  
      |--------|  
      |<span data-ttu-id="6ff59-144">DateKey</span><span class="sxs-lookup"><span data-stu-id="6ff59-144">DateKey</span></span>|  
      |<span data-ttu-id="6ff59-145">**SpanishDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="6ff59-145">**SpanishDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="6ff59-146">**FrenchDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="6ff59-146">**FrenchDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="6ff59-147">**SpanishMonthName**</span><span class="sxs-lookup"><span data-stu-id="6ff59-147">**SpanishMonthName**</span></span>|  
      |<span data-ttu-id="6ff59-148">**FrenchMonthName**</span><span class="sxs-lookup"><span data-stu-id="6ff59-148">**FrenchMonthName**</span></span>|  
  
    <span data-ttu-id="6ff59-149">**DimGeography**</span><span class="sxs-lookup"><span data-stu-id="6ff59-149">**DimGeography**</span></span>
  
      |<span data-ttu-id="6ff59-150">열</span><span class="sxs-lookup"><span data-stu-id="6ff59-150">Column</span></span>|  
      |-------------|  
      |<span data-ttu-id="6ff59-151">**SpanishCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="6ff59-151">**SpanishCountryRegionName**</span></span>|  
      |<span data-ttu-id="6ff59-152">**FrenchCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="6ff59-152">**FrenchCountryRegionName**</span></span>|  
      |<span data-ttu-id="6ff59-153">**IpAddressLocator**</span><span class="sxs-lookup"><span data-stu-id="6ff59-153">**IpAddressLocator**</span></span>|  
  
    <span data-ttu-id="6ff59-154">**DimProduct**</span><span class="sxs-lookup"><span data-stu-id="6ff59-154">**DimProduct**</span></span>
  
      |<span data-ttu-id="6ff59-155">열</span><span class="sxs-lookup"><span data-stu-id="6ff59-155">Column</span></span>|  
      |-----------|  
      |<span data-ttu-id="6ff59-156">**SpanishProductName**</span><span class="sxs-lookup"><span data-stu-id="6ff59-156">**SpanishProductName**</span></span>|  
      |<span data-ttu-id="6ff59-157">**FrenchProductName**</span><span class="sxs-lookup"><span data-stu-id="6ff59-157">**FrenchProductName**</span></span>|  
      |<span data-ttu-id="6ff59-158">**FrenchDescription**</span><span class="sxs-lookup"><span data-stu-id="6ff59-158">**FrenchDescription**</span></span>|  
      |<span data-ttu-id="6ff59-159">**ChineseDescription**</span><span class="sxs-lookup"><span data-stu-id="6ff59-159">**ChineseDescription**</span></span>|  
      |<span data-ttu-id="6ff59-160">**ArabicDescription**</span><span class="sxs-lookup"><span data-stu-id="6ff59-160">**ArabicDescription**</span></span>|  
      |<span data-ttu-id="6ff59-161">**HebrewDescription**</span><span class="sxs-lookup"><span data-stu-id="6ff59-161">**HebrewDescription**</span></span>|  
      |<span data-ttu-id="6ff59-162">**ThaiDescription**</span><span class="sxs-lookup"><span data-stu-id="6ff59-162">**ThaiDescription**</span></span>|  
      |<span data-ttu-id="6ff59-163">**GermanDescription**</span><span class="sxs-lookup"><span data-stu-id="6ff59-163">**GermanDescription**</span></span>|  
      |<span data-ttu-id="6ff59-164">**JapaneseDescription**</span><span class="sxs-lookup"><span data-stu-id="6ff59-164">**JapaneseDescription**</span></span>|  
      |<span data-ttu-id="6ff59-165">**TurkishDescription**</span><span class="sxs-lookup"><span data-stu-id="6ff59-165">**TurkishDescription**</span></span>|  
  
    <span data-ttu-id="6ff59-166">**DimProductCategory**</span><span class="sxs-lookup"><span data-stu-id="6ff59-166">**DimProductCategory**</span></span>
  
      |<span data-ttu-id="6ff59-167">열</span><span class="sxs-lookup"><span data-stu-id="6ff59-167">Column</span></span>|  
      |--------------------|  
      |<span data-ttu-id="6ff59-168">**SpanishProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="6ff59-168">**SpanishProductCategoryName**</span></span>|  
      |<span data-ttu-id="6ff59-169">**FrenchProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="6ff59-169">**FrenchProductCategoryName**</span></span>|  
  
    <span data-ttu-id="6ff59-170">**DimProductSubcategory**</span><span class="sxs-lookup"><span data-stu-id="6ff59-170">**DimProductSubcategory**</span></span>
  
      |<span data-ttu-id="6ff59-171">열</span><span class="sxs-lookup"><span data-stu-id="6ff59-171">Column</span></span>|  
      |-----------------------|  
      |<span data-ttu-id="6ff59-172">**SpanishProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="6ff59-172">**SpanishProductSubcategoryName**</span></span>|  
      |<span data-ttu-id="6ff59-173">**FrenchProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="6ff59-173">**FrenchProductSubcategoryName**</span></span>|  
  
    <span data-ttu-id="6ff59-174">**FactInternetSales**</span><span class="sxs-lookup"><span data-stu-id="6ff59-174">**FactInternetSales**</span></span>
  
      |<span data-ttu-id="6ff59-175">열</span><span class="sxs-lookup"><span data-stu-id="6ff59-175">Column</span></span>|  
      |------------------|  
      |<span data-ttu-id="6ff59-176">**OrderDateKey**</span><span class="sxs-lookup"><span data-stu-id="6ff59-176">**OrderDateKey**</span></span>|  
      |<span data-ttu-id="6ff59-177">**DueDateKey**</span><span class="sxs-lookup"><span data-stu-id="6ff59-177">**DueDateKey**</span></span>|  
      |<span data-ttu-id="6ff59-178">**ShipDateKey**</span><span class="sxs-lookup"><span data-stu-id="6ff59-178">**ShipDateKey**</span></span>|   
  
## <span data-ttu-id="6ff59-179"><a name="Import"></a>Hello 선택한 테이블 및 열 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="6ff59-179"><a name="Import"></a>Import hello selected tables and column data</span></span>  
<span data-ttu-id="6ff59-180">미리 보기 하 고 불필요 한 데이터를 필터링 했으므로 hello 나머지 않을 hello 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-180">Now that you've previewed and filtered out unnecessary data, you can import hello rest of hello data you do want.</span></span> <span data-ttu-id="6ff59-181">hello 마법사 hello 테이블 데이터를 함께 테이블 간 관계를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-181">hello wizard imports hello table data along with any relationships between tables.</span></span> <span data-ttu-id="6ff59-182">Hello 모델에서 만들어진 새 테이블 및 열 및 필터링 하는 데이터를 가져올 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-182">New tables and columns are created in hello model and data that you filtered out is not be imported.</span></span>  
  
#### <a name="tooimport-hello-selected-tables-and-column-data"></a><span data-ttu-id="6ff59-183">테이블 및 열 데이터 tooimport hello 선택</span><span class="sxs-lookup"><span data-stu-id="6ff59-183">tooimport hello selected tables and column data</span></span>  
  
1.  <span data-ttu-id="6ff59-184">선택 항목을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-184">Review your selections.</span></span> <span data-ttu-id="6ff59-185">잘못된 항목이 없으면, **가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-185">If everything looks okay, click **Import**.</span></span> <span data-ttu-id="6ff59-186">hello 데이터 처리 대화 상자에는 hello 상태를 작업 영역 데이터베이스에 사용자 데이터 원본에서 가져올 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-186">hello Data Processing dialog shows hello status of data being imported from your datasource into your workspace database.</span></span>
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  <span data-ttu-id="6ff59-188">**닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-188">Click **Close**.</span></span>  

  
## <a name="save-your-model-project"></a><span data-ttu-id="6ff59-189">모델 프로젝트를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-189">Save your model project</span></span>  
<span data-ttu-id="6ff59-190">toofrequently 모델 프로젝트를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-190">It's important toofrequently save your model project.</span></span>  
  
#### <a name="toosave-hello-model-project"></a><span data-ttu-id="6ff59-191">toosave hello 모델 프로젝트</span><span class="sxs-lookup"><span data-stu-id="6ff59-191">toosave hello model project</span></span>  
  
-   <span data-ttu-id="6ff59-192">**파일** > **모두 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff59-192">Click **File** > **Save All**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="6ff59-193">다음 작업</span><span class="sxs-lookup"><span data-stu-id="6ff59-193">What's next?</span></span>
<span data-ttu-id="6ff59-194">[단원 3: 날짜 테이블로 표시](../tutorials/aas-lesson-3-mark-as-date-table.md)</span><span class="sxs-lookup"><span data-stu-id="6ff59-194">[Lesson 3: Mark as Date Table](../tutorials/aas-lesson-3-mark-as-date-table.md).</span></span>

  
  
