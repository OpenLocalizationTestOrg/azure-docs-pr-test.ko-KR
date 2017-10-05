---
title: "Azure Analysis Services 자습서 단원 2: 데이터 가져오기 | Microsoft Docs"
description: "Azure Analysis Services 자습서 프로젝트에서 데이터를 가져오는 방법을 설명합니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: e77de4b9a74b528fa8a7ce86424fc14628b2cacc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-2-get-data"></a><span data-ttu-id="7fb86-103">단원 2: 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="7fb86-103">Lesson 2: Get data</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="7fb86-104">이 단원에서는 SSDT의 데이터 가져오기를 사용하여 AdventureWorksDW2014 예제 데이터베이스에 연결하고 데이터를 선택하며, 미리 보기 및 필터를 수행한 후 모델 작업 영역으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-104">In this lesson, you use Get Data in SSDT to connect to the AdventureWorksDW2014 sample database, select data, preview and filter, and then import into your model workspace.</span></span>  
  
<span data-ttu-id="7fb86-105">데이터 가져오기를 사용하여 Azure SQL Database, Oracle, Sybase, OData Feed, Teradata, 파일 등 다양한 원본에서 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-105">By using Get Data, you can import data from a wide variety of sources: Azure SQL Database, Oracle, Sybase, OData Feed, Teradata, files and more.</span></span> <span data-ttu-id="7fb86-106">파워 쿼리 M 수식을 사용하여 데이터를 쿼리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-106">Data can also be queried using a Power Query M formula expression.</span></span>
  
<span data-ttu-id="7fb86-107">이 단원을 완료하기 위한 예상 시간: **10분**</span><span class="sxs-lookup"><span data-stu-id="7fb86-107">Estimated time to complete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="7fb86-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7fb86-108">Prerequisites</span></span>  
<span data-ttu-id="7fb86-109">이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-109">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="7fb86-110">이 단원의 작업을 수행하기 전에 이전 단원인 [단원 1: 새 테이블 형식 모델 프로젝트 만들기](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-110">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 1: Create a new tabular model project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
## <a name="create-a-connection"></a><span data-ttu-id="7fb86-111">연결 만들기</span><span class="sxs-lookup"><span data-stu-id="7fb86-111">Create a connection</span></span>  
  
#### <a name="to-create-a-connection-to-the-adventureworksdw2014-database"></a><span data-ttu-id="7fb86-112">AdventureWorksDW2014 데이터베이스에 대한 연결을 만들려면</span><span class="sxs-lookup"><span data-stu-id="7fb86-112">To create a connection to the AdventureWorksDW2014 database</span></span>  
  
1.  <span data-ttu-id="7fb86-113">테이블 형식 모델 탐색기에서 **데이터 원본** > **데이터 원본에서 가져오기**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-113">In Tabular Model Explorer, right-click **Data Sources** > **Import from Data Source**.</span></span>  
  
    <span data-ttu-id="7fb86-114">그러면 데이터 가져오기가 시작되고 데이터 원본에 연결하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-114">This launches Get Data, which guides you through connecting to a data source.</span></span> <span data-ttu-id="7fb86-115">테이블 형식 모델 탐색기가 표시되지 않으면 **솔루션 탐색기**에서 **Model.bim**을 두 번 클릭하여 디자이너에서 모델을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-115">If you don't see Tabular Model Explorer, in **Solution Explorer**, double-click **Model.bim** to open the model in the designer.</span></span> 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  <span data-ttu-id="7fb86-117">데이터 가져오기에서 **데이터베이스** > **SQL Server 데이터베이스** > **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-117">In Get Data, click **Database** > **SQL Server Database** > **Connect**.</span></span>  
  
3.  <span data-ttu-id="7fb86-118">**SQL Server 데이터베이스** 대화 상자의 **서버**에서 AdventureWorksDW2014 데이터베이스를 설치한 서버 이름을 입력한 후 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-118">In the **SQL Server Database** dialog, in **Server**, type the name of the server where you installed the AdventureWorksDW2014 database, and then click **Connect**.</span></span>  

