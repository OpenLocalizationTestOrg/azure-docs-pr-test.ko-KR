---
title: "Application Insights로 SCOM 통합 | Microsoft Docs"
description: "SCOM 사용자인 경우 Application Insights로 성능을 모니터링하고 문제를 진단합니다. 포괄적 대시보드, 스마트 경고, 강력한 진단 도구 및 분석 쿼리."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 606e9d03-c0e6-4a77-80e8-61b75efacde0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/12/2016
ms.author: bwren
ms.openlocfilehash: 9c205465981fabdbb696cdc44f765532bbb992b5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a><span data-ttu-id="3474d-104">SCOM에 대해 Application Insights를 사용하여 응용 프로그램 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="3474d-104">Application Performance Monitoring using Application Insights for SCOM</span></span>
<span data-ttu-id="3474d-105">서버를 관리하는 데 SCOM(System Center Operations Manager)을 사용하는 경우 [Azure Application Insights](app-insights-asp-net.md)를 활용해 성능을 모니터링하고 성능 문제를 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-105">If you use System Center Operations Manager (SCOM) to manage your servers, you can monitor performance and diagnose performance issues with the help of [Azure Application Insights](app-insights-asp-net.md).</span></span> <span data-ttu-id="3474d-106">Application Insights는 사용자 웹 응용 프로그램에 들어오는 요청과 나가는 REST 및 SQL 호출, 예외 및 로그 추적을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-106">Application Insights monitors your web application's incoming requests, outgoing REST and SQL calls, exceptions, and log traces.</span></span> <span data-ttu-id="3474d-107">메트릭 차트 및 스마트 경고뿐만 아니라 이 원격 분석을 통한 강력한 진단 검색 및 분석 쿼리가 포함된 대시보드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-107">It provides dashboards with metric charts and smart alerts, as well as powerful diagnostic search and analytical queries over this telemetry.</span></span> 

<span data-ttu-id="3474d-108">SCOM 관리 팩을 사용하여 Application Insights 모니터링으로 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-108">You can switch on Application Insights monitoring by using an SCOM management pack.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="3474d-109">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="3474d-109">Before you start</span></span>
<span data-ttu-id="3474d-110">다음을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-110">We assume:</span></span>

