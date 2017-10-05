---
title: "새 Azure Application Insights 리소스 만들기 | Microsoft Docs"
description: "새 라이브 응용 프로그램에 대한 Application Insights 모니터링을 수동으로 설정합니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 878b007e-161c-4e36-8ab2-3d7047d8a92d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: bwren
ms.openlocfilehash: 5f8814ee943424c1c278ab3732129d4459f83819
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-insights-resource"></a><span data-ttu-id="aedf9-103">Application Insights 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="aedf9-103">Create an Application Insights resource</span></span>
<span data-ttu-id="aedf9-104">Azure Application Insights는 Microsoft Azure *리소스*에 응용 프로그램에 대한 데이터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-104">Azure Application Insights displays data about your application in a Microsoft Azure *resource*.</span></span> <span data-ttu-id="aedf9-105">따라서 새 리소스 만들기는 [새 응용 프로그램을 모니터링하도록 Application Insights를 설정][start]하는 과정에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-105">Creating a new resource is therefore part of [setting up Application Insights to monitor a new application][start].</span></span> <span data-ttu-id="aedf9-106">대부분의 경우에 리소스를 만드는 작업은 IDE에 의해 자동으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-106">In many cases, creating a resource can be done automatically by the IDE.</span></span> <span data-ttu-id="aedf9-107">하지만 일부 경우에는 리소스를 수동으로 만듭니다. 예를 들어, 응용 프로그램의 제품 개발과 빌드를 위한 별도의 리소스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-107">But in some cases, you create a resource manually - for example, to have separate resources for development and production builds of your application.</span></span>

<span data-ttu-id="aedf9-108">리소스를 만든 후에 해당 계측 키를 가져오고 이 키를 사용하여 응용 프로그램에서 SDK를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-108">After you have created the resource, you get its instrumentation key and use that to configure the SDK in the application.</span></span> <span data-ttu-id="aedf9-109">리소스 키는 원격 분석을 리소스로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-109">The resource key links the telemetry to the resource.</span></span>

