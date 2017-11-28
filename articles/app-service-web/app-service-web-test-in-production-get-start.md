---
title: "웹앱에 대한 프로덕션에서 테스트 시작"
description: "Azure 앱 서비스 웹앱에서 프로덕션(TiP) 기능의 테스트에 대해 알아봅니다."
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
ms.openlocfilehash: 9f38b635140cacf0513c75385bce3c110a930969
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-test-in-production-for-web-apps"></a><span data-ttu-id="731af-103">웹앱에 대한 프로덕션에서 테스트 시작</span><span class="sxs-lookup"><span data-stu-id="731af-103">Get started with test in production for Web Apps</span></span>
<span data-ttu-id="731af-104">프로덕션에서 테스트 또는 라이브 고객 트래픽을 사용하는 웹앱 라이브 테스트는 앱 개발자가 [민첩한 개발](https://en.wikipedia.org/wiki/Agile_software_development) 방법론에 점차 통합하는 테스트 전략입니다.</span><span class="sxs-lookup"><span data-stu-id="731af-104">Testing in production, or live-testing your web app using live customer traffic, is a test strategy that app developers increasingly integrate into their [agile development](https://en.wikipedia.org/wiki/Agile_software_development) methodology.</span></span> <span data-ttu-id="731af-105">테스트 환경에서 합성된 데이터와 달리 프로덕션 환경의 라이브 사용자 트래픽을 사용하는 앱의 품질을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="731af-105">It enables you to test the quality of your apps with live user traffic in your production environment, as opposed to synthesized data in a test environment.</span></span> <span data-ttu-id="731af-106">실제 사용자에게 새 앱을 노출하여 앱을 배포한 후에 앱에서 발생할 수 있는 실제 문제에 대한 알림을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="731af-106">By exposing your new app to real users, you can be informed on the real problems your app may face once it is deployed.</span></span> <span data-ttu-id="731af-107">앱의 기능, 성능 및 값을 확인하고 볼륨, 속도 및 다양한 실제 사용자 트래픽을 업데이트하며 이는 테스트 환경에서 대략적으로 구하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="731af-107">You can verify the functionality, performance, and value of your app updates against the volume, velocity, and variety of real user traffic, which you can never approximate in a test environment.</span></span>

## <a name="traffic-routing-in-app-service-web-apps"></a><span data-ttu-id="731af-108">앱 서비스 웹앱에서 트래픽 라이팅</span><span class="sxs-lookup"><span data-stu-id="731af-108">Traffic Routing in App Service Web Apps</span></span>
<span data-ttu-id="731af-109">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)의 트래픽을 라우팅 기능을 사용하여 하나 이상의 [배포 슬롯](web-sites-staged-publishing.md)에 라이브 사용자 트래픽의 일부를 지원하고 [Azure Application Insights](/services/application-insights/)를 사용하여 앱을 분석하며 또는 [Azure HDInsight](/services/hdinsight/) 또는 [New Relic](/marketplace/partners/newrelic/newrelic/)같은 타사 도구로 변경을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="731af-109">With the Traffic Routing feature in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can direct a portion of live user traffic to one or more [deployment slots](web-sites-staged-publishing.md), and then analyze your app with [Azure Application Insights](/services/application-insights/) or [Azure HDInsight](/services/hdinsight/), or a third-party tool like [New Relic](/marketplace/partners/newrelic/newrelic/) to validate your change.</span></span> <span data-ttu-id="731af-110">예를 들어 앱 서비스를 사용하여 다음과 같은 시나리오를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="731af-110">For example, you can implement the following scenarios with App Service:</span></span>

