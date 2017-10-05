---
title: Azure Application Insights Funnels
description: "Funnels를 사용하여 고객이 응용 프로그램과 상호 작용하는 방법을 검색하는 방법을 알아봅니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: cfreeman
ms.openlocfilehash: 85f47daaaff8967eb83c330bab839023f128b486
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="discover-how-customers-are-using-your-application-with-the-application-insights-funnels"></a><span data-ttu-id="a7863-103">Application Insights Funnels를 사용하여 고객이 응용 프로그램을 사용하는 방법 검색</span><span class="sxs-lookup"><span data-stu-id="a7863-103">Discover how customers are using your application with the Application Insights Funnels</span></span>

<span data-ttu-id="a7863-104">고객 환경을 이해하는 것이 비즈니스에 가장 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="a7863-104">Understanding customer experience is of the utmost importance to your business.</span></span> <span data-ttu-id="a7863-105">응용 프로그램이 여러 단계와 관련된 경우, 고객 대부분이 전체 프로세스를 거치는지 아니면 특정 시점에서 프로세스를 종료하는지를 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7863-105">If your application involves multiple stages, you will need to know if most customers are progressing through the entire process, or if they are ending the process at some point.</span></span> <span data-ttu-id="a7863-106">웹 응용 프로그램에서 일련의 단계를 거치는 것을 “깔때기”라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7863-106">The progression through a series of steps in a web application is known as a "funnel".</span></span> <span data-ttu-id="a7863-107">Application Insights Funnels를 사용하여 사용자에 대한 정보를 얻고 단계별 전환율을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7863-107">You can use the Application Insights Funnels to gain insights into your users and monitor step-by-step conversion rates.</span></span> 

## <a name="get-started-with-the-funnels-blade"></a><span data-ttu-id="a7863-108">Funnels 블레이드 시작</span><span class="sxs-lookup"><span data-stu-id="a7863-108">Get started with the Funnels blade</span></span>
<span data-ttu-id="a7863-109">Funnels에 대해 알아보는 가장 쉬운 방법은 예제를 살펴보는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a7863-109">The easiest way to learn about Funnels is to walk though an example.</span></span> <span data-ttu-id="a7863-110">다음 그림에서는 전자상거래 비즈니스 소유자가 고객이 자사 웹 응용 프로그램과 상호 작용하는 방법을 알아보기 위해 수행하는 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a7863-110">The following illustrations demonstrate the steps owners of an e-commerce business would take to learn how their customers interact with their web application.</span></span>  

### <a name="create-your-funnel"></a><span data-ttu-id="a7863-111">깔때기 만들기</span><span class="sxs-lookup"><span data-stu-id="a7863-111">Create your funnel</span></span>
<span data-ttu-id="a7863-112">깔때기를 만들기 전에 먼저 답변하려는 질문에 관해 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7863-112">Before you create your funnel, you need to decide on the question you want to answer.</span></span> <span data-ttu-id="a7863-113">예를 들어 홈페이지를 보는 고객 중 광고를 클릭하는 고객이 얼마나 되는지를 알고 싶을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7863-113">For example, you might want to know how many customers viewing your home page click on an advertisement.</span></span> <span data-ttu-id="a7863-114">이 예제에서는 Fabrikam Fiber 회사 소유자가 지난 달에 쇼핑 카트에 항목을 추가한 후 구매한 고객의 비율을 알고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7863-114">In this example, the owners of the Fabrikam Fiber company want to know the percentage of customers who make a purchase after adding items to their shopping cart during the last month.</span></span>

<span data-ttu-id="a7863-115">깔때기를 만들기 위해 수행하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a7863-115">Here are the steps they take to create their funnel.</span></span>

1. <span data-ttu-id="a7863-116">Funnels 블레이드에서 새로 만들기 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7863-116">Click the New button on the Funnels blade.</span></span>
1. <span data-ttu-id="a7863-117">**시간 범위** 드롭다운에서 “지난 달” 시간 범위를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7863-117">Select the time range of "Last month" from the **Time Range** drop-down.</span></span> 
1. <span data-ttu-id="a7863-118">**1단계** 드롭다운 목록에서 **제품 페이지** 이벤트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7863-118">Select the **Product page** event from the **Step 1** drop-down list.</span></span> 
1. <span data-ttu-id="a7863-119">**2단계** 드롭다운 목록에서 **쇼핑 카트에 추가** 이벤트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7863-119">Select the **Add to shopping cart** event from the **Step 2** drop-down list.</span></span>
1. <span data-ttu-id="a7863-120">**3단계** 드롭다운 목록에서 **구매 클릭** 이벤트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7863-120">Select the **Click purchase** event from the **Step 3** drop-down list.</span></span>
1. <span data-ttu-id="a7863-121">깔때기에 이름을 추가하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7863-121">Add a name to the funnel and click **Save**.</span></span>

<span data-ttu-id="a7863-122">다음 그림에서는 Funnels 블레이드에서 생성하는 데이터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a7863-122">The following illustration demonstrates the data the Funnels blade generates.</span></span> <span data-ttu-id="a7863-123">여기서 Fabrikam 소유자는 지난 주 동안 쇼핑 카트에 항목을 추가한 고객의 22.7%가 구매를 완료한 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7863-123">From here the Fabrikam owners can see that during the last week, 22.7% of their customers who added an item to their shopping cart completed the purchase.</span></span> <span data-ttu-id="a7863-124">또한 고객의 1%는 제품 페이지를 방문하기 전에 광고를 클릭했으며, 고객의 20%는 구매를 완료한 후 로그아웃한 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7863-124">They can also see that 1% of the customers clicked an advertisement before visiting the product page, and 20% of their customers signed out after completing their purchase.</span></span>


![데이터가 포함된 Funnels 블레이드](./media/app-insights-understand-usage-patterns/funnel1.png)

## <a name="next-steps"></a><span data-ttu-id="a7863-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a7863-126">Next steps</span></span>
- <span data-ttu-id="a7863-127">[사용량 분석](app-insights-usage-overview.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a7863-127">Learn more about [usage analysis](app-insights-usage-overview.md).</span></span> 
