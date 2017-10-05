---
title: "Azure Analysis Services 자습서 추가 단원: 동적 보안 | Microsoft Docs"
description: "Azure Analysis Services 자습서의 행 필터를 사용하여 동적 보안을 사용하는 방법에 대해 설명합니다."
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
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 4e97a558ae1a2601b5275a73164b483351f03857
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="supplemental-lesson---dynamic-security"></a><span data-ttu-id="ba541-103">추가 단원 - 동적 보안</span><span class="sxs-lookup"><span data-stu-id="ba541-103">Supplemental lesson - Dynamic security</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="ba541-104">이 추가 단원에서는 동적 보안을 구현하는 추가 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-104">In this supplemental lesson, you create an additional role that implements dynamic security.</span></span> <span data-ttu-id="ba541-105">동적 보안은 현재 로그온한 사용자의 사용자 이름 또는 로그인 ID를 기반으로 행 수준 보안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-105">Dynamic security provides row-level security based on the user name or login id of the user currently logged on.</span></span> 
  
<span data-ttu-id="ba541-106">동적 보안을 구현하려면 모델에 연결하여 모델 개체 및 데이터를 찾아볼 수 있는 사용자의 사용자 이름이 들어있는 모델에 테이블을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-106">To implement dynamic security, you add a table to your model containing the user names of those users that can connect to the model and browse model objects and data.</span></span> <span data-ttu-id="ba541-107">이 자습서를 사용하여 만드는 모델은 Adventure Works의 컨텍스트에 있지만 이 단원을 완료하려면 사용자 고유의 도메인에서 사용자가 포함된 테이블을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-107">The model you create using this tutorial is in the context of Adventure Works; however, to complete this lesson, you must add a table containing users from your own domain.</span></span> <span data-ttu-id="ba541-108">추가된 사용자 이름에 대한 암호는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-108">You do not need the passwords for the user names that are added.</span></span> <span data-ttu-id="ba541-109">사용자 고유 도메인의 작은 사용자 샘플과 함께 EmployeeSecurity 테이블을 만들려면 붙여넣기 기능을 사용하여 Excel 스프레드시트에서 직원 데이터를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-109">To create an EmployeeSecurity table, with a small sample of users from your own domain, you use the Paste feature, pasting employee data from an Excel spreadsheet.</span></span> <span data-ttu-id="ba541-110">실제 시나리오에서는 사용자 이름이 들어있는 테이블이 일반적으로 데이터 원본으로 사용되는 실제 데이터베이스의 테이블입니다(예: 실제 DimEmployee 테이블).</span><span class="sxs-lookup"><span data-stu-id="ba541-110">In a real-world scenario, the table containing user names would typically be a table from an actual database as a data source; for example, a real DimEmployee table.</span></span>  
  
