---
title: "Azure 앱 서비스에서 웹 앱 관리"
description: "Azure 앱 서비스에서 웹 앱 관리를 위한 리소스에 대한 링크입니다."
services: app-service\web
documentationcenter: 
author: erikre
manager: erikre
editor: 
ms.assetid: d5e2887a-84f9-4747-a573-867635cb8b39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: rachelap
ms.openlocfilehash: 9e19618a1b24bbdf3163ddfc3423c5c932dcd7af
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a><span data-ttu-id="c814f-103">Azure 앱 서비스에서 웹 앱 관리</span><span class="sxs-lookup"><span data-stu-id="c814f-103">Manage a web app in Azure App Service</span></span>
<span data-ttu-id="c814f-104">이 항목에는 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)에서 웹앱을 관리하는 리소스의 링크가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-104">This topic contains links to resources for managing a web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="c814f-105">관리에는 웹 앱을 지속적으로 원활하게 실행하는 모든 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-105">Management includes all of the tasks that keep your web app running smoothly.</span></span> 

<span data-ttu-id="c814f-106">웹 앱의 수명 주기 동안 초기 배포에서 일반 작업, 유지 관리 및 업데이트를 거치면서 여러 관리 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-106">Over the lifetime of a web app, you will perform different management tasks, as you move from initial deployment to normal operation, maintenance, and updates.</span></span>

<span data-ttu-id="c814f-107">Azure 포털에서 다양한 웹앱 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-107">Many web app management tasks can be performed in the Azure Portal.</span></span>