* <span data-ttu-id="731af-111">사이트 전체를 배포하기 전에 업데이트에서 기능 버그를 검색하거나 성능 병목 지점을 정확히 짚어봅니다.</span><span class="sxs-lookup"><span data-stu-id="731af-111">Discover functional bugs or pinpoint performance bottlenecks in your updates prior to site-wide deployment</span></span>
* <span data-ttu-id="731af-112">베타 앱에서 사용성 메트릭을 측정하여 변경된 "통제된 테스트 항공편"을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="731af-112">Perform "controlled test flights" of your changes by measuring usability metrics on the beta app</span></span>
* <span data-ttu-id="731af-113">오류가 발생하는 경우 새 업데이트까지 점차적으로 규모를 확장하고 현재 버전에 정상적으로 돌아옵니다.</span><span class="sxs-lookup"><span data-stu-id="731af-113">Gradually ramp up to a new update, and gracefully back down to the current version if an error occurs</span></span> 
* <span data-ttu-id="731af-114">여러 배포 슬롯에 [A/B 테스트](https://en.wikipedia.org/wiki/A/B_testing) 또는 [다변량 테스트](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing)를 실행하여 앱의 비즈니스 결과를 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="731af-114">Optimize your app's business results by running [A/B tests](https://en.wikipedia.org/wiki/A/B_testing) or [multivariate tests](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing) in multiple deployment slots</span></span>

### <a name="requirements-for-using-traffic-routing-in-web-apps"></a><span data-ttu-id="731af-115">웹앱에서 트래픽 라우팅을 사용하는 데 대한 요구 사항</span><span class="sxs-lookup"><span data-stu-id="731af-115">Requirements for using Traffic Routing in Web Apps</span></span>
* <span data-ttu-id="731af-116">웹앱은 여러 배포 슬롯에 대해 필요한 대로 **표준** 또는 **프리미엄** 계층에서 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="731af-116">Your web app must run in **Standard** or **Premium** tier, as it is required for multiple deployment slots.</span></span>
* <span data-ttu-id="731af-117">제대로 작동하려면 트래픽 라우팅은 쿠키를 사용자의 브라우저에서 사용하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="731af-117">In order to work properly, Traffic Routing requires cookies to be enabled in the users' browser.</span></span> <span data-ttu-id="731af-118">트래픽 라우팅은 클라이언트 세션 수명에 대한 배포 슬롯에 클라이언트 브라우저를 고정하는 데  쿠키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="731af-118">Traffic Routing uses cookies to pin a client browser to a deployment slot for the life the client session.</span></span>
* <span data-ttu-id="731af-119">트래픽 라우팅은 Azure PowerShell cmdlet를 통해 고급 TiP 시나리오를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="731af-119">Traffic Routing supports advanced TiP scenarios through Azure PowerShell cmdlets.</span></span>

## <a name="route-traffic-segment-to-a-deployment-slot"></a><span data-ttu-id="731af-120">배포 슬롯에 라우팅 트래픽 세그먼트</span><span class="sxs-lookup"><span data-stu-id="731af-120">Route traffic segment to a deployment slot</span></span>
<span data-ttu-id="731af-121">모든 TiP 시나리오의 기본 수준에서 비프로덕션 배포 슬롯에 미리 정의된 비율의 라이브 트래픽을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="731af-121">At the basic level in every TiP scenario, you route a predefined percentage of your live traffic to a non-production deployment slot.</span></span> <span data-ttu-id="731af-122">이렇게 하려면 다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="731af-122">To do this, follow the steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="731af-123">여기에서 단계는 [비-프로덕션 배포 슬롯](web-sites-staged-publishing.md) 및 웹앱 콘텐츠가 이미 [배포](web-sites-deploy.md)되었기를 원합니다.</span><span class="sxs-lookup"><span data-stu-id="731af-123">The steps here assumes that you already have a [non-production deployment slot](web-sites-staged-publishing.md) and that the desired web app content is already [deployed](web-sites-deploy.md) to it.</span></span>
> 
> 

1. <span data-ttu-id="731af-124">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="731af-124">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="731af-125">웹앱의 블레이드에서 **설정** > **트래픽 라우팅**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="731af-125">In your web app's blade, click **Settings** > **Traffic Routing**.</span></span>
   ![](./media/app-service-web-test-in-production/01-traffic-routing.png)
3. <span data-ttu-id="731af-126">라우트하려는 슬롯을 **저장**하면 트래픽 라우팅을 하려는 슬롯 및 원하는 총 트래픽의 비율을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="731af-126">Select the slot that you want to route traffic to and the percentage of the total traffic you desire, then click **Save**.</span></span>
   
    ![](./media/app-service-web-test-in-production/02-select-slot.png)
4. <span data-ttu-id="731af-127">배포 슬롯의 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="731af-127">Go to the deployment slot's blade.</span></span> <span data-ttu-id="731af-128">이제 라우팅된 라이브 트래픽을 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="731af-128">You should now see live traffic being routed to it.</span></span>
   
    ![](./media/app-service-web-test-in-production/03-traffic-routed.png)

<span data-ttu-id="731af-129">트래픽 라우팅이 구성되면 클라이언트의 지정된 백분율은 비-프로덕션 슬롯에 임의로 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="731af-129">Once Traffic Routing is configured, the specified percentage of clients will be randomly routed to your non-production slot.</span></span> <span data-ttu-id="731af-130">그러나 클라이언트가 특정 슬롯에 자동으로 라우팅되면 해당 슬롯에 클라이언트 세션의 수명 동안 "고정"되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="731af-130">However, it is important to note that once a client is automatically routed to a specific slot, it will be "pinned" to that slot for the life of that client session.</span></span> <span data-ttu-id="731af-131">이 작업은 쿠키를 사용하여 사용자 세션을 고정합니다.</span><span class="sxs-lookup"><span data-stu-id="731af-131">This done using a cookie to pin the user session.</span></span> <span data-ttu-id="731af-132">HTTP 요청을 조사하여 모든 후속 요청에서 `TipMix` 쿠키를 찾을 수 있습입니다.</span><span class="sxs-lookup"><span data-stu-id="731af-132">If you inspect the HTTP requests, you will find a `TipMix` cookie in every subsequent request.</span></span>

![](./media/app-service-web-test-in-production/04-tip-cookie.png)

## <a name="force-client-requests-to-a-specific-slot"></a><span data-ttu-id="731af-133">특정 슬롯에 클라이언트 요청을 강제로</span><span class="sxs-lookup"><span data-stu-id="731af-133">Force client requests to a specific slot</span></span>
<span data-ttu-id="731af-134">자동 트래픽 라우팅 외에도 앱 서비스는 특정 슬롯에 요청을 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="731af-134">In addition to automatic traffic routing, App Service is able to route requests to a specific slot.</span></span> <span data-ttu-id="731af-135">사용자가 베타 앱에 참여 또는 탈퇴를 선택할 수 있도록 하려는 경우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="731af-135">This is useful when you want your users to be able to opt-into or opt-out of your beta app.</span></span> <span data-ttu-id="731af-136">이를 수행하기 위해 `x-ms-routing-name` 쿼리 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="731af-136">To do this, you use the `x-ms-routing-name` query parameter.</span></span>

<span data-ttu-id="731af-137">`x-ms-routing-name`을 사용하여 사용자를 특정 슬롯에 다시 라우팅하려면 슬롯이 트래픽 라우팅 목록에 이미 추가되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="731af-137">To reroute users to a specific slot using `x-ms-routing-name`, you must make sure that the slot is already added to the Traffic Routing list.</span></span> <span data-ttu-id="731af-138">명시적으로 슬롯에 라우팅하려 하기 때문에 설정한 실제 라우팅 백분율은 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="731af-138">Since you want to route to a slot explicitly, the actual routing percentage you set doesn't matter.</span></span> <span data-ttu-id="731af-139">원하는 경우 베타 앱에 액세스하기 위해 사용자가 클릭할 수 있는 "베타 링크"를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="731af-139">If you want, you can craft a "beta link" that users can click to access the beta app.</span></span>

![](./media/app-service-web-test-in-production/06-enable-x-ms-routing-name.png)

### <a name="opt-users-out-of-beta-app"></a><span data-ttu-id="731af-140">베타 앱에서 사용자 탈퇴</span><span class="sxs-lookup"><span data-stu-id="731af-140">Opt users out of beta app</span></span>
<span data-ttu-id="731af-141">예를 들어 사용자가 베타 앱에 참여하지 않도록 하려면 웹 페이지에 이 링크를 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="731af-141">To let users opt out of your beta app, for example, you can put this link in your web page:</span></span>

    <a href="<webappname>.azurewebsites.net/?x-ms-routing-name=self">Go back to production app</a>

<span data-ttu-id="731af-142">문자열 `x-ms-routing-name=self` 는 프로덕션 슬롯을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="731af-142">The string `x-ms-routing-name=self` specifies the production slot.</span></span> <span data-ttu-id="731af-143">클라이언트 브라우저가 링크에 액세스하면 프로덕션 슬롯으로 리디렉션될 뿐만 아니라 모든 후속 요청이 프로덕션 슬롯에 세션을 고정하는 `x-ms-routing-name=self` 쿠키를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="731af-143">Once the client browser access the link, not only is it redirected to the production slot, but every subsequent request will contain the `x-ms-routing-name=self` cookie that pins the session to the production slot.</span></span>

![](./media/app-service-web-test-in-production/05-access-production-slot.png)

### <a name="opt-users-in-to-beta-app"></a><span data-ttu-id="731af-144">베타 앱에서 사용자 참여</span><span class="sxs-lookup"><span data-stu-id="731af-144">Opt users in to beta app</span></span>
<span data-ttu-id="731af-145">예를 들어 사용자가 베타 앱에 참여하게 하려면 비-프로덕션 슬롯의 이름에 동일한 쿼리 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="731af-145">To let users opt in to your beta app, set the same query parameter to the name of the non-production slot, for example:</span></span>

        <webappname>.azurewebsites.net/?x-ms-routing-name=staging

## <a name="more-resources"></a><span data-ttu-id="731af-146">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="731af-146">More resources</span></span>
* [<span data-ttu-id="731af-147">Azure 앱 서비스에서 웹 앱에 대한 스테이징 환경 설정</span><span class="sxs-lookup"><span data-stu-id="731af-147">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)
* [<span data-ttu-id="731af-148">Azure에서 예측 가능하도록 복잡한 응용 프로그램을 배포</span><span class="sxs-lookup"><span data-stu-id="731af-148">Deploy a complex application predictably in Azure</span></span>](app-service-deploy-complex-application-predictably.md)
* [<span data-ttu-id="731af-149">Azure 앱 서비스를 사용하여 Agile 소프트웨어 개발</span><span class="sxs-lookup"><span data-stu-id="731af-149">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)
* [<span data-ttu-id="731af-150">웹 앱에서 DevOps 환경을 효과적으로 사용하기</span><span class="sxs-lookup"><span data-stu-id="731af-150">Use DevOps environments effectively for your web apps</span></span>](app-service-web-staged-publishing-realworld-scenarios.md)

