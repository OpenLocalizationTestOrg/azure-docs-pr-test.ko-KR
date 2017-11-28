---
title: "Azure 앱 서비스의 작동 aaaHow"
description: "앱 서비스 작동 방법 알아보기"
keywords: "앱 서비스, Azure 앱 서비스, 규모, 확장성, 앱 서비스 계획, 앱 서비스 비용"
services: app-service
documentationcenter: 
author: yochay
manager: erikre
editor: 
ms.assetid: ae74fc32-969e-4580-8d61-02c922f1f184
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/23/2017
ms.author: yochayk
ms.openlocfilehash: b20733ec8844773d063e2b6918605c4a48db1f5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-app-service-works"></a><span data-ttu-id="cc2f6-104">App Service 작동 방법</span><span class="sxs-lookup"><span data-stu-id="cc2f6-104">How App Service works</span></span>
<span data-ttu-id="cc2f6-105">Azure 앱 서비스는 엔지니어 오늘날 직면 하는 디자인 된 toosolve hello 실제 문제를 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-105">Azure App Service is a cloud service that's designed toosolve hello practical problems that engineers face today.</span></span>
<span data-ttu-id="cc2f6-106">앱 서비스 중점적으로 hello 훼손 하지 않고 상위 개발자의 생산성을 제공 하는 클라우드 범위에서 toodeliver 응용 프로그램이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-106">App Service focuses on providing superior developer productivity without compromising on hello need toodeliver applications at cloud scale.</span></span> 

<span data-ttu-id="cc2f6-107">앱 서비스는 hello 기능 및 엔터프라이즈 기간 업무 응용 프로그램을 만드는 데 필요한 프레임 워크 또한 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-107">App Service also provides hello features and frameworks that are necessary for creating enterprise line-of-business applications.</span></span> <span data-ttu-id="cc2f6-108">앱 서비스를 사용 하면 가장 인기 있는 개발 언어에서는 Java, PHP, Node.js, Python 및 hello Microsoft.NET 언어를 포함 하 여 앱을 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-108">App Service lets you develop apps in most popular development languages, including Java, PHP, Node.js, Python, and hello Microsoft .NET languages.</span></span> <span data-ttu-id="cc2f6-109">App Service를 통해 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-109">With App Service, you can:</span></span>

* <span data-ttu-id="cc2f6-110">확장성이 뛰어난 웹앱을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-110">Build highly scalable web apps.</span></span>
* <span data-ttu-id="cc2f6-111">Mobile Apps 백 엔드를 데이터 백 엔드, 사용자 인증 및 푸시 알림과 같은 사용하기 쉬운 모바일 기능 집합으로 신속하게 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-111">Quickly build Mobile Apps back ends with a set of easy-to-use mobile capabilities such as data back ends, user authentication, and push notifications.</span></span>
* <span data-ttu-id="cc2f6-112">API Apps을 사용하여 API를 게시, 구현 및 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-112">Implement, deploy, and publish APIs with API Apps.</span></span>
* <span data-ttu-id="cc2f6-113">비즈니스 응용 프로그램을 워크플로에 서로 연결하고 논리 앱을 사용하여 데이터를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-113">Tie business applications together into workflows and transform data with Logic Apps.</span></span>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

<span data-ttu-id="cc2f6-114">Hello 확장 가능 하며 유연한 웹 응용 프로그램 플랫폼에 최적화 된 전체 수명 주기는 응용 프로그램 디자인 tooapp 유지 관리에서의 경험이 개발자 toohave 수 있는 모든 응용 프로그램 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-114">All app types rely on hello scalable and flexible Web Apps platform, which enables developers toohave an optimized full lifecycle experience from app design tooapp maintenance.</span></span> <span data-ttu-id="cc2f6-115">hello 수명 주기 기능 hello 다음 사용:</span><span class="sxs-lookup"><span data-stu-id="cc2f6-115">hello lifecycle capabilities enable hello following:</span></span>

* <span data-ttu-id="cc2f6-116">**빠른 앱 만들기**.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-116">**Quick app creation**.</span></span> <span data-ttu-id="cc2f6-117">처음부터 시작 하 하거나 hello Azure Marketplace에서에서 프로그램 operational 지원 시스템 (OS) 패키지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-117">Start from scratch or pick an operational support system (OSS) package from hello Azure Marketplace.</span></span>
* <span data-ttu-id="cc2f6-118">**연속 배포**.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-118">**Continuous deployment**.</span></span> <span data-ttu-id="cc2f6-119">OneDrive 및 DropBox와 같은 온라인 저장소 서비스의 동기화 콘텐츠 및 TFS, GitHub, BitBucket처럼 인기 있는 원본 제어 솔루션에서 자동으로 새 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-119">Automatically deploy new code from popular source control solutions such as TFS, GitHub, and Bitbucket, and sync content from online storage services such as OneDrive and Dropbox.</span></span>
* <span data-ttu-id="cc2f6-120">**프로덕션에서 테스트**.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-120">**Test in production**.</span></span> <span data-ttu-id="cc2f6-121">프리 프로덕션 환경은 만들고 hello toothem 일어나는 트래픽 양을 관리 원활 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-121">Smoothly create pre-production environments and manage hello amount of traffic that's going toothem.</span></span> <span data-ttu-id="cc2f6-122">필요한 경우 hello 클라우드에서 디버그 하 고 문제가 발견 되 면에 다시 롤포워드할 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-122">Debug in hello cloud when needed, and roll back when issues are found.</span></span>
* <span data-ttu-id="cc2f6-123">**비동기 작업 및 배치 작업 실행**.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-123">**Running asynchronous tasks and batch jobs**.</span></span> <span data-ttu-id="cc2f6-124">백그라운드 프로세스에서 코드를 실행하거나 이벤트(예: Azure Storage 큐에 메시지 도착) 및 예약된 시간(CRON)에 따라 코드를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-124">Run code in a background process or activate your code based on events (such as messages landing in an Azure Storage queue) and scheduled times (CRON).</span></span>
* <span data-ttu-id="cc2f6-125">**크기 조정 hello 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-125">**Scaling hello app**.</span></span> <span data-ttu-id="cc2f6-126">트래픽 및 리소스 사용률에 기반 하는 가로 및 세로로 여러 서비스를 확장할 많은 옵션 tooautomatically 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-126">Use one of many options tooautomatically scale your service horizontally and vertically based on traffic and resource utilization.</span></span> <span data-ttu-id="cc2f6-127">전용된 tooyour 앱이 개인 환경을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-127">Configure private environments that are dedicated tooyour apps.</span></span>   
* <span data-ttu-id="cc2f6-128">**유지 관리 hello 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-128">**Maintaining hello app**.</span></span> <span data-ttu-id="cc2f6-129">많은 hello 디버깅을 사용 하 고 문제 및 tooefficiently 미리 진단 기능 toostay 실시간 (으로 자동 복구 및 라이브 디버깅 하는 등의 기능)에서 해결 하거나 로그 및 메모리를 분석 하 여 hello 팩트 후 덤프 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-129">Use many of hello debugging and diagnostics features toostay ahead of problems and tooefficiently resolve them either in real time (with features such as auto-healing and live debugging) or after hello fact by analyzing logs and memory dumps.</span></span>