<span data-ttu-id="ba541-111">동적 보안을 구현하려면 두 개의 DAX 함수 즉, [USERNAME 함수(DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f) 및 [LOOKUPVALUE 함수(DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-111">To implement dynamic security, you use two DAX functions: [USERNAME Function (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f) and [LOOKUPVALUE Function (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab).</span></span> <span data-ttu-id="ba541-112">행 필터 수식에 적용된 이러한 함수는 새 역할에 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-112">These functions, applied in a row filter formula, are defined in a new role.</span></span> <span data-ttu-id="ba541-113">LOOKUPVALUE 함수를 사용하여 수식은 EmployeeSecurity 테이블에서 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-113">By using the LOOKUPVALUE function, the formula specifies a value from the EmployeeSecurity table.</span></span> <span data-ttu-id="ba541-114">그런 다음 수식은 이 역할에 속해 있는 로그온한 사용자의 사용자 이름을 지정하는 USERNAME 함수에 해당 값을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-114">The formula then passes that value to the USERNAME function, which specifies the user name of the user logged on belongs to this role.</span></span> <span data-ttu-id="ba541-115">그러면 사용자는 역할의 행 필터에 지정된 데이터만 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-115">The user can then browse only data specified by the role’s row filters.</span></span> <span data-ttu-id="ba541-116">이 시나리오에서는 영업 직원이 자신이 속한 판매 지역의 인터넷 판매 데이터만 찾아볼 수 있도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-116">In this scenario, you specify that sales employees can only browse Internet sales data for the sales territories in which they are a member.</span></span>  
  
<span data-ttu-id="ba541-117">이러한 작업은 이 Adventure Works 테이블 형식 모델 시나리오에는 고유하지만 실제 시나리오에 반드시 적용되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-117">Those tasks that are unique to this Adventure Works tabular model scenario, but would not necessarily apply to a real-world scenario are identified as such.</span></span> <span data-ttu-id="ba541-118">각 작업에는 작업의 목적을 설명하는 추가 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-118">Each task includes additional information describing the purpose of the task.</span></span>  
  
<span data-ttu-id="ba541-119">이 단원을 완료하기 위한 예상 시간: **30분**</span><span class="sxs-lookup"><span data-stu-id="ba541-119">Estimated time to complete this lesson: **30 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="ba541-120">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ba541-120">Prerequisites</span></span>  
<span data-ttu-id="ba541-121">이 추가 단원 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-121">This supplemental lesson topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="ba541-122">이 추가 단원의 작업을 수행하기 전에 이전의 단원을 모두 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-122">Before performing the tasks in this supplemental lesson, you should have completed all previous lessons.</span></span>  
  
## <a name="add-the-dimsalesterritory-table-to-the-aw-internet-sales-tabular-model-project"></a><span data-ttu-id="ba541-123">DimSalesTerritory 테이블을 AW Internet Sales Tabular Model 프로젝트에 추가</span><span class="sxs-lookup"><span data-stu-id="ba541-123">Add the DimSalesTerritory table to the AW Internet Sales Tabular Model Project</span></span>  
<span data-ttu-id="ba541-124">이 Adventure Works 시나리오에 대한 동적 보안을 구현하려면 모델에 두 개의 테이블을 더 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-124">To implement dynamic security for this Adventure Works scenario, you must add two additional tables to your model.</span></span> <span data-ttu-id="ba541-125">추가할 첫 번째 테이블은 동일한 AdventureWorksDW 데이터베이스의 DimSalesTerritory(판매 지역으로)입니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-125">The first table you add is DimSalesTerritory (as Sales Territory) from the same AdventureWorksDW database.</span></span> <span data-ttu-id="ba541-126">로그온한 사용자가 찾아볼 수 있는 특정 데이터를 정의하는 SalesTerritory 테이블에 행 필터를 나중에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-126">You later apply a row filter to the SalesTerritory table that defines the particular data the logged on user can browse.</span></span>  
  
#### <a name="to-add-the-dimsalesterritory-table"></a><span data-ttu-id="ba541-127">DimSalesTerritory 테이블을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="ba541-127">To add the DimSalesTerritory table</span></span>  
  
1.  <span data-ttu-id="ba541-128">테이블 형식 모델 탐색기의 > **데이터 원본**에서 해당 연결을 마우스 오른쪽 단추로 클릭한 다음 **새 테이블 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-128">In Tabular Model Explorer > **Data Sources**, right-click your connection, and then click **Import New Tables**.</span></span>  

    <span data-ttu-id="ba541-129">[가장 자격 증명] 대화 상자가 나타나면 2단원: 데이터 추가에 사용된 가장 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-129">If the Impersonation Credentials dialog box appears, type the impersonation credentials you used in Lesson 2: Add Data.</span></span>
  
2.  <span data-ttu-id="ba541-130">탐색기에서 **DimSalesTerritory** 테이블을 선택한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-130">In Navigator, select the **DimSalesTerritory** table, and then click **OK**.</span></span>    
  
3.  <span data-ttu-id="ba541-131">쿼리 편집기에서 **DimSalesTerritory** 쿼리를 클릭한 후 **SalesTerritoryAlternateKey** 열을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-131">In Query Editor, click the **DimSalesTerritory** query, and then remove **SalesTerritoryAlternateKey** column.</span></span>  
  
7.  <span data-ttu-id="ba541-132">**가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-132">Click **Import**.</span></span>  
  
    <span data-ttu-id="ba541-133">새 테이블이 모델 작업 영역에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-133">The new table is added to the model workspace.</span></span> <span data-ttu-id="ba541-134">그러면 원본 DimSalesTerritory 테이블의 개체 및 데이터를 AW Internet Sales Tabular Model로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-134">Objects and data from the source DimSalesTerritory table are then imported into your AW Internet Sales Tabular Model.</span></span>  
  
9. <span data-ttu-id="ba541-135">테이블을 성공적으로 가져온 후 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-135">After the table has been imported successfully, click **Close**.</span></span>  

## <a name="add-a-table-with-user-name-data"></a><span data-ttu-id="ba541-136">사용자 이름 데이터가 있는 테이블 추가</span><span class="sxs-lookup"><span data-stu-id="ba541-136">Add a table with user name data</span></span>  
<span data-ttu-id="ba541-137">AdventureWorksDW 샘플 데이터베이스의 DimEmployee 테이블은 AdventureWorks 도메인의 사용자를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-137">The DimEmployee table in the AdventureWorksDW sample database contains users from the AdventureWorks domain.</span></span> <span data-ttu-id="ba541-138">해당 사용자 이름은 사용자 환경에 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-138">Those user names do not exist in your own environment.</span></span> <span data-ttu-id="ba541-139">모델에 조직에서 실제 사용자의 작은 샘플(3개 이상)을 포함하는 테이블을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-139">You must create a table in your model that contains a small sample (at least three) of actual users from your organization.</span></span> <span data-ttu-id="ba541-140">그런 다음 이러한 사용자를 새 역할의 멤버로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-140">You then add these users as members to the new role.</span></span> <span data-ttu-id="ba541-141">샘플 사용자 이름에 대한 암호는 필요하지 않지만 사용자 고유 도메인의 실제 Windows 사용자 이름은 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-141">You do not need the passwords for the sample user names, but you do need actual Windows user names from your own domain.</span></span>  
  
#### <a name="to-add-an-employeesecurity-table"></a><span data-ttu-id="ba541-142">EmployeeSecurity 테이블을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="ba541-142">To add an EmployeeSecurity table</span></span>  
  
1.  <span data-ttu-id="ba541-143">Microsoft Excel을 열어 워크시트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-143">Open Microsoft Excel, creating a worksheet.</span></span>  
  
2.  <span data-ttu-id="ba541-144">머리글 행을 포함하여 다음 테이블을 복사한 후 워크시트에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-144">Copy the following table, including the header row, and then paste it into the worksheet.</span></span>  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  <span data-ttu-id="ba541-145">성명 및 domain\username을 조직에서 세 사용자의 이름 및 로그인 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-145">Replace the first name, last name, and domain\username with the names and login ids of three users in your organization.</span></span> <span data-ttu-id="ba541-146">EmployeeId 1에 대해 이 사용자가 둘 이상의 영업 지역에 속함을 보여 주는 처음 두 행에 동일한 사용자를 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-146">Put the same user on the first two rows, for EmployeeId 1, showing this user belongs to more than one sales territory.</span></span> <span data-ttu-id="ba541-147">EmployeeId 및 SalesTerritoryId 필드는 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-147">Leave the EmployeeId and SalesTerritoryId fields as they are.</span></span>  
  
4.  <span data-ttu-id="ba541-148">워크시트를 **SampleEmployee**로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-148">Save the worksheet as **SampleEmployee**.</span></span>  
  
5.  <span data-ttu-id="ba541-149">워크시트에서 머리글을 포함하여 직원 데이터가 있는 모든 셀을 선택한 후 선택한 데이터를 마우스 오른쪽 단추로 클릭한 후 **복사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-149">In the worksheet, select all the cells with employee data, including the headers, then right-click the selected data, and then click **Copy**.</span></span>  
  
6.  <span data-ttu-id="ba541-150">SSDT에서 **편집** 메뉴를 클릭한 다음 **붙여넣기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-150">In SSDT, click the **Edit** menu, and then click **Paste**.</span></span>  
  
    <span data-ttu-id="ba541-151">붙여넣기가 회색으로 표시되면 모델 디자이너 창에서 모든 테이블의 모든 행을 클릭하고 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-151">If Paste is grayed out, click any column in any table in the model designer window, and try again.</span></span>  
  
7.  <span data-ttu-id="ba541-152">**붙여넣기 미리 보기** 대화 상자의 **테이블 이름**에 **EmployeeSecurity**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-152">In the **Paste Preview** dialog box, in **Table Name**, type **EmployeeSecurity**.</span></span>  
  
8.  <span data-ttu-id="ba541-153">**붙여 넣을 데이터**에서 데이터에 SampleEmployee 워크시트의 모든 사용자 데이터 및 머리글이 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-153">In **Data to be pasted**, verify the data includes all the user data and headers from the SampleEmployee worksheet.</span></span>  
  
9. <span data-ttu-id="ba541-154">**첫 행을 열 머리글로 사용**이 선택되어 있는지 확인한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-154">Verify **Use first row as column headers** is checked, and then click **Ok**.</span></span>  
  
    <span data-ttu-id="ba541-155">SampleEmployee 워크시트에서 복사된 직원 데이터가 있는 EmployeeSecurity라는 새 테이블이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-155">A new table named EmployeeSecurity with employee data copied from the SampleEmployee worksheet is created.</span></span>  
  
## <a name="create-relationships-between-factinternetsales-dimgeography-and-dimsalesterritory-table"></a><span data-ttu-id="ba541-156">FactInternetSales, DimGeography 및 DimSalesTerritory 테이블 간의 관계 만들기</span><span class="sxs-lookup"><span data-stu-id="ba541-156">Create relationships between FactInternetSales, DimGeography, and DimSalesTerritory table</span></span>  
<span data-ttu-id="ba541-157">FactInternetSales, DimGeography 및 DimSalesTerritory 테이블은 모두 SalesTerritoryId라는 공통의 열을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-157">The FactInternetSales, DimGeography, and DimSalesTerritory table all contain a common column, SalesTerritoryId.</span></span> <span data-ttu-id="ba541-158">DimSalesTerritory 테이블의 SalesTerritoryId 열에는 판매 지역마다 다른 ID가 있는 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-158">The SalesTerritoryId column in the DimSalesTerritory table contains values with a different Id for each sales territory.</span></span>  
  
#### <a name="to-create-relationships-between-the-factinternetsales-dimgeography-and-the-dimsalesterritory-table"></a><span data-ttu-id="ba541-159">FactInternetSales, DimGeography 및 DimSalesTerritory 테이블 간의 관계를 만들려면</span><span class="sxs-lookup"><span data-stu-id="ba541-159">To create relationships between the FactInternetSales, DimGeography, and the DimSalesTerritory table</span></span>  
  
1.  <span data-ttu-id="ba541-160">다이어그램 뷰에서 **DimGeography** 테이블의 **SalesTerritoryId** 열을 클릭한 채로 커서를 **DimSalesTerritory** 테이블의 **SalesTerritoryId** 열로 끌어다 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-160">In Diagram View, in the **DimGeography** table, click, and hold on the **SalesTerritoryId** column, then drag the cursor to the **SalesTerritoryId** column in the **DimSalesTerritory** table, and then release.</span></span>  
  
2.  <span data-ttu-id="ba541-161">**FactInternetSales** 테이블에서 **SalesTerritoryId** 열을 클릭한 채로 커서를 **DimSalesTerritory** 테이블의 **SalesTerritoryId** 열로 끌어다 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-161">In the **FactInternetSales** table, click, and hold on the **SalesTerritoryId** column, then drag the cursor to the **SalesTerritoryId** column in the **DimSalesTerritory** table, and then release.</span></span>  
  
    <span data-ttu-id="ba541-162">이 관계의 활성 속성은 False이며 비활성을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-162">Notice the Active property for this relationship is False, meaning it's inactive.</span></span> <span data-ttu-id="ba541-163">FactInternetSales 테이블에는 이미 다른 활성 관계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-163">The FactInternetSales table already has another active relationship.</span></span>  
  
## <a name="hide-the-employeesecurity-table-from-client-applications"></a><span data-ttu-id="ba541-164">클라이언트 응용 프로그램에서 EmployeeSecurity 테이블 숨기기</span><span class="sxs-lookup"><span data-stu-id="ba541-164">Hide the EmployeeSecurity Table from client applications</span></span>  
<span data-ttu-id="ba541-165">이 작업에서는 EmployeeSecurity 테이블을 숨겨서 클라이언트 응용 프로그램의 필드 목록에 나타나지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-165">In this task, you hide the EmployeeSecurity table, keeping it from appearing in a client application’s field list.</span></span> <span data-ttu-id="ba541-166">테이블을 숨긴다고 해서 안전한 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-166">Keep in mind that hiding a table does not secure it.</span></span> <span data-ttu-id="ba541-167">사용자는 EmployeeSecurity 테이블 데이터를 계속 쿼리할 수 있습니다(알고 있는 경우).</span><span class="sxs-lookup"><span data-stu-id="ba541-167">Users can still query EmployeeSecurity table data if they know how.</span></span> <span data-ttu-id="ba541-168">사용자가 어떤 데이터도 쿼리하지 못하도록 하고 EmployeeSecurity 테이블 데이터의 보안을 유지하려면 나중 작업에 필터를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-168">To secure the EmployeeSecurity table data, preventing users from being able to query any of its data, you apply a filter in a later task.</span></span>  
  
#### <a name="to-hide-the-employeesecurity-table-from-client-applications"></a><span data-ttu-id="ba541-169">클라이언트 응용 프로그램에서 EmployeeSecurity 테이블을 숨기려면</span><span class="sxs-lookup"><span data-stu-id="ba541-169">To hide the EmployeeSecurity table from client applications</span></span>  
  
-   <span data-ttu-id="ba541-170">모델 디자이너의 다이어그램 뷰에서 **Employee** 테이블 머리글을 마우스 오른쪽 단추로 클릭한 후 **클라이언트 도구에서 숨기기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-170">In the model designer, in Diagram View, right-click the **Employee** table heading, and then click **Hide from Client Tools**.</span></span>  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a><span data-ttu-id="ba541-171">Sales Employees by Territory(지역별 영업 직원) 사용자 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="ba541-171">Create a Sales Employees by Territory user role</span></span>  
<span data-ttu-id="ba541-172">이 작업에서는 사용자 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-172">In this task, you create a user role.</span></span> <span data-ttu-id="ba541-173">이 역할은 사용자에게 표시되는 DimSalesTerritory 테이블의 행을 정의하는 행 필터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-173">This role includes a row filter defining which rows of the DimSalesTerritory table are visible to users.</span></span> <span data-ttu-id="ba541-174">필터는 DimSalesTerritory와 관련된 모든 다른 테이블에 대해 일대다 관계 방향으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-174">The filter is then applied in the one-to-many relationship direction to all other tables related to DimSalesTerritory.</span></span> <span data-ttu-id="ba541-175">또한 해당 역할의 멤버인 모든 사용자가 전체 EmployeeSecurity 테이블을 쿼리할 수 없도록 보호하는 필터도 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-175">You also apply a filter that secures the entire EmployeeSecurity table from being queryable by any user that is a member of the role.</span></span>  
  
> [!NOTE]  
> <span data-ttu-id="ba541-176">이 단원에서 만든 Sales Employees by Territory(지역별 영업 직원) 역할은 멤버가 사용자가 속한 판매 지역에 대한 판매 데이터만 찾아보도록(또는 쿼리) 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-176">The Sales Employees by Territory role you create in this lesson restricts members to browse (or query) only sales data for the sales territory to which they belong.</span></span> <span data-ttu-id="ba541-177">[단원 11: 역할 만들기](../tutorials/aas-lesson-11-create-roles.md)에서 생성된 역할의 멤버로 존재하는 Sales Employees by Territory(지역별 영업 직원) 역할에 사용자를 멤버로 추가하는 경우 결합된 권한을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-177">If you add a user as a member to the Sales Employees by Territory role that also exists as a member in a role created in [Lesson 11: Create Roles](../tutorials/aas-lesson-11-create-roles.md), you get a combination of permissions.</span></span> <span data-ttu-id="ba541-178">사용자가 여러 역할, 권한 및 각 역할에 대해 정의 된 행 필터의 멤버인 경우 누적 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-178">When a user is a member of multiple roles, the permissions, and row filters defined for each role are cumulative.</span></span> <span data-ttu-id="ba541-179">즉, 이 사용자는 역할의 조합으로 결정된 더 큰 권한을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-179">That is, the user has the greater permissions determined by the combination of roles.</span></span>  
  
#### <a name="to-create-a-sales-employees-by-territory-user-role"></a><span data-ttu-id="ba541-180">Sales Employees by Territory(지역별 영업 직원) 사용자 역할을 만들려면</span><span class="sxs-lookup"><span data-stu-id="ba541-180">To create a Sales Employees by Territory user role</span></span>  
  
1.  <span data-ttu-id="ba541-181">SSDT에서 **모델** 메뉴를 클릭한 후 **역할**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-181">In SSDT, click the **Model** menu, and then click **Roles**.</span></span>  
  
2.  <span data-ttu-id="ba541-182">**역할 관리자**에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-182">In **Role Manager**, click **New**.</span></span>  
  
    <span data-ttu-id="ba541-183">권한이 없는 새 역할이 목록에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-183">A new role with the None permission is added to the list.</span></span>  
  
3.  <span data-ttu-id="ba541-184">새 역할을 클릭한 후 **이름** 열에서 역할의 이름을 **Sales Employees by Territory(지역별 영업 직원)**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-184">Click the new role, and then in the **Name** column, rename the role to **Sales Employees by Territory**.</span></span>  
  
4.  <span data-ttu-id="ba541-185">**사용 권한** 열에서 드롭다운 목록을 클릭한 후 **읽기** 권한을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-185">In the **Permissions** column, click the dropdown list, and then select the **Read** permission.</span></span>  
  
5.  <span data-ttu-id="ba541-186">**멤버** 탭을 클릭한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-186">Click the **Members** tab, and then click **Add**.</span></span>  
  
6.  <span data-ttu-id="ba541-187">**사용자 또는 그룹 선택** 대화 상자의 **선택할 개체 이름 입력**에서 EmployeeSecurity 테이블을 만들 때 사용한 첫 번째 예제 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-187">In the **Select User or Group** dialog box, in **Enter the object named to select**, type the first sample user name you used when creating the EmployeeSecurity table.</span></span> <span data-ttu-id="ba541-188">**이름 확인**을 클릭하여 사용자 이름이 올바른지 확인한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-188">Click **Check Names** to verify the user name is valid, and then click **Ok**.</span></span>  
  
    <span data-ttu-id="ba541-189">이 단계를 반복하여 EmployeeSecurity 테이블을 만들 때 사용한 다른 예제 사용자 이름을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-189">Repeat this step, adding the other sample user names you used when creating the EmployeeSecurity table.</span></span>  
  
7.  <span data-ttu-id="ba541-190">**행 필터** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-190">Click the **Row Filters** tab.</span></span>  
  
8.  <span data-ttu-id="ba541-191">**EmployeeSecurity** 테이블의 **DAX 필터** 열에서 다음 수식을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-191">For the **EmployeeSecurity** table, in the **DAX Filter** column, type the following formula:</span></span>  
  
    ```
      =FALSE()  
    ```
  
    <span data-ttu-id="ba541-192">이 수식은 false 부울 조건으로 확인하는 모든 열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-192">This formula specifies that all columns resolve to the false Boolean condition.</span></span> <span data-ttu-id="ba541-193">EmployeeSecurity 테이블에 대한 열은 Territory 사용자 역할로 판매 직원의 멤버로 쿼리될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-193">No columns for the EmployeeSecurity table can be queried by a member of the Sales Employees by Territory user role.</span></span>  
  
9. <span data-ttu-id="ba541-194">**DimSalesTerritory** 테이블에 대해 다음 수식을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-194">For the **DimSalesTerritory** table, type the following formula:</span></span>  

    ```  
    ='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 
      'Employee Security'[Login Id], USERNAME(), 
      'Employee Security'[Sales Territory Id], 
      'Sales Territory'[Sales Territory Id]) 
    ```
  
    <span data-ttu-id="ba541-195">이 수식에서 LOOKUPVALUE 함수는 DimEmployeeSecurity[SalesTerritoryId] 열에 대한 모든 값을 반환합니다. 여기서 EmployeeSecurity[LoginId]는 현재 로그온한 Windows 사용자 이름과 같고 EmployeeSecurity[SalesTerritoryId]는 DimSalesTerritory[SalesTerritoryId]와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-195">In this formula, the LOOKUPVALUE function returns all values for the DimEmployeeSecurity[SalesTerritoryId] column, where the EmployeeSecurity[LoginId] is the same as the current logged on Windows user name, and EmployeeSecurity[SalesTerritoryId] is the same as the DimSalesTerritory[SalesTerritoryId].</span></span>  
  
    <span data-ttu-id="ba541-196">LOOKUPVALUE에서 반환된 판매 지역 ID 집합은 DimSalesTerritory 테이블에 표시된 행을 제한하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-196">The set of sales territory IDs returned by LOOKUPVALUE is then used to restrict the rows shown in the DimSalesTerritory table.</span></span> <span data-ttu-id="ba541-197">행의 SalesTerritoryID가 LOOKUPVALUE 함수에서 반환한 ID 집합에 있는 행만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-197">Only rows where the SalesTerritoryID for the row is in the set of IDs returned by the LOOKUPVALUE function are displayed.</span></span>  
  
10. <span data-ttu-id="ba541-198">역할 관리자에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-198">In Role Manager, click **Ok**.</span></span>  
  
## <a name="test-the-sales-employees-by-territory-user-role"></a><span data-ttu-id="ba541-199">Sales Employees by Territory(지역별 영업 직원) 사용자 역할 테스트</span><span class="sxs-lookup"><span data-stu-id="ba541-199">Test the Sales Employees by Territory User Role</span></span>  
<span data-ttu-id="ba541-200">이 작업에서는 SSDT에서 Excel에서 분석 기능을 사용하여 Sales Employees by Territory(지역별 영업 직원) 사용자 역할의 효율성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-200">In this task, you use the Analyze in Excel feature in SSDT to test the efficacy of the Sales Employees by Territory user role.</span></span> <span data-ttu-id="ba541-201">EmployeeSecurity 테이블에 추가한 사용자 이름 중 하나를 역할의 멤버로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-201">You specify one of the user names you added to the EmployeeSecurity table and as a member of the role.</span></span> <span data-ttu-id="ba541-202">그러면 이 사용자 이름이 Excel과 모델 간에 생성된 연결의 유효한 사용자 이름으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-202">This user name is then used as the effective user name in the connection created between Excel and the model.</span></span>  
  
#### <a name="to-test-the-sales-employees-by-territory-user-role"></a><span data-ttu-id="ba541-203">Sales Employees by Territory(지역별 영업 직원) 사용자 역할을 테스트하려면</span><span class="sxs-lookup"><span data-stu-id="ba541-203">To test the Sales Employees by Territory user role</span></span>  
  
1.  <span data-ttu-id="ba541-204">SSDT에서 **모델** 메뉴를 클릭한 후 **Excel에서 분석**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-204">In SSDT, click the **Model** menu, and then click **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="ba541-205">**Excel에서 분석** 대화 상자의 **모델에 연결하기 위해 사용할 사용자 이름 또는 역할 지정**에서 **다른 Windows 사용자**를 선택한 후 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-205">In the **Analyze in Excel** dialog box, in **Specify the user name or role to use to connect to the model**, select **Other Windows User**, and then click **Browse**.</span></span>  
  
3.  <span data-ttu-id="ba541-206">**사용자 또는 그룹 선택** 대화 상자의 **선택할 개체 이름 입력**에서 EmployeeSecurity 테이블에 포함된 사용자 이름을 입력한 후 **이름 확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-206">In the **Select User or Group** dialog box, in **Enter the object name to select**, type a user name you included in the EmployeeSecurity table, and then click **Check Names**.</span></span>  
  
4.  <span data-ttu-id="ba541-207">**확인**을 클릭하여 **사용자 또는 그룹 선택** 대화 상자를 닫은 후 **확인**을 클릭하여 **Excel에서 분석** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-207">Click **Ok** to close the **Select User or Group** dialog box, and then click **Ok** to close the **Analyze in Excel** dialog box.</span></span>  
  
    <span data-ttu-id="ba541-208">Excel에서 새 통합 문서가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-208">Excel opens with a new workbook.</span></span> <span data-ttu-id="ba541-209">피벗 테이블이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-209">A PivotTable is automatically created.</span></span> <span data-ttu-id="ba541-210">피벗 테이블 필드 목록에는 새 모델에 사용할 수 있는 대부분의 데이터 필드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-210">The PivotTable Fields list includes most of the data fields available in your new model.</span></span>  
  
    <span data-ttu-id="ba541-211">EmployeeSecurity 테이블은 피벗 테이블 필드 목록에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-211">Notice the EmployeeSecurity table is not visible in the PivotTable Fields list.</span></span> <span data-ttu-id="ba541-212">이전 작업의 클라이언트 도구에서 이 테이블을 숨겼습니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-212">You hid this table from client tools in a previous task.</span></span>  
  
5.  <span data-ttu-id="ba541-213">**필드** 목록의 **∑ 인터넷 판매**(측정값)에서 **InternetTotalSales** 측정값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-213">In the **Fields** list, in **∑ Internet Sales** (measures), select the **InternetTotalSales** measure.</span></span> <span data-ttu-id="ba541-214">측정값이 **값** 필드에 입력됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-214">The measure is entered into the **Values** fields.</span></span>  
  
6.  <span data-ttu-id="ba541-215">**DimSalesTerritory** 테이블에서 **SalesTerritoryId** 열을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-215">Select the **SalesTerritoryId** column from the **DimSalesTerritory** table.</span></span> <span data-ttu-id="ba541-216">열이 **행 레이블** 필드에 입력됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-216">The column is entered into the **Row Labels** fields.</span></span>  
  
    <span data-ttu-id="ba541-217">인터넷 판매 수치는 사용한 유효 사용자 이름이 속하는 한 지역에 대해서만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-217">Notice Internet sales figures appear only for the one region to which the effective user name you used belongs.</span></span> <span data-ttu-id="ba541-218">DimGeography 테이블에서 행 레이블 필드로 다른 열을 선택하는 경우(예를 들어 도시) 유효 사용자가 속한 판매 지역의 도시만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-218">If you select another column, like City from the DimGeography table as Row Label field, only cities in the sales territory to which the effective user belongs are displayed.</span></span>  
  
    <span data-ttu-id="ba541-219">이 사용자는 자신이 속하지 않는 지역에 대한 인터넷 판매 데이터를 찾아보거나 쿼리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-219">This user cannot browse or query any Internet sales data for territories other than the one they belong to.</span></span> <span data-ttu-id="ba541-220">이렇게 제한하는 이유는 Sales Employees by Territory(지역별 영업 직원) 사용자 역할에서 DimSalesTerritory 테이블에 대해 정의한 행 필터가 다른 판매 지역과 관련된 모든 데이터에 대해 데이터를 보호하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="ba541-220">This restriction is because the row filter defined for the DimSalesTerritory table, in the Sales Employees by Territory user role, secures data for all data related to other sales territories.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ba541-221">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ba541-221">See Also</span></span>  
[<span data-ttu-id="ba541-222">USERNAME 함수(DAX)</span><span class="sxs-lookup"><span data-stu-id="ba541-222">USERNAME Function (DAX)</span></span>](https://msdn.microsoft.com/library/hh230954.aspx)  
[<span data-ttu-id="ba541-223">LOOKUPVALUE 함수(DAX)</span><span class="sxs-lookup"><span data-stu-id="ba541-223">LOOKUPVALUE Function (DAX)</span></span>](https://msdn.microsoft.com/library/gg492170.aspx)  
[<span data-ttu-id="ba541-224">CUSTOMDATA 함수(DAX)</span><span class="sxs-lookup"><span data-stu-id="ba541-224">CUSTOMDATA Function (DAX)</span></span>](https://msdn.microsoft.com/library/hh213140.aspx)  