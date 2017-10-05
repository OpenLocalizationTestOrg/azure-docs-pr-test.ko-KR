---
title: "Azure Analysis Services 자습서 단원 12: Excel에서 분석 | Microsoft Docs"
description: "Azure Analysis Services 자습서 프로젝트에서 Excel에서 분석을 사용하는 방법을 설명합니다."
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
ms.openlocfilehash: 6f47de43ff8d94de22f8b7c12fa0707a8d7ffbbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-12-analyze-in-excel"></a><span data-ttu-id="95d67-103">단원 12: Excel에서 분석</span><span class="sxs-lookup"><span data-stu-id="95d67-103">Lesson 12: Analyze in Excel</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="95d67-104">이 단원에서는 Excel에서 분석 기능을 사용하여 Microsoft Excel을 열고 모델 작업 영역에 대한 연결을 자동으로 만들고 피벗 테이블을 워크시트에 자동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-104">In this lesson, you use the Analyze in Excel feature to open Microsoft Excel, automatically create a connection to the model workspace, and automatically add a PivotTable to the worksheet.</span></span> <span data-ttu-id="95d67-105">Excel에서 분석 기능은 모델을 배포하기 전에 모델 디자인의 효율성을 테스트하기 위한 쉽고 빠른 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-105">The Analyze in Excel feature is meant to provide a quick and easy way to test the efficacy of your model design prior to deploying your model.</span></span> <span data-ttu-id="95d67-106">이 단원에서는 어떠한 데이터 분석도 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-106">You do not perform any data analysis in this lesson.</span></span> <span data-ttu-id="95d67-107">이 단원의 목적은 모델 작성자인 사용자가 모델 디자인을 테스트하는 데 사용할 수 있는 도구를 습득하게 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-107">The purpose of this lesson is to familiarize you, the model author, with the tools you can use to test your model design.</span></span>   
  
<span data-ttu-id="95d67-108">이 단원을 완료하려면 SSDT와 같은 컴퓨터에 Excel이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-108">To complete this lesson, Excel must be installed on the same computer as SSDT.</span></span>
  
<span data-ttu-id="95d67-109">이 단원을 완료하기 위한 예상 시간: **5분**</span><span class="sxs-lookup"><span data-stu-id="95d67-109">Estimated time to complete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="95d67-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="95d67-110">Prerequisites</span></span>  
<span data-ttu-id="95d67-111">이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="95d67-112">이 단원의 작업을 수행하기 전에 이전 단원인 [단원 11: 역할 만들기](../tutorials/aas-lesson-11-create-roles.md)를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 11: Create roles](../tutorials/aas-lesson-11-create-roles.md).</span></span>  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a><span data-ttu-id="95d67-113">기본 및 인터넷 판매 큐브 뷰를 사용하여 찾아보기</span><span class="sxs-lookup"><span data-stu-id="95d67-113">Browse using the Default and Internet Sales perspectives</span></span>  
<span data-ttu-id="95d67-114">다음 첫 번째 작업에서는 모든 모델 개체를 포함하는 기본 큐브 뷰와 이전의 인터넷 판매 큐브 뷰를 모두 사용하여 모델을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-114">In these first tasks, you browse your model by using both the default perspective, which includes all model objects, and also by using the Internet Sales perspective you earlier.</span></span> <span data-ttu-id="95d67-115">인터넷 판매 큐브 뷰에는 고객 테이블 개체가 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-115">The Internet Sales perspective excludes the Customer table object.</span></span>  
  
#### <a name="to-browse-by-using-the-default-perspective"></a><span data-ttu-id="95d67-116">기본 큐브 뷰를 사용하여 찾아보려면</span><span class="sxs-lookup"><span data-stu-id="95d67-116">To browse by using the Default perspective</span></span>  
  
1.  <span data-ttu-id="95d67-117">**모델** 메뉴 > **Excel에서 분석**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-117">Click the **Model** menu > **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="95d67-118">**Excel에서 분석** 대화 상자에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-118">In the **Analyze in Excel** dialog box, click **OK**.</span></span>  
  
    <span data-ttu-id="95d67-119">Excel에서 새 통합 문서가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-119">Excel opens with a new workbook.</span></span> <span data-ttu-id="95d67-120">데이터 원본 연결이 현재 사용자 계정을 사용하여 생성되고 볼 수 있는 필드를 정의하는 데 기본 큐브 뷰가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-120">A data source connection is created using the current user account and the Default perspective is used to define viewable fields.</span></span> <span data-ttu-id="95d67-121">피벗 테이블은 워크시트에 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-121">A PivotTable is automatically added to the worksheet.</span></span>  
  