## <a name="before-you-deploy-your-web-app-to-production"></a><span data-ttu-id="c814f-108">웹 앱을 프로덕션으로 배포하기 전에 수행할 작업</span><span class="sxs-lookup"><span data-stu-id="c814f-108">Before you deploy your web app to production</span></span>
### <a name="choose-a-tier"></a><span data-ttu-id="c814f-109">계층 선택</span><span class="sxs-lookup"><span data-stu-id="c814f-109">Choose a tier</span></span>
<span data-ttu-id="c814f-110">Azure 앱 서비스는 5개의 계층, 무료, 공유, 기본, 표준 및 프리미엄으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-110">Azure App Service is offered in five tiers: Free, Shared, Basic, Standard, and Premium.</span></span> <span data-ttu-id="c814f-111">각 계층의 기능 및 가격에 대한 자세한 내용은 [가격 세부 정보](https://azure.microsoft.com/pricing/details/app-service/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c814f-111">For information about the features and pricing for each tier, see [Pricing details](https://azure.microsoft.com/pricing/details/app-service/).</span></span> 

* <span data-ttu-id="c814f-112">[앱 서비스 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) 에서는 같은 계층에 여러 웹 앱을 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-112">[App Service plans](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) let you group multiple web apps under the same tier.</span></span>
* <span data-ttu-id="c814f-113">웹 앱을 만든 후에 언제든지 [계층을 전환](web-sites-scale.md) 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-113">You can always [switch tiers](web-sites-scale.md) after you create your web app.</span></span>

### <a name="configuration"></a><span data-ttu-id="c814f-114">구성</span><span class="sxs-lookup"><span data-stu-id="c814f-114">Configuration</span></span>
<span data-ttu-id="c814f-115">[Azure 포털](https://portal.azure.com/) 을 사용하여 다양한 구성 옵션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-115">Use the [Azure Portal](https://portal.azure.com/) to set various configuration options.</span></span> <span data-ttu-id="c814f-116">자세한 내용은 [Azure 앱 서비스에서 웹 앱 구성](web-sites-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c814f-116">For details, see [Configure web apps in Azure App Service](web-sites-configure.md).</span></span> <span data-ttu-id="c814f-117">아래에 간단한 검사 목록이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-117">Here is a quick checklist:</span></span>

* <span data-ttu-id="c814f-118">필요에 따라 .NET, PHP, Java 또는 Python의 **런타임 버전** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-118">Select **runtime versions** for .NET, PHP, Java, or Python, if needed.</span></span>
* <span data-ttu-id="c814f-119">웹 앱에서 WebSocket 프로토콜을 사용하는 경우 **WebSockets** 을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-119">Enable **WebSockets** if your web app uses the WebSocket protocol.</span></span> <span data-ttu-id="c814f-120">여기에는 [ASP.NET SignalR](http://www.asp.net/signalr) 또는 [socket.io](web-sites-nodejs-chat-app-socketio.md)를 사용하는 앱이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-120">(This includes apps that use [ASP.NET SignalR](http://www.asp.net/signalr) or [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span></span>
* <span data-ttu-id="c814f-121">연속적인 웹 작업을 실행하는 경우</span><span class="sxs-lookup"><span data-stu-id="c814f-121">Are you running continuous web jobs?</span></span> <span data-ttu-id="c814f-122">**무중단**을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-122">If so, enable **Always On**.</span></span>
* <span data-ttu-id="c814f-123">index.html 등의 **기본 문서**를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-123">Set the **default document**, such as index.html.</span></span>

<span data-ttu-id="c814f-124">이러한 기본 구성 설정 외에 다음 항목도 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-124">In addition to these basic configuration settings, you may want to configure the following:</span></span>

* <span data-ttu-id="c814f-125">**SSL(Secure Socket Layer)** 암호화.</span><span class="sxs-lookup"><span data-stu-id="c814f-125">**Secure Socket Layer (SSL)** encryption.</span></span> <span data-ttu-id="c814f-126">사용자 지정 도메인 이름과 SSL을 사용하려면 SSL 인증서를 가져와 웹 앱이 해당 인증서를 사용하도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-126">To use SSL with a custom domain name, you must get an SSL certificate and configure your web app to use it.</span></span> <span data-ttu-id="c814f-127">[Azure 앱 서비스에서 웹 앱에 대한 HTTPS를 사용하도록 설정](app-service-web-tutorial-custom-ssl.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c814f-127">See [Enable HTTPS for a web app in Azure App Service](app-service-web-tutorial-custom-ssl.md).</span></span>
* <span data-ttu-id="c814f-128">**사용자 지정 도메인 이름.**</span><span class="sxs-lookup"><span data-stu-id="c814f-128">**Custom domain name.**</span></span> <span data-ttu-id="c814f-129">웹 앱에는 자동으로 azurewebsites.net 하위 도메인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-129">Your web app automatically has a subdomain under azurewebsites.net.</span></span> <span data-ttu-id="c814f-130">Contoso.com 등의 사용자 지정 도메인 이름을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-130">You can associate a custom domain name, such as contoso.com.</span></span> <span data-ttu-id="c814f-131">[Azure 앱 서비스에서 사용자 지정 도메인 이름 구성](app-service-web-tutorial-custom-domain.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c814f-131">See [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span>

<span data-ttu-id="c814f-132">언어별 구성:</span><span class="sxs-lookup"><span data-stu-id="c814f-132">Language-specific configuration:</span></span>

* <span data-ttu-id="c814f-133">**PHP**: [Azure 앱 서비스 웹 앱에서 PHP를 구성합니다.](web-sites-php-configure.md)</span><span class="sxs-lookup"><span data-stu-id="c814f-133">**PHP**: [Configure PHP in Azure App Service Web Apps](web-sites-php-configure.md).</span></span>
* <span data-ttu-id="c814f-134">**Python**: [Azure 앱 서비스 웹 앱에서 Python을 구성합니다.](web-sites-python-configure.md)</span><span class="sxs-lookup"><span data-stu-id="c814f-134">**Python**: [Configuring Python with Azure App Service Web Apps](web-sites-python-configure.md)</span></span>

## <a name="while-your-web-app-is-running"></a><span data-ttu-id="c814f-135">웹 앱을 실행하는 동안 수행할 작업</span><span class="sxs-lookup"><span data-stu-id="c814f-135">While your web app is running</span></span>
<span data-ttu-id="c814f-136">웹 앱이 실행되는 동안에는 웹 앱이 사용 가능하며 사용자 트래픽을 충족하도록 크기가 조정되는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-136">While your web app is running, you want to make sure it is available, and that it scales to meet user traffic.</span></span> <span data-ttu-id="c814f-137">오류가 발생하는 경우 오류 문제도 해결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-137">You may also need to troubleshoot errors.</span></span>

### <a name="monitoring"></a><span data-ttu-id="c814f-138">모니터링</span><span class="sxs-lookup"><span data-stu-id="c814f-138">Monitoring</span></span>
* <span data-ttu-id="c814f-139">Azure 포털을 통해 CPU 사용량, 클라이언트 요청 수 등의 [성능 메트릭을 추가](web-sites-monitor.md) 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-139">Through the Azure Portal, you can [add performance metrics](web-sites-monitor.md) such as CPU usage and number of client requests.</span></span>
* <span data-ttu-id="c814f-140">[웹 앱 크기를 조정](web-sites-scale.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-140">[Scale your web app](web-sites-scale.md) in response to traffic.</span></span> <span data-ttu-id="c814f-141">계층에 따라 VM의 수 및/또는 VM 인스턴스의 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-141">Depending on your tier, you can scale the number of VMs and/or the size of the VM instances.</span></span> <span data-ttu-id="c814f-142">표준 및 프리미엄 계층에서는 자동 크기 조정도 설정할 수 있으므로, 고정된 일정 또는 부하에 따라 웹 앱 크기가 자동으로 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-142">In the Standard and Premium tiers, you can also set up autoscaling, so your web app scales automatically, either on a fixed schedule, or in response to load.</span></span>  

### <a name="backups"></a><span data-ttu-id="c814f-143">백업</span><span class="sxs-lookup"><span data-stu-id="c814f-143">Backups</span></span>
* <span data-ttu-id="c814f-144">웹 앱의 [자동 백업](web-sites-backup.md) 을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-144">Set [automatic backups](web-sites-backup.md) of your web app.</span></span> <span data-ttu-id="c814f-145">백업에 대해 자세히 알아보려면 [이 비디오](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/)를 시청하세요.</span><span class="sxs-lookup"><span data-stu-id="c814f-145">Learn more about backups in [this video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span></span>
* <span data-ttu-id="c814f-146">Azure SQL 데이터베이스의 [재해 복구](../sql-database/sql-database-business-continuity.md) 용 옵션에 대해서도 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-146">Learn about the options for [database recovery](../sql-database/sql-database-business-continuity.md) in Azure SQL Database.</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="c814f-147">문제 해결</span><span class="sxs-lookup"><span data-stu-id="c814f-147">Troubleshooting</span></span>
* <span data-ttu-id="c814f-148">문제 발생 시에는 클라우드의 진단 로그 및 라이브 디버깅 기능을 사용하여 [Visual Studio에서 문제를 해결](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-148">If something goes wrong, you can [troubleshoot in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), using diagnostic logs and live debugging in the cloud.</span></span> 
* <span data-ttu-id="c814f-149">Visual Studio 외에도 다양한 방식을 통해 진단 로그를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-149">Outside of Visual Studio, there are various ways to collect diagnostic logs.</span></span> <span data-ttu-id="c814f-150">[Azure 앱 서비스에서 웹 앱에 대한 진단 로깅 설정](web-sites-enable-diagnostic-log.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c814f-150">See [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span></span>
* <span data-ttu-id="c814f-151">Node.js 응용 프로그램의 경우, [Azure 앱 서비스에서 Node.js 웹 앱을 디버그하는 방법](web-sites-nodejs-debug.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c814f-151">For Node.js applications, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

### <a name="restoring-data"></a><span data-ttu-id="c814f-152">데이터 복원</span><span class="sxs-lookup"><span data-stu-id="c814f-152">Restoring Data</span></span>
* <span data-ttu-id="c814f-153">[복원](web-sites-restore.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-153">[Restore](web-sites-restore.md) a web app that was previously backed up.</span></span>

## <a name="when-you-update-your-web-app"></a><span data-ttu-id="c814f-154">웹 앱을 업데이트하는 시기</span><span class="sxs-lookup"><span data-stu-id="c814f-154">When you update your web app</span></span>
<span data-ttu-id="c814f-155">자동 백업을 사용하도록 설정하지 않은 경우 [수동 백업](web-sites-backup.md)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-155">If you have not enabled automatic backups, you can create a [manual backup](web-sites-backup.md).</span></span>

<span data-ttu-id="c814f-156">[단계적 배포](web-sites-staged-publishing.md)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-156">Consider using [staged deployment](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="c814f-157">이 옵션을 사용하면 프로덕션 배포와 나란히 실행되는 스테이징 배포에 업데이트를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c814f-157">This option lets you publish updates to a staging deployment that runs side-by-side with your production deployment.</span></span> 


<!-- Anchors. -->

[Before you deploy your site to production]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


