---
title: "aaaI 모바일 서비스를 사용 하 여, 앱 서비스 도움이 됩니까?"
description: "어떤 이점을 앱 서비스 가지 tooyour 기존 모바일 서비스 프로젝트에 알아봅니다."
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 26b68a11-8352-4f78-acd2-e4e0ec177781
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 315cc6eedcdca6c3f9f9bb9fd5ec7baf655b7e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="919c0-103"><a name="getting-started"> </a>모바일 서비스를 사용하고 있습니다. 앱 서비스가 어떤 도움을 주나요?</span><span class="sxs-lookup"><span data-stu-id="919c0-103"><a name="getting-started"> </a>I use Mobile Services, how does App Service help?</span></span>
## <a name="overview"></a><span data-ttu-id="919c0-104">개요</span><span class="sxs-lookup"><span data-stu-id="919c0-104">Overview</span></span>
<span data-ttu-id="919c0-105">기존 모바일 서비스는 안전하며 계속 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="919c0-105">Your existing Mobile Service is safe and will remain supported.</span></span> <span data-ttu-id="919c0-106">그러나 장점 hello 수가 *Azure 앱 서비스* 모바일 서비스를 현재 사용할 수 없는 모바일 앱에 대 한 플랫폼 제공:</span><span class="sxs-lookup"><span data-stu-id="919c0-106">However there are number of advantages hello *Azure App Service* platform provides for your mobile app that are not available today with Mobile Services:</span></span>

* <span data-ttu-id="919c0-107">웹 클라이언트와 모바일 클라이언트를 둘 다 포함하는 앱을 위한 더 간단하고 쉽고 비용 효과적인 제품</span><span class="sxs-lookup"><span data-stu-id="919c0-107">Simpler, easier and more cost effective offering for apps that include both web and mobile clients</span></span>
* <span data-ttu-id="919c0-108">웹 작업, 사용자 지정 CName, 향상된 모니터링을 포함하는 새로운 호스트 기능</span><span class="sxs-lookup"><span data-stu-id="919c0-108">New host features including Web Jobs, custom CNames, better monitoring</span></span>
* <span data-ttu-id="919c0-109">트래픽 관리자와의 완성 인도 통합</span><span class="sxs-lookup"><span data-stu-id="919c0-109">Turnkey integration with Traffic Manager</span></span>
* <span data-ttu-id="919c0-110">연결 tooyour 온-프레미스 리소스 및 추가 tooHybrid 연결에서에서 VNet을 사용 하 여 Vpn</span><span class="sxs-lookup"><span data-stu-id="919c0-110">Connectivity tooyour on-premises resources and VPNs using VNet in addition tooHybrid Connections</span></span>
* <span data-ttu-id="919c0-111">NewRelic 또는 AppInsights를 사용하여 앱에 대한 모니터링, 경고 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="919c0-111">Monitoring, alerting and  troubleshooting for your app using NewRelic or AppInsights</span></span>
* <span data-ttu-id="919c0-112">다양 한 종류의 hello 기본 계산 리소스 및 가격</span><span class="sxs-lookup"><span data-stu-id="919c0-112">Richer spectrum of hello underlying compute resources and pricing</span></span>
* <span data-ttu-id="919c0-113">기본 제공되는 자동 크기 조정, 부하 분산 및 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="919c0-113">Built-in auto scale, load balancing, and performance monitoring.</span></span>
* <span data-ttu-id="919c0-114">기본 제공되는 스테이징, 백업, 롤백 및 프로덕션에서 테스트 기능</span><span class="sxs-lookup"><span data-stu-id="919c0-114">Built-in staging, backup, roll-back, and testing-in-production capabilities</span></span>

## <a name="new-hosting-features"></a><span data-ttu-id="919c0-115">새로운 호스팅 기능</span><span class="sxs-lookup"><span data-stu-id="919c0-115">New hosting features</span></span>
<span data-ttu-id="919c0-116">*Azure 앱 서비스* hello *모바일 앱* 동일한 웹 응용 프로그램으로 컨테이너 및 API 앱 백엔드에 코드를 실행 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="919c0-116">In *Azure App Service* hello *Mobile App* backend code runs in hello same container as Web App and API App.</span></span> <span data-ttu-id="919c0-117">따라서 모바일 서비스에서 현재 존재 하지 않는 그 중 일부를 포함 하 여이 컨테이너의 모든 hello 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="919c0-117">As such you can take advantage of all hello features in this container, including some of those that are not currently present in Mobile Services:</span></span>

