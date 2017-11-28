---
title: "aaaWeb 앱 개요 | Microsoft Docs"
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
ms.openlocfilehash: ce27519bddd62a7fca6ba1fb23c763d0fc378c2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="web-apps-overview"></a><span data-ttu-id="7bb77-103">웹앱 개요</span><span class="sxs-lookup"><span data-stu-id="7bb77-103">Web Apps overview</span></span>
<span data-ttu-id="7bb77-104">*앱 서비스 웹앱* 은 웹 사이트와 웹 응용 프로그램 호스팅을 위해 최적화된 완전히 관리되는 계산 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-104">*App Service Web Apps* is a fully managed compute platform that is optimized for hosting websites and web applications.</span></span> <span data-ttu-id="7bb77-105">이 [플랫폼-as a service](https://en.wikipedia.org/wiki/Platform_as_a_service) Microsoft azure 서비스 (PaaS)를 사용 하면 Azure hello 인프라 toorun는 담당 하는 동안 비즈니스 논리에 집중 하 고 앱의 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-105">This [platform-as-a-service](https://en.wikipedia.org/wiki/Platform_as_a_service) (PaaS) offering of Microsoft Azure lets you focus on your business logic while Azure takes care of hello infrastructure toorun and scale your apps.</span></span>

<span data-ttu-id="7bb77-106">5 분 분량의 비디오를 따라 hello Azure 앱 서비스 웹 앱을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-106">hello following 5-minute video introduces Azure App Service Web Apps.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Web-Apps-with-Yochay-Kiriaty/player]
>
>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

## <a name="what-is-a-web-app-in-app-service"></a><span data-ttu-id="7bb77-107">앱 서비스에서 웹앱은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="7bb77-107">What is a web app in App Service?</span></span>
<span data-ttu-id="7bb77-108">앱 서비스에서 한 *웹 앱* 는 hello 호스팅 웹 사이트 또는 웹 응용 프로그램에 대 한 Azure에서 제공 하는 계산 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-108">In App Service, a *web app* is hello compute resources that Azure provides for hosting a website or web application.</span></span>  

<span data-ttu-id="7bb77-109">hello 계산 리소스 공유 또는 전용 (Vm)에 따라 가상 컴퓨터 가격 책정 계층 선택 하는 hello에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-109">hello compute resources may be on shared or dedicated virtual machines (VMs), depending on hello pricing tier that you choose.</span></span> <span data-ttu-id="7bb77-110">응용 프로그램 코드는 다른 고객과 격리되는 관리되는 VM에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-110">Your application code runs in a managed VM that is isolated from other customers.</span></span>

<span data-ttu-id="7bb77-111">사용자 코드는 [Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md)(ASP.NET, Node.js, Java, PHP, Python)에서 지원되는 모든 언어 또는 프레임워크일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-111">Your code can be in any language or framework that is supported by [Azure App Service](../app-service/app-service-value-prop-what-is.md), such as ASP.NET, Node.js, Java, PHP, or Python.</span></span> <span data-ttu-id="7bb77-112">웹앱에서 [PowerShell 및 기타 스크립트 언어](web-sites-create-web-jobs.md#acceptablefiles) 를 사용하는 스크립트를 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-112">You can also run scripts that use [PowerShell and other scripting languages](web-sites-create-web-jobs.md#acceptablefiles) in a web app.</span></span>

<span data-ttu-id="7bb77-113">참조에 대해 웹 응용 프로그램을 사용할 수 있는 일반적인 응용 프로그램 시나리오의 예제에 대 한 [웹 응용 프로그램 시나리오](https://azure.microsoft.com/documentation/scenarios/web-app/) 및 hello **시나리오 및 권장 사항** 섹션 [Azure 앱 서비스, 가상 컴퓨터, 서비스 패브릭 및 클라우드 서비스 비교](choose-web-site-cloud-service-vm.md#scenarios)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-113">For examples of typical application scenarios that you can use Web Apps for, see [Web app scenarios](https://azure.microsoft.com/documentation/scenarios/web-app/) and hello **Scenarios and recommendations** section of [Azure App Service, Virtual Machines, Service Fabric, and Cloud Services comparison](choose-web-site-cloud-service-vm.md#scenarios).</span></span>

## <a name="why-use-web-apps"></a><span data-ttu-id="7bb77-114">웹앱을 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="7bb77-114">Why use Web Apps?</span></span>
<span data-ttu-id="7bb77-115">TooWeb 앱 적용 되거나 적용 하는 앱 서비스의 주요 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-115">Here are some key features of App Service that apply tooWeb Apps:</span></span>

* <span data-ttu-id="7bb77-116">**여러 언어 및 프레임워크** - 앱 서비스에서는 ASP.NET, Node.js, Java, PHP 및 Python을 최고 수준으로 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-116">**Multiple languages and frameworks** - App Service has first-class support for ASP.NET, Node.js, Java, PHP, and Python.</span></span> <span data-ttu-id="7bb77-117">앱 서비스 VM에서 [PowerShell 및 기타 스크립트 또는 실행 파일](web-sites-create-web-jobs.md) 을 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-117">You can also run [PowerShell and other scripts or executables](web-sites-create-web-jobs.md) on App Service VMs.</span></span>
* <span data-ttu-id="7bb77-118">**DevOps 최적화** - Visual Studio Team Services, GitHub, BitBucket으로 [연속 통합 및 배포](app-service-continuous-deployment.md) 를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-118">**DevOps optimization** - Set up [continuous integration and deployment](app-service-continuous-deployment.md) with Visual Studio Team Services, GitHub, or BitBucket.</span></span> <span data-ttu-id="7bb77-119">[테스트 및 스테이징 환경](web-sites-staged-publishing.md)을 통해 업데이트를 승격합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-119">Promote updates through [test and staging environments](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="7bb77-120">[A/B 테스트](app-service-web-test-in-production-get-start.md)를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-120">Perform [A/B testing](app-service-web-test-in-production-get-start.md).</span></span> <span data-ttu-id="7bb77-121">앱 서비스에서 앱을 사용 하 여 관리 [Azure PowerShell](/powershell/azureps-cmdlets-docs) 또는 hello [플랫폼 간 명령줄 인터페이스 (CLI)](../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-121">Manage your apps in App Service by using [Azure PowerShell](/powershell/azureps-cmdlets-docs) or hello [cross-platform command-line interface (CLI)](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="7bb77-122">**고가용성을 가진 글로벌 규모 조정** - 수동 또는 자동으로 규모를 [강화](web-sites-scale.md) 또는 [확장](../monitoring-and-diagnostics/insights-how-to-scale.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-122">**Global scale with high availability** - Scale [up](web-sites-scale.md) or [out](../monitoring-and-diagnostics/insights-how-to-scale.md) manually or automatically.</span></span> <span data-ttu-id="7bb77-123">Microsoft의 글로벌 데이터 센터 인프라의 아무 곳 이나 앱을 호스트 하 고 응용 프로그램 서비스 hello [SLA](https://azure.microsoft.com/support/legal/sla/app-service/) 고가용성을 약속 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-123">Host your apps anywhere in Microsoft's global datacenter infrastructure, and hello App Service [SLA](https://azure.microsoft.com/support/legal/sla/app-service/) promises high availability.</span></span>
* <span data-ttu-id="7bb77-124">**연결 tooSaaS 플랫폼 및 온-프레미스 데이터** -50 개 이상의 중에서 선택할 [커넥터](../connectors/apis-list.md) SaaS 서비스 (예: SAP, Siebel, Oracle) 엔터프라이즈 시스템의 경우 (예: Salesforce 및 Office 365) 및 인터넷 서비스 (예: Facebook 및 Twitter)입니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-124">**Connections tooSaaS platforms and on-premises data** - Choose from more than 50 [connectors](../connectors/apis-list.md) for enterprise systems (such as SAP, Siebel, and Oracle), SaaS services (such as Salesforce and Office 365), and internet services (such as Facebook and Twitter).</span></span> <span data-ttu-id="7bb77-125">[하이브리드 연결](../biztalk-services/integration-hybrid-connection-overview.md) 및 [Azure Virtual Networks](web-sites-integrate-with-vnet.md)를 사용하여 온-프레미스 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-125">Access on-premises data using [Hybrid Connections](../biztalk-services/integration-hybrid-connection-overview.md) and [Azure Virtual Networks](web-sites-integrate-with-vnet.md).</span></span>
* <span data-ttu-id="7bb77-126">**보안 및 규정 준수** - 앱 서비스는 [ISO, SOC 및 PCI 규격](https://www.microsoft.com/TrustCenter/)입니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-126">**Security and compliance** - App Service is [ISO, SOC, and PCI compliant](https://www.microsoft.com/TrustCenter/).</span></span>
* <span data-ttu-id="7bb77-127">**응용 프로그램 템플릿** -hello에 대 한 응용 프로그램 템플릿 확장 목록에서 선택 [Azure 마켓플레이스](https://azure.microsoft.com/marketplace/) WordPress, Drupal, Joomla와 같은 마법사 tooinstall 인기 있는 오픈 소스 소프트웨어를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-127">**Application templates** - Choose from an extensive list of application templates in hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) that let you use a wizard tooinstall popular open-source software such as WordPress, Joomla, and Drupal.</span></span>
* <span data-ttu-id="7bb77-128">**Visual Studio 통합** -Visual Studio에서 전용된 도구 hello 작업 만들기, 배포 및 디버깅을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-128">**Visual Studio integration** - Dedicated tools in Visual Studio streamline hello work of creating, deploying, and debugging.</span></span>

<span data-ttu-id="7bb77-129">또한 웹앱은 [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md)(예: CORS 지원) 및 [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md)(예: 푸시 알림)에서 제공하는 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-129">In addition, a web app can take advantage of features offered by [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) (such as CORS support) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) (such as push notifications).</span></span> <span data-ttu-id="7bb77-130">앱 서비스에서 앱 유형에 대한 자세한 내용은 [Azure 앱 서비스 개요](../app-service/app-service-value-prop-what-is.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7bb77-130">For more information about app types in App Service, see [Azure App Service overview](../app-service/app-service-value-prop-what-is.md).</span></span>

<span data-ttu-id="7bb77-131">Azure는 앱 서비스의 웹앱 뿐만 아니라 웹 사이트와 웹 응용 프로그램 호스팅에 사용할 수 있는 다른 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-131">Besides Web Apps in App Service, Azure offers other services that can be used for hosting websites and web applications.</span></span> <span data-ttu-id="7bb77-132">대부분의 시나리오에 대 한 웹 앱이 hello 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-132">For most scenarios, Web Apps is hello best choice.</span></span>  <span data-ttu-id="7bb77-133">마이크로 서비스 아키텍처에 대 한 고려 [서비스 패브릭](https://azure.microsoft.com/documentation/services/service-fabric), 더 많이 제어할 hello Vm에서 실행 되는 코드는 필요한 경우 고 [Azure 가상 컴퓨터](https://azure.microsoft.com/documentation/services/virtual-machines/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-133">For microservice architecture, consider [Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric), and if you need more control over hello VMs that your code runs on, consider [Azure Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span> <span data-ttu-id="7bb77-134">방법에 대 한 자세한 내용은 이러한 Azure 서비스 간의 toochoose 참조 [Azure 앱 서비스, 가상 컴퓨터, 서비스 패브릭 및 클라우드 서비스 비교](choose-web-site-cloud-service-vm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-134">For more information about how toochoose between these Azure services, see [Azure App Service, Virtual Machines, Service Fabric, and Cloud Services comparison](choose-web-site-cloud-service-vm.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="7bb77-135">시작</span><span class="sxs-lookup"><span data-stu-id="7bb77-135">Getting started</span></span>
<span data-ttu-id="7bb77-136">앱 서비스의 샘플 코드 tooa 새 웹 앱을 배포 하 여 시작 tooget hello 드롭다운 상자 뒤의 hello 자습서 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-136">tooget started by deploying sample code tooa new web app in App Service, follow one of hello tutorials in hello following dropdown box.</span></span> <span data-ttu-id="7bb77-137">무료 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-137">You'll need a free Azure account.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7bb77-138">첫 번째 여 ASP.NET 웹 응용 프로그램 tooAzure 5 분 이내에 배포</span><span class="sxs-lookup"><span data-stu-id="7bb77-138">Deploy your first ASP.NET web app tooAzure in 5 minutes</span></span>](app-service-web-get-started-dotnet.md)
> * [<span data-ttu-id="7bb77-139">첫 번째 여 PHP 웹 응용 프로그램 tooAzure 5 분 이내에 배포</span><span class="sxs-lookup"><span data-stu-id="7bb77-139">Deploy your first PHP web app tooAzure in 5 minutes</span></span>](app-service-web-get-started-php.md)
> * [<span data-ttu-id="7bb77-140">첫 번째 프로그램 Node.js 웹 응용 프로그램 tooAzure 5 분 이내에 배포</span><span class="sxs-lookup"><span data-stu-id="7bb77-140">Deploy your first Node.js web app tooAzure in 5 minutes</span></span>](app-service-web-get-started-nodejs.md)
> * [<span data-ttu-id="7bb77-141">5 분 이내에 첫 번째 Java 웹 응용 프로그램 tooAzure 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="7bb77-141">Deploy your first Java web app tooAzure in 5 minutes</span></span>](app-service-web-get-started-java.md)
> * [<span data-ttu-id="7bb77-142">첫 번째 여 Python 웹 응용 프로그램 tooAzure 5 분 이내에 배포</span><span class="sxs-lookup"><span data-stu-id="7bb77-142">Deploy your first Python web app tooAzure in 5 minutes</span></span>](app-service-web-get-started-python.md)
> * [<span data-ttu-id="7bb77-143">5 분 이내에 첫 번째 HTML 사이트 tooAzure 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="7bb77-143">Deploy your first HTML site tooAzure in 5 minutes</span></span>](app-service-web-get-started-html.md)
> 
> 

> [!NOTE]
> <span data-ttu-id="7bb77-144">Azure 계정 없이 [App Service를 체험](https://azure.microsoft.com/try/app-service/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-144">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="7bb77-145">시작 응용 프로그램 만들기 및 신용 카드가 필요 없는, 없음의 노력과 헌신 함께 tooan 시간-를 재생 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bb77-145">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 
