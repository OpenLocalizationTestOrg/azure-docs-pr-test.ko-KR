---
title: "Azure App Service의 Mobile Apps 정보"
description: "App Service가 엔터프라이즈 모바일 앱에 제공하는 이점을 알아봅니다."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: 4e96cb9d-a632-4cf6-8219-0810d8ade3f9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-multiple
ms.devlang: na
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: ac35ff9fe1c5f315c4de08de951f505627ec412b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <span data-ttu-id="e8659-103"><a name="getting-started"> </a>Azure App Service의 Mobile Apps 정보</span><span class="sxs-lookup"><span data-stu-id="e8659-103"><a name="getting-started"> </a>About Mobile Apps in Azure App Service</span></span>
<span data-ttu-id="e8659-104">Azure App Service는 완전히 관리되는 PaaS([platform as a service](https://azure.microsoft.com/overview/what-is-paas/))로써 전문 개발자를 위해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-104">Azure App Service is a fully managed [platform as a service](https://azure.microsoft.com/overview/what-is-paas/) (PaaS) offering for professional developers.</span></span> <span data-ttu-id="e8659-105">이 서비스는 웹, 모바일 및 통합 시나리오에 풍부한 기능 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-105">The service brings a rich set of capabilities to web, mobile, and integration scenarios.</span></span> 

<span data-ttu-id="e8659-106">Azure App Service의 Mobile Apps 기능은 엔터프라이즈 개발자 및 시스템 통합자에게 확장성이 뛰어나고 전 세계에서 사용 가능한 모바일 응용 프로그램 개발 플랫폼을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-106">The Mobile Apps feature of Azure App Service gives enterprise developers and system integrators a mobile-application development platform that's highly scalable and globally available.</span></span>

![Mobile Apps 기능에 대한 시각적 개요](./media/app-service-mobile-value-prop/overview.png)

## <a name="why-mobile-apps"></a><span data-ttu-id="e8659-108">Mobile Apps 사용 이유</span><span class="sxs-lookup"><span data-stu-id="e8659-108">Why Mobile Apps?</span></span>
<span data-ttu-id="e8659-109">Mobile Apps 기능을 사용하면 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-109">With the Mobile Apps feature, you can:</span></span>

* <span data-ttu-id="e8659-110">**네이티브 앱 및 크로스 플랫폼 앱 빌드**: 빌드하는 앱이 네이티브 iOS, Android 및 Windows 앱인지 또는 크로스 플랫폼 Xamarin 앱이나 Cordova(PhoneGap) 앱인지에 관계없이 네이티브 SDK를 통해 App Service를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-110">**Build native and cross-platform apps**: Whether you're building native iOS, Android, and Windows apps or cross-platform Xamarin or Cordova (PhoneGap) apps, you can take advantage of App Service by using native SDKs.</span></span>
* <span data-ttu-id="e8659-111">**엔터프라이즈 시스템에 연결**: Mobile Apps 기능을 사용하면 몇 분 내에 회사 로그인을 추가하고 엔터프라이즈 온-프레미스 또는 클라우드 리소스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-111">**Connect to your enterprise systems**: With the Mobile Apps feature, you can add corporate sign-in in minutes, and connect to your enterprise on-premises or cloud resources.</span></span>
* <span data-ttu-id="e8659-112">**데이터 동기화를 사용하여 오프라인 지원 앱 빌드**: 오프라인에서 작동하는 앱을 빌드하여 모바일 작업자의 생산성을 높이고 엔터프라이즈 데이터 원본이나 SaaS(software as a service) API와 연결된 경우 Mobile Apps를 사용하여 백그라운드에서 데이터를 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-112">**Build offline-ready apps with data sync**: Make your mobile workforce more productive by building apps that work offline, and use Mobile Apps to sync data in the background when connectivity is present with any of your enterprise data sources or software as a service (SaaS) APIs.</span></span>
* <span data-ttu-id="e8659-113">**몇 초 내에 수백만 명에게 푸시 알림 전송**: 요구에 맞게 개인 설정되고 적절한 시간에 전송되는 인스턴트 푸시 알림을 모든 장치에서 지원하여 고객을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-113">**Push notifications to millions in seconds**: Engage your customers with instant push notifications on any device, personalized to their needs and sent when the time is right.</span></span>

## <a name="mobile-apps-features"></a><span data-ttu-id="e8659-114">Mobile Apps 기능</span><span class="sxs-lookup"><span data-stu-id="e8659-114">Mobile Apps features</span></span>
<span data-ttu-id="e8659-115">다음 기능은 클라우드 사용 모바일 개발에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-115">The following features are important to cloud-enabled mobile development:</span></span>

* <span data-ttu-id="e8659-116">**인증 및 권한 부여**: 엔터프라이즈 인증을 위한 Azure Active Directory 및 Facebook, Google, Twitter, Microsoft 계정과 같은 소셜 공급자를 포함하여 점점 증가하는 ID 공급자 목록에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-116">**Authentication and authorization**: Select from an ever-growing list of identity providers, including Azure Active Directory for enterprise authentication, plus social providers such as Facebook, Google, Twitter, and Microsoft accounts.</span></span> <span data-ttu-id="e8659-117">Mobile Apps은 각 공급자에 대해 OAuth 2.0 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-117">Mobile Apps offers an OAuth 2.0 service for each provider.</span></span> <span data-ttu-id="e8659-118">또한 공급자 특정 기능에 대한 ID 공급자의 SDK도 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-118">You can also integrate the SDK for the identity provider for provider-specific functionality.</span></span>

    <span data-ttu-id="e8659-119">[인증 기능]에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="e8659-119">Discover more about our [authentication features].</span></span>

* <span data-ttu-id="e8659-120">**데이터 액세스**: Mobile Apps는 Azure SQL Database 또는 온-프레미스 SQL Server에 연결된 모바일 친화적인 OData v3 데이터 원본을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-120">**Data access**: Mobile Apps provides a mobile-friendly OData v3 data source that's linked to Azure SQL Database or an on-premises SQL server.</span></span> <span data-ttu-id="e8659-121">이 서비스가 Entity Framework를 기반으로 할 수 있기 때문에 [Azure Table Storage], MongoDB, [Azure Cosmos DB] 및 SaaS API 공급자(예: Office 365 및 Salesforce.com)를 비롯한 다른 NoSQL 및 SQL 데이터 공급자와 쉽게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-121">Because this service can be based on Entity Framework, you can easily integrate with other NoSQL and SQL data providers, including [Azure Table storage], MongoDB, [Azure Cosmos DB], and SaaS API providers such as Office 365 and Salesforce.com.</span></span>

* <span data-ttu-id="e8659-122">**오프라인 동기화**: 클라이언트 SDK를 통해 오프라인 데이터 집합에서 작동하는 강력하고 응답성이 뛰어난 모바일 응용 프로그램을 쉽게 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-122">**Offline sync**: Our client SDKs make it easy to build robust and responsive mobile applications that operate with an offline dataset.</span></span> <span data-ttu-id="e8659-123">충돌 해결 지원을 비롯하여 백 엔드 데이터와 이 데이터 집합을 자동으로 동기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-123">You can sync this dataset automatically with the back-end data, including conflict-resolution support.</span></span>

  <span data-ttu-id="e8659-124">[데이터 기능]에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="e8659-124">Discover more about our [data features].</span></span>

* <span data-ttu-id="e8659-125">**푸시 알림**: 클라이언트 SDK는 Azure Notification Hubs의 등록 기능과 원활하게 통합되어 동시에 수백만 명의 사용자에게 푸시 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-125">**Push notifications**: Our client SDKs integrate seamlessly with the registration capabilities of Azure Notification Hubs, so you can send push notifications to millions of users simultaneously.</span></span>

  <span data-ttu-id="e8659-126">[푸시 알림 기능]에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="e8659-126">Discover more about our [push notification features].</span></span>

* <span data-ttu-id="e8659-127">**클라이언트 SDK**: 네이티브 개발([iOS], [Android] 및 [Windows]), 플랫폼 간 개발([Xamarin.iOS 및 Xamarin.Android], [Xamarin.Forms]) 및 하이브리드 응용 프로그램 개발([Apache Cordova])을 포함하는 전체 집합의 클라이언트 SDK를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-127">**Client SDKs**: We provide a complete set of client SDKs that cover native development ([iOS], [Android], and [Windows]), cross-platform development ([Xamarin.iOS and Xamarin.Android], [Xamarin.Forms]), and hybrid application development ([Apache Cordova]).</span></span> <span data-ttu-id="e8659-128">각 클라이언트 SDK는 MIT 라이선스로 사용할 수 있으며 오픈 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-128">Each client SDK is available with an MIT license and is open source.</span></span>

## <a name="azure-app-service-features"></a><span data-ttu-id="e8659-129">Azure App Service 기능</span><span class="sxs-lookup"><span data-stu-id="e8659-129">Azure App Service features</span></span>
<span data-ttu-id="e8659-130">다음 플랫폼 기능은 모바일 프로덕션 사이트에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-130">The following platform features are useful for mobile production sites:</span></span>

* <span data-ttu-id="e8659-131">**자동 크기 조정**: App Service를 사용하여 들어오는 고객 부하를 처리하기 위해 신속하게 확장하거나 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-131">**Autoscaling**: With App Service, you can quickly scale up or scale out to handle any incoming customer load.</span></span> <span data-ttu-id="e8659-132">VM 수와 크기를 수동으로 선택하거나 부하 또는 일정에 따라 모바일 앱 백 엔드의 크기를 조정하도록 자동 크기 조정을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-132">Manually select the number and size of VMs, or set up autoscaling to scale your mobile-app back end based on load or schedule.</span></span>

  <span data-ttu-id="e8659-133">[자동 크기 조정]에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="e8659-133">Discover more about [autoscaling].</span></span>

* <span data-ttu-id="e8659-134">**스테이징 환경**: App Service는 여러 버전의 사이트를 실행할 수 있으므로 A/B 테스트, 대규모 DevOps 계획의 일부로 프로덕션에서 테스트 및 새로운 백 엔드의 현재 위치 스테이징을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-134">**Staging environments**: App Service can run multiple versions of your site, so you can perform A/B testing, test in production as part of a larger DevOps plan, and do in-place staging of a new back end.</span></span>

  <span data-ttu-id="e8659-135">[스테이징 환경]에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="e8659-135">Discover more about [staging environments].</span></span>

* <span data-ttu-id="e8659-136">**지속적인 배포**: App Service는 일반 SCM(공급 체인 관리) 시스템과 통합할 수 있으므로 SCM 시스템의 분기에 푸시하여 새 버전의 백 엔드를 자동으로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-136">**Continuous deployment**: App Service can integrate with common supply chain management (SCM) systems, so you can automatically deploy a new version of your back end by pushing to a branch of your SCM system.</span></span>

  <span data-ttu-id="e8659-137">[배포 옵션]에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="e8659-137">Discover more about [deployment options].</span></span>

* <span data-ttu-id="e8659-138">**가상 네트워킹**: App Service는 가상 네트워크, Azure ExpressRoute 또는 하이브리드 연결을 사용하여 온-프레미스 리소스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-138">**Virtual networking**: App Service can connect to on-premises resources by using virtual network, Azure ExpressRoute, or hybrid connections.</span></span>

  <span data-ttu-id="e8659-139">[하이브리드 연결], [가상 네트워크] 및 [ExpressRoute]에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="e8659-139">Discover more about [hybrid connections], [virtual networks], and [ExpressRoute].</span></span>

* <span data-ttu-id="e8659-140">**격리 및 전용 환경**: 높은 확장성으로 Azure App Service 앱을 안전하게 실행하기 위해 완전히 격리된 전용 환경에서 App Service를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-140">**Isolated and dedicated environments**: You can run App Service in a fully isolated and dedicated environment for securely running Azure App Service apps at high scale.</span></span> <span data-ttu-id="e8659-141">이 환경은 높은 확장성, 격리 또는 보안된 네트워크 액세스가 요구되는 응용 프로그램 워크로드에 이상적입니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-141">This environment is ideal for application workloads that require high scale, isolation, or secure network access.</span></span>

  <span data-ttu-id="e8659-142">[App Service 환경]에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="e8659-142">Discover more about [App Service environments].</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8659-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e8659-143">Next steps</span></span>

<span data-ttu-id="e8659-144">Azure App Service에서 Mobile Apps를 시작하려면 [시작] 자습서를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-144">To get started with Mobile Apps in Azure App Service, complete the [getting started] tutorial.</span></span> <span data-ttu-id="e8659-145">자습서에서는 선택한 모바일 백 엔드과 클라이언트를 생성하는 기본 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-145">The tutorial covers the basics of producing a mobile back end and client of your choice.</span></span> <span data-ttu-id="e8659-146">인증 통합, 오프라인 동기화 및 푸시 알림에 대해서도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-146">It also covers integrating authentication, offline sync, and push notifications.</span></span> <span data-ttu-id="e8659-147">각 클라이언트 응용 프로그램에 한 번씩, 여러 번 이 자습서를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8659-147">You can complete the tutorial multiple times, once for each client application.</span></span>

<span data-ttu-id="e8659-148">Mobile Apps에 대한 자세한 내용은 [학습 맵]을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="e8659-148">For more information about Mobile Apps, review our [learning map].</span></span>
<span data-ttu-id="e8659-149">Azure App Service 플랫폼에 대한 자세한 내용은 [Azure App Service]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8659-149">For more information about the Azure App Service platform, see [Azure App Service].</span></span>

<!-- URLs. -->
[Migrate your mobile service to App Service]: app-service-mobile-migrating-from-mobile-services.md
[Azure App Service]: ../app-service/app-service-value-prop-what-is.md
[시작]: app-service-mobile-ios-get-started.md
[Azure Table Storage]:../cosmos-db/table-storage-how-to-use-dotnet.md
[Azure Cosmos DB]: ../cosmos-db/documentdb-get-started.md
[인증 기능]: ./app-service-mobile-auth.md
[데이터 기능]: ./app-service-mobile-offline-data-sync.md
[푸시 알림 기능]: ../notification-hubs/notification-hubs-push-notification-overview.md
[iOS]: ./app-service-mobile-ios-how-to-use-client-library.md
[Android]: ./app-service-mobile-android-how-to-use-client-library.md
[Windows]: ./app-service-mobile-dotnet-how-to-use-client-library.md
[Xamarin.iOS 및 Xamarin.Android]: ./app-service-mobile-dotnet-how-to-use-client-library.md
[Xamarin.Forms]: ./app-service-mobile-xamarin-forms-get-started.md
[Apache Cordova]: ./app-service-mobile-cordova-how-to-use-client-library.md
[자동 크기 조정]: ../app-service-web/web-sites-scale.md
[스테이징 환경]: ../app-service-web/web-sites-staged-publishing.md
[배포 옵션]: ../app-service-web/web-sites-deploy.md
[하이브리드 연결]: ../app-service-web/web-sites-hybrid-connection-get-started.md
[가상 네트워크]: ../app-service-web/web-sites-integrate-with-vnet.md
[ExpressRoute]: ../app-service-web/app-service-app-service-environment-network-configuration-expressroute.md
[App Service 환경]: ../app-service-web/app-service-app-service-environment-intro.md
[학습 맵]: https://azure.microsoft.com/en-us/documentation/learning-paths/appservice-mobileapps/
