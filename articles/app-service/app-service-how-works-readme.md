---
title: "Azure App Service 작동 방법"
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
ms.openlocfilehash: 2d830963d3d2adba71a6ca99f79eac0fc8cbfb12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-app-service-works"></a><span data-ttu-id="924ce-104">App Service 작동 방법</span><span class="sxs-lookup"><span data-stu-id="924ce-104">How App Service works</span></span>
<span data-ttu-id="924ce-105">Azure App Service는 오늘날 엔지니어가 직면한 실제 문제를 해결하기 위해 설계된 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="924ce-105">Azure App Service is a cloud service that's designed to solve the practical problems that engineers face today.</span></span>
<span data-ttu-id="924ce-106">App Service는 응용 프로그램을 클라우드 규모로 전달해야 하는 요구를 존중하면서 우수한 개발자 생산성을 제공하는 데 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="924ce-106">App Service focuses on providing superior developer productivity without compromising on the need to deliver applications at cloud scale.</span></span> 

<span data-ttu-id="924ce-107">App Service에는 엔터프라이즈 기간 업무 응용 프로그램을 만드는 데 필요한 프레임워크 및 기능도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="924ce-107">App Service also provides the features and frameworks that are necessary for creating enterprise line-of-business applications.</span></span> <span data-ttu-id="924ce-108">App Service를 사용하면 Java, PHP, Node.js, Python 및 Microsoft .NET 언어를 비롯한 가장 인기 있는 개발 언어로 앱을 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="924ce-108">App Service lets you develop apps in most popular development languages, including Java, PHP, Node.js, Python, and the Microsoft .NET languages.</span></span> <span data-ttu-id="924ce-109">App Service를 통해 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="924ce-109">With App Service, you can:</span></span>

* <span data-ttu-id="924ce-110">확장성이 뛰어난 웹앱을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="924ce-110">Build highly scalable web apps.</span></span>
* <span data-ttu-id="924ce-111">Mobile Apps 백 엔드를 데이터 백 엔드, 사용자 인증 및 푸시 알림과 같은 사용하기 쉬운 모바일 기능 집합으로 신속하게 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="924ce-111">Quickly build Mobile Apps back ends with a set of easy-to-use mobile capabilities such as data back ends, user authentication, and push notifications.</span></span>
* <span data-ttu-id="924ce-112">API Apps을 사용하여 API를 게시, 구현 및 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="924ce-112">Implement, deploy, and publish APIs with API Apps.</span></span>
* <span data-ttu-id="924ce-113">비즈니스 응용 프로그램을 워크플로에 서로 연결하고 논리 앱을 사용하여 데이터를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="924ce-113">Tie business applications together into workflows and transform data with Logic Apps.</span></span>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

<span data-ttu-id="924ce-114">모든 앱 형식은 개발자가 앱 설계에서 앱 유지 관리까지의 전체 수명 주기 환경을 최적화하는 확장성과 유연성이 있는 Web Apps 플랫폼을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="924ce-114">All app types rely on the scalable and flexible Web Apps platform, which enables developers to have an optimized full lifecycle experience from app design to app maintenance.</span></span> <span data-ttu-id="924ce-115">수명 주기 기능은 다음을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="924ce-115">The lifecycle capabilities enable the following:</span></span>

* <span data-ttu-id="924ce-116">**빠른 앱 만들기**.</span><span class="sxs-lookup"><span data-stu-id="924ce-116">**Quick app creation**.</span></span> <span data-ttu-id="924ce-117">처음부터 시작하거나 Azure Marketplace에서 OSS(운영 지원 시스템) 패키지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="924ce-117">Start from scratch or pick an operational support system (OSS) package from the Azure Marketplace.</span></span>
* <span data-ttu-id="924ce-118">**연속 배포**.</span><span class="sxs-lookup"><span data-stu-id="924ce-118">**Continuous deployment**.</span></span> <span data-ttu-id="924ce-119">OneDrive 및 DropBox와 같은 온라인 저장소 서비스의 동기화 콘텐츠 및 TFS, GitHub, BitBucket처럼 인기 있는 원본 제어 솔루션에서 자동으로 새 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="924ce-119">Automatically deploy new code from popular source control solutions such as TFS, GitHub, and Bitbucket, and sync content from online storage services such as OneDrive and Dropbox.</span></span>
* <span data-ttu-id="924ce-120">**프로덕션에서 테스트**.</span><span class="sxs-lookup"><span data-stu-id="924ce-120">**Test in production**.</span></span> <span data-ttu-id="924ce-121">원활하게 사전 프로덕션 환경을 만들고 이 환경으로 이동하는 트래픽의 양을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="924ce-121">Smoothly create pre-production environments and manage the amount of traffic that's going to them.</span></span> <span data-ttu-id="924ce-122">필요할 때 클라우드에서 디버깅하고 문제가 발견되면 롤백합니다.</span><span class="sxs-lookup"><span data-stu-id="924ce-122">Debug in the cloud when needed, and roll back when issues are found.</span></span>
* <span data-ttu-id="924ce-123">**비동기 작업 및 배치 작업 실행**.</span><span class="sxs-lookup"><span data-stu-id="924ce-123">**Running asynchronous tasks and batch jobs**.</span></span> <span data-ttu-id="924ce-124">백그라운드 프로세스에서 코드를 실행하거나 이벤트(예: Azure Storage 큐에 메시지 도착) 및 예약된 시간(CRON)에 따라 코드를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="924ce-124">Run code in a background process or activate your code based on events (such as messages landing in an Azure Storage queue) and scheduled times (CRON).</span></span>
* <span data-ttu-id="924ce-125">**앱 크기 조정**.</span><span class="sxs-lookup"><span data-stu-id="924ce-125">**Scaling the app**.</span></span> <span data-ttu-id="924ce-126">트래픽 및 리소스 사용률에 따라 가로 및 세로 방향으로 자동으로 서비스를 확장하기 위해 여러 옵션 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="924ce-126">Use one of many options to automatically scale your service horizontally and vertically based on traffic and resource utilization.</span></span> <span data-ttu-id="924ce-127">앱 전용인 개인 환경을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="924ce-127">Configure private environments that are dedicated to your apps.</span></span>   
* <span data-ttu-id="924ce-128">**앱 유지 관리**.</span><span class="sxs-lookup"><span data-stu-id="924ce-128">**Maintaining the app**.</span></span> <span data-ttu-id="924ce-129">다양한 디버깅 및 진단 기능을 활용하여 효율적으로 문제를 미리 알아차리고 실시간 해결하거나(자동 복구 및 라이브 디버깅 기능 사용) 로그 및 메모리 덤프를 분석하여 사실을 확인한 후 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="924ce-129">Use many of the debugging and diagnostics features to stay ahead of problems and to efficiently resolve them either in real time (with features such as auto-healing and live debugging) or after the fact by analyzing logs and memory dumps.</span></span>

