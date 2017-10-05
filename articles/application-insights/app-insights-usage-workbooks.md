---
title: "Azure Application Insights에서 대화형 통합 문서를 사용하여 사용 현황 데이터 조사 및 공유 | Microsoft docs"
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
ms.openlocfilehash: 75028b4fbda43d90f56690a33c7eb624fce049c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a><span data-ttu-id="171a3-103">Application Insights에서 대화형 통합 문서를 사용하여 사용 현황 데이터 조사 및 공유</span><span class="sxs-lookup"><span data-stu-id="171a3-103">Investigate and share usage data with interactive workbooks in Application Insights</span></span>

<span data-ttu-id="171a3-104">통합 문서는 [Azure Application Insights](app-insights-overview.md) 데이터 시각화, [분석 쿼리](app-insights-analytics.md) 및 텍스트를 대화형 문서로 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-104">Workbooks combine [Azure Application Insights](app-insights-overview.md) data visualizations, [Analytics queries](app-insights-analytics.md), and text into interactive documents.</span></span> <span data-ttu-id="171a3-105">통합 문서는 동일한 Azure 리소스에 대한 액세스로 다른 팀 멤버가 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-105">Workbooks are editable by other team members with access to the same Azure resource.</span></span> <span data-ttu-id="171a3-106">즉 통합 문서를 만드는 데 사용되는 쿼리 및 컨트롤을 통합 문서를 읽고 오류를 탐색, 확장 및 확인하기 쉽게 만드는 다른 사용자가 사용할 수 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-106">This means the queries and controls used to create a workbook are available to other people reading the workbook, making them easy to explore, extend, and check for mistakes.</span></span>

<span data-ttu-id="171a3-107">통합 문서는 다음과 같은 시나리오에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-107">Workbooks are helpful for scenarios like:</span></span>

