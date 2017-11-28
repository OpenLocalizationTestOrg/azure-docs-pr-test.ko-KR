---
title: "만들고 Azure 로그 분석에서 로그 쿼리를 편집 하기 위한 aaaPortals | Microsoft Docs"
description: "이 문서에서는 hello 포털 toocreate Azure 로그 분석에서에서 사용 하 고 로그 검색을 편집할 수 있는지를 설명 합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 7a2657574a132b2c4298511bb31259e68113ac91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="portals-for-creating-and-editing-log-queries-in-azure-log-analytics"></a><span data-ttu-id="e0253-103">Azure Log Analytics에서 로그 쿼리를 만들고 편집하기 위한 포털 | Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="e0253-103">Portals for creating and editing log queries in Azure Log Analytics</span></span>

> [!NOTE]
> <span data-ttu-id="e0253-104">이 문서에서는 hello 새로운 쿼리 언어를 사용 하 여 Azure 로그 분석에서 포털을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0253-104">This article describes portals in Azure Log Analytics using hello new query language.</span></span>  <span data-ttu-id="e0253-105">Hello 새 언어에 대 한 자세한 정보를 hello 프로시저 tooupgrade 작업 영역을 가져올 수 [Azure 로그 분석 작업 영역 toonew 로그 검색을 업그레이드](log-analytics-log-search-upgrade.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0253-105">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  
>
> <span data-ttu-id="e0253-106">작업 영역에는 업그레이드 된 toohello 새로운 쿼리 언어 되지 않았는지를 하는 경우를 참조 해야 너무[로그 분석 로그 검색을 사용 하 여 데이터를 찾을](log-analytics-log-searches.md) hello hello 로그 검색 포털의 최신 버전에 대 한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0253-106">If your workspace hasn't been upgraded toohello new query language, you should refer too[Find data using log searches in Log Analytics](log-analytics-log-searches.md) for information on hello current version of hello Log Search portal.</span></span>

<span data-ttu-id="e0253-107">Hello 작업 영역에서 다양 한 로그 분석 tooretrieve 데이터 부분에서에서 로그 검색을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0253-107">You use log searches in a variety of places throughout Log Analytics tooretrieve data from hello workspace.</span></span>  <span data-ttu-id="e0253-108">실제로 만들고 쿼리를 편집 하기 위한 또한 tooworking와 대화형 데이터를 반환 하지만, 아래에 설명한 두 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0253-108">For actually creating and editing queries in addition tooworking interactively with returned data though, you have two options that are described below.</span></span>  

## <a name="log-search-portal"></a><span data-ttu-id="e0253-109">로그 검색 포털</span><span class="sxs-lookup"><span data-stu-id="e0253-109">Log search portal</span></span>
<span data-ttu-id="e0253-110">hello 로그 검색 포털은 Azure 포털 hello 또는 hello OMS 포털에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0253-110">hello Log Search portal is accessible from hello Azure portal or hello OMS portal.</span></span>  <span data-ttu-id="e0253-111">한 줄에 만들 수 있는 기본 쿼리를 만들기에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="e0253-111">It's suitable for creating basic queries that can be created on a single line.</span></span>  <span data-ttu-id="e0253-112">hello 로그 검색 포털 외부 포털을 시작 하지 않고도 사용할 수 있으며 경고 규칙을 만들고 컴퓨터 그룹을 만들고, hello hello 쿼리 결과 내보내는 포함 하 여 로그 검색으로 다양 한 기능 tooperform 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0253-112">hello Log Search portal can be used without launching an external portal, and you can use it tooperform a variety of functions with log searches including creating alert rules, creating computer groups, and exporting hello results of hello query.</span></span>  

<span data-ttu-id="e0253-113">hello 로그 검색 포털 hello 쿼리 언어의 완전 한 지식이 필요 없이 hello 쿼리를 편집 하기 위해 여러 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0253-113">hello Log Search portal provides multiple features for editing hello query without having a full knowledge of hello query language.</span></span>  <span data-ttu-id="e0253-114">이러한 기능에 대 한 요약을 가져올 수 있습니다 [hello 로그 검색 포털을 사용 하는 Azure 로그 분석에서 Create 로그 검색](log-analytics-log-search-log-search-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0253-114">You can get a summary of these features in [Create log searches in Azure Log Analytics using hello Log Search portal](log-analytics-log-search-log-search-portal.md).</span></span>


![로그 검색 포털](media/log-analytics-log-search-portals/log-search-portal.png)

