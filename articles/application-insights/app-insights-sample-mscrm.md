---
title: aaaMicrosoft Dynamics CRM, Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: a39398060d6553fb18a26c101f085b7d87443636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a><span data-ttu-id="42aba-104">연습: Application Insights를 사용하여 Microsoft Dynamics CRM Online 작업에 대한 원격 분석 설정</span><span class="sxs-lookup"><span data-stu-id="42aba-104">Walkthrough: Enabling Telemetry for Microsoft Dynamics CRM Online using Application Insights</span></span>
<span data-ttu-id="42aba-105">이 문서에서는 어떻게 tooget 원격 분석 데이터를 [Microsoft Dynamics CRM Online](https://www.dynamics.com/) 를 사용 하 여 [Azure Application Insights](https://azure.microsoft.com/services/application-insights/)합니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-105">This article shows you how tooget telemetry data from [Microsoft Dynamics CRM Online](https://www.dynamics.com/) using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span></span> <span data-ttu-id="42aba-106">Application Insights 스크립트 tooyour 응용 프로그램을 추가, 데이터 및 데이터 시각화 캡처 hello 전체 과정을 단계별로 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-106">We’ll walk through hello complete process of adding Application Insights script tooyour application, capturing data, and data visualization.</span></span>

> [!NOTE]
> <span data-ttu-id="42aba-107">[Hello 샘플 솔루션을 찾아보기](https://dynamicsandappinsights.codeplex.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-107">[Browse hello sample solution](https://dynamicsandappinsights.codeplex.com/).</span></span>
> 
> 

## <a name="add-application-insights-toonew-or-existing-crm-online-instance"></a><span data-ttu-id="42aba-108">Application Insights toonew 또는 기존 CRM Online 인스턴스에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-108">Add Application Insights toonew or existing CRM Online instance</span></span>
<span data-ttu-id="42aba-109">toomonitor 응용 프로그램에 Application Insights SDK tooyour 응용 프로그램을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-109">toomonitor your application, you add an Application Insights SDK tooyour application.</span></span> <span data-ttu-id="42aba-110">hello SDK 원격 분석 toohello 보냅니다 [Application Insights 포털](https://portal.azure.com), 여기서 강력한 분석 및 진단 도구를 사용 하거나 내보낼 수 있습니다 hello 데이터 toostorage 합니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-110">hello SDK sends telemetry toohello [Application Insights portal](https://portal.azure.com), where you can use our powerful analysis and diagnostic tools, or export hello data toostorage.</span></span>

### <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="42aba-111">Azure에서 Application Insights 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="42aba-111">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="42aba-112">[Microsoft Azure에서 계정](http://azure.com/pricing)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-112">Get [an account in Microsoft Azure](http://azure.com/pricing).</span></span> 
2. <span data-ttu-id="42aba-113">Hello에 로그인 [Azure 포털](https://portal.azure.com) 새 Application Insights 리소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-113">Sign into hello [Azure portal](https://portal.azure.com) and add a new Application Insights resource.</span></span> <span data-ttu-id="42aba-114">데이터가 처리되어 표시될 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-114">This is where your data will be processed and displayed.</span></span>
   
    ![+, 개발자 서비스, Application Insights를 클릭합니다.](./media/app-insights-sample-mscrm/01.png)
   
    <span data-ttu-id="42aba-116">ASP.NET hello 응용 프로그램 유형으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-116">Choose ASP.NET as hello application type.</span></span>
3. <span data-ttu-id="42aba-117">Hello 시작 페이지를 열고 열기 "모니터 및 클라이언트 쪽 진단"입니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-117">Open hello Getting Started page and open "Monitor and diagnose client side".</span></span>
   
    ![웹 페이지에서 삽입에 대한 코드 조각](./media/app-insights-sample-mscrm/03.png)

<span data-ttu-id="42aba-119">**Hello 코드 페이지를 열어** 다른 브라우저 창에서 다음 단계를 hello 수행 하는 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-119">**Keep hello code page open** while you do hello next step in another browser window.</span></span> <span data-ttu-id="42aba-120">곧 hello 코드가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-120">You'll need hello code soon.</span></span> 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a><span data-ttu-id="42aba-121">Microsoft Dynamics CRM의 JavaScript 웹 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="42aba-121">Create a JavaScript web resource in Microsoft Dynamics CRM</span></span>
1. <span data-ttu-id="42aba-122">CRM Online 인스턴스를 열고 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-122">Open your CRM Online instance and login with administrator privileges.</span></span>
2. <span data-ttu-id="42aba-123">Microsoft Dynamics CRM 설정, 사용자 지정, 사용자 지정 hello 시스템을 열려면</span><span class="sxs-lookup"><span data-stu-id="42aba-123">Open Microsoft Dynamics CRM Settings, Customizations, Customize hello System</span></span>
   
    ![Microsoft Dynamics CRM 설정](./media/app-insights-sample-mscrm/04.png)
   
    ![설정 > 사용자 지정](./media/app-insights-sample-mscrm/05.png)

    ![Hello 시스템 옵션을 사용자 지정](./media/app-insights-sample-mscrm/06.png)

1. <span data-ttu-id="42aba-127">JavaScript 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-127">Create a JavaScript resource.</span></span>
   
    ![새 웹 리소스 대화 상자](./media/app-insights-sample-mscrm/07.png)
   
    <span data-ttu-id="42aba-129">이름을 선택 **스크립트 (JScript)** 및 열기 hello 텍스트 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-129">Give it a name, select **Script (JScript)** and open hello text editor.</span></span>
   
    ![열기 hello 텍스트 편집기](./media/app-insights-sample-mscrm/08.png)
2. <span data-ttu-id="42aba-131">Application Insights에서 hello 코드를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-131">Copy hello code from Application Insights.</span></span> <span data-ttu-id="42aba-132">복사 하는 동안 있는지 tooignore 스크립트 태그를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-132">While copying make sure tooignore script tags.</span></span> <span data-ttu-id="42aba-133">아래 스크린샷을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="42aba-133">Refer below screenshot:</span></span>
   
    ![계측 키 설정](./media/app-insights-sample-mscrm/09.png)
   
    <span data-ttu-id="42aba-135">hello 코드 포함 Application insights 리소스를 식별 하는 hello 계측 키가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-135">hello code includes hello instrumentation key that identifies your Application insights resource.</span></span>
3. <span data-ttu-id="42aba-136">저장하고 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-136">Save and publish.</span></span>
   
    ![저장 및 게시](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a><span data-ttu-id="42aba-138">계측 양식</span><span class="sxs-lookup"><span data-stu-id="42aba-138">Instrument Forms</span></span>
1. <span data-ttu-id="42aba-139">Microsoft CRM Online에서 hello 계정 양식을 엽니다</span><span class="sxs-lookup"><span data-stu-id="42aba-139">In Microsoft CRM Online, open hello Account form</span></span>
   
    ![계정 양식](./media/app-insights-sample-mscrm/11.png)
2. <span data-ttu-id="42aba-141">Hello 폼 속성 열기</span><span class="sxs-lookup"><span data-stu-id="42aba-141">Open hello form Properties</span></span>
   
    ![양식 속성](./media/app-insights-sample-mscrm/12.png)
3. <span data-ttu-id="42aba-143">Hello 만든 JavaScript 웹 리소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-143">Add hello JavaScript web resource that you created</span></span>
   
    ![추가 메뉴](./media/app-insights-sample-mscrm/13.png)
   
    ![Hello 웹 리소스 추가](./media/app-insights-sample-mscrm/14.png)
4. <span data-ttu-id="42aba-146">양식 사용자 지정 항목을 저장하고 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-146">Save and publish your form customizations.</span></span>

## <a name="metrics-captured"></a><span data-ttu-id="42aba-147">캡처된 메트릭</span><span class="sxs-lookup"><span data-stu-id="42aba-147">Metrics captured</span></span>
<span data-ttu-id="42aba-148">이제 hello 폼에 대 한 원격 분석 캡처를 설정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-148">You have now set up telemetry capture for hello form.</span></span> <span data-ttu-id="42aba-149">사용할 때마다 tooyour Application Insights 리소스로 데이터가 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-149">Whenever it is used, data will be sent tooyour Application Insights resource.</span></span>

<span data-ttu-id="42aba-150">다음은 표시 하는 hello 데이터의 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-150">Here are samples of hello data that you'll see.</span></span>

#### <a name="application-health"></a><span data-ttu-id="42aba-151">응용 프로그램 상태</span><span class="sxs-lookup"><span data-stu-id="42aba-151">Application health</span></span>
![예제 페이지 로드 시간](./media/app-insights-sample-mscrm/15.png)

![예제 페이지 보기 차트](./media/app-insights-sample-mscrm/16.png)

<span data-ttu-id="42aba-154">브라우저 예외:</span><span class="sxs-lookup"><span data-stu-id="42aba-154">Browser exceptions:</span></span>

![브라우저 예외 차트](./media/app-insights-sample-mscrm/17.png)

<span data-ttu-id="42aba-156">Hello 차트 tooget 자세히를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-156">Click hello chart tooget more detail:</span></span>

![예외 목록](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a><span data-ttu-id="42aba-158">사용</span><span class="sxs-lookup"><span data-stu-id="42aba-158">Usage</span></span>
![사용자, 세션 및 페이지 보기](./media/app-insights-sample-mscrm/19.png)

![세션 차트](./media/app-insights-sample-mscrm/20.png)

![브라우저 버전](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a><span data-ttu-id="42aba-162">브라우저</span><span class="sxs-lookup"><span data-stu-id="42aba-162">Browsers</span></span>
![페이지 로드 시간 분석](./media/app-insights-sample-mscrm/22.png)

![브라우저 버전별 세션 수](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a><span data-ttu-id="42aba-165">지리적 위치</span><span class="sxs-lookup"><span data-stu-id="42aba-165">Geolocation</span></span>
![국가별 세션 수](./media/app-insights-sample-mscrm/24.png)

![국가별 세션 및 사용자](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a><span data-ttu-id="42aba-168">내부 페이지 보기 요청</span><span class="sxs-lookup"><span data-stu-id="42aba-168">Inside page view request</span></span>
![페이지 보기 요약](./media/app-insights-sample-mscrm/26.png)

![페이지 보기 이벤트 검색](./media/app-insights-sample-mscrm/27.png)

![비슷한 페이지 보기](./media/app-insights-sample-mscrm/28.png)

![페이지 보기 속성](./media/app-insights-sample-mscrm/29.png)

![세션별 페이지](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a><span data-ttu-id="42aba-174">샘플 코드</span><span class="sxs-lookup"><span data-stu-id="42aba-174">Sample code</span></span>
<span data-ttu-id="42aba-175">[Hello 샘플 코드를 찾아보려면](https://dynamicsandappinsights.codeplex.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-175">[Browse hello sample code](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="power-bi"></a><span data-ttu-id="42aba-176">Power BI</span><span class="sxs-lookup"><span data-stu-id="42aba-176">Power BI</span></span>
<span data-ttu-id="42aba-177">경우에 자세히 분석을 수행할 수 있습니다 있습니다 [hello 데이터 tooMicrosoft Power BI 내보내기](app-insights-export-power-bi.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-177">You can do even deeper analysis if you [export hello data tooMicrosoft Power BI](app-insights-export-power-bi.md).</span></span>

## <a name="sample-microsoft-dynamics-crm-solution"></a><span data-ttu-id="42aba-178">샘플 Microsoft Dynamics CRM 솔루션</span><span class="sxs-lookup"><span data-stu-id="42aba-178">Sample Microsoft Dynamics CRM Solution</span></span>
<span data-ttu-id="42aba-179">[다음은 Microsoft Dynamics CRM에서 구현 된 hello 샘플 솔루션](https://dynamicsandappinsights.codeplex.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="42aba-179">[Here is hello sample solution implemented in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="learn-more"></a><span data-ttu-id="42aba-180">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="42aba-180">Learn more</span></span>
* [<span data-ttu-id="42aba-181">Application Insights란?</span><span class="sxs-lookup"><span data-stu-id="42aba-181">What is Application Insights?</span></span>](app-insights-overview.md)
* [<span data-ttu-id="42aba-182">웹 페이지용 Application Insights</span><span class="sxs-lookup"><span data-stu-id="42aba-182">Application Insights for web pages</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="42aba-183">추가 샘플 및 연습</span><span class="sxs-lookup"><span data-stu-id="42aba-183">More samples and walkthroughs</span></span>](app-insights-code-samples.md)