* <span data-ttu-id="171a3-108">관심 있는 메트릭을 사전에 모르는 경우 앱의 사용 현황 탐색: 사용자 수, 재방문 주기율, 변환율 등 Application Insights의 다른 사용 현황 분석 도구와는 달리 통합 문서를 통해 이러한 종류의 자유 형식 탐색에 매우 유용하도록 여러 종류의 시각화 및 분석을 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-108">Exploring the usage of your app when you don't know the metrics of interest in advance: numbers of users, retention rates, conversion rates, etc. Unlike other usage analytics tools in Application Insights, workbooks let you combine multiple kinds of visualizations and analyses, making them great for this kind of free-form exploration.</span></span>
* <span data-ttu-id="171a3-109">팀에 주요 상호 작용 및 다른 메트릭에 대한 사용자 수를 보여 주어 새로 릴리스된 기능이 수행되는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-109">Explaining to your team how a newly released feature is performing, by showing user counts for key interactions and other metrics.</span></span>
* <span data-ttu-id="171a3-110">앱에서 A/B 실험의 결과를 팀의 다른 멤버와 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-110">Sharing the results of an A/B experiment in your app with other members of your team.</span></span> <span data-ttu-id="171a3-111">텍스트로 실험에 대한 목표를 설명한 다음 각 메트릭이 위 또는 아래-대상이었는지 여부에 대한 분명한 설명선과 함께 실험을 평가하는 데 사용되는 각 사용 현황 메트릭 및 분석 쿼리를 보여줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-111">You can explain the goals for the experiment with text, then show each usage metric and Analytics query used to evaluate the experiment, along with clear call-outs for whether each metric was above- or below-target.</span></span>
* <span data-ttu-id="171a3-112">데이터, 텍스트 설명 및 차후의 중단을 방지하기 위한 다음 단계의 논의를 결합하여 앱의 사용 현황에 대한 중단의 영향을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-112">Reporting the impact of an outage on the usage of your app, combining data, text explanation, and a discussion of next steps to prevent outages in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="171a3-113">Application Insights 리소스는 통합 문서를 사용하기 위한 페이지 뷰 또는 사용자 지정 이벤트를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-113">Your Application Insights resource must contain page views or custom events to use workbooks.</span></span> <span data-ttu-id="171a3-114">[Application Insights JavaScript SDK를 사용하여 자동으로 페이지 뷰를 수집하도록 앱을 설정하는 방법에 대해 알아봅니다](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="171a3-114">[Learn how to set up your app to collect page views automatically with the Application Insights JavaScript SDK](app-insights-javascript.md).</span></span>
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a><span data-ttu-id="171a3-115">통합 문서 섹션 편집, 다시 정렬, 복제 및 삭제</span><span class="sxs-lookup"><span data-stu-id="171a3-115">Editing, rearranging, cloning, and deleting workbook sections</span></span>

<span data-ttu-id="171a3-116">통합 문서는 개별 편집 가능한 사용 현황 시각화, 차트, 테이블, 텍스트 또는 분석 쿼리 결과의 섹션으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-116">A workbook is a made of sections: independently editable usage visualizations, charts, tables, text, or Analytics query results.</span></span>

<span data-ttu-id="171a3-117">통합 문서 섹션의 콘텐츠를 편집하려면 아래쪽의 **편집** 단추를 클릭하고 통합 문서 섹션의 오른쪽을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-117">To edit the contents of a workbook section, click the **Edit** button below and to the right of the workbook section.</span></span>

![Application Insights 통합 문서 섹션 편집 컨트롤](./media/app-insights-usage-workbooks/editing-controls.png)

1. <span data-ttu-id="171a3-119">섹션 편집을 완료하면 섹션의 왼쪽 아래 모서리에 있는 **편집 완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-119">When you're done editing a section, click **Done Editing** in the bottom left corner of the section.</span></span>

2. <span data-ttu-id="171a3-120">중복 섹션을 만들려면 **이 섹션 복제** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-120">To create a duplicate of a section, click the **Clone this section** icon.</span></span> <span data-ttu-id="171a3-121">중복 섹션을 만드는 것은 이전 반복을 손실하지 않고 쿼리를 반복하는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-121">Creating duplicate sections is a great to way to iterate on a query without losing previous iterations.</span></span>

3. <span data-ttu-id="171a3-122">통합 문서에서 섹션을 이동하려면 **위로 이동** 또는 **아래로 이동** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-122">To move up a section in a workbook, click the **Move up** or **Move down** icon.</span></span>

4. <span data-ttu-id="171a3-123">섹션을 영구적으로 제거하려면 **제거** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-123">To remove a section permanently, click the **Remove** icon.</span></span>

## <a name="adding-usage-data-visualization-sections"></a><span data-ttu-id="171a3-124">사용 현황 데이터 시각화 섹션 추가</span><span class="sxs-lookup"><span data-stu-id="171a3-124">Adding usage data visualization sections</span></span>

<span data-ttu-id="171a3-125">통합 문서는 네 가지 유형의 기본 제공 사용 현황 분석 시각화를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-125">Workbooks offer four types of built-in usage analytics visualizations.</span></span> <span data-ttu-id="171a3-126">각각은 앱의 사용 현황에 대한 일반적인 질문에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-126">Each answers a common question about the usage of your app.</span></span> <span data-ttu-id="171a3-127">이러한 4개의 섹션 이외의 테이블 및 차트를 추가하려면 분석 쿼리 섹션을 추가합니다(아래 참조).</span><span class="sxs-lookup"><span data-stu-id="171a3-127">To add tables and charts other than these four sections, add Analytics query sections (see below).</span></span>

<span data-ttu-id="171a3-128">통합 문서에 사용자, 세션, 이벤트 또는 재방문 주기 섹션을 추가하려면 **사용자 추가** 또는 통합 문서의 맨 아래 또는 섹션의 맨 아래에 있는 기타 해당 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-128">To add a Users, Sessions, Events, or Retention section to your workbook, use the **Add Users** or other corresponding button at the bottom of the workbook, or at the bottom of any section.</span></span>

![통합 문서의 사용자 섹션](./media/app-insights-usage-workbooks/users-section.png)

<span data-ttu-id="171a3-130">**사용자** 섹션은 "내 사이트의 일부 페이지를 보거나 일부 기능을 사용한 사용자의 수는?"에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-130">**Users** sections answer "How many users viewed some page or used some feature of my site?"</span></span>

<span data-ttu-id="171a3-131">**세션** 섹션은 "사용자가 내 사이트의 일부 페이지를 보거나 일부 기능을 사용하는 데 소비한 세션의 수는?"에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-131">**Sessions** sections answer "How many sessions did users spend viewing some page or using some feature of my site?"</span></span>

<span data-ttu-id="171a3-132">**이벤트** 섹션은 "사용자가 내 사이트의 일부 페이지를 보거나 일부 기능을 사용한 시간은?"에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-132">**Events** sections answer "How many times did users view some page or use some feature of my site?"</span></span>

<span data-ttu-id="171a3-133">이러한 각 세 가지 섹션 유형은 동일한 컨트롤 및 시각화 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-133">Each of these three section types offers the same sets of controls and visualizations:</span></span>

* [<span data-ttu-id="171a3-134">사용자, 세션 및 이벤트 섹션 편집에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="171a3-134">Learn more about editing Users, Sessions, and Events sections</span></span>](app-insights-usage-segmentation.md)
* <span data-ttu-id="171a3-135">각 섹션 맨 위에 있는 **차트 표시**, **표 표시**, **Insights 표시** 및 **이러한 사용자의 샘플** 확인란을 선택하여 기본 차트, 히스토그램 표, 자동 insights 및 샘플 사용자 시각화를 설정/해제합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-135">Toggle the main chart, histogram grids, automatic insights, and sample users visualizations using the **Show Chart**, **Show Grid**, **Show Insights**, and **Sample of These Users** checkboxes at the top of each section.</span></span>

![통합 문서의 재방문 주기 섹션](./media/app-insights-usage-workbooks/retention-section.png)

<span data-ttu-id="171a3-137">**재방문 주기** 섹션은 "1일 또는 1주일에 일부 페이지를 보거나 일부 기능을 사용한 사용자 중 다음 날이나 다음 주에 다시 방문한 사용자 수는?"에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-137">**Retention** sections answer "Of people who viewed some page or used some feature on one day or week, how many came back in a subsequent day or week?"</span></span>

* [<span data-ttu-id="171a3-138">재방문 주기 섹션 편집에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="171a3-138">Learn more about editing Retention sections</span></span>](app-insights-usage-retention.md)
* <span data-ttu-id="171a3-139">섹션 맨 위에 있는 **전체 재방문 주기 차트 표시** 확인란을 사용하여 선택 가능한 전체 재방문 주기 차트를 설정/해제합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-139">Toggle the optional Overall Retention chart using the **Show overall retention chart** checkbox at the top of the section.</span></span>

## <a name="adding-application-insights-analytics-sections"></a><span data-ttu-id="171a3-140">Application Insights 분석 섹션 추가</span><span class="sxs-lookup"><span data-stu-id="171a3-140">Adding Application Insights Analytics sections</span></span>

![통합 문서의 분석 섹션](./media/app-insights-usage-workbooks/analytics-section.png)

<span data-ttu-id="171a3-142">통합 문서에 Application Insights 분석 섹션을 추가하려면 통합 문서의 맨 아래 또는 섹션의 맨 아래에 있는 **분석 쿼리 추가** 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-142">To add an Application Insights Analytics query section to your workbook, use the **Add Analytics query** button at the bottom of the workbook, or at the bottom of any section.</span></span>

<span data-ttu-id="171a3-143">분석 쿼리 섹션을 사용하면 통합 문서에 Application Insights 데이터에 대해 임의 쿼리를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-143">Analytics query sections let you add arbitrary queries over your Application Insights data into workbooks.</span></span> <span data-ttu-id="171a3-144">이러한 유연성은 분석 쿼리 섹션이 다음과 같은 사용자, 세션, 이벤트 및 재방문 주기에 대해 위에 나열된 4개 이외의 다른 사이트에 대한 질문에 응답하기 위한 go-to(즐겨찾기)가 되어야 함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-144">This flexibility means Analytics query sections should be your go-to for answering any questions about your site other than the four listed above for Users, Sessions, Events, and Retention, like:</span></span>

* <span data-ttu-id="171a3-145">사용 현황의 감소와 동일한 기간 동안 사이트에서 throw한 예외의 수는?</span><span class="sxs-lookup"><span data-stu-id="171a3-145">How many exceptions did your site throw during the same time period as a decline in usage?</span></span>
* <span data-ttu-id="171a3-146">일부 페이지를 보는 사용자에 대한 페이지 로드 시간의 분포는 무엇이었습니까?</span><span class="sxs-lookup"><span data-stu-id="171a3-146">What was the distribution of page load times for users viewing some page?</span></span>
* <span data-ttu-id="171a3-147">사이트의 일부 페이지 집합을 봤지만 다른 일부 페이지 집합을 보지 않은 사용자의 수는?</span><span class="sxs-lookup"><span data-stu-id="171a3-147">How many users viewed some set of pages on your site, but not some other set of pages?</span></span> <span data-ttu-id="171a3-148">사이트 기능의 여러 하위 집합을 사용하는 사용자의 클러스터가 있는지 이해하는 데 유용할 수 있습니다(Log Analytics 쿼리 언어에서 `kind=leftanti` 한정자가 포함된 `join` 연산자 사용).</span><span class="sxs-lookup"><span data-stu-id="171a3-148">This can be useful to understand if you have clusters of users who use different subsets of your site's functionality (use the `join` operator with the `kind=leftanti` modifier in the Log Analytics query language).</span></span>

<span data-ttu-id="171a3-149">[Log Analytics 쿼리 언어 참조](https://docs.loganalytics.io/)를 사용하여 쿼리 작성에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-149">Use the [Log Analytics query language reference](https://docs.loganalytics.io/) to learn more about writing queries.</span></span>

## <a name="adding-text-and-markdown-sections"></a><span data-ttu-id="171a3-150">텍스트 및 Markdown 섹션 추가</span><span class="sxs-lookup"><span data-stu-id="171a3-150">Adding text and Markdown sections</span></span>

<span data-ttu-id="171a3-151">통합 문서에 제목, 설명 및 해설을 추가하면 테이블 및 차트의 집합을 설명으로 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-151">Adding headings, explanations, and commentary to your workbooks helps turn a set of tables and charts into a narrative.</span></span> <span data-ttu-id="171a3-152">통합 문서의 텍스트 섹션은 머리글, 굵게, 기울임꼴 및 글머리 기호 목록과 같은 텍스트 서식 지정에 대해 [Markdown 구문](https://daringfireball.net/projects/markdown/)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-152">Text sections in workbooks support the [Markdown syntax](https://daringfireball.net/projects/markdown/) for text formatting, like headings, bold, italics, and bulleted lists.</span></span>

<span data-ttu-id="171a3-153">통합 문서에 텍스트 섹션을 추가하려면 통합 문서의 맨 아래 또는 섹션의 맨 아래에 있는 **텍스트 추가** 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-153">To add a text section to your workbook, use the **Add text** button at the bottom of the workbook, or at the bottom of any section.</span></span>

## <a name="saving-and-sharing-workbooks-with-your-team"></a><span data-ttu-id="171a3-154">팀과 통합 문서 저장 및 공유</span><span class="sxs-lookup"><span data-stu-id="171a3-154">Saving and sharing workbooks with your team</span></span>

<span data-ttu-id="171a3-155">통합 문서는 사용자 전용인 **내 보고서** 섹션 또는 Application Insights 리소스에 대한 액세스가 있는 모든 사용자에게 액세스가 허용되는 **공유 보고서** 섹션에서 Application Insights 리소스 내에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-155">Workbooks are saved within an Application Insights resource, either in the **My Reports** section that's private to you or in the **Shared Reports** section that's accessible to everyone with access to the Application Insights resource.</span></span> <span data-ttu-id="171a3-156">리소스에서 모든 통합 문서를 보려면 작업 모음에서 **열기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-156">To view all the workbooks in the resource, click the **Open** button in the action bar.</span></span>

<span data-ttu-id="171a3-157">현재 **내 보고서**에 있는 통합 문서를 공유하려면:</span><span class="sxs-lookup"><span data-stu-id="171a3-157">To share a workbook that's currently in **My Reports**:</span></span>

1. <span data-ttu-id="171a3-158">작업 모음에서 **열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-158">Click **Open** in the action bar</span></span>
2. <span data-ttu-id="171a3-159">공유하려는 통합 문서 옆에 있는 "..." 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-159">Click the "..." button beside the workbook you want to share</span></span>
3. <span data-ttu-id="171a3-160">**공유 보고서로 이동**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-160">Click **Move to Shared Reports**.</span></span>

<span data-ttu-id="171a3-161">링크 또는 전자 메일을 통해 통합 문서를 공유하려면 작업 모음에서 **공유**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-161">To share a workbook with a link or via email, click **Share** in the action bar.</span></span> <span data-ttu-id="171a3-162">통합 문서를 보려면 링크의 수신자는 Azure Portal에서 이 리소스에 대한 액세스가 필요함을 명심하세요.</span><span class="sxs-lookup"><span data-stu-id="171a3-162">Keep in mind that recipients of the link need access to this resource in the Azure portal to view the workbook.</span></span> <span data-ttu-id="171a3-163">편집하려면 수신자는 최소한 리소스에 대한 참가자 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-163">To make edits, recipients need at least Contributor permissions for the resource.</span></span>

<span data-ttu-id="171a3-164">Azure 대시보드에 통합 문서에 대한 링크를 고정하려면:</span><span class="sxs-lookup"><span data-stu-id="171a3-164">To pin a link to a workbook to an Azure Dashboard:</span></span>

1. <span data-ttu-id="171a3-165">작업 모음에서 **열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-165">Click **Open** in the action bar</span></span>
2. <span data-ttu-id="171a3-166">고정하려는 통합 문서 옆에 있는 "..." 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-166">Click the "..." button beside the workbook you want to pin</span></span>
3. <span data-ttu-id="171a3-167">**대시보드에 고정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-167">Click **Pin to dashboard**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="171a3-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="171a3-168">Next steps</span></span>

## <a name="next-steps"></a><span data-ttu-id="171a3-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="171a3-169">Next steps</span></span>
- <span data-ttu-id="171a3-170">사용 현황 환경을 활성화하려면 [사용자 지정 이벤트](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) 또는 [페이지 보기](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views) 보내기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-170">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="171a3-171">사용자 지정 이벤트 또는 페이지 보기를 이미 보낸 경우 사용자가 서비스를 사용하는 방법에 대해 알아보려면 사용 현황 도구를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="171a3-171">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="171a3-172">사용자, 세션, 이벤트</span><span class="sxs-lookup"><span data-stu-id="171a3-172">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="171a3-173">깔때기</span><span class="sxs-lookup"><span data-stu-id="171a3-173">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="171a3-174">보존</span><span class="sxs-lookup"><span data-stu-id="171a3-174">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="171a3-175">사용자 흐름</span><span class="sxs-lookup"><span data-stu-id="171a3-175">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="171a3-176">사용자 컨텍스트 추가</span><span class="sxs-lookup"><span data-stu-id="171a3-176">Add user context</span></span>](app-insights-usage-send-user-context.md)
    