## <a name="advanced-analytics-portal"></a><span data-ttu-id="e0253-116">고급 분석 포털</span><span class="sxs-lookup"><span data-stu-id="e0253-116">Advanced Analytics portal</span></span>
<span data-ttu-id="e0253-117">hello 고급 분석 포털은 hello 로그 검색 포털에서 사용할 수 없는 고급 기능을 제공 하는 전용된 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="e0253-117">hello Advanced Analytics portal is a dedicated portal that provides advanced functionality not available in hello Log Search portal.</span></span>  <span data-ttu-id="e0253-118">기능으로는 hello 기능 tooedit 여러 줄에 대 한 쿼리, 선택적으로 코드, 상황에 맞는 Intellisense 및 스마트 분석을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0253-118">Features include hello ability tooedit a query on multiple lines, selectively execute code, context sensitive Intellisense, and Smart Analytics.</span></span>  <span data-ttu-id="e0253-119">hello Advanced Analytics 포털은 복잡 한 쿼리는 다음 로그 검색으로 저장 하거나 복사 하 여 다른 로그 분석 요소에 붙여 넣은 디자인 하는 데 가장 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0253-119">hello Advanced Analytics portal is most suitable for designing complex queries that are either saved as a log search or copied and pasted into other Log Analytics elements.</span></span>  <span data-ttu-id="e0253-120">하면 hello 로그 검색 포털의 링크에서 hello Advanced Analytics 포털을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e0253-120">You launch hello Advanced Analytics portal from a link in hello Log Search portal.</span></span>

![고급 분석 포털](media/log-analytics-log-search-portals/advanced-analytics-portal.png)


<span data-ttu-id="e0253-122">고급 기능으로 인해 일반적으로 사용 hello 고급 분석 포털 기본 도구를 만들고 쿼리를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0253-122">Because of its advanced features, you'll usually use hello Advanced Analytics portal as your primary tool for creating and editing queries.</span></span>  <span data-ttu-id="e0253-123">확인 한 후 예상 대로 작동 하는 hello 쿼리 다음 복사 하 고 로그 검색 포털 hello 또는 뷰 디자이너와 같은 다른 곳에서 붙여 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0253-123">Once you've determined that hello query works as expected, then you'll copy and paste it elsewhere such as hello Log Search portal or View Designer.</span></span>  <span data-ttu-id="e0253-124">Hello Advanced Analytics 포털 여러 줄이 포함 된 쿼리를 통해 지원 하므로이 포털에서 쿼리를 복사 하는 경우 tootake hello 다음 사항을 고려 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0253-124">Because hello Advanced Analytics portal supports queries with multiple lines though, you need tootake hello following into consideration when copying a query from this portal.</span></span>

- <span data-ttu-id="e0253-125">에 복사 하 고 다른 위치에 붙여 hello 쿼리에서 주석은 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0253-125">Comments must be removed from hello query before it's copied and pasted into another location.</span></span>  <span data-ttu-id="e0253-126">줄 앞에 슬래시(//) 두 개를 삽입하면 주석을 달 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0253-126">You can comment a line by preceding it with two slashes (//).</span></span>  <span data-ttu-id="e0253-127">여러 줄 쿼리를 한 줄로 붙여넣는 경우 줄 바꿈이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0253-127">When you paste a multiple line query into a single line, line breaks are removed.</span></span>  <span data-ttu-id="e0253-128">코멘트가 포함 hello 첫 번째 주석 뒤의 모든 문자가 hello 주석 처리를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0253-128">If comments are included, all characters after hello first comment are considered part of hello comment.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e0253-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e0253-129">Next steps</span></span>

- <span data-ttu-id="e0253-130">Hello를 사용 하는 자습서를 살펴보면서 [로그 검색 포털](log-analytics-log-search-log-search-portal.md) 또는 hello [Advanced Analytics 포털](https://go.microsoft.com/fwlink/?linkid=856587) toocreate 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0253-130">Walk through a tutorial on using hello [Log Search portal](log-analytics-log-search-log-search-portal.md) or hello [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587) toocreate queries.</span></span>
- <span data-ttu-id="e0253-131">체크 아웃 한 [쿼리 작성의 자습서](https://go.microsoft.com/fwlink/?linkid=856078) hello 새로운 쿼리 언어를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0253-131">Check out a [tutorial on writing queries](https://go.microsoft.com/fwlink/?linkid=856078) using hello new query language.</span></span>