3.  <span data-ttu-id="95d67-122">Excel에서 **피벗 테이블 필드 목록**에 **DimDate** 및 **FactInternetSales** 측정값 그룹이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-122">In Excel, in the **PivotTable Field List**, notice the **DimDate** and **FactInternetSales** measure groups appear.</span></span> <span data-ttu-id="95d67-123">해당 열과 함께 **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory** 및 **FactInternetSales** 테이블도 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-123">The **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales** tables with their respective columns also appear.</span></span>  
  
4.  <span data-ttu-id="95d67-124">통합 문서를 저장하지 않고 Excel을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-124">Close Excel without saving the workbook.</span></span>  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a><span data-ttu-id="95d67-125">인터넷 판매 큐브 뷰를 사용하여 찾아보려면</span><span class="sxs-lookup"><span data-stu-id="95d67-125">To browse by using the Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="95d67-126">**모델** 메뉴를 클릭한 후 **Excel에서 분석**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-126">Click the **Model** menu, and then click **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="95d67-127">**Excel에서 분석** 대화 상자에서 **현재 Windows 사용자**가 선택된 상태로 두고 **큐브 뷰** 드롭다운 목록 상자에서 **인터넷 판매**를 선택한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-127">In the **Analyze in Excel** dialog box, leave **Current Windows User** selected, then in the **Perspective** drop-down listbox, select **Internet Sales**, and then click **OK**.</span></span> 
    
    ![aas-lesson12-perspective](../tutorials/media/aas-lesson12-perspective.png)
    
3.  <span data-ttu-id="95d67-129">Excel의 **피벗 테이블 필드**에서 DimCustomer 테이블이 필드 목록에서 제외되는 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-129">In Excel, in **PivotTable Fields**, notice the DimCustomer table is excluded from the field list.</span></span>  
    
    ![aas-lesson12-fields](../tutorials/media/aas-lesson12-fields.png)
    
4.  <span data-ttu-id="95d67-131">통합 문서를 저장하지 않고 Excel을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-131">Close Excel without saving the workbook.</span></span>  
  
## <a name="browse-by-using-roles"></a><span data-ttu-id="95d67-132">역할을 사용하여 찾아보기</span><span class="sxs-lookup"><span data-stu-id="95d67-132">Browse by using roles</span></span>  
<span data-ttu-id="95d67-133">역할은 테이블 형식 모델의 중요한 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-133">Roles are an important part of any tabular model.</span></span> <span data-ttu-id="95d67-134">사용자가 멤버로 추가되는 역할이 하나도 경우 사용자는 모델을 사용하여 데이터에 액세스 및 분석할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-134">Without at least one role to which users are added as members, users cannot access and analyze data using your model.</span></span> <span data-ttu-id="95d67-135">Excel에서 분석 기능은 정의한 역할을 테스트하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-135">The Analyze in Excel feature provides a way for you to test the roles you have defined.</span></span>  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a><span data-ttu-id="95d67-136">Sales Manager 사용자 역할을 사용하여 찾아보려면</span><span class="sxs-lookup"><span data-stu-id="95d67-136">To browse by using the Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="95d67-137">SSDT에서 **모델** 메뉴를 클릭한 후 **Excel에서 분석**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-137">In SSDT, click the **Model** menu, and then click **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="95d67-138">**모델에 연결하기 위해 사용할 사용자 이름 또는 역할 지정**에서 **역할**을 선택한 후 드롭다운 목록 상자에서 **Sales Manager**를 선택한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-138">In **Specify the user name or role to use to connect to the model**, select **Role**, and then in the drop-down listbox, select **Sales Manager**, and then click **OK**.</span></span>  
  
    <span data-ttu-id="95d67-139">Excel에서 새 통합 문서가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-139">Excel opens with a new workbook.</span></span> <span data-ttu-id="95d67-140">피벗 테이블이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-140">A PivotTable is automatically created.</span></span> <span data-ttu-id="95d67-141">피벗 테이블 필드 목록에는 새 모델에 사용할 수 있는 모든 데이터 필드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-141">The Pivot Table Field List includes all the data fields available in your new model.</span></span>  
      
3.  <span data-ttu-id="95d67-142">통합 문서를 저장하지 않고 Excel을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-142">Close Excel without saving the workbook.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="95d67-143">다음 작업</span><span class="sxs-lookup"><span data-stu-id="95d67-143">What's next?</span></span>
<span data-ttu-id="95d67-144">다음 단원인 [단원 13: 배포](../tutorials/aas-lesson-13-deploy.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="95d67-144">Go to the next lesson: [Lesson 13: Deploy](../tutorials/aas-lesson-13-deploy.md).</span></span>

  
  
  
