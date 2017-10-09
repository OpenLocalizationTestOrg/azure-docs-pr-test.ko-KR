---
title: "Azure 앱 서비스의 웹 앱 aaaManage"
description: "Azure 앱 서비스의 웹 앱을 관리 하기 위한 링크 tooresources 합니다."
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
ms.openlocfilehash: daf69245e66068b0e97e3ae1c3fb5fce45605b91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a><span data-ttu-id="9d75d-103">Azure 앱 서비스에서 웹 앱 관리</span><span class="sxs-lookup"><span data-stu-id="9d75d-103">Manage a web app in Azure App Service</span></span>
<span data-ttu-id="9d75d-104">이 항목에서는의 웹 앱을 관리 하기 위한 링크 tooresources [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-104">This topic contains links tooresources for managing a web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="9d75d-105">관리에 웹 앱을 원활 하 게 실행 상태로 유지 하는 hello 작업을 모두 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-105">Management includes all of hello tasks that keep your web app running smoothly.</span></span> 

<span data-ttu-id="9d75d-106">웹 앱의 hello 동안 초기 배포 toonormal 운영, 유지 관리 및 업데이트에서 이동 하면 다른 관리 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-106">Over hello lifetime of a web app, you will perform different management tasks, as you move from initial deployment toonormal operation, maintenance, and updates.</span></span>

<span data-ttu-id="9d75d-107">Hello Azure 포털에서에서 다양 한 웹 앱 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-107">Many web app management tasks can be performed in hello Azure Portal.</span></span>

## <a name="before-you-deploy-your-web-app-tooproduction"></a><span data-ttu-id="9d75d-108">웹 앱 tooproduction를 배포 하기 전에</span><span class="sxs-lookup"><span data-stu-id="9d75d-108">Before you deploy your web app tooproduction</span></span>
### <a name="choose-a-tier"></a><span data-ttu-id="9d75d-109">계층 선택</span><span class="sxs-lookup"><span data-stu-id="9d75d-109">Choose a tier</span></span>
<span data-ttu-id="9d75d-110">Azure 앱 서비스는 5개의 계층, 무료, 공유, 기본, 표준 및 프리미엄으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-110">Azure App Service is offered in five tiers: Free, Shared, Basic, Standard, and Premium.</span></span> <span data-ttu-id="9d75d-111">Hello 기능 및 각 계층에 대 한 가격 책정에 대 한 정보를 참조 하십시오. [가격 정보](https://azure.microsoft.com/pricing/details/app-service/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-111">For information about hello features and pricing for each tier, see [Pricing details](https://azure.microsoft.com/pricing/details/app-service/).</span></span> 

* <span data-ttu-id="9d75d-112">[앱 서비스 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) hello에서 여러 웹 앱을 그룹화 할 수와 동일한 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-112">[App Service plans](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) let you group multiple web apps under hello same tier.</span></span>
* <span data-ttu-id="9d75d-113">웹 앱을 만든 후에 언제든지 [계층을 전환](web-sites-scale.md) 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-113">You can always [switch tiers](web-sites-scale.md) after you create your web app.</span></span>

### <a name="configuration"></a><span data-ttu-id="9d75d-114">구성</span><span class="sxs-lookup"><span data-stu-id="9d75d-114">Configuration</span></span>
<span data-ttu-id="9d75d-115">사용 하 여 hello [Azure 포털](https://portal.azure.com/) tooset 다양 한 구성 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-115">Use hello [Azure Portal](https://portal.azure.com/) tooset various configuration options.</span></span> <span data-ttu-id="9d75d-116">자세한 내용은 [Azure 앱 서비스에서 웹 앱 구성](web-sites-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d75d-116">For details, see [Configure web apps in Azure App Service](web-sites-configure.md).</span></span> <span data-ttu-id="9d75d-117">아래에 간단한 검사 목록이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-117">Here is a quick checklist:</span></span>

* <span data-ttu-id="9d75d-118">필요에 따라 .NET, PHP, Java 또는 Python의 **런타임 버전** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-118">Select **runtime versions** for .NET, PHP, Java, or Python, if needed.</span></span>
* <span data-ttu-id="9d75d-119">사용 하도록 설정 **Websocket** 웹 앱 hello WebSocket 프로토콜을 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="9d75d-119">Enable **WebSockets** if your web app uses hello WebSocket protocol.</span></span> <span data-ttu-id="9d75d-120">여기에는 [ASP.NET SignalR](http://www.asp.net/signalr) 또는 [socket.io](web-sites-nodejs-chat-app-socketio.md)를 사용하는 앱이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-120">(This includes apps that use [ASP.NET SignalR](http://www.asp.net/signalr) or [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span></span>
* <span data-ttu-id="9d75d-121">연속적인 웹 작업을 실행하는 경우</span><span class="sxs-lookup"><span data-stu-id="9d75d-121">Are you running continuous web jobs?</span></span> <span data-ttu-id="9d75d-122">**무중단**을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-122">If so, enable **Always On**.</span></span>
* <span data-ttu-id="9d75d-123">집합 hello **기본 문서**, index.html 등입니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-123">Set hello **default document**, such as index.html.</span></span>

<span data-ttu-id="9d75d-124">또한 toothese 기본 구성 설정을 tooconfigure hello 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-124">In addition toothese basic configuration settings, you may want tooconfigure hello following:</span></span>

* <span data-ttu-id="9d75d-125">**SSL(Secure Socket Layer)** 암호화.</span><span class="sxs-lookup"><span data-stu-id="9d75d-125">**Secure Socket Layer (SSL)** encryption.</span></span> <span data-ttu-id="9d75d-126">사용자 지정 도메인 이름과 함께 SSL을 toouse, 가져와야 하는 SSL 인증서 및 웹 응용 프로그램 toouse 구성할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-126">toouse SSL with a custom domain name, you must get an SSL certificate and configure your web app toouse it.</span></span> <span data-ttu-id="9d75d-127">[Azure 앱 서비스에서 웹 앱에 대한 HTTPS를 사용하도록 설정](app-service-web-tutorial-custom-ssl.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d75d-127">See [Enable HTTPS for a web app in Azure App Service](app-service-web-tutorial-custom-ssl.md).</span></span>
* <span data-ttu-id="9d75d-128">**사용자 지정 도메인 이름.**</span><span class="sxs-lookup"><span data-stu-id="9d75d-128">**Custom domain name.**</span></span> <span data-ttu-id="9d75d-129">웹 앱에는 자동으로 azurewebsites.net 하위 도메인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-129">Your web app automatically has a subdomain under azurewebsites.net.</span></span> <span data-ttu-id="9d75d-130">Contoso.com 등의 사용자 지정 도메인 이름을 연결할 수 있습니다. [Azure 앱 서비스에서 사용자 지정 도메인 이름 구성](app-service-web-tutorial-custom-domain.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d75d-130">You can associate a custom domain name, such as contoso.com. See [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span>

<span data-ttu-id="9d75d-131">언어별 구성:</span><span class="sxs-lookup"><span data-stu-id="9d75d-131">Language-specific configuration:</span></span>

* <span data-ttu-id="9d75d-132">**PHP**: [Azure 앱 서비스 웹 앱에서 PHP를 구성합니다.](web-sites-php-configure.md)</span><span class="sxs-lookup"><span data-stu-id="9d75d-132">**PHP**: [Configure PHP in Azure App Service Web Apps](web-sites-php-configure.md).</span></span>
* <span data-ttu-id="9d75d-133">**Python**: [Azure 앱 서비스 웹 앱에서 Python을 구성합니다.](web-sites-python-configure.md)</span><span class="sxs-lookup"><span data-stu-id="9d75d-133">**Python**: [Configuring Python with Azure App Service Web Apps](web-sites-python-configure.md)</span></span>

## <a name="while-your-web-app-is-running"></a><span data-ttu-id="9d75d-134">웹 앱을 실행하는 동안 수행할 작업</span><span class="sxs-lookup"><span data-stu-id="9d75d-134">While your web app is running</span></span>
<span data-ttu-id="9d75d-135">웹 앱이 실행 되는 동안 원하는 toomake toomeet 사용자 트래픽을 확장 하 고를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-135">While your web app is running, you want toomake sure it is available, and that it scales toomeet user traffic.</span></span> <span data-ttu-id="9d75d-136">Tootroubleshoot 오류 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-136">You may also need tootroubleshoot errors.</span></span>

### <a name="monitoring"></a><span data-ttu-id="9d75d-137">모니터링</span><span class="sxs-lookup"><span data-stu-id="9d75d-137">Monitoring</span></span>
* <span data-ttu-id="9d75d-138">수 hello Azure 포털을 통해 [성능 메트릭 추가](web-sites-monitor.md) 예: CPU 사용량 및 클라이언트 요청 수입니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-138">Through hello Azure Portal, you can [add performance metrics](web-sites-monitor.md) such as CPU usage and number of client requests.</span></span>
* <span data-ttu-id="9d75d-139">[웹 앱의 크기를 조정](web-sites-scale.md) 응답 tootraffic에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-139">[Scale your web app](web-sites-scale.md) in response tootraffic.</span></span> <span data-ttu-id="9d75d-140">에서는 계층에 따라 Vm hello 수 및/또는 hello hello VM 인스턴스 크기를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-140">Depending on your tier, you can scale hello number of VMs and/or hello size of hello VM instances.</span></span> <span data-ttu-id="9d75d-141">Hello 표준 및 프리미엄 계층에서 설정할 수 있습니다 또한 자동 크기 조정, 응답 tooload 또는 고정된 된 일정에서 웹 앱을 자동으로 확장 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-141">In hello Standard and Premium tiers, you can also set up autoscaling, so your web app scales automatically, either on a fixed schedule, or in response tooload.</span></span>  

### <a name="backups"></a><span data-ttu-id="9d75d-142">백업</span><span class="sxs-lookup"><span data-stu-id="9d75d-142">Backups</span></span>
* <span data-ttu-id="9d75d-143">웹 앱의 [자동 백업](web-sites-backup.md) 을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-143">Set [automatic backups](web-sites-backup.md) of your web app.</span></span> <span data-ttu-id="9d75d-144">백업에 대해 자세히 알아보려면 [이 비디오](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/)를 시청하세요.</span><span class="sxs-lookup"><span data-stu-id="9d75d-144">Learn more about backups in [this video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span></span>
* <span data-ttu-id="9d75d-145">Hello 옵션에 대 한 자세한 내용은 [데이터베이스 복구](../sql-database/sql-database-business-continuity.md) Azure SQL 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-145">Learn about hello options for [database recovery](../sql-database/sql-database-business-continuity.md) in Azure SQL Database.</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="9d75d-146">문제 해결</span><span class="sxs-lookup"><span data-stu-id="9d75d-146">Troubleshooting</span></span>
* <span data-ttu-id="9d75d-147">문제가 발생 하는 경우 다음을 할 수 있습니다 [Visual Studio에서 문제를 해결](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug)진단 로그를 사용 하 여을 라이브 hello 클라우드에서 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-147">If something goes wrong, you can [troubleshoot in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), using diagnostic logs and live debugging in hello cloud.</span></span> 
* <span data-ttu-id="9d75d-148">Visual Studio 외부에서 다양 한 방법으로 toocollect 진단 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-148">Outside of Visual Studio, there are various ways toocollect diagnostic logs.</span></span> <span data-ttu-id="9d75d-149">[Azure 앱 서비스에서 웹 앱에 대한 진단 로깅 설정](web-sites-enable-diagnostic-log.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d75d-149">See [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span></span>
* <span data-ttu-id="9d75d-150">Node.js 응용 프로그램에 대 한 참조 [어떻게 toodebug는 Node.js 웹 Azure 앱 서비스의 앱](web-sites-nodejs-debug.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-150">For Node.js applications, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

### <a name="restoring-data"></a><span data-ttu-id="9d75d-151">데이터 복원</span><span class="sxs-lookup"><span data-stu-id="9d75d-151">Restoring Data</span></span>
* <span data-ttu-id="9d75d-152">[복원](web-sites-restore.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-152">[Restore](web-sites-restore.md) a web app that was previously backed up.</span></span>

## <a name="when-you-update-your-web-app"></a><span data-ttu-id="9d75d-153">웹 앱을 업데이트하는 시기</span><span class="sxs-lookup"><span data-stu-id="9d75d-153">When you update your web app</span></span>
<span data-ttu-id="9d75d-154">자동 백업을 사용하도록 설정하지 않은 경우 [수동 백업](web-sites-backup.md)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-154">If you have not enabled automatic backups, you can create a [manual backup](web-sites-backup.md).</span></span>

<span data-ttu-id="9d75d-155">[단계적 배포](web-sites-staged-publishing.md)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-155">Consider using [staged deployment](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="9d75d-156">이 옵션을 사용 하면 게시-나란히 실행 하는 배포를 준비 하는 업데이트 tooa 프로덕션 배포에 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d75d-156">This option lets you publish updates tooa staging deployment that runs side-by-side with your production deployment.</span></span> 


<!-- Anchors. -->

[Before you deploy your site tooproduction]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


