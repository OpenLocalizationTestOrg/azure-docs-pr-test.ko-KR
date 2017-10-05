---
title: "Web Apps 개요 | Microsoft Docs"
description: "Azure 앱 서비스로 웹 응용 프로그램을 개발 및 호스팅하는 방법에 대해 알아보세요."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 94af2caf-a2ec-4415-a097-f60694b860b3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 01/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3db15e9dcdd510481f4982198da5ac950f2c7e4f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="web-apps-overview"></a><span data-ttu-id="76620-103">웹앱 개요</span><span class="sxs-lookup"><span data-stu-id="76620-103">Web Apps overview</span></span>
<span data-ttu-id="76620-104">*앱 서비스 웹앱* 은 웹 사이트와 웹 응용 프로그램 호스팅을 위해 최적화된 완전히 관리되는 계산 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="76620-104">*App Service Web Apps* is a fully managed compute platform that is optimized for hosting websites and web applications.</span></span> <span data-ttu-id="76620-105">Azure가 앱의 실행 및 크기 조정을 위해 인프라를 관리하는 동안 Microsoft Azure의 이 PaaS [(Platform-as-a-Service)](https://en.wikipedia.org/wiki/Platform_as_a_service) 를 통해 비즈니스 논리에 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76620-105">This [platform-as-a-service](https://en.wikipedia.org/wiki/Platform_as_a_service) (PaaS) offering of Microsoft Azure lets you focus on your business logic while Azure takes care of the infrastructure to run and scale your apps.</span></span>

<span data-ttu-id="76620-106">다음 5분 비디오에서는 Azure 앱 서비스 웹앱을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="76620-106">The following 5-minute video introduces Azure App Service Web Apps.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Web-Apps-with-Yochay-Kiriaty/player]
>
>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

## <a name="what-is-a-web-app-in-app-service"></a><span data-ttu-id="76620-107">앱 서비스에서 웹앱은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="76620-107">What is a web app in App Service?</span></span>
<span data-ttu-id="76620-108">앱 서비스에서 *웹앱* 은 Azure에서 웹 사이트 또는 웹 응용 프로그램을 호스팅하기 위해 제공하는 계산 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="76620-108">In App Service, a *web app* is the compute resources that Azure provides for hosting a website or web application.</span></span>  

<span data-ttu-id="76620-109">계산 리소스는 선택한 가격 책정 계층에 따라 공유 또는 전용 가상 컴퓨터(VM)일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76620-109">The compute resources may be on shared or dedicated virtual machines (VMs), depending on the pricing tier that you choose.</span></span> <span data-ttu-id="76620-110">응용 프로그램 코드는 다른 고객과 격리되는 관리되는 VM에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="76620-110">Your application code runs in a managed VM that is isolated from other customers.</span></span>

