---
title: "모바일 서비스를 사용하고 있습니다. 앱 서비스가 어떤 도움을 주나요?"
description: "앱 서비스가 기존 모바일 서비스 프로젝트에 제공하는 이점을 알아봅니다."
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
ms.openlocfilehash: 22397b6b448b418d5b54a457c3bafaf5c68ecc7b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <span data-ttu-id="26d7b-103"><a name="getting-started"> </a>모바일 서비스를 사용하고 있습니다. 앱 서비스가 어떤 도움을 주나요?</span><span class="sxs-lookup"><span data-stu-id="26d7b-103"><a name="getting-started"> </a>I use Mobile Services, how does App Service help?</span></span>
## <a name="overview"></a><span data-ttu-id="26d7b-104">개요</span><span class="sxs-lookup"><span data-stu-id="26d7b-104">Overview</span></span>
<span data-ttu-id="26d7b-105">기존 모바일 서비스는 안전하며 계속 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="26d7b-105">Your existing Mobile Service is safe and will remain supported.</span></span> <span data-ttu-id="26d7b-106">그러나 *Azure 앱 서비스* 플랫폼은 현재 모바일 서비스에서 사용할 수 없는 다음과 같은 많은 이점을 모바일 앱에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="26d7b-106">However there are number of advantages the *Azure App Service* platform provides for your mobile app that are not available today with Mobile Services:</span></span>

* <span data-ttu-id="26d7b-107">웹 클라이언트와 모바일 클라이언트를 둘 다 포함하는 앱을 위한 더 간단하고 쉽고 비용 효과적인 제품</span><span class="sxs-lookup"><span data-stu-id="26d7b-107">Simpler, easier and more cost effective offering for apps that include both web and mobile clients</span></span>
* <span data-ttu-id="26d7b-108">웹 작업, 사용자 지정 CName, 향상된 모니터링을 포함하는 새로운 호스트 기능</span><span class="sxs-lookup"><span data-stu-id="26d7b-108">New host features including Web Jobs, custom CNames, better monitoring</span></span>
* <span data-ttu-id="26d7b-109">트래픽 관리자와의 완성 인도 통합</span><span class="sxs-lookup"><span data-stu-id="26d7b-109">Turnkey integration with Traffic Manager</span></span>
* <span data-ttu-id="26d7b-110">하이브리드 연결뿐만 아니라 VNet을 사용하여 온-프레미스 리소스 및 VPN에 연결</span><span class="sxs-lookup"><span data-stu-id="26d7b-110">Connectivity to your on-premises resources and VPNs using VNet in addition to Hybrid Connections</span></span>
* <span data-ttu-id="26d7b-111">NewRelic 또는 AppInsights를 사용하여 앱에 대한 모니터링, 경고 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="26d7b-111">Monitoring, alerting and  troubleshooting for your app using NewRelic or AppInsights</span></span>
* <span data-ttu-id="26d7b-112">보다 풍부한 기본 계산 리소스 및 가격 책정</span><span class="sxs-lookup"><span data-stu-id="26d7b-112">Richer spectrum of the underlying compute resources and pricing</span></span>
* <span data-ttu-id="26d7b-113">기본 제공되는 자동 크기 조정, 부하 분산 및 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="26d7b-113">Built-in auto scale, load balancing, and performance monitoring.</span></span>
* <span data-ttu-id="26d7b-114">기본 제공되는 스테이징, 백업, 롤백 및 프로덕션에서 테스트 기능</span><span class="sxs-lookup"><span data-stu-id="26d7b-114">Built-in staging, backup, roll-back, and testing-in-production capabilities</span></span>

## <a name="new-hosting-features"></a><span data-ttu-id="26d7b-115">새로운 호스팅 기능</span><span class="sxs-lookup"><span data-stu-id="26d7b-115">New hosting features</span></span>
<span data-ttu-id="26d7b-116">*Azure App Service*에서 *Mobile App* 백 엔드 코드는 Web App 및 API App과 동일한 컨테이너에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="26d7b-116">In *Azure App Service* the *Mobile App* backend code runs in the same container as Web App and API App.</span></span> <span data-ttu-id="26d7b-117">따라서 현재 모바일 서비스에 없는 다음 일부 기능을 포함하여 이 컨테이너의 모든 기능을 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26d7b-117">As such you can take advantage of all the features in this container, including some of those that are not currently present in Mobile Services:</span></span>