## <a name="sign-up-to-microsoft-azure"></a><span data-ttu-id="aedf9-110">Microsoft Azure에 등록</span><span class="sxs-lookup"><span data-stu-id="aedf9-110">Sign up to Microsoft Azure</span></span>
<span data-ttu-id="aedf9-111">[Microsoft 계정이 없는 경우 계정을 만듭니다](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="aedf9-111">If you haven't got a [Microsoft account, get one now](http://live.com).</span></span> <span data-ttu-id="aedf9-112">Outlook.com, OneDrive, Windows Phone 또는 XBox Live 등의 서비스를 이용하는 경우 Microsoft 계정이 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-112">(If you use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, you already have a Microsoft account.)</span></span>

<span data-ttu-id="aedf9-113">또한 [Microsoft Azure](http://azure.com)를 구독해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-113">You also need a subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="aedf9-114">팀 또는 조직이 Azure를 구독하는 경우 소유자가 사용자의 Windows Live ID를 사용하여 사용자를 구독에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-114">If your team or organization has an Azure subscription, the owner can add you to it, using your Windows Live ID.</span></span> <span data-ttu-id="aedf9-115">사용하는 구독에 대해서만 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-115">You're only charged for what you use.</span></span> <span data-ttu-id="aedf9-116">기본 계획은 무료로 일정 시험 사용을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-116">The default basic plan allows for a certain amount of experimental use free of charge.</span></span>

<span data-ttu-id="aedf9-117">구독에 액세스할 수 있으면 [http://portal.azure.com](https://portal.azure.com)에서 Application Insights에 로그인하고 Live ID를 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-117">When you've got access to a subscription, log in to Application Insights at [http://portal.azure.com](https://portal.azure.com), and use your Live ID to login.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="aedf9-118">Application Insights 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="aedf9-118">Create an Application Insights resource</span></span>
<span data-ttu-id="aedf9-119">[portal.azure.com](https://portal.azure.com)에서 Application Insights 리소스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-119">In the [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![새로 만들기, Application Insights 클릭](./media/app-insights-create-new-resource/01-new.png)

* <span data-ttu-id="aedf9-121">**응용 프로그램 유형**은 개요 블레이드에 표시되는 내용 및 [메트릭 탐색기][metrics]에서 사용할 수 있는 속성에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-121">**Application type** affects what you see on the overview blade and the properties available in [metric explorer][metrics].</span></span> <span data-ttu-id="aedf9-122">앱 유형이 표시되지 않으면 일반을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-122">If you don't see your type of app, choose General.</span></span>
* <span data-ttu-id="aedf9-123">**구독** 은 Azure의 지불 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-123">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="aedf9-124">**리소스 그룹** 은 액세스 제어와 같은 속성을 관리하기 위한 편의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-124">**Resource group** is a convenience for managing properties like access control.</span></span> <span data-ttu-id="aedf9-125">이미 다른 Azure 리소스를 만든 경우 동일한 그룹에 이 새 리소스를 두도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-125">If you have already created other Azure resources, you can choose to put this new resource in the same group.</span></span>
* <span data-ttu-id="aedf9-126">**위치** 는 데이터를 보관하는 곳입니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-126">**Location** is where we keep your data.</span></span>
* <span data-ttu-id="aedf9-127">**대시보드에 고정**은 Azure 홈 페이지의 리소스에 대한 빠른 액세스 타일을 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-127">**Pin to dashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> <span data-ttu-id="aedf9-128">권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-128">Recommended.</span></span>

<span data-ttu-id="aedf9-129">앱이 만들어지면 새 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-129">When your app has been created, a new blade opens.</span></span> <span data-ttu-id="aedf9-130">이 블레이드에서 앱의 성능 및 사용량 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-130">This blade is where you see performance and usage data about your app.</span></span> 

<span data-ttu-id="aedf9-131">다음에 Azure에 로그인할 때 이곳으로 다시 돌아오려면 시작 보드(홈 화면)에서 앱의 빠른 시작 타일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-131">To get back to it next time you log in to Azure, look for your app's quick-start tile on the start board (home screen).</span></span> <span data-ttu-id="aedf9-132">또는 찾아보기를 클릭하여 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-132">Or click Browse to find it.</span></span>

## <a name="copy-the-instrumentation-key"></a><span data-ttu-id="aedf9-133">계측 키 복사</span><span class="sxs-lookup"><span data-stu-id="aedf9-133">Copy the instrumentation key</span></span>
<span data-ttu-id="aedf9-134">계측 키는 사용자가 만든 리소스를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-134">The instrumentation key identifies the resource that you created.</span></span> <span data-ttu-id="aedf9-135">SDK를 제공하기 위해 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-135">You need it to give to the SDK.</span></span>

![Essentials과 계측 키를 차례로 클릭하고, CTRL + C 누릅니다.](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-the-sdk-in-your-app"></a><span data-ttu-id="aedf9-137">응용 프로그램에 SDK를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-137">Install the SDK in your app</span></span>
<span data-ttu-id="aedf9-138">Application Insights SDK를 응용 프로그램에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-138">Install the Application Insights SDK in your app.</span></span> <span data-ttu-id="aedf9-139">이 단계는 응용 프로그램의 형식에 따라 크게 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-139">This step depends heavily on the type of your application.</span></span> 

<span data-ttu-id="aedf9-140">계측 키를 사용하여 [응용 프로그램에 설치한 SDK][start]를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-140">Use the instrumentation key to configure [the SDK that you install in your application][start].</span></span>

<span data-ttu-id="aedf9-141">SDK는 표준 모듈을 포함하고 있기 때문에 원격 분석을 전송할 때 코드를 작성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-141">The SDK includes standard modules that send telemetry without you having to write any code.</span></span> <span data-ttu-id="aedf9-142">사용자 작업을 추적하거나 문제를 보다 세부적으로 진단하려면 [API를 사용][api]하여 사용자 고유의 원격 분석을 보내도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-142">To track user actions or diagnose issues in more detail, [use the API][api] to send your own telemetry.</span></span>

## <span data-ttu-id="aedf9-143"><a name="monitor"></a>원격 분석 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="aedf9-143"><a name="monitor"></a>See telemetry data</span></span>
<span data-ttu-id="aedf9-144">빠른 시작 블레이드를 닫으면 Azure 포털의 사용자 응용 프로그램 블레이드로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-144">Close the quick start blade to return to your application blade in the Azure portal.</span></span>

<span data-ttu-id="aedf9-145">검색 타일을 클릭하여 첫 번째 이벤트가 표시되는 [진단 검색][diagnostic]을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-145">Click the Search tile to see [Diagnostic Search][diagnostic], where the first events appear.</span></span> 

<span data-ttu-id="aedf9-146">더 많은 데이터를 보려면 몇 초 후에 **새로 고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-146">If you're expecting more data, click **Refresh** after a few seconds  .</span></span>

## <a name="creating-a-resource-automatically"></a><span data-ttu-id="aedf9-147">자동으로 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="aedf9-147">Creating a resource automatically</span></span>
<span data-ttu-id="aedf9-148">리소스를 자동으로 만드는 [PowerShell 스크립트](app-insights-powershell.md) 를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedf9-148">You can write a [PowerShell script](app-insights-powershell.md) to create a resource automatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aedf9-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aedf9-149">Next steps</span></span>
* [<span data-ttu-id="aedf9-150">대시보드 만들기</span><span class="sxs-lookup"><span data-stu-id="aedf9-150">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="aedf9-151">진단 검색</span><span class="sxs-lookup"><span data-stu-id="aedf9-151">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="aedf9-152">메트릭 탐색</span><span class="sxs-lookup"><span data-stu-id="aedf9-152">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="aedf9-153">분석 쿼리 작성</span><span class="sxs-lookup"><span data-stu-id="aedf9-153">Write Analytics queries</span></span>](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