4.  <span data-ttu-id="7fb86-119">자격 증명을 입력하라는 메시지가 표시되면 데이터를 가져오고 처리할 때 Analysis Services가 데이터 원본에 연결하는 데 사용할 자격 증명을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-119">When prompted to enter credentials, you need to specify the credentials Analysis Services uses to connect to the data source when importing and processing data.</span></span> <span data-ttu-id="7fb86-120">**가장 모드**에서 **계정 가장**을 선택한 다음 자격 증명을 입력하고 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-120">In **Impersonation Mode**, select **Impersonate Account**, then enter credentials, and then click **Connect**.</span></span> <span data-ttu-id="7fb86-121">암호 만료되지 않은 계정을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-121">It's recommended you use an account where the password doesn't expire.</span></span>

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > <span data-ttu-id="7fb86-123">Windows 사용자 계정 및 암호를 사용하면 데이터 원본에 연결하는 가장 안전한 방법이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-123">Using a Windows user account and password provides the most secure method of connecting to a data source.</span></span>
  
5.  <span data-ttu-id="7fb86-124">탐색기에서 **AdventureWorksDW2014** 데이터베이스를 선택한 다음 **확인**을 클릭합니다. 그러면 데이터베이스에 대한 연결이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-124">In Navigator, select the **AdventureWorksDW2014** database, and then click **OK**.This creates the connection to the database.</span></span> 
  
6.  <span data-ttu-id="7fb86-125">탐색기에서 다음 테이블에 대한 확인란을 선택합니다. **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory** 및 **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="7fb86-125">In Navigator, select the check box for the following tables: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales**.</span></span>  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
<span data-ttu-id="7fb86-127">확인을 클릭하면 쿼리 편집기가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-127">After you click OK, Query Editor opens.</span></span> <span data-ttu-id="7fb86-128">다음 섹션에서 가져오려는 데이터만 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-128">In the next section, you select only the data you want to import.</span></span>

  
## <a name="filter-the-table-data"></a><span data-ttu-id="7fb86-129">테이블 데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="7fb86-129">Filter the table data</span></span>  
<span data-ttu-id="7fb86-130">AdventureWorksDW2014 예제 데이터베이스의 테이블에는 모델에 포함할 필요가 없는 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-130">Tables in the AdventureWorksDW2014 sample database have data that isn't necessary to include in your model.</span></span> <span data-ttu-id="7fb86-131">가능하면, 모델에 사용된 메모리 내 공간을 절약하기 위해 불필요한 데이터를 필터링하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-131">When possible, you want to filter out unnecessary data to save in-memory space used by the model.</span></span> <span data-ttu-id="7fb86-132">테이블에서 열의 일부를 필터링하여 작업 영역 데이터베이스나 모델 데이터베이스(배포 후)로 가져오지 못하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-132">You filter out some of the columns from tables so they're not imported into the workspace database, or the model database after it has been deployed.</span></span> 
  
#### <a name="to-filter-the-table-data-before-importing"></a><span data-ttu-id="7fb86-133">가져오기 전에 테이블 데이터를 필터링하려면</span><span class="sxs-lookup"><span data-stu-id="7fb86-133">To filter the table data before importing</span></span>  
  
1.  <span data-ttu-id="7fb86-134">쿼리 편집기에서 **DimCustomer** 테이블을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-134">In Query Editor, select the **DimCustomer** table.</span></span> <span data-ttu-id="7fb86-135">데이터 원본(AdventureWorksDWQ2014 예제 데이터베이스)에서 DimCustomer 테이블 뷰가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-135">A view of the DimCustomer table at the datasource (your AdventureWorksDWQ2014 sample database) appears.</span></span> 
  
2.  <span data-ttu-id="7fb86-136">**SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**을 다중 선택(Ctrl + 클릭)한 후 마우스 오른쪽 단추를 클릭한 후 **열 제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-136">Multi-select (Ctrl + click) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, then right-click, and then click **Remove Columns**.</span></span> 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    <span data-ttu-id="7fb86-138">이러한 열에 대한 값은 인터넷 판매 분석과 관련이 없으므로 이러한 열을 가져올 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-138">Since the values for these columns are not relevant to Internet sales analysis, there is no need to import these columns.</span></span> <span data-ttu-id="7fb86-139">불필요한 열을 제거하여 모델을 더 작고 효율적으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-139">Eliminating unnecessary columns makes your model smaller and more efficient.</span></span>  
  
