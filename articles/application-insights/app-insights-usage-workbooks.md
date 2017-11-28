---
title: "Azure Application Insights의 대화형 통합 문서와 aaaInvestigate 및 공유 사용 현황 데이터 | Microsoft docs"
description: "웹앱의 사용자 인구 통계 분석입니다."
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: bdcebe0f97fdad0a0b301df5950dc09698f5a4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a><span data-ttu-id="60b87-103">Application Insights에서 대화형 통합 문서를 사용하여 사용 현황 데이터 조사 및 공유</span><span class="sxs-lookup"><span data-stu-id="60b87-103">Investigate and share usage data with interactive workbooks in Application Insights</span></span>

<span data-ttu-id="60b87-104">통합 문서는 [Azure Application Insights](app-insights-overview.md) 데이터 시각화, [분석 쿼리](app-insights-analytics.md) 및 텍스트를 대화형 문서로 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-104">Workbooks combine [Azure Application Insights](app-insights-overview.md) data visualizations, [Analytics queries](app-insights-analytics.md), and text into interactive documents.</span></span> <span data-ttu-id="60b87-105">통합 문서는 편집 가능한 다른 팀 멤버가 액세스 toohello와 같은 Azure 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-105">Workbooks are editable by other team members with access toohello same Azure resource.</span></span> <span data-ttu-id="60b87-106">즉, hello 쿼리와 컨트롤 사용 되는 toocreate 통합 문서는 쉽게 tooexplore 있도록 hello 통합 문서를 읽는 사용 가능한 tooother 사용자, 확장 및 실수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-106">This means hello queries and controls used toocreate a workbook are available tooother people reading hello workbook, making them easy tooexplore, extend, and check for mistakes.</span></span>

<span data-ttu-id="60b87-107">통합 문서는 다음과 같은 시나리오에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-107">Workbooks are helpful for scenarios like:</span></span>

