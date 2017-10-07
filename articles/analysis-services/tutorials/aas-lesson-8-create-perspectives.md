---
title: "aaa \"Azure Analysis Services 자습서 단원 8 만들기 큐브 뷰 | \"Microsoft Docs"
description: "큐브 뷰 toocreate Azure Analysis Services tutorial 프로젝트 hello 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 25391813e1969ecb22af4d6f9c1ccd8358d812fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-8-create-perspectives"></a><span data-ttu-id="ef01c-103">단원 8: 큐브 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="ef01c-103">Lesson 8: Create perspectives</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="ef01c-104">이 단원에서는 인터넷 판매 큐브 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef01c-104">In this lesson, you create an Internet Sales perspective.</span></span> <span data-ttu-id="ef01c-105">큐브 뷰는 포커스가 있는, 비즈니스 또는 응용 프로그램별 관점을 제공하는 모델의 볼 수 있는 하위 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ef01c-105">A perspective defines a viewable subset of a model that provides focused, business-specific, or application-specific viewpoints.</span></span> <span data-ttu-id="ef01c-106">Tooa 모델 큐브 뷰를 사용 하 여 연결 하는 사용자, 이러한 모델 개체 (테이블, 열, 측정값, 계층 및 Kpi) 해당 큐브 뷰에 정의 된 필드로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef01c-106">When a user connects tooa model by using a perspective, they see only those model objects (tables, columns, measures, hierarchies, and KPIs) as fields defined in that perspective.</span></span> <span data-ttu-id="ef01c-107">toolearn 더 참조 [큐브 뷰](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef01c-107">toolearn more, see [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span></span>
  
<span data-ttu-id="ef01c-108">이 단원에서 만드는 Internet Sales 큐브 뷰에 hello hello DimCustomer 테이블 개체는 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef01c-108">hello Internet Sales perspective you create in this lesson excludes hello DimCustomer table object.</span></span> <span data-ttu-id="ef01c-109">보기에서 특정 개체를 제외 하는 큐브 뷰를 만들 때 해당 개체는 여전히 hello 모델에 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef01c-109">When you create a perspective that excludes certain objects from view, that object still exists in hello model.</span></span> <span data-ttu-id="ef01c-110">그러나 보고 클라이언트 필드 목록에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ef01c-110">However, it is not visible in a reporting client field list.</span></span> <span data-ttu-id="ef01c-111">큐브 뷰에 포함되었거나 포함되지 않은 계산된 열과 측정값은 여전히 제외된 개체 데이터에서 계산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef01c-111">Calculated columns and measures either included in a perspective or not can still calculate from object data that is excluded.</span></span>  
  
<span data-ttu-id="ef01c-112">hello이 단원의 목적은 toodescribe 어떻게 toocreate 큐브 뷰 및 hello 테이블 형식 모델 작성 도구에 잘 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef01c-112">hello purpose of this lesson is toodescribe how toocreate perspectives and become familiar with hello tabular model authoring tools.</span></span> <span data-ttu-id="ef01c-113">나중에이 모델 tooinclude 추가 테이블을 확장 하는 경우 toodefine 다양 한 뷰포인트 hello 모델의 예를 들어: Inventory 및 Sales 큐브 뷰를 추가로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef01c-113">If you later expand this model tooinclude additional tables, you can create additional perspectives toodefine different viewpoints of hello model, for example, Inventory and Sales.</span></span>  
  
<span data-ttu-id="ef01c-114">이 단원에서는 시간 toocomplete 예상: **5 분**</span><span class="sxs-lookup"><span data-stu-id="ef01c-114">Estimated time toocomplete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="ef01c-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ef01c-115">Prerequisites</span></span>  
<span data-ttu-id="ef01c-116">이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef01c-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="ef01c-117">이 단원에서는 hello 작업을 수행 하기 전에 완료 해야 hello 이전 단원: [7 단원: 핵심 성과 지표 만들기](../tutorials/aas-lesson-7-create-key-performance-indicators.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef01c-117">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  
  
## <a name="create-perspectives"></a><span data-ttu-id="ef01c-118">큐브 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="ef01c-118">Create perspectives</span></span>  
  
#### <a name="toocreate-an-internet-sales-perspective"></a><span data-ttu-id="ef01c-119">toocreate를 인터넷 판매 큐브 뷰</span><span class="sxs-lookup"><span data-stu-id="ef01c-119">toocreate an Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="ef01c-120">Hello 클릭 **모델** 메뉴 > **큐브 뷰** > **만들기 및 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef01c-120">Click hello **Model** menu > **Perspectives** > **Create and Manage**.</span></span>  
  
2.  <span data-ttu-id="ef01c-121">Hello에 **큐브 뷰** 대화 상자를 클릭 **새 큐브 뷰**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef01c-121">In hello **Perspectives** dialog box, click **New Perspective**.</span></span>  
  
3.  <span data-ttu-id="ef01c-122">Hello를 두 번 클릭 **새 큐브 뷰** 열 머리글을 한 후 이름 바꾸기를 **인터넷 판매**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef01c-122">Double-click hello **New Perspective** column heading, and then rename **Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="ef01c-123">선택 hello 모든 hello 테이블 *제외 하 고* **DimCustomer**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef01c-123">Select hello all hello tables *except* **DimCustomer**.</span></span>  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    <span data-ttu-id="ef01c-125">이후의 단원에서는 기능 tootest Excel에서에서 분석 hello이 큐브이 뷰를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef01c-125">In a later lesson, you use hello Analyze in Excel feature tootest this perspective.</span></span> <span data-ttu-id="ef01c-126">Excel 피벗 테이블 필드 목록 hello hello DimCustomer 테이블을 제외한 각 테이블이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef01c-126">hello Excel PivotTable Fields List includes each table except hello DimCustomer table.</span></span>  

## <a name="whats-next"></a><span data-ttu-id="ef01c-127">다음 작업</span><span class="sxs-lookup"><span data-stu-id="ef01c-127">What's next?</span></span>
<span data-ttu-id="ef01c-128">[단원 9: 계층 구조 만들기](../tutorials/aas-lesson-9-create-hierarchies.md)</span><span class="sxs-lookup"><span data-stu-id="ef01c-128">[Lesson 9: Create hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>
  
  
  
  