* <span data-ttu-id="26d7b-118">웹 작업을 통해 연속 실행되는 백 엔드 논리 추가</span><span class="sxs-lookup"><span data-stu-id="26d7b-118">Add continuously running backend logic via Web Jobs</span></span>
* <span data-ttu-id="26d7b-119">백 엔드 코드가 항상 실행되도록 유지</span><span class="sxs-lookup"><span data-stu-id="26d7b-119">Ensure your backend code is always running</span></span>
* <span data-ttu-id="26d7b-120">사용자 지정 CName을 사용하여 모바일 백 엔드 끝점에 친숙하고 안정적인 이름 제공</span><span class="sxs-lookup"><span data-stu-id="26d7b-120">Use custom CNames to provide friendly and stable names to your mobile backend endpoints</span></span>
* <span data-ttu-id="26d7b-121">트래픽 관리자를 사용하여 앱 지역 크기 조정</span><span class="sxs-lookup"><span data-stu-id="26d7b-121">Geo-scale your app with Traffic Manager</span></span>
* <span data-ttu-id="26d7b-122">원하는 모든 라이브러리 및 패키지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="26d7b-122">Include any libraries and packages you want.</span></span>
* <span data-ttu-id="26d7b-123">(.NET에 대해) MVC를 포함한 ASP.NET의 기능 활용</span><span class="sxs-lookup"><span data-stu-id="26d7b-123">(For .NET) Leverage any feature of ASP.NET, including MVC</span></span>
* <span data-ttu-id="26d7b-124">(Node.js에 대해) 일반적인 MVC 라이브러리를 포함하여 노드 에코 시스템의 순수 JavaScript 라이브러리를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="26d7b-124">(For Node.js) Leverage any pure JavaScript library of the Node ecosystem, including common MVC libraries.</span></span>

## <a name="access-on-premises-data-using-vnet"></a><span data-ttu-id="26d7b-125">VNet을 사용하여 온-프레미스 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="26d7b-125">Access on-premises data using VNet</span></span>
<span data-ttu-id="26d7b-126">현재 Mobile Services를 사용하면 이미 하이브리드 연결을 사용하여 온-프레미스 리소스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26d7b-126">With Mobile Services today you can already use Hybrid Connections to access on-premises resources.</span></span> <span data-ttu-id="26d7b-127">그러나 VPN 솔루션이 선호되는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26d7b-127">However there are situations where a VPN solution is preferred.</span></span> <span data-ttu-id="26d7b-128">*Azure 앱 서비스* 에서는 Azure VNet을 모바일 앱 백 엔드 코드에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26d7b-128">With *Azure App Service* you can use Azure VNet for your Mobile App backend code.</span></span>

## <a name="use-your-favorite-backend-language"></a><span data-ttu-id="26d7b-129">좋아하는 백 엔드 언어 사용</span><span class="sxs-lookup"><span data-stu-id="26d7b-129">Use your favorite backend language</span></span>
<span data-ttu-id="26d7b-130">*Azure 앱 서비스* 는 최신 런타임에 대한 액세스를 포함하여 ASP.NET 및 Node.js 플랫폼에 대한 광범위하고 풍부한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="26d7b-130">*Azure App Service* offers broader and richer support for ASP.NET and Node.js platforms, including access to the latest runtimes.</span></span>