<span data-ttu-id="76620-111">사용자 코드는 [Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md)(ASP.NET, Node.js, Java, PHP, Python)에서 지원되는 모든 언어 또는 프레임워크일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76620-111">Your code can be in any language or framework that is supported by [Azure App Service](../app-service/app-service-value-prop-what-is.md), such as ASP.NET, Node.js, Java, PHP, or Python.</span></span> <span data-ttu-id="76620-112">웹앱에서 [PowerShell 및 기타 스크립트 언어](web-sites-create-web-jobs.md#acceptablefiles) 를 사용하는 스크립트를 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76620-112">You can also run scripts that use [PowerShell and other scripting languages](web-sites-create-web-jobs.md#acceptablefiles) in a web app.</span></span>

<span data-ttu-id="76620-113">Web Apps을 사용할 수 있는 일반적인 응용 프로그램 시나리오의 예는 [Azure App Service, Virtual Machines, Service Fabric 및 클라우드 서비스 비교](choose-web-site-cloud-service-vm.md#scenarios)의 [웹앱 시나리오](https://azure.microsoft.com/documentation/scenarios/web-app/) 및 **시나리오 및 권장 사항** 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76620-113">For examples of typical application scenarios that you can use Web Apps for, see [Web app scenarios](https://azure.microsoft.com/documentation/scenarios/web-app/) and the **Scenarios and recommendations** section of [Azure App Service, Virtual Machines, Service Fabric, and Cloud Services comparison](choose-web-site-cloud-service-vm.md#scenarios).</span></span>

## <a name="why-use-web-apps"></a><span data-ttu-id="76620-114">웹앱을 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="76620-114">Why use Web Apps?</span></span>
<span data-ttu-id="76620-115">웹앱에 적용하는 앱 서비스의 주요 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="76620-115">Here are some key features of App Service that apply to Web Apps:</span></span>

* <span data-ttu-id="76620-116">**여러 언어 및 프레임워크** - 앱 서비스에서는 ASP.NET, Node.js, Java, PHP 및 Python을 최고 수준으로 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="76620-116">**Multiple languages and frameworks** - App Service has first-class support for ASP.NET, Node.js, Java, PHP, and Python.</span></span> <span data-ttu-id="76620-117">앱 서비스 VM에서 [PowerShell 및 기타 스크립트 또는 실행 파일](web-sites-create-web-jobs.md) 을 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76620-117">You can also run [PowerShell and other scripts or executables](web-sites-create-web-jobs.md) on App Service VMs.</span></span>
* <span data-ttu-id="76620-118">**DevOps 최적화** - Visual Studio Team Services, GitHub, BitBucket으로 [연속 통합 및 배포](app-service-continuous-deployment.md) 를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="76620-118">**DevOps optimization** - Set up [continuous integration and deployment](app-service-continuous-deployment.md) with Visual Studio Team Services, GitHub, or BitBucket.</span></span> <span data-ttu-id="76620-119">[테스트 및 스테이징 환경](web-sites-staged-publishing.md)을 통해 업데이트를 승격합니다.</span><span class="sxs-lookup"><span data-stu-id="76620-119">Promote updates through [test and staging environments](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="76620-120">[A/B 테스트](app-service-web-test-in-production-get-start.md)를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="76620-120">Perform [A/B testing](app-service-web-test-in-production-get-start.md).</span></span> <span data-ttu-id="76620-121">[Azure PowerShell](/powershell/azureps-cmdlets-docs) 또는 [플랫폼 간 CLI(명령줄 인터페이스)](../cli-install-nodejs.md)를 사용하여 App Service에서 앱을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="76620-121">Manage your apps in App Service by using [Azure PowerShell](/powershell/azureps-cmdlets-docs) or the [cross-platform command-line interface (CLI)](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="76620-122">**고가용성을 가진 글로벌 규모 조정** - 수동 또는 자동으로 규모를 [강화](web-sites-scale.md) 또는 [확장](../monitoring-and-diagnostics/insights-how-to-scale.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="76620-122">**Global scale with high availability** - Scale [up](web-sites-scale.md) or [out](../monitoring-and-diagnostics/insights-how-to-scale.md) manually or automatically.</span></span> <span data-ttu-id="76620-123">Microsoft의 글로벌 데이터 센터 인프라의 모든 위치에서 앱을 호스팅하고 앱 서비스 [SLA](https://azure.microsoft.com/support/legal/sla/app-service/) 를 사용하면 고가용성이 보장됩니다.</span><span class="sxs-lookup"><span data-stu-id="76620-123">Host your apps anywhere in Microsoft's global datacenter infrastructure, and the App Service [SLA](https://azure.microsoft.com/support/legal/sla/app-service/) promises high availability.</span></span>
* <span data-ttu-id="76620-124">**SaaS 플랫폼 및 온-프레미스 데이터에 연결** - 엔터프라이즈 시스템(예: SAP, Siebel 및 Oracle), SaaS 서비스(예: Salesforce 및 Office 365), 인기 있는 인터넷 서비스(예: Facebook 및 Twitter) 등을 위한 50개 이상의 [커넥터](../connectors/apis-list.md) 에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76620-124">**Connections to SaaS platforms and on-premises data** - Choose from more than 50 [connectors](../connectors/apis-list.md) for enterprise systems (such as SAP, Siebel, and Oracle), SaaS services (such as Salesforce and Office 365), and internet services (such as Facebook and Twitter).</span></span> <span data-ttu-id="76620-125">[하이브리드 연결](../biztalk-services/integration-hybrid-connection-overview.md) 및 [Azure Virtual Networks](web-sites-integrate-with-vnet.md)를 사용하여 온-프레미스 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="76620-125">Access on-premises data using [Hybrid Connections](../biztalk-services/integration-hybrid-connection-overview.md) and [Azure Virtual Networks](web-sites-integrate-with-vnet.md).</span></span>
* <span data-ttu-id="76620-126">**보안 및 규정 준수** - 앱 서비스는 [ISO, SOC 및 PCI 규격](https://www.microsoft.com/TrustCenter/)입니다.</span><span class="sxs-lookup"><span data-stu-id="76620-126">**Security and compliance** - App Service is [ISO, SOC, and PCI compliant](https://www.microsoft.com/TrustCenter/).</span></span>
* <span data-ttu-id="76620-127">**응용 프로그램 템플릿** - WordPress, Joomla, Drupal 등의 인기 있는 오픈 소스 소프트웨어를 설치하는 마법사를 사용할 수 있는 [Azure 마켓플레이스](https://azure.microsoft.com/marketplace/) 의 광범위한 응용 프로그램 템플릿 목록에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76620-127">**Application templates** - Choose from an extensive list of application templates in the [Azure Marketplace](https://azure.microsoft.com/marketplace/) that let you use a wizard to install popular open-source software such as WordPress, Joomla, and Drupal.</span></span>
* <span data-ttu-id="76620-128">**Visual Studio 통합** - Visual Studio의 전용 도구는 생성, 배포, 디버깅 작업을 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="76620-128">**Visual Studio integration** - Dedicated tools in Visual Studio streamline the work of creating, deploying, and debugging.</span></span>

<span data-ttu-id="76620-129">또한 웹앱은 [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md)(예: CORS 지원) 및 [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md)(예: 푸시 알림)에서 제공하는 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76620-129">In addition, a web app can take advantage of features offered by [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) (such as CORS support) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) (such as push notifications).</span></span> <span data-ttu-id="76620-130">앱 서비스에서 앱 유형에 대한 자세한 내용은 [Azure 앱 서비스 개요](../app-service/app-service-value-prop-what-is.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76620-130">For more information about app types in App Service, see [Azure App Service overview](../app-service/app-service-value-prop-what-is.md).</span></span>

<span data-ttu-id="76620-131">Azure는 앱 서비스의 웹앱 뿐만 아니라 웹 사이트와 웹 응용 프로그램 호스팅에 사용할 수 있는 다른 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="76620-131">Besides Web Apps in App Service, Azure offers other services that can be used for hosting websites and web applications.</span></span> <span data-ttu-id="76620-132">대부분의 시나리오의 경우 웹앱을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="76620-132">For most scenarios, Web Apps is the best choice.</span></span>  <span data-ttu-id="76620-133">마이크로 서비스 아키텍처의 경우 [Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric)을 사용하는 것이 좋으며 코드가 실행되는 VM을 보다 자세히 제어해야 하는 경우 [Azure Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="76620-133">For microservice architecture, consider [Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric), and if you need more control over the VMs that your code runs on, consider [Azure Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span> <span data-ttu-id="76620-134">이러한 Azure 서비스 중에서 하나를 선택하는 방법에 대한 자세한 내용은 [Azure 앱 서비스, 가상 컴퓨터, 서비스 패브릭 및 클라우드 서비스 비교](choose-web-site-cloud-service-vm.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76620-134">For more information about how to choose between these Azure services, see [Azure App Service, Virtual Machines, Service Fabric, and Cloud Services comparison](choose-web-site-cloud-service-vm.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="76620-135">시작</span><span class="sxs-lookup"><span data-stu-id="76620-135">Getting started</span></span>
<span data-ttu-id="76620-136">App Service의 새 웹앱에 샘플 코드를 배포하여 시작하려면 다음 드롭다운 상자의 자습서 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="76620-136">To get started by deploying sample code to a new web app in App Service, follow one of the tutorials in the following dropdown box.</span></span> <span data-ttu-id="76620-137">무료 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="76620-137">You'll need a free Azure account.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="76620-138">5분 내 Azure에 첫 번째 ASP.NET 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="76620-138">Deploy your first ASP.NET web app to Azure in 5 minutes</span></span>](app-service-web-get-started-dotnet.md)
> * [<span data-ttu-id="76620-139">5분 내 Azure에 첫 번째 PHP 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="76620-139">Deploy your first PHP web app to Azure in 5 minutes</span></span>](app-service-web-get-started-php.md)
> * [<span data-ttu-id="76620-140">5분 내 Azure에 첫 번째 Node.js 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="76620-140">Deploy your first Node.js web app to Azure in 5 minutes</span></span>](app-service-web-get-started-nodejs.md)
> * [<span data-ttu-id="76620-141">5분 내 Azure에 첫 번째 Java 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="76620-141">Deploy your first Java web app to Azure in 5 minutes</span></span>](app-service-web-get-started-java.md)
> * [<span data-ttu-id="76620-142">5분 내 Azure에 첫 번째 Python 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="76620-142">Deploy your first Python web app to Azure in 5 minutes</span></span>](app-service-web-get-started-python.md)
> * [<span data-ttu-id="76620-143">5분 내 Azure에 첫 번째 HTML 사이트 배포</span><span class="sxs-lookup"><span data-stu-id="76620-143">Deploy your first HTML site to Azure in 5 minutes</span></span>](app-service-web-get-started-html.md)
> 
> 

> [!NOTE]
> <span data-ttu-id="76620-144">Azure 계정 없이 [App Service를 체험](https://azure.microsoft.com/try/app-service/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76620-144">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="76620-145">시작 앱을 만들고 최대 한 시간 동안 해당 앱을 사용하여 재생합니다. -- 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76620-145">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 
