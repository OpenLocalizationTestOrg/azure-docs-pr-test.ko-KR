---
title: "새 Azure Application Insights 리소스 aaaCreate | Microsoft Docs"
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
ms.openlocfilehash: 3aba7045e1f8fe43d473f0be01dd52106ab992a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-insights-resource"></a><span data-ttu-id="6117b-103">Application Insights 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="6117b-103">Create an Application Insights resource</span></span>
<span data-ttu-id="6117b-104">Azure Application Insights는 Microsoft Azure *리소스*에 응용 프로그램에 대한 데이터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-104">Azure Application Insights displays data about your application in a Microsoft Azure *resource*.</span></span> <span data-ttu-id="6117b-105">새 리소스 만들기의 일부가 되 [Application Insights toomonitor 새 응용 프로그램 설정][start]합니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-105">Creating a new resource is therefore part of [setting up Application Insights toomonitor a new application][start].</span></span> <span data-ttu-id="6117b-106">대부분의 경우에서 리소스를 만들고 여 수행할 수 있습니다 자동으로 hello IDE.</span><span class="sxs-lookup"><span data-stu-id="6117b-106">In many cases, creating a resource can be done automatically by hello IDE.</span></span> <span data-ttu-id="6117b-107">하지만 경우에 따라 리소스를 만들 수동으로-toohave 개발 및 프로덕션에 대 한 별도 리소스 응용 프로그램의 예를 들어 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-107">But in some cases, you create a resource manually - for example, toohave separate resources for development and production builds of your application.</span></span>

<span data-ttu-id="6117b-108">Hello 리소스를 만든 후 하면의 계측 키를 가져오고 hello 응용 프로그램에 해당 tooconfigure hello SDK를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-108">After you have created hello resource, you get its instrumentation key and use that tooconfigure hello SDK in hello application.</span></span> <span data-ttu-id="6117b-109">hello 리소스 키 링크 hello 원격 분석 toohello 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-109">hello resource key links hello telemetry toohello resource.</span></span>