4.  <span data-ttu-id="7fb86-140">각 테이블에서 다음 열을 제거하여 나머지 테이블을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-140">Filter the remaining tables by removing the following columns in each table:</span></span>  
    
    <span data-ttu-id="7fb86-141">**DimDate**</span><span class="sxs-lookup"><span data-stu-id="7fb86-141">**DimDate**</span></span>
    
      |<span data-ttu-id="7fb86-142">열</span><span class="sxs-lookup"><span data-stu-id="7fb86-142">Column</span></span>|  
      |--------|  
      |<span data-ttu-id="7fb86-143">DateKey</span><span class="sxs-lookup"><span data-stu-id="7fb86-143">DateKey</span></span>|  
      |<span data-ttu-id="7fb86-144">**SpanishDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="7fb86-144">**SpanishDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="7fb86-145">**FrenchDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="7fb86-145">**FrenchDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="7fb86-146">**SpanishMonthName**</span><span class="sxs-lookup"><span data-stu-id="7fb86-146">**SpanishMonthName**</span></span>|  
      |<span data-ttu-id="7fb86-147">**FrenchMonthName**</span><span class="sxs-lookup"><span data-stu-id="7fb86-147">**FrenchMonthName**</span></span>|  
  
    <span data-ttu-id="7fb86-148">**DimGeography**</span><span class="sxs-lookup"><span data-stu-id="7fb86-148">**DimGeography**</span></span>
  
      |<span data-ttu-id="7fb86-149">열</span><span class="sxs-lookup"><span data-stu-id="7fb86-149">Column</span></span>|  
      |-------------|  
      |<span data-ttu-id="7fb86-150">**SpanishCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="7fb86-150">**SpanishCountryRegionName**</span></span>|  
      |<span data-ttu-id="7fb86-151">**FrenchCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="7fb86-151">**FrenchCountryRegionName**</span></span>|  
      |<span data-ttu-id="7fb86-152">**IpAddressLocator**</span><span class="sxs-lookup"><span data-stu-id="7fb86-152">**IpAddressLocator**</span></span>|  
  
    <span data-ttu-id="7fb86-153">**DimProduct**</span><span class="sxs-lookup"><span data-stu-id="7fb86-153">**DimProduct**</span></span>
  
      |<span data-ttu-id="7fb86-154">열</span><span class="sxs-lookup"><span data-stu-id="7fb86-154">Column</span></span>|  
      |-----------|  
      |<span data-ttu-id="7fb86-155">**SpanishProductName**</span><span class="sxs-lookup"><span data-stu-id="7fb86-155">**SpanishProductName**</span></span>|  
      |<span data-ttu-id="7fb86-156">**FrenchProductName**</span><span class="sxs-lookup"><span data-stu-id="7fb86-156">**FrenchProductName**</span></span>|  
      |<span data-ttu-id="7fb86-157">**FrenchDescription**</span><span class="sxs-lookup"><span data-stu-id="7fb86-157">**FrenchDescription**</span></span>|  
      |<span data-ttu-id="7fb86-158">**ChineseDescription**</span><span class="sxs-lookup"><span data-stu-id="7fb86-158">**ChineseDescription**</span></span>|  
      |<span data-ttu-id="7fb86-159">**ArabicDescription**</span><span class="sxs-lookup"><span data-stu-id="7fb86-159">**ArabicDescription**</span></span>|  
      |<span data-ttu-id="7fb86-160">**HebrewDescription**</span><span class="sxs-lookup"><span data-stu-id="7fb86-160">**HebrewDescription**</span></span>|  
      |<span data-ttu-id="7fb86-161">**ThaiDescription**</span><span class="sxs-lookup"><span data-stu-id="7fb86-161">**ThaiDescription**</span></span>|  
      |<span data-ttu-id="7fb86-162">**GermanDescription**</span><span class="sxs-lookup"><span data-stu-id="7fb86-162">**GermanDescription**</span></span>|  
      |<span data-ttu-id="7fb86-163">**JapaneseDescription**</span><span class="sxs-lookup"><span data-stu-id="7fb86-163">**JapaneseDescription**</span></span>|  
      |<span data-ttu-id="7fb86-164">**TurkishDescription**</span><span class="sxs-lookup"><span data-stu-id="7fb86-164">**TurkishDescription**</span></span>|  
  
    <span data-ttu-id="7fb86-165">**DimProductCategory**</span><span class="sxs-lookup"><span data-stu-id="7fb86-165">**DimProductCategory**</span></span>
  
      |<span data-ttu-id="7fb86-166">열</span><span class="sxs-lookup"><span data-stu-id="7fb86-166">Column</span></span>|  
      |--------------------|  
      |<span data-ttu-id="7fb86-167">**SpanishProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="7fb86-167">**SpanishProductCategoryName**</span></span>|  
      |<span data-ttu-id="7fb86-168">**FrenchProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="7fb86-168">**FrenchProductCategoryName**</span></span>|  
  
    <span data-ttu-id="7fb86-169">**DimProductSubcategory**</span><span class="sxs-lookup"><span data-stu-id="7fb86-169">**DimProductSubcategory**</span></span>
  
      |<span data-ttu-id="7fb86-170">열</span><span class="sxs-lookup"><span data-stu-id="7fb86-170">Column</span></span>|  
      |-----------------------|  
      |<span data-ttu-id="7fb86-171">**SpanishProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="7fb86-171">**SpanishProductSubcategoryName**</span></span>|  
      |<span data-ttu-id="7fb86-172">**FrenchProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="7fb86-172">**FrenchProductSubcategoryName**</span></span>|  
  
    <span data-ttu-id="7fb86-173">**FactInternetSales**</span><span class="sxs-lookup"><span data-stu-id="7fb86-173">**FactInternetSales**</span></span>
  
      |<span data-ttu-id="7fb86-174">열</span><span class="sxs-lookup"><span data-stu-id="7fb86-174">Column</span></span>|  
      |------------------|  
      |<span data-ttu-id="7fb86-175">**OrderDateKey**</span><span class="sxs-lookup"><span data-stu-id="7fb86-175">**OrderDateKey**</span></span>|  
      |<span data-ttu-id="7fb86-176">**DueDateKey**</span><span class="sxs-lookup"><span data-stu-id="7fb86-176">**DueDateKey**</span></span>|  
      |<span data-ttu-id="7fb86-177">**ShipDateKey**</span><span class="sxs-lookup"><span data-stu-id="7fb86-177">**ShipDateKey**</span></span>|   
  