<span data-ttu-id="924ce-130">전체적으로 App Service 기능을 통해 개발자는 코드 작성에 집중할 수 있으므로 안정적이고 확장성이 뛰어난 프로덕션 상태를 신속하게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="924ce-130">As a whole, App Service capabilities enable developers to focus on their code and quickly reach a stable and highly scalable production state.</span></span> <span data-ttu-id="924ce-131">API Apps 및 Logic Apps 기능을 사용하면 개발자는 온-프레미스에서 클라우드 통합 및 비즈니스 솔루션 간에 존재하는 장벽을 연결하는 실제 엔터프라이즈 응용 프로그램을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="924ce-131">With the API Apps and Logic Apps features, developers can build real-world enterprise applications that bridge barriers between business solutions and on-premises to cloud integration.</span></span> 

## <a name="videos"></a><span data-ttu-id="924ce-132">비디오</span><span class="sxs-lookup"><span data-stu-id="924ce-132">Videos</span></span>
* [<span data-ttu-id="924ce-133">Azure 앱 서비스 아키텍처</span><span class="sxs-lookup"><span data-stu-id="924ce-133">Azure App Service Architecture</span></span>](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)

## <a name="next-steps"></a><span data-ttu-id="924ce-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="924ce-134">Next steps</span></span>

<span data-ttu-id="924ce-135">App Service에 대한 자세한 내용은 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="924ce-135">Learn more about App Service in one of the following topics:</span></span>

* [<span data-ttu-id="924ce-136">Azure 앱 서비스 정의</span><span class="sxs-lookup"><span data-stu-id="924ce-136">What is Azure App Service?</span></span>](app-service-value-prop-what-is.md)
  * [<span data-ttu-id="924ce-137">웹앱</span><span class="sxs-lookup"><span data-stu-id="924ce-137">Web App</span></span>](../app-service-web/app-service-web-overview.md)
  * [<span data-ttu-id="924ce-138">모바일 앱</span><span class="sxs-lookup"><span data-stu-id="924ce-138">Mobile App</span></span>](../app-service-mobile/app-service-mobile-value-prop.md)
  * [<span data-ttu-id="924ce-139">API 앱</span><span class="sxs-lookup"><span data-stu-id="924ce-139">API App</span></span>](../app-service-api/app-service-api-apps-why-best-platform.md)
* [<span data-ttu-id="924ce-140">Azure 앱 서비스 아키텍처(프레젠테이션)</span><span class="sxs-lookup"><span data-stu-id="924ce-140">Azure App Service Architecture (presentation)</span></span>](http://www.slideshare.net/maartenba/windows-azure-web-sites-things-they-dont-teach-kids-in-school-comunity-day-2013)
* [<span data-ttu-id="924ce-141">Azure 앱 서비스, 클라우드 서비스 및 가상 컴퓨터 비교</span><span class="sxs-lookup"><span data-stu-id="924ce-141">Azure App Service, Cloud Services, and Virtual Machines comparison</span></span>](../app-service-web/choose-web-site-cloud-service-vm.md)
* [<span data-ttu-id="924ce-142">앱 서비스 계획 이해</span><span class="sxs-lookup"><span data-stu-id="924ce-142">Understanding App Service Plans</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
* [<span data-ttu-id="924ce-143">앱 서비스 환경 소개</span><span class="sxs-lookup"><span data-stu-id="924ce-143">Introduction to App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
  * [<span data-ttu-id="924ce-144">연습: 앱 서비스 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="924ce-144">Exercise: Create an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="924ce-145">Azure 앱 서비스 개발 스택 지원</span><span class="sxs-lookup"><span data-stu-id="924ce-145">Azure App Service Development Stacks Support</span></span>](https://azure.microsoft.com/blog/windows-azure-websites-development-stacks-support/)



