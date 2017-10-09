---
title: "웹 앱에 대 한 프로덕션에서에서 테스트 aaaGet 시작"
description: "Azure 앱 서비스 웹 앱의 프로덕션 (TiP) 기능에 hello 테스트 방법을 알아봅니다."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 4623468d-886e-4203-8012-8f86deb2790b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: cephalin
ms.openlocfilehash: 2ddbd532ffe2a4f3e07fd386d9741a3fde3639ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-test-in-production-for-web-apps"></a><span data-ttu-id="64078-103">웹앱에 대한 프로덕션에서 테스트 시작</span><span class="sxs-lookup"><span data-stu-id="64078-103">Get started with test in production for Web Apps</span></span>
<span data-ttu-id="64078-104">프로덕션에서 테스트 또는 라이브 고객 트래픽을 사용하는 웹앱 라이브 테스트는 앱 개발자가 [민첩한 개발](https://en.wikipedia.org/wiki/Agile_software_development) 방법론에 점차 통합하는 테스트 전략입니다.</span><span class="sxs-lookup"><span data-stu-id="64078-104">Testing in production, or live-testing your web app using live customer traffic, is a test strategy that app developers increasingly integrate into their [agile development](https://en.wikipedia.org/wiki/Agile_software_development) methodology.</span></span> <span data-ttu-id="64078-105">하면 tootest hello 품질 프로덕션 환경의 실시간 사용자 트래픽이 응용 프로그램의 테스트 환경에 사용 되는 것과 반대로 toosynthesized 데이터로.</span><span class="sxs-lookup"><span data-stu-id="64078-105">It enables you tootest hello quality of your apps with live user traffic in your production environment, as opposed toosynthesized data in a test environment.</span></span> <span data-ttu-id="64078-106">새 앱 tooreal 사용자가 노출 하 여 앱을 배포한 후에 직면할 수 hello 실제 문제에 알릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64078-106">By exposing your new app tooreal users, you can be informed on hello real problems your app may face once it is deployed.</span></span> <span data-ttu-id="64078-107">Hello 기능, 성능 및 hello 볼륨, 속도 및 다양 한 되지 작은 변경 사항을 테스트 환경에는 실제 사용자 트래픽이 응용 프로그램 업데이트의 값을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64078-107">You can verify hello functionality, performance, and value of your app updates against hello volume, velocity, and variety of real user traffic, which you can never approximate in a test environment.</span></span>

## <a name="traffic-routing-in-app-service-web-apps"></a><span data-ttu-id="64078-108">앱 서비스 웹앱에서 트래픽 라이팅</span><span class="sxs-lookup"><span data-stu-id="64078-108">Traffic Routing in App Service Web Apps</span></span>
<span data-ttu-id="64078-109">트래픽 라우팅을 hello로 기능에서 [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)를 전달할 수 있습니다. 사용 중인 사용자 트래픽 tooone 이상의 부분 [배포 슬롯](web-sites-staged-publishing.md), 사용 하 여 앱을 분석 [Azure 응용 프로그램 Insights](/services/application-insights/) 또는 [Azure HDInsight](/services/hdinsight/)와 같은 타사 도구 또는 [New Relic](/marketplace/partners/newrelic/newrelic/) toovalidate 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="64078-109">With hello Traffic Routing feature in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can direct a portion of live user traffic tooone or more [deployment slots](web-sites-staged-publishing.md), and then analyze your app with [Azure Application Insights](/services/application-insights/) or [Azure HDInsight](/services/hdinsight/), or a third-party tool like [New Relic](/marketplace/partners/newrelic/newrelic/) toovalidate your change.</span></span> <span data-ttu-id="64078-110">예를 들어 hello 다음 응용 프로그램 서비스와 시나리오를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64078-110">For example, you can implement hello following scenarios with App Service:</span></span>

* <span data-ttu-id="64078-111">기능 버그를 검색 하거나 업데이트 이전 toosite 전체 배포에 성능 병목 상태를 정확히 파악</span><span class="sxs-lookup"><span data-stu-id="64078-111">Discover functional bugs or pinpoint performance bottlenecks in your updates prior toosite-wide deployment</span></span>
* <span data-ttu-id="64078-112">Hello 베타 앱에 대 한 유용성 메트릭을 측정 하 여 변경 내용을의 "통제 된 테스트 비행 연착"를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="64078-112">Perform "controlled test flights" of your changes by measuring usability metrics on hello beta app</span></span>
* <span data-ttu-id="64078-113">점진적으로 성능을 향상 시키는 tooa 새 업데이트 하 고 오류가 발생 하면 정상적으로 다운 toohello 현재 버전 다시</span><span class="sxs-lookup"><span data-stu-id="64078-113">Gradually ramp up tooa new update, and gracefully back down toohello current version if an error occurs</span></span> 
* <span data-ttu-id="64078-114">여러 배포 슬롯에 [A/B 테스트](https://en.wikipedia.org/wiki/A/B_testing) 또는 [다변량 테스트](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing)를 실행하여 앱의 비즈니스 결과를 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="64078-114">Optimize your app's business results by running [A/B tests](https://en.wikipedia.org/wiki/A/B_testing) or [multivariate tests](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing) in multiple deployment slots</span></span>

### <a name="requirements-for-using-traffic-routing-in-web-apps"></a><span data-ttu-id="64078-115">웹앱에서 트래픽 라우팅을 사용하는 데 대한 요구 사항</span><span class="sxs-lookup"><span data-stu-id="64078-115">Requirements for using Traffic Routing in Web Apps</span></span>
* <span data-ttu-id="64078-116">웹앱은 여러 배포 슬롯에 대해 필요한 대로 **표준** 또는 **프리미엄** 계층에서 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64078-116">Your web app must run in **Standard** or **Premium** tier, as it is required for multiple deployment slots.</span></span>
* <span data-ttu-id="64078-117">순서 toowork 제대로 hello 사용자의 브라우저에서 사용 하도록 설정 하는 쿠키 toobe 트래픽 라우팅이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="64078-117">In order toowork properly, Traffic Routing requires cookies toobe enabled in hello users' browser.</span></span> <span data-ttu-id="64078-118">트래픽 라우팅 hello 수명 hello 클라이언트 세션에 대 한 쿠키 toopin 클라이언트 브라우저 tooa 배포 슬롯을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="64078-118">Traffic Routing uses cookies toopin a client browser tooa deployment slot for hello life hello client session.</span></span>
* <span data-ttu-id="64078-119">트래픽 라우팅은 Azure PowerShell cmdlet를 통해 고급 TiP 시나리오를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="64078-119">Traffic Routing supports advanced TiP scenarios through Azure PowerShell cmdlets.</span></span>

## <a name="route-traffic-segment-tooa-deployment-slot"></a><span data-ttu-id="64078-120">경로 트래픽 세그먼트 tooa 배포 슬롯</span><span class="sxs-lookup"><span data-stu-id="64078-120">Route traffic segment tooa deployment slot</span></span>
<span data-ttu-id="64078-121">모든 팁 시나리오에서 hello 기본적인 수준에서의 실시간 트래픽 tooa 비-프로덕션 배포 슬롯을 사용 하 여 미리 정의 된 백분율이 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64078-121">At hello basic level in every TiP scenario, you route a predefined percentage of your live traffic tooa non-production deployment slot.</span></span> <span data-ttu-id="64078-122">toodo 다음,이 따라 hello 단계:</span><span class="sxs-lookup"><span data-stu-id="64078-122">toodo this, follow hello steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="64078-123">hello 여기에 나오는 단계 이미 있다고 가정는 [비-프로덕션 배포 슬롯](web-sites-staged-publishing.md) 및 해당 hello 원하는 웹 응용 프로그램 콘텐츠를 이미 [배포](web-sites-deploy.md) tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="64078-123">hello steps here assumes that you already have a [non-production deployment slot](web-sites-staged-publishing.md) and that hello desired web app content is already [deployed](web-sites-deploy.md) tooit.</span></span>
> 
> 

1. <span data-ttu-id="64078-124">Hello에 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="64078-124">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="64078-125">웹앱의 블레이드에서 **설정** > **트래픽 라우팅**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64078-125">In your web app's blade, click **Settings** > **Traffic Routing**.</span></span>
   ![](./media/app-service-web-test-in-production/01-traffic-routing.png)
3. <span data-ttu-id="64078-126">Tooroute 트래픽 tooand hello 비율을 다음 클릭 총 트래픽 hello의 원하는 선택 hello 슬롯 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="64078-126">Select hello slot that you want tooroute traffic tooand hello percentage of hello total traffic you desire, then click **Save**.</span></span>
   
    ![](./media/app-service-web-test-in-production/02-select-slot.png)
4. <span data-ttu-id="64078-127">Toohello 배포 슬롯 블레이드로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="64078-127">Go toohello deployment slot's blade.</span></span> <span data-ttu-id="64078-128">이제 실시간 트래픽 라우팅된 tooit 되 고 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64078-128">You should now see live traffic being routed tooit.</span></span>
   
    ![](./media/app-service-web-test-in-production/03-traffic-routed.png)

<span data-ttu-id="64078-129">트래픽 라우팅을 구성한 후에 hello 지정한 클라이언트의 백분율이 임의로 라우트된 tooyour 비-프로덕션 슬롯 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64078-129">Once Traffic Routing is configured, hello specified percentage of clients will be randomly routed tooyour non-production slot.</span></span> <span data-ttu-id="64078-130">그러나 것이 중요 한 toonote 클라이언트를 자동으로 라우팅된 tooa 특정 슬롯 하다는 점을 해당 클라이언트 세션의 라이프 hello에 대 한 "고정된" toothat 슬롯입니다.</span><span class="sxs-lookup"><span data-stu-id="64078-130">However, it is important toonote that once a client is automatically routed tooa specific slot, it will be "pinned" toothat slot for hello life of that client session.</span></span> <span data-ttu-id="64078-131">이 작업 수행 쿠키 toopin hello 사용자 세션을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="64078-131">This done using a cookie toopin hello user session.</span></span> <span data-ttu-id="64078-132">Hello HTTP 요청을 검사 하는 경우 찾을 수 있습니다는 `TipMix` 모든 후속 요청에서 쿠키입니다.</span><span class="sxs-lookup"><span data-stu-id="64078-132">If you inspect hello HTTP requests, you will find a `TipMix` cookie in every subsequent request.</span></span>

![](./media/app-service-web-test-in-production/04-tip-cookie.png)

## <a name="force-client-requests-tooa-specific-slot"></a><span data-ttu-id="64078-133">클라이언트 요청 tooa 특정 슬롯을 강제 적용</span><span class="sxs-lookup"><span data-stu-id="64078-133">Force client requests tooa specific slot</span></span>
<span data-ttu-id="64078-134">또한 tooautomatic 트래픽 라우팅에 서비스 응용 프로그램은 수 tooroute 요청 tooa 특정 슬롯입니다.</span><span class="sxs-lookup"><span data-stu-id="64078-134">In addition tooautomatic traffic routing, App Service is able tooroute requests tooa specific slot.</span></span> <span data-ttu-id="64078-135">사용자가 toobe 수 tooopt 하려는 경우 유용-또는 베타 응용 프로그램의 수신 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="64078-135">This is useful when you want your users toobe able tooopt-into or opt-out of your beta app.</span></span> <span data-ttu-id="64078-136">toodo이 hello를 사용 하 여 `x-ms-routing-name` 쿼리 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="64078-136">toodo this, you use hello `x-ms-routing-name` query parameter.</span></span>

<span data-ttu-id="64078-137">tooreroute 사용자 tooa 특정 슬롯을 사용 하 여 `x-ms-routing-name`, 해당 hello 슬롯 toohello 트래픽 라우팅 목록에 이미 추가 되어 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64078-137">tooreroute users tooa specific slot using `x-ms-routing-name`, you must make sure that hello slot is already added toohello Traffic Routing list.</span></span> <span data-ttu-id="64078-138">Tooroute tooa 슬롯을 명시적으로 지정할 것 이므로 hello 실제 라우팅 비율이 설정한 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="64078-138">Since you want tooroute tooa slot explicitly, hello actual routing percentage you set doesn't matter.</span></span> <span data-ttu-id="64078-139">원하는 경우 사용자가 클릭할 수 있는 "베타 링크"를 만들 수 있습니다 tooaccess hello 베타 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="64078-139">If you want, you can craft a "beta link" that users can click tooaccess hello beta app.</span></span>

![](./media/app-service-web-test-in-production/06-enable-x-ms-routing-name.png)

### <a name="opt-users-out-of-beta-app"></a><span data-ttu-id="64078-140">베타 앱에서 사용자 탈퇴</span><span class="sxs-lookup"><span data-stu-id="64078-140">Opt users out of beta app</span></span>
<span data-ttu-id="64078-141">toolet 사용자 베타 응용 프로그램을 취소, 예를 들어 웹 페이지에이 링크를 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64078-141">toolet users opt out of your beta app, for example, you can put this link in your web page:</span></span>

    <a href="<webappname>.azurewebsites.net/?x-ms-routing-name=self">Go back tooproduction app</a>

<span data-ttu-id="64078-142">문자열 hello `x-ms-routing-name=self` hello 프로덕션 슬롯을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="64078-142">hello string `x-ms-routing-name=self` specifies hello production slot.</span></span> <span data-ttu-id="64078-143">일단 hello 클라이언트 브라우저 액세스 hello 링크 뿐만 아니라 toohello 프로덕션 슬롯을 리디렉션 하지만 모든 후속 요청 hello 들어갑니다 `x-ms-routing-name=self` hello 세션 toohello 프로덕션 슬롯을 고정 하는 쿠키입니다.</span><span class="sxs-lookup"><span data-stu-id="64078-143">Once hello client browser access hello link, not only is it redirected toohello production slot, but every subsequent request will contain hello `x-ms-routing-name=self` cookie that pins hello session toohello production slot.</span></span>

![](./media/app-service-web-test-in-production/05-access-production-slot.png)

### <a name="opt-users-in-toobeta-app"></a><span data-ttu-id="64078-144">Toobeta 응용 프로그램에서 사용자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="64078-144">Opt users in toobeta app</span></span>
<span data-ttu-id="64078-145">tooyour 베타 응용 프로그램에 옵트인 toolet 사용자, 동일한 집합 hello 예를 들어 hello 비-프로덕션 슬롯의 toohello 이름 매개 변수를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="64078-145">toolet users opt in tooyour beta app, set hello same query parameter toohello name of hello non-production slot, for example:</span></span>

        <webappname>.azurewebsites.net/?x-ms-routing-name=staging

## <a name="more-resources"></a><span data-ttu-id="64078-146">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="64078-146">More resources</span></span>
* [<span data-ttu-id="64078-147">Azure 앱 서비스에서 웹 앱에 대한 스테이징 환경 설정</span><span class="sxs-lookup"><span data-stu-id="64078-147">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)
* [<span data-ttu-id="64078-148">Azure에서 예측 가능하도록 복잡한 응용 프로그램을 배포</span><span class="sxs-lookup"><span data-stu-id="64078-148">Deploy a complex application predictably in Azure</span></span>](app-service-deploy-complex-application-predictably.md)
* [<span data-ttu-id="64078-149">Azure 앱 서비스를 사용하여 Agile 소프트웨어 개발</span><span class="sxs-lookup"><span data-stu-id="64078-149">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)
* [<span data-ttu-id="64078-150">웹 앱에서 DevOps 환경을 효과적으로 사용하기</span><span class="sxs-lookup"><span data-stu-id="64078-150">Use DevOps environments effectively for your web apps</span></span>](app-service-web-staged-publishing-realworld-scenarios.md)