## <span data-ttu-id="7fb86-178"><a name="Import"></a>선택한 테이블 및 열 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="7fb86-178"><a name="Import"></a>Import the selected tables and column data</span></span>  
<span data-ttu-id="7fb86-179">이제 불필요한 데이터를 미리보고 필터링했으며 원하는 나머지 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-179">Now that you've previewed and filtered out unnecessary data, you can import the rest of the data you do want.</span></span> <span data-ttu-id="7fb86-180">마법사가 테이블 간의 관계와 함께 테이블 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-180">The wizard imports the table data along with any relationships between tables.</span></span> <span data-ttu-id="7fb86-181">모델에 새 테이블 및 열이 생성되고 필터링된 데이터는 가져오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-181">New tables and columns are created in the model and data that you filtered out is not be imported.</span></span>  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a><span data-ttu-id="7fb86-182">선택한 테이블 및 열 데이터를 가져오려면</span><span class="sxs-lookup"><span data-stu-id="7fb86-182">To import the selected tables and column data</span></span>  
  
1.  <span data-ttu-id="7fb86-183">선택 항목을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-183">Review your selections.</span></span> <span data-ttu-id="7fb86-184">잘못된 항목이 없으면, **가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-184">If everything looks okay, click **Import**.</span></span> <span data-ttu-id="7fb86-185">데이터 처리 대화 상자에 데이터 원본에서 작업 영역 데이터베이스로 가져온 데이터 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-185">The Data Processing dialog shows the status of data being imported from your datasource into your workspace database.</span></span>
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  <span data-ttu-id="7fb86-187">**닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-187">Click **Close**.</span></span>  

  
## <a name="save-your-model-project"></a><span data-ttu-id="7fb86-188">모델 프로젝트를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-188">Save your model project</span></span>  
<span data-ttu-id="7fb86-189">모델 프로젝트를 자주 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-189">It's important to frequently save your model project.</span></span>  
  
#### <a name="to-save-the-model-project"></a><span data-ttu-id="7fb86-190">모델 프로젝트를 저장하려면</span><span class="sxs-lookup"><span data-stu-id="7fb86-190">To save the model project</span></span>  
  
-   <span data-ttu-id="7fb86-191">**파일** > **모두 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7fb86-191">Click **File** > **Save All**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="7fb86-192">다음 작업</span><span class="sxs-lookup"><span data-stu-id="7fb86-192">What's next?</span></span>
<span data-ttu-id="7fb86-193">[단원 3: 날짜 테이블로 표시](../tutorials/aas-lesson-3-mark-as-date-table.md)</span><span class="sxs-lookup"><span data-stu-id="7fb86-193">[Lesson 3: Mark as Date Table](../tutorials/aas-lesson-3-mark-as-date-table.md).</span></span>

  
  