<span data-ttu-id="cc2f6-130">전체적으로 신속 하 게 안정적이 고 확장성이 높은 프로덕션 상태가 될 때까지 및 응용 프로그램 서비스 기능 코드에 대 한 개발자 toofocus를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-130">As a whole, App Service capabilities enable developers toofocus on their code and quickly reach a stable and highly scalable production state.</span></span> <span data-ttu-id="cc2f6-131">API 앱 hello 및 논리 앱 기능을 사용 개발자는 비즈니스 솔루션 및 온-프레미스 toocloud 통합 간의 장벽을 브리지 하는 실제 엔터프라이즈 응용 프로그램을 구축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc2f6-131">With hello API Apps and Logic Apps features, developers can build real-world enterprise applications that bridge barriers between business solutions and on-premises toocloud integration.</span></span> 

## <a name="videos"></a><span data-ttu-id="cc2f6-132">비디오</span><span class="sxs-lookup"><span data-stu-id="cc2f6-132">Videos</span></span>
* [<span data-ttu-id="cc2f6-133">Azure 앱 서비스 아키텍처</span><span class="sxs-lookup"><span data-stu-id="cc2f6-133">Azure App Service Architecture</span></span>](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)

## <a name="next-steps"></a><span data-ttu-id="cc2f6-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cc2f6-134">Next steps</span></span>

<span data-ttu-id="cc2f6-135">Hello 다음 항목 중 하나에서 응용 프로그램 서비스에 대 한 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="cc2f6-135">Learn more about App Service in one of hello following topics:</span></span>

* [<span data-ttu-id="cc2f6-136">Azure 앱 서비스 정의</span><span class="sxs-lookup"><span data-stu-id="cc2f6-136">What is Azure App Service?</span></span>](app-service-value-prop-what-is.md)
  * [<span data-ttu-id="cc2f6-137">웹앱</span><span class="sxs-lookup"><span data-stu-id="cc2f6-137">Web App</span></span>](../app-service-web/app-service-web-overview.md)
  * [<span data-ttu-id="cc2f6-138">모바일 앱</span><span class="sxs-lookup"><span data-stu-id="cc2f6-138">Mobile App</span></span>](../app-service-mobile/app-service-mobile-value-prop.md)
  * [<span data-ttu-id="cc2f6-139">API 앱</span><span class="sxs-lookup"><span data-stu-id="cc2f6-139">API App</span></span>](../app-service-api/app-service-api-apps-why-best-platform.md)
* [<span data-ttu-id="cc2f6-140">Azure 앱 서비스 아키텍처(프레젠테이션)</span><span class="sxs-lookup"><span data-stu-id="cc2f6-140">Azure App Service Architecture (presentation)</span></span>](http://www.slideshare.net/maartenba/windows-azure-web-sites-things-they-dont-teach-kids-in-school-comunity-day-2013)
* [<span data-ttu-id="cc2f6-141">Azure 앱 서비스, 클라우드 서비스 및 가상 컴퓨터 비교</span><span class="sxs-lookup"><span data-stu-id="cc2f6-141">Azure App Service, Cloud Services, and Virtual Machines comparison</span></span>](../app-service-web/choose-web-site-cloud-service-vm.md)
* [<span data-ttu-id="cc2f6-142">앱 서비스 계획 이해</span><span class="sxs-lookup"><span data-stu-id="cc2f6-142">Understanding App Service Plans</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
* [<span data-ttu-id="cc2f6-143">소개 tooApp 서비스 환경</span><span class="sxs-lookup"><span data-stu-id="cc2f6-143">Introduction tooApp Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
  * [<span data-ttu-id="cc2f6-144">연습: 앱 서비스 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="cc2f6-144">Exercise: Create an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="cc2f6-145">Azure 앱 서비스 개발 스택 지원</span><span class="sxs-lookup"><span data-stu-id="cc2f6-145">Azure App Service Development Stacks Support</span></span>](https://azure.microsoft.com/blog/windows-azure-websites-development-stacks-support/)