## <a name="set-up-automatic-scale"></a><span data-ttu-id="26d7b-131">자동 크기 조정 설정</span><span class="sxs-lookup"><span data-stu-id="26d7b-131">Set up automatic scale</span></span>
<span data-ttu-id="26d7b-132">모바일 서비스에서는 백 엔드 코드의 모든 인스턴스가 작은 VM에서 실행되었습니다.</span><span class="sxs-lookup"><span data-stu-id="26d7b-132">With Mobile Services, all instances of your backend code were running on Small VMs.</span></span> <span data-ttu-id="26d7b-133">*Azure 앱 서비스* 를 사용하면 훨씬 다양한 옵션 집합에서 VM의 크기를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26d7b-133">*Azure App Service* enables you to select the size of the VMs from a much richer set of options.</span></span> <span data-ttu-id="26d7b-134">다양한 성능 메트릭에 따라 들어오는 고객 부하에 맞게 크기를 신속하게 확장하거나 축소할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26d7b-134">You can also  quickly scale up or out to handle any incoming customer load, based on various performance metrics.</span></span>

## <a name="be-in-the-know"></a><span data-ttu-id="26d7b-135">풍부한 정보 제공</span><span class="sxs-lookup"><span data-stu-id="26d7b-135">Be in the “know”</span></span>
<span data-ttu-id="26d7b-136">모니터링 및 사용자와 팀에 자동으로 알리는 경고를 사용하여 실시간으로 문제에 대응합니다.</span><span class="sxs-lookup"><span data-stu-id="26d7b-136">React to issues in real-time with monitoring and alerts to automatically notify you and your team.</span></span> <span data-ttu-id="26d7b-137">New Relic과 AppInsights의 고급 앱 분석 및 모니터링 기능을 통합하여 모바일 앱의 성능을 보다 완전하게 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="26d7b-137">Integrate advanced app analytics and monitoring functionality from New Relic and AppInsights to get even richer insight into how your Mobile app is performing.</span></span> <span data-ttu-id="26d7b-138">*Azure 앱 서비스* 에서는 프로그래밍 방식으로 또는 Azure 포털을 통해 다양한 성능 메트릭에 기반하여 경고를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26d7b-138">With *Azure App Service* you can now setup alerts based on variety of performance metrics, either programatically and via the Azure Portal.</span></span>

## <a name="keep-your-assets-safe"></a><span data-ttu-id="26d7b-139">자산을 안전하게 유지</span><span class="sxs-lookup"><span data-stu-id="26d7b-139">Keep your assets safe</span></span>
<span data-ttu-id="26d7b-140">백 엔드 및 데이터베이스를 자동으로 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="26d7b-140">Automatically back up your backend and database.</span></span> <span data-ttu-id="26d7b-141">코드와 데이터가 재해로부터 보호되고 쉽게 복원되므로 안심하고 비즈니스를 운영할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26d7b-141">Your code and data is secure from disaster and easily restored, allowing you to run your business with confidence.</span></span>

## <a name="ready-stage-go"></a><span data-ttu-id="26d7b-142">준비, 스테이징, 실행</span><span class="sxs-lookup"><span data-stu-id="26d7b-142">Ready, Stage, Go!</span></span>
<span data-ttu-id="26d7b-143">*Azure 앱 서비스* 에서는 모바일 앱에 대한 비공개 테스트 및 스테이징 환경을 여러 개 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26d7b-143">With *Azure App Service* you can now create multiple private testing and staging environments for your mobile apps.</span></span> <span data-ttu-id="26d7b-144">배포 전에 이러한 환경을 사용하여 테스트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="26d7b-144">Use them to perform testing before you deploy.</span></span> <span data-ttu-id="26d7b-145">가동 중지 시간 없이 프로덕션으로 교환합니다.</span><span class="sxs-lookup"><span data-stu-id="26d7b-145">Swap to production with no downtime.</span></span> <span data-ttu-id="26d7b-146">웹앱이 미리 로드되어 최상의 고객 경험을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="26d7b-146">Web apps are pre-loaded, ensuring the best customer experience.</span></span>

<span data-ttu-id="26d7b-147">이 *자습서* 에 따라 기존 모바일 서비스에 [앱 서비스](app-service-mobile-migrating-from-mobile-services.md)를 이용하기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26d7b-147">You can get start taking advantage of *App Service* for your existing Mobile Service by following this [tutorial](app-service-mobile-migrating-from-mobile-services.md).</span></span>
