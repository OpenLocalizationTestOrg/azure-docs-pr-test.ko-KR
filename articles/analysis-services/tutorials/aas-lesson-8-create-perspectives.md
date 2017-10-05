---
title: "Azure Analysis Services 자습서 단원 8: 큐브 뷰 만들기 | Microsoft Docs"
description: "Azure Analysis Services 자습서 프로젝트에서 큐브 뷰를 만드는 방법을 설명합니다."
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
ms.openlocfilehash: 491500909b0de0360afae45e172e85999d764fe0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-8-create-perspectives"></a><span data-ttu-id="60be1-103">단원 8: 큐브 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="60be1-103">Lesson 8: Create perspectives</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="60be1-104">이 단원에서는 인터넷 판매 큐브 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60be1-104">In this lesson, you create an Internet Sales perspective.</span></span> <span data-ttu-id="60be1-105">큐브 뷰는 포커스가 있는, 비즈니스 또는 응용 프로그램별 관점을 제공하는 모델의 볼 수 있는 하위 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="60be1-105">A perspective defines a viewable subset of a model that provides focused, business-specific, or application-specific viewpoints.</span></span> <span data-ttu-id="60be1-106">사용자가 큐브 뷰를 사용하여 모델에 연결하면 해당 큐브 뷰에 정의된 필드로 해당 모델 개체(테이블, 열, 측정값, 계층 구조 및 KPI)만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="60be1-106">When a user connects to a model by using a perspective, they see only those model objects (tables, columns, measures, hierarchies, and KPIs) as fields defined in that perspective.</span></span> <span data-ttu-id="60be1-107">자세한 내용은 [큐브 뷰](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60be1-107">To learn more, see [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span></span>
  
<span data-ttu-id="60be1-108">이 단원에서 만드는 인터넷 판매 큐브 뷰에서는 DimCustomer 테이블 개체가 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="60be1-108">The Internet Sales perspective you create in this lesson excludes the DimCustomer table object.</span></span> <span data-ttu-id="60be1-109">뷰에서 특정 개체가 제외된 큐브 뷰를 만드는 경우 이 개체는 모델에 계속 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="60be1-109">When you create a perspective that excludes certain objects from view, that object still exists in the model.</span></span> <span data-ttu-id="60be1-110">그러나 보고 클라이언트 필드 목록에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60be1-110">However, it is not visible in a reporting client field list.</span></span> <span data-ttu-id="60be1-111">큐브 뷰에 포함되었거나 포함되지 않은 계산된 열과 측정값은 여전히 제외된 개체 데이터에서 계산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60be1-111">Calculated columns and measures either included in a perspective or not can still calculate from object data that is excluded.</span></span>  
  
<span data-ttu-id="60be1-112">이 단원의 목적은 큐브 뷰를 만드는 방법을 설명하고 사용자가 테이블 형식 모델 작성 도구를 습득하도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="60be1-112">The purpose of this lesson is to describe how to create perspectives and become familiar with the tabular model authoring tools.</span></span> <span data-ttu-id="60be1-113">나중에 다른 테이블을 포함하도록 이 모델을 확장하면 모델의 다양한 관점(예: 재고 및 판매)을 정의하는 추가 큐브 뷰를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60be1-113">If you later expand this model to include additional tables, you can create additional perspectives to define different viewpoints of the model, for example, Inventory and Sales.</span></span>  
  
<span data-ttu-id="60be1-114">이 단원을 완료하기 위한 예상 시간: **5분**</span><span class="sxs-lookup"><span data-stu-id="60be1-114">Estimated time to complete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="60be1-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="60be1-115">Prerequisites</span></span>  
<span data-ttu-id="60be1-116">이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60be1-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="60be1-117">이 단원의 작업을 수행하기 전에 이전 단원인 [단원 7: 핵심 성과 지표 만들기](../tutorials/aas-lesson-7-create-key-performance-indicators.md)를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60be1-117">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  
  
## <a name="create-perspectives"></a><span data-ttu-id="60be1-118">큐브 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="60be1-118">Create perspectives</span></span>  
  
#### <a name="to-create-an-internet-sales-perspective"></a><span data-ttu-id="60be1-119">인터넷 판매 큐브 뷰를 만들려면</span><span class="sxs-lookup"><span data-stu-id="60be1-119">To create an Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="60be1-120">**모델** 메뉴 > **큐브 뷰** > **만들기 및 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60be1-120">Click the **Model** menu > **Perspectives** > **Create and Manage**.</span></span>  
  
2.  <span data-ttu-id="60be1-121">**큐브 뷰** 대화 상자에서 **새 큐브 뷰**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60be1-121">In the **Perspectives** dialog box, click **New Perspective**.</span></span>  
  
3.  <span data-ttu-id="60be1-122">**새 큐브 뷰** 열 머리글을 두 번 클릭한 후 **Internet Sales**로 이름을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="60be1-122">Double-click the **New Perspective** column heading, and then rename **Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="60be1-123">**DimCustomer**를 *제외*하고 모든 테이블을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60be1-123">Select the all the tables *except* **DimCustomer**.</span></span>  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    <span data-ttu-id="60be1-125">이후 단원에서는 Excel에서 분석 기능을 사용하여 이 큐브 뷰를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="60be1-125">In a later lesson, you use the Analyze in Excel feature to test this perspective.</span></span> <span data-ttu-id="60be1-126">Excel 피벗 테이블 필드 목록에는 DimCustomer 테이블을 제외한 각 테이블이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="60be1-126">The Excel PivotTable Fields List includes each table except the DimCustomer table.</span></span>  

## <a name="whats-next"></a><span data-ttu-id="60be1-127">다음 작업</span><span class="sxs-lookup"><span data-stu-id="60be1-127">What's next?</span></span>
<span data-ttu-id="60be1-128">[단원 9: 계층 구조 만들기](../tutorials/aas-lesson-9-create-hierarchies.md)</span><span class="sxs-lookup"><span data-stu-id="60be1-128">[Lesson 9: Create hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>
  
  
  
  