* <span data-ttu-id="3474d-111">SCOM에 대해 잘 알고 있으며 SCOM 2012 R2 또는 2016을 사용하여 IIS 웹 서버를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-111">You're familiar with SCOM, and that you use SCOM 2012 R2 or 2016 to manage your IIS web servers.</span></span>
* <span data-ttu-id="3474d-112">서버에 Application Insights로 모니터링하려는 웹 응용 프로그램을 이미 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-112">You have already installed on your servers a web application that you want to monitor with Application Insights.</span></span>
* <span data-ttu-id="3474d-113">앱 프레임워크 버전은 .NET 4.5 이상입니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-113">App framework version is .NET 4.5 or later.</span></span>
* <span data-ttu-id="3474d-114">[Microsoft Azure](https://azure.com)에서 구독에 액세스하여 [Azure Portal](https://portal.azure.com)에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-114">You have access to a subscription in [Microsoft Azure](https://azure.com) and can sign in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="3474d-115">조직에 구독이 있으면 해당 구독에 Microsoft 계정을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-115">Your organization may have a subscription, and can add your Microsoft account to it.</span></span>

<span data-ttu-id="3474d-116">(개발 팀은 [Application Insights SDK](app-insights-asp-net.md)를 웹앱으로 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-116">(The development team might build the [Application Insights SDK](app-insights-asp-net.md) into the web app.</span></span> <span data-ttu-id="3474d-117">이 빌드 시간 계측은 사용자 지정 원격 분석을 작성하는 데 더 많은 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-117">This build-time instrumentation gives them greater flexibility in writing custom telemetry.</span></span> <span data-ttu-id="3474d-118">하지만 이것은 크게 중요하지 않습니다. SDK가 기본 제공되는지 여부에 관계없이 여기에 설명된 단계를 따르면 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="3474d-118">However, it doesn't matter: you can follow the steps described here either with or without the SDK built in.)</span></span>

## <a name="one-time-install-application-insights-management-pack"></a><span data-ttu-id="3474d-119">(한 번) Application Insights 관리 팩 설치</span><span class="sxs-lookup"><span data-stu-id="3474d-119">(One time) Install Application Insights management pack</span></span>
<span data-ttu-id="3474d-120">Operations Manager를 실행하는 컴퓨터에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-120">On the machine where you run Operations Manager:</span></span>

1. <span data-ttu-id="3474d-121">이전 버전의 관리 팩을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-121">Uninstall any old version of the management pack:</span></span>
   1. <span data-ttu-id="3474d-122">Operations Manager에서 관리, 관리 팩을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-122">In Operations Manager, open Administration, Management Packs.</span></span> 
   2. <span data-ttu-id="3474d-123">이전 버전을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-123">Delete the old version.</span></span>
2. <span data-ttu-id="3474d-124">카탈로그에서 관리 팩을 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-124">Download and install the management pack from the catalog.</span></span>
3. <span data-ttu-id="3474d-125">Operations Manager를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-125">Restart Operations Manager.</span></span>

## <a name="create-a-management-pack"></a><span data-ttu-id="3474d-126">관리 팩 만들기</span><span class="sxs-lookup"><span data-stu-id="3474d-126">Create a management pack</span></span>
1. <span data-ttu-id="3474d-127">Operations Manager에서 **작성**, **.NET...with Application Insights**, **모니터링 추가 마법사**를 열고 **.NET...with Application Insights**를 한 번 더 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-127">In Operations Manager, open **Authoring**, **.NET...with Application Insights**, **Add Monitoring Wizard**, and again choose **.NET...with Application Insights**.</span></span>
   
    ![](./media/app-insights-scom/020.png)
2. <span data-ttu-id="3474d-128">앱 다음에 구성의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-128">Name the configuration after your app.</span></span> <span data-ttu-id="3474d-129">(한 번에 하나의 앱을 계측해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="3474d-129">(You have to instrument one app at a time.)</span></span>
   
    ![](./media/app-insights-scom/030.png)
3. <span data-ttu-id="3474d-130">동일한 마법사 페이지에서 새 관리 팩을 만들거나 Application Insights에 대해 이전에 만든 팩을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-130">On the same wizard page, either create a new management pack, or select a pack that you created for Application Insights earlier.</span></span>
   
     <span data-ttu-id="3474d-131">(Application Insights [관리 팩](https://technet.microsoft.com/library/cc974491.aspx) 은 인스턴스를 만들 수 있는 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-131">(The Application Insights [management pack](https://technet.microsoft.com/library/cc974491.aspx) is a template, from which you create an instance.</span></span> <span data-ttu-id="3474d-132">동일한 인스턴스를 나중에 재사용할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="3474d-132">You can reuse the same instance later.)</span></span>

    ![일반 속성 탭에서 앱의 이름을 입력합니다.](./media/app-insights-scom/040.png)

1. <span data-ttu-id="3474d-136">모니터링할 앱을 하나 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-136">Choose one app that you want to monitor.</span></span> <span data-ttu-id="3474d-137">검색 기능으로 서버에 설치된 앱을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-137">The search feature searches among apps installed on your servers.</span></span>
   
    ![모니터링할 항목 탭에서 추가를 클릭하고 앱 이름 부분을 입력하며, 검색을 클릭하고 앱을 선택한 후 추가, 확인을 선택합니다.](./media/app-insights-scom/050.png)
   
    <span data-ttu-id="3474d-139">일부 서버의 앱만 모니터링하려는 경우 모니터링 범위 필드(선택 사항)를 사용하여 서버의 서브넷을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-139">The optional Monitoring scope field can be used to specify a subset of your servers, if you don't want to monitor the app in all servers.</span></span>
2. <span data-ttu-id="3474d-140">다음 마법사 페이지에서는 먼저 Microsoft Azure에 로그인할 자격 증명을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-140">On the next wizard page, you must first provide your credentials to sign in to Microsoft Azure.</span></span>
   
    <span data-ttu-id="3474d-141">이 페이지에서 원격 분석 데이터를 분석하고 표시할 Application Insights 리소스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-141">On this page, you choose the Application Insights resource where you want the telemetry data to be analyzed and displayed.</span></span> 
   
   * <span data-ttu-id="3474d-142">개발 중에 Application Insights에 대해 응용 프로그램이 구성된 경우 기존 리소스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-142">If the application was configured for Application Insights during development, select its existing resource.</span></span>
   * <span data-ttu-id="3474d-143">그렇지 않은 경우 해당 앱에 대해 명명된 새 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-143">Otherwise, create a new resource named for the app.</span></span> <span data-ttu-id="3474d-144">동일한 시스템의 구성 요소인 다른 앱이 있는 경우 이를 동일한 리소스 그룹에 배치하면 원격 분석에 보다 쉽게 액세스하여 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-144">If there are other apps that are components of the same system, put them in the same resource group, to make access to the telemetry easier to manage.</span></span>
     
     <span data-ttu-id="3474d-145">나중에 이러한 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-145">You can change these settings later.</span></span>
     
     ![Application Insights 설정 탭에서 '로그인'을 클릭하고 Azure에 대한 Microsoft 계정 자격 증명을 제공합니다.](./media/app-insights-scom/060.png)
3. <span data-ttu-id="3474d-148">마법사를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-148">Complete the wizard.</span></span>
   
    ![만들기 클릭](./media/app-insights-scom/070.png)

<span data-ttu-id="3474d-150">모니터링할 각 앱에 대해 다음 절차를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-150">Repeat this procedure for each app that you want to monitor.</span></span>

<span data-ttu-id="3474d-151">나중에 설정을 변경해야 하는 경우 작업 창에서 모니터의 속성을 다시 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-151">If you need to change settings later, re-open the properties of the monitor from the Authoring window.</span></span>

![작성에서 .NET Application Performance Monitoring with Application Insights를 선택하고 모니터를 선택한 후 속성을 클릭합니다.](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a><span data-ttu-id="3474d-153">모니터링 확인</span><span class="sxs-lookup"><span data-stu-id="3474d-153">Verify monitoring</span></span>
<span data-ttu-id="3474d-154">설치한 모니터가 모든 서버에서 앱을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-154">The monitor that you have installed searches for your app on every server.</span></span> <span data-ttu-id="3474d-155">여기서 앱을 찾으면 Application Insights 상태 모니터를 구성하여 앱을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-155">Where it finds the app, it configures Application Insights Status Monitor to monitor the app.</span></span> <span data-ttu-id="3474d-156">필요한 경우 먼저 서버에 상태 모니터를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-156">If necessary, it first installs Status Monitor on the server.</span></span>

<span data-ttu-id="3474d-157">찾은 앱의 인스턴스를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-157">You can verify which instances of the app it has found:</span></span>

![모니터링에서 Application Insights를 엽니다.](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a><span data-ttu-id="3474d-159">Application Insights에서 원격 분석 보기</span><span class="sxs-lookup"><span data-stu-id="3474d-159">View telemetry in Application Insights</span></span>
<span data-ttu-id="3474d-160">[Azure 포털](https://portal.azure.com)에서 앱에 대한 리소스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-160">In the [Azure portal](https://portal.azure.com), browse to the resource for your app.</span></span> <span data-ttu-id="3474d-161">앱에서 [원격 분석을 보여 주는 차트를 확인](app-insights-dashboards.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-161">You [see charts showing telemetry](app-insights-dashboards.md) from your app.</span></span> <span data-ttu-id="3474d-162">(기본 페이지에 표시되지 않으면 라이브 메트릭 스트림을 클릭합니다.)</span><span class="sxs-lookup"><span data-stu-id="3474d-162">(If it hasn't shown up on the main page yet, click Live Metrics Stream.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="3474d-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3474d-163">Next steps</span></span>
* <span data-ttu-id="3474d-164">[대시보드를 설정](app-insights-dashboards.md) 하여 현재 항목 및 기타 앱을 모니터링하는 가장 중요한 차트를 모읍니다.</span><span class="sxs-lookup"><span data-stu-id="3474d-164">[Set up a dashboard](app-insights-dashboards.md) to bring together the most important charts monitoring this and other apps.</span></span>
* [<span data-ttu-id="3474d-165">매트릭에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="3474d-165">Learn about metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="3474d-166">경고 설정</span><span class="sxs-lookup"><span data-stu-id="3474d-166">Set up alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="3474d-167">성능 문제 진단</span><span class="sxs-lookup"><span data-stu-id="3474d-167">Diagnosing performance issues</span></span>](app-insights-detect-triage-diagnose.md)
* [<span data-ttu-id="3474d-168">강력한 분석 쿼리</span><span class="sxs-lookup"><span data-stu-id="3474d-168">Powerful Analytics queries</span></span>](app-insights-analytics.md)
* [<span data-ttu-id="3474d-169">가용성 웹 테스트</span><span class="sxs-lookup"><span data-stu-id="3474d-169">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)