* <span data-ttu-id="919c0-118">웹 작업을 통해 연속 실행되는 백 엔드 논리 추가</span><span class="sxs-lookup"><span data-stu-id="919c0-118">Add continuously running backend logic via Web Jobs</span></span>
* <span data-ttu-id="919c0-119">백 엔드 코드가 항상 실행되도록 유지</span><span class="sxs-lookup"><span data-stu-id="919c0-119">Ensure your backend code is always running</span></span>
* <span data-ttu-id="919c0-120">친숙 한 사용자 지정 CNames tooprovide를 사용 하 여 이름과 안정적인 tooyour 모바일 백 엔드 끝점</span><span class="sxs-lookup"><span data-stu-id="919c0-120">Use custom CNames tooprovide friendly and stable names tooyour mobile backend endpoints</span></span>
* <span data-ttu-id="919c0-121">트래픽 관리자를 사용하여 앱 지역 크기 조정</span><span class="sxs-lookup"><span data-stu-id="919c0-121">Geo-scale your app with Traffic Manager</span></span>
* <span data-ttu-id="919c0-122">원하는 모든 라이브러리 및 패키지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="919c0-122">Include any libraries and packages you want.</span></span>
* <span data-ttu-id="919c0-123">(.NET에 대해) MVC를 포함한 ASP.NET의 기능 활용</span><span class="sxs-lookup"><span data-stu-id="919c0-123">(For .NET) Leverage any feature of ASP.NET, including MVC</span></span>
* <span data-ttu-id="919c0-124">(Node.js)에 대 한 일반적인 MVC 라이브러리를 포함 하 여 hello 노드 에코 시스템의 모든 순수 JavaScript 라이브러리를 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="919c0-124">(For Node.js) Leverage any pure JavaScript library of hello Node ecosystem, including common MVC libraries.</span></span>

## <a name="access-on-premises-data-using-vnet"></a><span data-ttu-id="919c0-125">VNet을 사용하여 온-프레미스 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="919c0-125">Access on-premises data using VNet</span></span>
<span data-ttu-id="919c0-126">모바일 서비스와 오늘 하이브리드 연결 tooaccess에서는 이미 온-프레미스 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="919c0-126">With Mobile Services today you can already use Hybrid Connections tooaccess on-premises resources.</span></span> <span data-ttu-id="919c0-127">그러나 VPN 솔루션이 선호되는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="919c0-127">However there are situations where a VPN solution is preferred.</span></span> <span data-ttu-id="919c0-128">*Azure 앱 서비스* 에서는 Azure VNet을 모바일 앱 백 엔드 코드에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="919c0-128">With *Azure App Service* you can use Azure VNet for your Mobile App backend code.</span></span>

## <a name="use-your-favorite-backend-language"></a><span data-ttu-id="919c0-129">좋아하는 백 엔드 언어 사용</span><span class="sxs-lookup"><span data-stu-id="919c0-129">Use your favorite backend language</span></span>
<span data-ttu-id="919c0-130">*Azure 앱 서비스* 혜택 보다 광범위 한 및 다양 한 지원을 비롯 하 여 ASP.NET 및 Node.js 플랫폼에 대 한 액세스 toohello 최신 런타임.</span><span class="sxs-lookup"><span data-stu-id="919c0-130">*Azure App Service* offers broader and richer support for ASP.NET and Node.js platforms, including access toohello latest runtimes.</span></span>