## <a name="sign-up-toomicrosoft-azure"></a><span data-ttu-id="6117b-110">TooMicrosoft Azure 등록</span><span class="sxs-lookup"><span data-stu-id="6117b-110">Sign up tooMicrosoft Azure</span></span>
<span data-ttu-id="6117b-111">[Microsoft 계정이 없는 경우 계정을 만듭니다](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="6117b-111">If you haven't got a [Microsoft account, get one now](http://live.com).</span></span> <span data-ttu-id="6117b-112">Outlook.com, OneDrive, Windows Phone 또는 XBox Live 등의 서비스를 이용하는 경우 Microsoft 계정이 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-112">(If you use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, you already have a Microsoft account.)</span></span>

<span data-ttu-id="6117b-113">또한 해야 구독 너무[Microsoft Azure](http://azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-113">You also need a subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="6117b-114">팀 또는 조직에 Azure 구독이 있으면 hello 소유자 추가할 수 있습니다 tooit, Windows Live ID를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6117b-114">If your team or organization has an Azure subscription, hello owner can add you tooit, using your Windows Live ID.</span></span> <span data-ttu-id="6117b-115">사용하는 구독에 대해서만 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-115">You're only charged for what you use.</span></span> <span data-ttu-id="6117b-116">hello 기본 기본 계획 일정량 무료로 실험용으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-116">hello default basic plan allows for a certain amount of experimental use free of charge.</span></span>

<span data-ttu-id="6117b-117">액세스 tooa 구독을가지고 때 tooApplication Insights에 로그인 [http://portal.azure.com](https://portal.azure.com), Live ID toologin를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-117">When you've got access tooa subscription, log in tooApplication Insights at [http://portal.azure.com](https://portal.azure.com), and use your Live ID toologin.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="6117b-118">Application Insights 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="6117b-118">Create an Application Insights resource</span></span>
<span data-ttu-id="6117b-119">Hello에 [portal.azure.com](https://portal.azure.com), Application Insights 리소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-119">In hello [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![새로 만들기, Application Insights 클릭](./media/app-insights-create-new-resource/01-new.png)

* <span data-ttu-id="6117b-121">**응용 프로그램 종류** hello 개요 블레이드 및에서 사용할 수 있는 hello 속성에 표시 되는 내용에 영향을 줍니다 [메트릭 탐색기][metrics]합니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-121">**Application type** affects what you see on hello overview blade and hello properties available in [metric explorer][metrics].</span></span> <span data-ttu-id="6117b-122">앱 유형이 표시되지 않으면 일반을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-122">If you don't see your type of app, choose General.</span></span>
* <span data-ttu-id="6117b-123">**구독** 은 Azure의 지불 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-123">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="6117b-124">**리소스 그룹** 은 액세스 제어와 같은 속성을 관리하기 위한 편의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-124">**Resource group** is a convenience for managing properties like access control.</span></span> <span data-ttu-id="6117b-125">이미 다른 Azure 리소스를 만든 경우 선택할 수 있습니다 tooput이 새 리소스 hello에 동일한 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-125">If you have already created other Azure resources, you can choose tooput this new resource in hello same group.</span></span>
* <span data-ttu-id="6117b-126">**위치** 는 데이터를 보관하는 곳입니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-126">**Location** is where we keep your data.</span></span>
* <span data-ttu-id="6117b-127">**Pin toodashboard** 리소스에 대 한 빠른 액세스 타일 Azure 홈 페이지에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-127">**Pin toodashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> <span data-ttu-id="6117b-128">권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-128">Recommended.</span></span>

<span data-ttu-id="6117b-129">앱이 만들어지면 새 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-129">When your app has been created, a new blade opens.</span></span> <span data-ttu-id="6117b-130">이 블레이드에서 앱의 성능 및 사용량 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-130">This blade is where you see performance and usage data about your app.</span></span> 

<span data-ttu-id="6117b-131">tooget 백 tooit 다음 tooAzure에 로그인 할 때 응용 프로그램의 빠른 시작 타일 hello에 대 한 확인은 보드 (홈 화면)를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-131">tooget back tooit next time you log in tooAzure, look for your app's quick-start tile on hello start board (home screen).</span></span> <span data-ttu-id="6117b-132">찾아보기 toofind 키를 누르거나 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-132">Or click Browse toofind it.</span></span>

## <a name="copy-hello-instrumentation-key"></a><span data-ttu-id="6117b-133">Hello 계측 키 복사</span><span class="sxs-lookup"><span data-stu-id="6117b-133">Copy hello instrumentation key</span></span>
<span data-ttu-id="6117b-134">hello 계측 키 만든 hello 리소스를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-134">hello instrumentation key identifies hello resource that you created.</span></span> <span data-ttu-id="6117b-135">해야 toogive toohello SDK.</span><span class="sxs-lookup"><span data-stu-id="6117b-135">You need it toogive toohello SDK.</span></span>

![Essentials, hello 계측 키, CTRL + C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-hello-sdk-in-your-app"></a><span data-ttu-id="6117b-137">응용 프로그램에서 hello SDK 설치</span><span class="sxs-lookup"><span data-stu-id="6117b-137">Install hello SDK in your app</span></span>
<span data-ttu-id="6117b-138">응용 프로그램에서 hello Application Insights SDK를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-138">Install hello Application Insights SDK in your app.</span></span> <span data-ttu-id="6117b-139">이 단계는 응용 프로그램의 hello 형식에 따라 크게 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-139">This step depends heavily on hello type of your application.</span></span> 

<span data-ttu-id="6117b-140">계측 키 tooconfigure hello를 사용 하 여 [SDK 응용 프로그램에서 설치 하는 hello][start]합니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-140">Use hello instrumentation key tooconfigure [hello SDK that you install in your application][start].</span></span>

<span data-ttu-id="6117b-141">hello SDK toowrite 코드 필요 없이 원격 분석을 전송 하는 표준 모듈을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-141">hello SDK includes standard modules that send telemetry without you having toowrite any code.</span></span> <span data-ttu-id="6117b-142">tootrack 사용자 작업 또는 문제를 보다 자세히 진단할 [hello API를 사용 하 여] [ api] toosend 직접 원격 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-142">tootrack user actions or diagnose issues in more detail, [use hello API][api] toosend your own telemetry.</span></span>

## <span data-ttu-id="6117b-143"><a name="monitor"></a>원격 분석 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="6117b-143"><a name="monitor"></a>See telemetry data</span></span>
<span data-ttu-id="6117b-144">빠른 닫기 hello hello Azure 포털에서에서 블레이드 tooreturn tooyour 응용 프로그램 블레이드를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-144">Close hello quick start blade tooreturn tooyour application blade in hello Azure portal.</span></span>

<span data-ttu-id="6117b-145">검색 타일 toosee hello 클릭 [진단 검색][diagnostic]hello 첫 번째 이벤트가 표시 되는 위치, 합니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-145">Click hello Search tile toosee [Diagnostic Search][diagnostic], where hello first events appear.</span></span> 

<span data-ttu-id="6117b-146">더 많은 데이터를 보려면 몇 초 후에 **새로 고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-146">If you're expecting more data, click **Refresh** after a few seconds  .</span></span>

## <a name="creating-a-resource-automatically"></a><span data-ttu-id="6117b-147">자동으로 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="6117b-147">Creating a resource automatically</span></span>
<span data-ttu-id="6117b-148">작성할 수 있습니다는 [PowerShell 스크립트](app-insights-powershell.md) toocreate 리소스 자동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6117b-148">You can write a [PowerShell script](app-insights-powershell.md) toocreate a resource automatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6117b-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6117b-149">Next steps</span></span>
* [<span data-ttu-id="6117b-150">대시보드 만들기</span><span class="sxs-lookup"><span data-stu-id="6117b-150">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="6117b-151">진단 검색</span><span class="sxs-lookup"><span data-stu-id="6117b-151">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="6117b-152">메트릭 탐색</span><span class="sxs-lookup"><span data-stu-id="6117b-152">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="6117b-153">분석 쿼리 작성</span><span class="sxs-lookup"><span data-stu-id="6117b-153">Write Analytics queries</span></span>](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

