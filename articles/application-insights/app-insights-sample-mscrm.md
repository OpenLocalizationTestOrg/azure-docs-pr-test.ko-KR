---
title: "Microsoft Dynamics CRM 및 Azure Application Insights | Microsoft Docs"
description: "Application Insights를 사용하여 Microsoft Dynamics CRM Online에서 원격 분석 가져오기 설정, 데이터 가져오기, 시각화 및 내보내기의 연습입니다."
services: application-insights
documentationcenter: 
author: mazharmicrosoft
manager: carmonm
ms.assetid: 04c66338-687e-49e5-9975-be935f98f156
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: bwren
ms.openlocfilehash: a9593d5f198e05db80451a599428a296ed02e781
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a><span data-ttu-id="ab007-104">연습: Application Insights를 사용하여 Microsoft Dynamics CRM Online 작업에 대한 원격 분석 설정</span><span class="sxs-lookup"><span data-stu-id="ab007-104">Walkthrough: Enabling Telemetry for Microsoft Dynamics CRM Online using Application Insights</span></span>
<span data-ttu-id="ab007-105">이 문서는 [Azure Application Insights](https://azure.microsoft.com/services/application-insights/)를 사용하여 [Microsoft Dynamics CRM Online](https://www.dynamics.com/)에서 원격 분석 데이터를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-105">This article shows you how to get telemetry data from [Microsoft Dynamics CRM Online](https://www.dynamics.com/) using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span></span> <span data-ttu-id="ab007-106">응용 프로그램에 Application Insights 스크립트 추가, 데이터 캡처 및 데이터 시각화의 전체 프로세스를 연습합니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-106">We’ll walk through the complete process of adding Application Insights script to your application, capturing data, and data visualization.</span></span>

> [!NOTE]
> <span data-ttu-id="ab007-107">[샘플 솔루션을 탐색합니다](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="ab007-107">[Browse the sample solution](https://dynamicsandappinsights.codeplex.com/).</span></span>
> 
> 

## <a name="add-application-insights-to-new-or-existing-crm-online-instance"></a><span data-ttu-id="ab007-108">기존 또는 새 CRM Online 인스턴스에 Application Insights를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-108">Add Application Insights to new or existing CRM Online instance</span></span>
<span data-ttu-id="ab007-109">응용 프로그램을 모니터링하려면 응용 프로그램에 Application Insights SDK를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-109">To monitor your application, you add an Application Insights SDK to your application.</span></span> <span data-ttu-id="ab007-110">SDK는 [Application Insights 포털](https://portal.azure.com)로 원격 분석을 보내며 여기서 강력한 분석 및 진단 도구를 사용하고 저장소로 데이터를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-110">The SDK sends telemetry to the [Application Insights portal](https://portal.azure.com), where you can use our powerful analysis and diagnostic tools, or export the data to storage.</span></span>

### <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="ab007-111">Azure에서 Application Insights 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="ab007-111">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="ab007-112">[Microsoft Azure에서 계정](http://azure.com/pricing)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-112">Get [an account in Microsoft Azure](http://azure.com/pricing).</span></span> 
2. <span data-ttu-id="ab007-113">[Azure 포털](https://portal.azure.com) 에 로그인한 다음 새 Application Insights 리소스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-113">Sign into the [Azure portal](https://portal.azure.com) and add a new Application Insights resource.</span></span> <span data-ttu-id="ab007-114">데이터가 처리되어 표시될 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-114">This is where your data will be processed and displayed.</span></span>
   
    ![+, 개발자 서비스, Application Insights를 클릭합니다.](./media/app-insights-sample-mscrm/01.png)
   
    <span data-ttu-id="ab007-116">응용 프로그램 유형으로 ASP.NET을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-116">Choose ASP.NET as the application type.</span></span>
3. <span data-ttu-id="ab007-117">시작 페이지를 열고 “클라이언트 쪽 모니터링 및 진단”을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-117">Open the Getting Started page and open "Monitor and diagnose client side".</span></span>
   
    ![웹 페이지에서 삽입에 대한 코드 조각](./media/app-insights-sample-mscrm/03.png)

<span data-ttu-id="ab007-119">**코드 페이지를 열린 상태로 유지** 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-119">**Keep the code page open** while you do the next step in another browser window.</span></span> <span data-ttu-id="ab007-120">코드가 곧 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-120">You'll need the code soon.</span></span> 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a><span data-ttu-id="ab007-121">Microsoft Dynamics CRM의 JavaScript 웹 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="ab007-121">Create a JavaScript web resource in Microsoft Dynamics CRM</span></span>
1. <span data-ttu-id="ab007-122">CRM Online 인스턴스를 열고 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-122">Open your CRM Online instance and login with administrator privileges.</span></span>
2. <span data-ttu-id="ab007-123">Microsoft Dynamics CDM 설정, 사용자 지정, 시스템 사용자 지정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-123">Open Microsoft Dynamics CRM Settings, Customizations, Customize the System</span></span>
   
    ![Microsoft Dynamics CRM 설정](./media/app-insights-sample-mscrm/04.png)
   
    ![설정 > 사용자 지정](./media/app-insights-sample-mscrm/05.png)

    ![시스템 옵션 사용자 지정](./media/app-insights-sample-mscrm/06.png)

1. <span data-ttu-id="ab007-127">JavaScript 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-127">Create a JavaScript resource.</span></span>
   
    ![새 웹 리소스 대화 상자](./media/app-insights-sample-mscrm/07.png)
   
    <span data-ttu-id="ab007-129">이름을 지정하고 **스크립트(JScript)** 를 선택하고 텍스트 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-129">Give it a name, select **Script (JScript)** and open the text editor.</span></span>
   
    ![텍스트 편집기 열기](./media/app-insights-sample-mscrm/08.png)
2. <span data-ttu-id="ab007-131">Application Insights에서 코드 복사</span><span class="sxs-lookup"><span data-stu-id="ab007-131">Copy the code from Application Insights.</span></span> <span data-ttu-id="ab007-132">복사하는 동안 스크립트 태그를 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-132">While copying make sure to ignore script tags.</span></span> <span data-ttu-id="ab007-133">아래 스크린샷을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ab007-133">Refer below screenshot:</span></span>
   
    ![계측 키 설정](./media/app-insights-sample-mscrm/09.png)
   
    <span data-ttu-id="ab007-135">코드는 Application insights 리소스를 식별하는 계측 키를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-135">The code includes the instrumentation key that identifies your Application insights resource.</span></span>
3. <span data-ttu-id="ab007-136">저장하고 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-136">Save and publish.</span></span>
   
    ![저장 및 게시](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a><span data-ttu-id="ab007-138">계측 양식</span><span class="sxs-lookup"><span data-stu-id="ab007-138">Instrument Forms</span></span>
1. <span data-ttu-id="ab007-139">Microsoft CRM Online에서 계정 양식을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-139">In Microsoft CRM Online, open the Account form</span></span>
   
    ![계정 양식](./media/app-insights-sample-mscrm/11.png)
2. <span data-ttu-id="ab007-141">양식 속성 열기</span><span class="sxs-lookup"><span data-stu-id="ab007-141">Open the form Properties</span></span>
   
    ![양식 속성](./media/app-insights-sample-mscrm/12.png)
3. <span data-ttu-id="ab007-143">만든 JavaScript 웹 리소스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-143">Add the JavaScript web resource that you created</span></span>
   
    ![추가 메뉴](./media/app-insights-sample-mscrm/13.png)
   
    ![웹 리소스 추가](./media/app-insights-sample-mscrm/14.png)
4. <span data-ttu-id="ab007-146">양식 사용자 지정 항목을 저장하고 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-146">Save and publish your form customizations.</span></span>

## <a name="metrics-captured"></a><span data-ttu-id="ab007-147">캡처된 메트릭</span><span class="sxs-lookup"><span data-stu-id="ab007-147">Metrics captured</span></span>
<span data-ttu-id="ab007-148">이제 양식에 대한 원격 분석 캡처를 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-148">You have now set up telemetry capture for the form.</span></span> <span data-ttu-id="ab007-149">사용할 때마다 Application Insights 리소스에 데이터가 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-149">Whenever it is used, data will be sent to your Application Insights resource.</span></span>

<span data-ttu-id="ab007-150">표시되는 데이터의 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-150">Here are samples of the data that you'll see.</span></span>

#### <a name="application-health"></a><span data-ttu-id="ab007-151">응용 프로그램 상태</span><span class="sxs-lookup"><span data-stu-id="ab007-151">Application health</span></span>
![예제 페이지 로드 시간](./media/app-insights-sample-mscrm/15.png)

![예제 페이지 보기 차트](./media/app-insights-sample-mscrm/16.png)

<span data-ttu-id="ab007-154">브라우저 예외:</span><span class="sxs-lookup"><span data-stu-id="ab007-154">Browser exceptions:</span></span>

![브라우저 예외 차트](./media/app-insights-sample-mscrm/17.png)

<span data-ttu-id="ab007-156">차트를 클릭하여 자세한 내용을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-156">Click the chart to get more detail:</span></span>

![예외 목록](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a><span data-ttu-id="ab007-158">사용</span><span class="sxs-lookup"><span data-stu-id="ab007-158">Usage</span></span>
![사용자, 세션 및 페이지 보기](./media/app-insights-sample-mscrm/19.png)

![세션 차트](./media/app-insights-sample-mscrm/20.png)

![브라우저 버전](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a><span data-ttu-id="ab007-162">브라우저</span><span class="sxs-lookup"><span data-stu-id="ab007-162">Browsers</span></span>
![페이지 로드 시간 분석](./media/app-insights-sample-mscrm/22.png)

![브라우저 버전별 세션 수](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a><span data-ttu-id="ab007-165">지리적 위치</span><span class="sxs-lookup"><span data-stu-id="ab007-165">Geolocation</span></span>
![국가별 세션 수](./media/app-insights-sample-mscrm/24.png)

![국가별 세션 및 사용자](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a><span data-ttu-id="ab007-168">내부 페이지 보기 요청</span><span class="sxs-lookup"><span data-stu-id="ab007-168">Inside page view request</span></span>
![페이지 보기 요약](./media/app-insights-sample-mscrm/26.png)

![페이지 보기 이벤트 검색](./media/app-insights-sample-mscrm/27.png)

![비슷한 페이지 보기](./media/app-insights-sample-mscrm/28.png)

![페이지 보기 속성](./media/app-insights-sample-mscrm/29.png)

![세션별 페이지](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a><span data-ttu-id="ab007-174">샘플 코드</span><span class="sxs-lookup"><span data-stu-id="ab007-174">Sample code</span></span>
<span data-ttu-id="ab007-175">[샘플 코드를 탐색합니다](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="ab007-175">[Browse the sample code](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="power-bi"></a><span data-ttu-id="ab007-176">Power BI</span><span class="sxs-lookup"><span data-stu-id="ab007-176">Power BI</span></span>
<span data-ttu-id="ab007-177">[Microsoft Power BI에 데이터를 내보내는](app-insights-export-power-bi.md)경우 훨씬 심도 깊은 분석을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab007-177">You can do even deeper analysis if you [export the data to Microsoft Power BI](app-insights-export-power-bi.md).</span></span>

## <a name="sample-microsoft-dynamics-crm-solution"></a><span data-ttu-id="ab007-178">샘플 Microsoft Dynamics CRM 솔루션</span><span class="sxs-lookup"><span data-stu-id="ab007-178">Sample Microsoft Dynamics CRM Solution</span></span>
<span data-ttu-id="ab007-179">[다음은 Microsoft Dynamics CRM에서 구현된 샘플 솔루션입니다.](https://dynamicsandappinsights.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="ab007-179">[Here is the sample solution implemented in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="learn-more"></a><span data-ttu-id="ab007-180">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="ab007-180">Learn more</span></span>
* [<span data-ttu-id="ab007-181">Application Insights란?</span><span class="sxs-lookup"><span data-stu-id="ab007-181">What is Application Insights?</span></span>](app-insights-overview.md)
* [<span data-ttu-id="ab007-182">웹 페이지용 Application Insights</span><span class="sxs-lookup"><span data-stu-id="ab007-182">Application Insights for web pages</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="ab007-183">추가 샘플 및 연습</span><span class="sxs-lookup"><span data-stu-id="ab007-183">More samples and walkthroughs</span></span>](app-insights-code-samples.md)