* <span data-ttu-id="60b87-108">응용 프로그램의 hello 사용을 탐색 하 여 관심 있는 메트릭 hello를 사전에 모르는 경우: 사용자, 보존 율이 높아지고, 변환율 등의 숫자입니다. Application Insights의 다른 사용 현황 분석 도구와는 달리 통합 문서를 통해 이러한 종류의 자유 형식 탐색에 매우 유용하도록 여러 종류의 시각화 및 분석을 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-108">Exploring hello usage of your app when you don't know hello metrics of interest in advance: numbers of users, retention rates, conversion rates, etc. Unlike other usage analytics tools in Application Insights, workbooks let you combine multiple kinds of visualizations and analyses, making them great for this kind of free-form exploration.</span></span>
* <span data-ttu-id="60b87-109">Tooyour 팀 새로 릴리스된 기능 수행 되는 방법을 설명 하는, 보여 주는 사용자에 의해 계산 키 상호 작용 및 기타 수치에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-109">Explaining tooyour team how a newly released feature is performing, by showing user counts for key interactions and other metrics.</span></span>
* <span data-ttu-id="60b87-110">공유는 A의 hello 결과 팀의 다른 멤버와 응용 프로그램에서 실험 B /입니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-110">Sharing hello results of an A/B experiment in your app with other members of your team.</span></span> <span data-ttu-id="60b87-111">Hello에 대 한 hello 목표 텍스트를 사용해 다음 각 사용량 메트릭을 표시 하 고 각 메트릭에 위 또는 아래-대상 했는지 여부에 대 한 지우기 설명선 함께 tooevaluate hello 실험을 사용 하는 분석 쿼리를 설명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-111">You can explain hello goals for hello experiment with text, then show each usage metric and Analytics query used tooevaluate hello experiment, along with clear call-outs for whether each metric was above- or below-target.</span></span>
* <span data-ttu-id="60b87-112">응용 프로그램 데이터, 텍스트 설명과 hello 앞에 다음 단계 tooprevent 중단에 대 한 내용은 결합의 hello 사용에 중단의 영향 hello를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-112">Reporting hello impact of an outage on hello usage of your app, combining data, text explanation, and a discussion of next steps tooprevent outages in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="60b87-113">Application Insights 리소스 페이지 뷰 또는 사용자 지정 이벤트 toouse 통합 문서에 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-113">Your Application Insights resource must contain page views or custom events toouse workbooks.</span></span> <span data-ttu-id="60b87-114">[Tooset 앱 toocollect 페이지를 자동으로 hello Application Insights JavaScript SDK로 보는 방법에 대해 알아봅니다](app-insights-javascript.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-114">[Learn how tooset up your app toocollect page views automatically with hello Application Insights JavaScript SDK](app-insights-javascript.md).</span></span>
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a><span data-ttu-id="60b87-115">통합 문서 섹션 편집, 다시 정렬, 복제 및 삭제</span><span class="sxs-lookup"><span data-stu-id="60b87-115">Editing, rearranging, cloning, and deleting workbook sections</span></span>

<span data-ttu-id="60b87-116">통합 문서는 개별 편집 가능한 사용 현황 시각화, 차트, 테이블, 텍스트 또는 분석 쿼리 결과의 섹션으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-116">A workbook is a made of sections: independently editable usage visualizations, charts, tables, text, or Analytics query results.</span></span>

<span data-ttu-id="60b87-117">통합 문서 섹션의 tooedit hello 내용을 클릭 hello **편집** 아래 단추 및 toohello hello 통합 문서 섹션의 오른쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-117">tooedit hello contents of a workbook section, click hello **Edit** button below and toohello right of hello workbook section.</span></span>

![Application Insights 통합 문서 섹션 편집 컨트롤](./media/app-insights-usage-workbooks/editing-controls.png)

1. <span data-ttu-id="60b87-119">완료 하면 클릭 섹션을 편집 **편집 수행** hello 하단 왼쪽된 모서리 hello 섹션에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-119">When you're done editing a section, click **Done Editing** in hello bottom left corner of hello section.</span></span>

2. <span data-ttu-id="60b87-120">섹션의 중복 toocreate 클릭 hello **이 섹션을 복제할** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-120">toocreate a duplicate of a section, click hello **Clone this section** icon.</span></span> <span data-ttu-id="60b87-121">중복 된 섹션을 만들기 이전 반복을 손실 하지 않고 쿼리에 훌륭한 tooway tooiterate입니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-121">Creating duplicate sections is a great tooway tooiterate on a query without losing previous iterations.</span></span>

3. <span data-ttu-id="60b87-122">통합 문서에서 섹션 toomove 클릭 hello **위로 이동** 또는 **아래로 이동** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-122">toomove up a section in a workbook, click hello **Move up** or **Move down** icon.</span></span>

4. <span data-ttu-id="60b87-123">영구적으로 클릭 하 여 hello tooremove 섹션 **제거** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-123">tooremove a section permanently, click hello **Remove** icon.</span></span>

## <a name="adding-usage-data-visualization-sections"></a><span data-ttu-id="60b87-124">사용 현황 데이터 시각화 섹션 추가</span><span class="sxs-lookup"><span data-stu-id="60b87-124">Adding usage data visualization sections</span></span>

<span data-ttu-id="60b87-125">통합 문서는 네 가지 유형의 기본 제공 사용 현황 분석 시각화를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-125">Workbooks offer four types of built-in usage analytics visualizations.</span></span> <span data-ttu-id="60b87-126">각 응용 프로그램의 hello 사용에 대 한 일반적인 질문에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-126">Each answers a common question about hello usage of your app.</span></span> <span data-ttu-id="60b87-127">tooadd 테이블 및 차트 이러한 4 개의 섹션 이외의 분석 쿼리 섹션 (아래 참조)를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-127">tooadd tables and charts other than these four sections, add Analytics query sections (see below).</span></span>

<span data-ttu-id="60b87-128">tooadd 사용자, 세션, 이벤트 또는 보존 섹션 tooyour 통합 문서를 사용 하 여 hello **사용자 추가** 또는 기타 해당 단추 hello hello 통합 문서 맨 아래에 또는 hello 섹션 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-128">tooadd a Users, Sessions, Events, or Retention section tooyour workbook, use hello **Add Users** or other corresponding button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

![통합 문서의 사용자 섹션](./media/app-insights-usage-workbooks/users-section.png)

<span data-ttu-id="60b87-130">**사용자** 섹션은 "내 사이트의 일부 페이지를 보거나 일부 기능을 사용한 사용자의 수는?"에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-130">**Users** sections answer "How many users viewed some page or used some feature of my site?"</span></span>

<span data-ttu-id="60b87-131">**세션** 섹션은 "사용자가 내 사이트의 일부 페이지를 보거나 일부 기능을 사용하는 데 소비한 세션의 수는?"에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-131">**Sessions** sections answer "How many sessions did users spend viewing some page or using some feature of my site?"</span></span>

<span data-ttu-id="60b87-132">**이벤트** 섹션은 "사용자가 내 사이트의 일부 페이지를 보거나 일부 기능을 사용한 시간은?"에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-132">**Events** sections answer "How many times did users view some page or use some feature of my site?"</span></span>

<span data-ttu-id="60b87-133">이러한 각 유형의 세 가지 섹션을 hello 컨트롤 및 시각화의 동일한 집합 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-133">Each of these three section types offers hello same sets of controls and visualizations:</span></span>

* [<span data-ttu-id="60b87-134">사용자, 세션 및 이벤트 섹션 편집에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="60b87-134">Learn more about editing Users, Sessions, and Events sections</span></span>](app-insights-usage-segmentation.md)
* <span data-ttu-id="60b87-135">Hello 기본 차트, 히스토그램 표, 자동 insights 및 hello를 사용 하 여 샘플 사용자 시각화를 설정/해제 **차트 표시**, **눈금 표시**, **표시 Insights**, 및 **이러한 사용자가 샘플** hello 위쪽 각 섹션의 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-135">Toggle hello main chart, histogram grids, automatic insights, and sample users visualizations using hello **Show Chart**, **Show Grid**, **Show Insights**, and **Sample of These Users** checkboxes at hello top of each section.</span></span>

![통합 문서의 재방문 주기 섹션](./media/app-insights-usage-workbooks/retention-section.png)

<span data-ttu-id="60b87-137">**재방문 주기** 섹션은 "1일 또는 1주일에 일부 페이지를 보거나 일부 기능을 사용한 사용자 중 다음 날이나 다음 주에 다시 방문한 사용자 수는?"에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-137">**Retention** sections answer "Of people who viewed some page or used some feature on one day or week, how many came back in a subsequent day or week?"</span></span>

* [<span data-ttu-id="60b87-138">재방문 주기 섹션 편집에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="60b87-138">Learn more about editing Retention sections</span></span>](app-insights-usage-retention.md)
* <span data-ttu-id="60b87-139">설정/해제 hello 선택적인 전반적인 보존 차트 hello를 사용 하 여 **표시 전반적인 보존 차트** hello 위쪽 hello 섹션의 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-139">Toggle hello optional Overall Retention chart using hello **Show overall retention chart** checkbox at hello top of hello section.</span></span>

## <a name="adding-application-insights-analytics-sections"></a><span data-ttu-id="60b87-140">Application Insights 분석 섹션 추가</span><span class="sxs-lookup"><span data-stu-id="60b87-140">Adding Application Insights Analytics sections</span></span>

![통합 문서의 분석 섹션](./media/app-insights-usage-workbooks/analytics-section.png)

<span data-ttu-id="60b87-142">응용 프로그램 통찰력 분석 쿼리 섹션 tooyour 통합 tooadd hello를 사용 하 여 **추가 분석 쿼리에서** hello hello 통합 문서 맨 아래에 또는 만큼의 hello 아래쪽 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-142">tooadd an Application Insights Analytics query section tooyour workbook, use hello **Add Analytics query** button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

<span data-ttu-id="60b87-143">분석 쿼리 섹션을 사용하면 통합 문서에 Application Insights 데이터에 대해 임의 쿼리를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-143">Analytics query sections let you add arbitrary queries over your Application Insights data into workbooks.</span></span> <span data-ttu-id="60b87-144">이러한 유연성 분석 쿼리 섹션 프로그램 go toofor hello와 같은 사용자, 세션, 이벤트 및 보존에 대 한 위에 나열 된 4 아닌 다른 사이트에 대 한 모든 질문에 대답 해야 합니다.을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-144">This flexibility means Analytics query sections should be your go-toofor answering any questions about your site other than hello four listed above for Users, Sessions, Events, and Retention, like:</span></span>

* <span data-ttu-id="60b87-145">예외 수 않은 사용량에서 감소 기간 시간이 hello 하는 동안 사용자 사이트 throw?</span><span class="sxs-lookup"><span data-stu-id="60b87-145">How many exceptions did your site throw during hello same time period as a decline in usage?</span></span>
* <span data-ttu-id="60b87-146">일부 페이지를 보는 사용자에 대 한 페이지 로드 시간의 hello 분포는 무엇 이었습니까?</span><span class="sxs-lookup"><span data-stu-id="60b87-146">What was hello distribution of page load times for users viewing some page?</span></span>
* <span data-ttu-id="60b87-147">사이트의 일부 페이지 집합을 봤지만 다른 일부 페이지 집합을 보지 않은 사용자의 수는?</span><span class="sxs-lookup"><span data-stu-id="60b87-147">How many users viewed some set of pages on your site, but not some other set of pages?</span></span> <span data-ttu-id="60b87-148">다른 사이트의 기능 하위 집합을 사용 하는 사용자의 클러스터가 있는 경우 유용 toounderstand 수 있습니다 (hello를 사용 하 여 `join` hello로 연산자 `kind=leftanti` hello 로그 분석 쿼리 언어에서에서 한정자).</span><span class="sxs-lookup"><span data-stu-id="60b87-148">This can be useful toounderstand if you have clusters of users who use different subsets of your site's functionality (use hello `join` operator with hello `kind=leftanti` modifier in hello Log Analytics query language).</span></span>

<span data-ttu-id="60b87-149">사용 하 여 hello [로그 분석 쿼리 언어 참조](https://docs.loganalytics.io/) toolearn 쿼리를 작성 하는 방법에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-149">Use hello [Log Analytics query language reference](https://docs.loganalytics.io/) toolearn more about writing queries.</span></span>

## <a name="adding-text-and-markdown-sections"></a><span data-ttu-id="60b87-150">텍스트 및 Markdown 섹션 추가</span><span class="sxs-lookup"><span data-stu-id="60b87-150">Adding text and Markdown sections</span></span>

<span data-ttu-id="60b87-151">제목, 설명 및 해설 tooyour 통합 문서 추가 narrative 테이블 및 차트의 집합을 변환 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-151">Adding headings, explanations, and commentary tooyour workbooks helps turn a set of tables and charts into a narrative.</span></span> <span data-ttu-id="60b87-152">통합 문서에 텍스트 부분 지원 hello [마크 다운 구문](https://daringfireball.net/projects/markdown/) 텍스트 서식 지정, 머리글, 굵게, 기울임꼴 등 글머리 기호 목록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-152">Text sections in workbooks support hello [Markdown syntax](https://daringfireball.net/projects/markdown/) for text formatting, like headings, bold, italics, and bulleted lists.</span></span>

<span data-ttu-id="60b87-153">tooadd 텍스트 섹션 tooyour 통합 문서를 사용 하 여 hello **텍스트 추가** 단추 hello hello 통합 문서 맨 아래에 또는 hello 섹션 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-153">tooadd a text section tooyour workbook, use hello **Add text** button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

## <a name="saving-and-sharing-workbooks-with-your-team"></a><span data-ttu-id="60b87-154">팀과 통합 문서 저장 및 공유</span><span class="sxs-lookup"><span data-stu-id="60b87-154">Saving and sharing workbooks with your team</span></span>

<span data-ttu-id="60b87-155">Hello에는 Application Insights 리소스 내에서 통합 문서 저장 **내 보고서** 개인 tooyou 인 구역 또는 hello **공유 보고서** 섹션에 액세스할 수 있는 액세스 가능한 tooeveryone Application Insights 리소스 toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-155">Workbooks are saved within an Application Insights resource, either in hello **My Reports** section that's private tooyou or in hello **Shared Reports** section that's accessible tooeveryone with access toohello Application Insights resource.</span></span> <span data-ttu-id="60b87-156">tooview hello 리소스에서 모든 hello 통합 문서 클릭 hello **열려** hello 작업 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-156">tooview all hello workbooks in hello resource, click hello **Open** button in hello action bar.</span></span>

<span data-ttu-id="60b87-157">통합 문서에 현재 있는 tooshare **내 보고서**:</span><span class="sxs-lookup"><span data-stu-id="60b87-157">tooshare a workbook that's currently in **My Reports**:</span></span>

1. <span data-ttu-id="60b87-158">클릭 **열려** hello 작업 모음에</span><span class="sxs-lookup"><span data-stu-id="60b87-158">Click **Open** in hello action bar</span></span>
2. <span data-ttu-id="60b87-159">Hello "..." 단추를 클릭 hello 통합 문서 옆에 있는 tooshare</span><span class="sxs-lookup"><span data-stu-id="60b87-159">Click hello "..." button beside hello workbook you want tooshare</span></span>
3. <span data-ttu-id="60b87-160">클릭 **tooShared 보고서 이동**합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-160">Click **Move tooShared Reports**.</span></span>

<span data-ttu-id="60b87-161">통합 문서 링크와 함께 또는 전자 메일을 통해 tooshare 클릭 **공유** hello 작업 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-161">tooshare a workbook with a link or via email, click **Share** in hello action bar.</span></span> <span data-ttu-id="60b87-162">Hello 링크의 받는 사람에 게 hello Azure 포털 tooview hello 통합 문서에서 toothis 리소스에 액세스할 필요 있음을 염두에서에 둬야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-162">Keep in mind that recipients of hello link need access toothis resource in hello Azure portal tooview hello workbook.</span></span> <span data-ttu-id="60b87-163">toomake 편집 받는 사람에 게 필요 이상의 참가자 권한을 hello 리소스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-163">toomake edits, recipients need at least Contributor permissions for hello resource.</span></span>

<span data-ttu-id="60b87-164">Azure 대시보드 링크 tooa 통합 문서 tooan toopin:</span><span class="sxs-lookup"><span data-stu-id="60b87-164">toopin a link tooa workbook tooan Azure Dashboard:</span></span>

1. <span data-ttu-id="60b87-165">클릭 **열려** hello 작업 모음에</span><span class="sxs-lookup"><span data-stu-id="60b87-165">Click **Open** in hello action bar</span></span>
2. <span data-ttu-id="60b87-166">Hello "..." 단추를 클릭 hello 통합 문서 옆에 있는 toopin</span><span class="sxs-lookup"><span data-stu-id="60b87-166">Click hello "..." button beside hello workbook you want toopin</span></span>
3. <span data-ttu-id="60b87-167">클릭 **Pin toodashboard**합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-167">Click **Pin toodashboard**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60b87-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="60b87-168">Next steps</span></span>

## <a name="next-steps"></a><span data-ttu-id="60b87-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="60b87-169">Next steps</span></span>
- <span data-ttu-id="60b87-170">tooenable 사용 경험을 보내기 시작 [사용자 지정 이벤트](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) 또는 [페이지 보기](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views)합니다.</span><span class="sxs-lookup"><span data-stu-id="60b87-170">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="60b87-171">사용자 지정 이벤트 또는 페이지 뷰 탐색 hello 사용 도구 toolearn 이미 보낼 사용자 서비스를 사용할 방법.</span><span class="sxs-lookup"><span data-stu-id="60b87-171">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="60b87-172">사용자, 세션, 이벤트</span><span class="sxs-lookup"><span data-stu-id="60b87-172">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="60b87-173">깔때기</span><span class="sxs-lookup"><span data-stu-id="60b87-173">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="60b87-174">보존</span><span class="sxs-lookup"><span data-stu-id="60b87-174">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="60b87-175">사용자 흐름</span><span class="sxs-lookup"><span data-stu-id="60b87-175">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="60b87-176">사용자 컨텍스트 추가</span><span class="sxs-lookup"><span data-stu-id="60b87-176">Add user context</span></span>](app-insights-usage-send-user-context.md)
    