## <a name="set-up-automatic-scale"></a><span data-ttu-id="919c0-131">자동 크기 조정 설정</span><span class="sxs-lookup"><span data-stu-id="919c0-131">Set up automatic scale</span></span>
<span data-ttu-id="919c0-132">모바일 서비스에서는 백 엔드 코드의 모든 인스턴스가 작은 VM에서 실행되었습니다.</span><span class="sxs-lookup"><span data-stu-id="919c0-132">With Mobile Services, all instances of your backend code were running on Small VMs.</span></span> <span data-ttu-id="919c0-133">*Azure 앱 서비스* tooselect hello 크기의 Vm에서 많은 다양 한 옵션 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="919c0-133">*Azure App Service* enables you tooselect hello size of the VMs from a much richer set of options.</span></span> <span data-ttu-id="919c0-134">확장할 수 있습니다 신속 하 게 또는 toohandle 다양 한 성능 메트릭을 기반으로 들어오는 고객 부하 모든.</span><span class="sxs-lookup"><span data-stu-id="919c0-134">You can also  quickly scale up or out toohandle any incoming customer load, based on various performance metrics.</span></span>

## <a name="be-in-hello-know"></a><span data-ttu-id="919c0-135">Hello에 "알고" 수</span><span class="sxs-lookup"><span data-stu-id="919c0-135">Be in hello “know”</span></span>
<span data-ttu-id="919c0-136">Tooissues 대응 하며의 모니터링 및 경고와 함께 실시간 tooautomatically 알림 및 사용자 팀입니다.</span><span class="sxs-lookup"><span data-stu-id="919c0-136">React tooissues in real-time with monitoring and alerts tooautomatically notify you and your team.</span></span> <span data-ttu-id="919c0-137">고급 응용 프로그램 분석 및에서 New Relic 및 AppInsights tooget 다양 한도에 대 한 정보 모바일 앱이 수행 되는 방법을 모니터링 기능을 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="919c0-137">Integrate advanced app analytics and monitoring functionality from New Relic and AppInsights tooget even richer insight into how your Mobile app is performing.</span></span> <span data-ttu-id="919c0-138">와 *Azure 앱 서비스* 이제 프로그래밍 및 hello Azure 포털을 통해 다양 한 성능 메트릭 기반으로 경고를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="919c0-138">With *Azure App Service* you can now setup alerts based on variety of performance metrics, either programatically and via hello Azure Portal.</span></span>

## <a name="keep-your-assets-safe"></a><span data-ttu-id="919c0-139">자산을 안전하게 유지</span><span class="sxs-lookup"><span data-stu-id="919c0-139">Keep your assets safe</span></span>
<span data-ttu-id="919c0-140">백 엔드 및 데이터베이스를 자동으로 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="919c0-140">Automatically back up your backend and database.</span></span> <span data-ttu-id="919c0-141">코드와 데이터는 재해 로부터 안전 하 고 쉽게 복원 toorun 수 있도록 비즈니스 확신을가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="919c0-141">Your code and data is secure from disaster and easily restored, allowing you toorun your business with confidence.</span></span>

## <a name="ready-stage-go"></a><span data-ttu-id="919c0-142">준비, 스테이징, 실행</span><span class="sxs-lookup"><span data-stu-id="919c0-142">Ready, Stage, Go!</span></span>
<span data-ttu-id="919c0-143">*Azure 앱 서비스* 에서는 모바일 앱에 대한 비공개 테스트 및 스테이징 환경을 여러 개 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="919c0-143">With *Azure App Service* you can now create multiple private testing and staging environments for your mobile apps.</span></span> <span data-ttu-id="919c0-144">배포 하기 전에 테스트 tooperform을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="919c0-144">Use them tooperform testing before you deploy.</span></span> <span data-ttu-id="919c0-145">중단 시간 없이 tooproduction을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="919c0-145">Swap tooproduction with no downtime.</span></span> <span data-ttu-id="919c0-146">웹 응용 프로그램 미리 로드 되어 hello 최상의 환경을 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="919c0-146">Web apps are pre-loaded, ensuring hello best customer experience.</span></span>

<span data-ttu-id="919c0-147">이 *자습서* 에 따라 기존 모바일 서비스에 [앱 서비스](app-service-mobile-migrating-from-mobile-services.md)를 이용하기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="919c0-147">You can get start taking advantage of *App Service* for your existing Mobile Service by following this [tutorial](app-service-mobile-migrating-from-mobile-services.md).</span></span>
