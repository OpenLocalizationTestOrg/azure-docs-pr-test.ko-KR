---
title: "Azure Analysis Services 자습서 단원 7: 핵심 성과 지표 만들기 | Microsoft Docs"
description: "Azure Analysis Services 자습서 프로젝트에서 핵심 성과 지표를 만드는 방법을 설명합니다."
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
ms.openlocfilehash: d78808421dd5acd907aa9e9000bb3b770a42c061
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-7-create-key-performance-indicators"></a><span data-ttu-id="e4fe3-103">단원 7: 핵심 성과 지표 만들기</span><span class="sxs-lookup"><span data-stu-id="e4fe3-103">Lesson 7: Create Key Performance Indicators</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="e4fe3-104">이 단원에서는 KPI(핵심 성과 지표)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-104">In this lesson, you create Key Performance Indicators (KPIs).</span></span> <span data-ttu-id="e4fe3-105">KPI는 *대상* 값에 대해, *기본* 측정값에 정의되고 측정값 또는 절대값으로도 정의된 값의 성과를 측정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-105">KPIs are used to gauge performance of a value defined by a *Base* measure, against a *Target* value also defined by a measure, or by an absolute value.</span></span> <span data-ttu-id="e4fe3-106">보고 클라이언트 응용 프로그램에서, 비즈니스 전문가는 KPI를 통해 비즈니스 성공 요약 및 추세 파악을 신속하고 간편하게 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-106">In reporting client applications, KPIs can provide business professionals a quick and easy way to understand a summary of business success or to identify trends.</span></span> <span data-ttu-id="e4fe3-107">자세한 내용은 [KPI](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-107">To learn more, see [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span></span>
  
<span data-ttu-id="e4fe3-108">이 단원을 완료하기 위한 예상 시간: **15분**</span><span class="sxs-lookup"><span data-stu-id="e4fe3-108">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="e4fe3-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e4fe3-109">Prerequisites</span></span>  
<span data-ttu-id="e4fe3-110">이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="e4fe3-111">이 단원의 작업을 수행하기 전에 이전 단원인 [단원 6: 측정값 만들기](../tutorials/aas-lesson-6-create-measures.md)를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-111">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>   
  
## <a name="create-key-performance-indicators"></a><span data-ttu-id="e4fe3-112">핵심 성과 지표 만들기</span><span class="sxs-lookup"><span data-stu-id="e4fe3-112">Create Key Performance Indicators</span></span>  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a><span data-ttu-id="e4fe3-113">InternetCurrentQuarterSalesPerformance KPI를 만들려면</span><span class="sxs-lookup"><span data-stu-id="e4fe3-113">To create an InternetCurrentQuarterSalesPerformance KPI</span></span>  
  
1.  <span data-ttu-id="e4fe3-114">모델 디자이너에서 **FactInternetSales** 테이블을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-114">In the model designer, click the **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="e4fe3-115">측정값 표에서 빈 셀을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-115">In the measure grid, click an empty cell.</span></span>  
  
3.  <span data-ttu-id="e4fe3-116">테이블 위의 수식 입력줄에 다음 수식을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-116">In the formula bar, above the table, type the following formula:</span></span> 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    <span data-ttu-id="e4fe3-117">이 측정값을 KPI에 대한 기본 측정값으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-117">This measure serves as the Base measure for the KPI.</span></span>  
  
4.  <span data-ttu-id="e4fe3-118">**InternetCurrentQuarterSalesPerformance** > **KPI 만들기**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-118">Right-click **InternetCurrentQuarterSalesPerformance** > **Create KPI**.</span></span>   
  
5.  <span data-ttu-id="e4fe3-119">KPI(핵심 성과 지표) 대화 상자의 **대상**에서 **절대값**을 선택한 후 **1.1**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-119">In the Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.1**.</span></span>  
  
7.  <span data-ttu-id="e4fe3-120">왼쪽(낮음) 슬라이더 필드에 **1**을 입력한 후 오른쪽(높음) 슬라이더 필드에 **1.07**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-120">In the left (low) slider field, type **1**, and then in the right (high) slider field, type **1.07**.</span></span>  
  
8.  <span data-ttu-id="e4fe3-121">**아이콘 스타일 선택**에서 다이아몬드(빨간색), 삼각형(노란색), 원형(녹색) 아이콘 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-121">In **Select Icon Style**, select the diamond (red), triangle (yellow), circle (green) icon type.</span></span>
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > <span data-ttu-id="e4fe3-123">제공되는 아이콘 스타일 아래 확장 가능한 **설명** 레이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-123">Notice the expandable **Descriptions** label below the available icon styles.</span></span> <span data-ttu-id="e4fe3-124">다양한 KPI 요소에 대한 설명을 사용하여 클라이언트 응용 프로그램에서 쉽게 식별할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-124">Use descriptions for the various KPI elements to make them more identifiable in client applications.</span></span>  
  
9. <span data-ttu-id="e4fe3-125">**확인**을 클릭하여 KPI를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-125">Click **OK** to complete the KPI.</span></span>  
  
    <span data-ttu-id="e4fe3-126">측정값 표에서 **InternetCurrentQuarterSalesPerformance** 측정값 옆에 아이콘이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-126">In the measure grid, notice the icon next to the **InternetCurrentQuarterSalesPerformance** measure.</span></span> <span data-ttu-id="e4fe3-127">이 아이콘은 이 측정값이 KPI에 대한 기본값으로 제공됨을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-127">This icon indicates that this measure serves as a Base value for a KPI.</span></span>  
  
#### <a name="to-create-an-internetcurrentquartermarginperformance-kpi"></a><span data-ttu-id="e4fe3-128">InternetCurrentQuarterMarginPerformance KPI를 만들려면</span><span class="sxs-lookup"><span data-stu-id="e4fe3-128">To create an InternetCurrentQuarterMarginPerformance KPI</span></span>  
  
1.  <span data-ttu-id="e4fe3-129">**FactInternetSales** 테이블에 대한 측정값 표에서 빈 셀을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-129">In the measure grid for the **FactInternetSales** table, click an empty cell.</span></span>  
  
2.  <span data-ttu-id="e4fe3-130">테이블 위의 수식 입력줄에 다음 수식을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-130">In the formula bar, above the table, type the following formula:</span></span>  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  <span data-ttu-id="e4fe3-131">**InternetCurrentQuarterMarginPerformance** > **KPI 만들기**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-131">Right-click **InternetCurrentQuarterMarginPerformance** > **Create KPI**.</span></span>  
  
4.  <span data-ttu-id="e4fe3-132">KPI(핵심 성과 지표) 대화 상자의 **대상**에서 **절대값**을 선택한 후 **1.25**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-132">In the Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.25**.</span></span>   
  
5.  <span data-ttu-id="e4fe3-133">왼쪽(낮음) 슬라이더에서 필드에 **0.8**이 표시될 때까지 밀고 오른쪽(높음) 슬라이더에서 필드에 **1.03**이 표시될 때까지 밉니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-133">In the left (low) slider field, slide until the field displays **0.8**, and then slide the right (high) slider field, until the field displays **1.03**.</span></span>  
  
6.  <span data-ttu-id="e4fe3-134">**아이콘 스타일 선택**에서 다이아몬드(빨간색), 삼각형(노란색), 원형(녹색) 아이콘 유형을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe3-134">In **Select Icon Style**, select the diamond (red), triangle (yellow), circle (green) icon type, and then click **OK**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="e4fe3-135">다음 작업</span><span class="sxs-lookup"><span data-stu-id="e4fe3-135">What's next?</span></span>
<span data-ttu-id="e4fe3-136">[단원 8: 큐브 뷰 만들기](../tutorials/aas-lesson-8-create-perspectives.md)</span><span class="sxs-lookup"><span data-stu-id="e4fe3-136">[Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>
  
  
