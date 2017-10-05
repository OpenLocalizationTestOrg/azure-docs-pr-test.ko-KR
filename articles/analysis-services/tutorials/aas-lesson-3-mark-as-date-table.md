---
title: "Azure Analysis Services 자습서 단원 3: 날짜 테이블로 표시 | Microsoft Docs"
description: "Azure Analysis Services 자습서 프로젝트에서 날짜 테이블로 표시하는 방법을 설명합니다."
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
ms.openlocfilehash: c62f2726fef5219155a08b70c61162c914600d1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-3-mark-as-date-table"></a><span data-ttu-id="a2a77-103">단원 3: 날짜 테이블로 표시</span><span class="sxs-lookup"><span data-stu-id="a2a77-103">Lesson 3: Mark as Date Table</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="a2a77-104">2단원: 데이터 가져오기에서는 이름이 DimDate인 차원 테이블을 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="a2a77-104">In Lesson 2: Get data, you imported a dimension table named DimDate.</span></span> <span data-ttu-id="a2a77-105">모델에서 이 테이블의 이름은 DimDate이지만 날짜 및 시간 데이터가 포함되어 있으므로 *날짜 테이블*이라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a77-105">While in your model this table is named DimDate, it can also be known as a *Date table*, in that it contains date and time data.</span></span>  
  
<span data-ttu-id="a2a77-106">DAX 시간 인텔리전스 함수를 사용할 때마다, 나중에 측정값을 만들 때와 같이 *날짜 테이블* 및 해당 테이블에 고유 식별자 *날짜 열*을 포함하는 속성을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a77-106">Whenever you use DAX time-intelligence functions, like when you create measures later, you must specify properties which include a *Date table* and a unique identifier *Date column* in that table.</span></span>
  
<span data-ttu-id="a2a77-107">이 단원에서는 DimDate 테이블을 *날짜 테이블*로, 날짜 열(날짜 테이블의)을 *날짜 열*(고유 식별자)로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a77-107">In this lesson, you mark the DimDate table as the *Date table* and the Date column (in the Date table) as the *Date column* (unique identifier).</span></span>  

<span data-ttu-id="a2a77-108">날짜 테이블 및 날짜 열을 표시하기 전에 모델을 더 쉽게 이해하려면 약간 관리 유지 작업을 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a2a77-108">Before you mark the date table and date column, it's a good time to do a little housekeeping to make your model easier to understand.</span></span> <span data-ttu-id="a2a77-109">DimDate 테이블에서 **FullDateAlternateKey**라는 열을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a77-109">Notice in the DimDate table a column named **FullDateAlternateKey**.</span></span> <span data-ttu-id="a2a77-110">이 열은 테이블에 포함된 각 달력 연도의 모든 날에 대한 하나의 행을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a77-110">This column contains one row for every day in each calendar year included in the table.</span></span> <span data-ttu-id="a2a77-111">측정 수식 및 보고서에서 이 열을 많이 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a77-111">You use this column a lot in measure formulas and in reports.</span></span> <span data-ttu-id="a2a77-112">하지만 실제로 FullDateAlternateKey는 이 열에 대한 적절한 식별자가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a2a77-112">But, FullDateAlternateKey isn't really a good identifier for this column.</span></span> <span data-ttu-id="a2a77-113">수식에서 쉽게 식별하고 포함할 수 있도록 이름을 **Date**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a77-113">You rename it to **Date**, making it easier to identify and include in formulas.</span></span> <span data-ttu-id="a2a77-114">가능하다면, 테이블 및 열과 같은 개체의 이름을 변경하여 SSDT 및 클라이언트 보고 응용 프로그램(Power BI 및 Excel)에서 쉽게 식별할 수 있도록 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a2a77-114">Whenever possible, it's a good idea to rename objects like tables and columns to make them easier to identify in SSDT and client reporting applications like Power BI and Excel.</span></span> 
  
<span data-ttu-id="a2a77-115">이 단원을 완료하기 위한 예상 시간: **3분**</span><span class="sxs-lookup"><span data-stu-id="a2a77-115">Estimated time to complete this lesson: **Three minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="a2a77-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a2a77-116">Prerequisites</span></span>  
<span data-ttu-id="a2a77-117">이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a77-117">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="a2a77-118">이 단원의 작업을 수행하기 전에 이전 단원인 [단원 2: 데이터 가져오기](../tutorials/aas-lesson-2-get-data.md)를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a77-118">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 2: Get data](../tutorials/aas-lesson-2-get-data.md).</span></span> 

### <a name="to-rename-the-fulldatealternatekey-column"></a><span data-ttu-id="a2a77-119">FullDateAlternateKey 열 이름을 바꾸려면</span><span class="sxs-lookup"><span data-stu-id="a2a77-119">To rename the FullDateAlternateKey column</span></span>

1.  <span data-ttu-id="a2a77-120">모델 디자이너에서 **DimDate** 테이블을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a77-120">In the model designer, click the **DimDate** table.</span></span>

2.  <span data-ttu-id="a2a77-121">**FullDateAlternateKey** 열에 대한 머리글을 두 번 클릭하고 **Date**로 이름을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a77-121">Double-click the header for the **FullDateAlternateKey** column, and then rename it to **Date**.</span></span>

  
### <a name="to-set-mark-as-date-table"></a><span data-ttu-id="a2a77-122">날짜 테이블로 표시를 설정하려면</span><span class="sxs-lookup"><span data-stu-id="a2a77-122">To set Mark as Date Table</span></span>  
  
1.  <span data-ttu-id="a2a77-123">**날짜** 열을 선택한 다음 **속성** 창의 **데이터 형식** 아래에서인 **Date**가 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a77-123">Select the **Date** column, and then in the **Properties** window, under **Data Type**, make sure  **Date** is selected.</span></span>  
  
2.  <span data-ttu-id="a2a77-124">**테이블** 메뉴를 클릭한 다음 **날짜**를 클릭하고 **날짜 테이블로 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a77-124">Click the **Table** menu, then click **Date**, and then click **Mark as Date Table**.</span></span>  
  
3.  <span data-ttu-id="a2a77-125">**날짜 테이블로 표시** 대화 상자의 **날짜** 목록 상자에서 **날짜** 열을 고유 식별자로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a77-125">In the **Mark as Date Table** dialog box, in the **Date** listbox, select the **Date** column as the unique identifier.</span></span> <span data-ttu-id="a2a77-126">보통은 기본적으로 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2a77-126">It's usually selected by default.</span></span> <span data-ttu-id="a2a77-127">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a77-127">Click **OK**.</span></span> 

    ![aas-lesson3-date-table](../tutorials/media/aas-lesson3-date-table.png)
  

## <a name="whats-next"></a><span data-ttu-id="a2a77-129">다음 작업</span><span class="sxs-lookup"><span data-stu-id="a2a77-129">What's next?</span></span>
<span data-ttu-id="a2a77-130">[단원 4: 관계 만들기](../tutorials/aas-lesson-4-create-relationships.md)</span><span class="sxs-lookup"><span data-stu-id="a2a77-130">[Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span>
  
