---
title: "Azure 앱 서비스에서 웹 앱 구성"
description: "Azure 앱 서비스에서 웹 앱을 구성 하는 방법"
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9af8a367-7d39-4399-9941-b80cbc5f39a0
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cacbcf879555907f81d824dc1069b05579dca010
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a><span data-ttu-id="2d15c-103">Azure 앱 서비스에서 웹 앱 구성</span><span class="sxs-lookup"><span data-stu-id="2d15c-103">Configure web apps in Azure App Service</span></span>
<span data-ttu-id="2d15c-104">이 항목에서는 [Azure Portal]을 사용하여 웹앱을 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-104">This topic explains how to configure a web app using the [Azure Portal].</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a><span data-ttu-id="2d15c-105">응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="2d15c-105">Application settings</span></span>
1. <span data-ttu-id="2d15c-106">[Azure Portal]에서, 웹 앱에 대한 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-106">In the [Azure Portal], open the blade for the web app.</span></span>
2. <span data-ttu-id="2d15c-107">**모든 설정**을 클릭합니다</span><span class="sxs-lookup"><span data-stu-id="2d15c-107">Click **All Settings**.</span></span>
3. <span data-ttu-id="2d15c-108">**응용 프로그램 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-108">Click **Application Settings**.</span></span>

![응용 프로그램 설정][configure01]

<span data-ttu-id="2d15c-110">**응용 프로그램 설정** 블레이드 설정이 여러 범주 아래에 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-110">The **Application settings** blade has settings grouped under several categories.</span></span>

### <a name="general-settings"></a><span data-ttu-id="2d15c-111">일반 설정</span><span class="sxs-lookup"><span data-stu-id="2d15c-111">General settings</span></span>
<span data-ttu-id="2d15c-112">**프레임워크 버전**.</span><span class="sxs-lookup"><span data-stu-id="2d15c-112">**Framework versions**.</span></span> <span data-ttu-id="2d15c-113">앱에서 다음 프레임워크를 사용하는 경우 이러한 옵션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-113">Set these options if your app uses any these frameworks:</span></span> 

* <span data-ttu-id="2d15c-114">**.NET Framework**: .NET Framework 버전을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-114">**.NET Framework**: Set the .NET framework version.</span></span> 
* <span data-ttu-id="2d15c-115">**PHP**: PHP 버전을 설정하거나 PHP를 사용하지 않으려면 **끄기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-115">**PHP**: Set the PHP version, or **OFF** to disable PHP.</span></span> 
* <span data-ttu-id="2d15c-116">**Java**: Java 버전을 선택하거나 Java를 사용하지 않도록 **끄기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-116">**Java**: Select the Java version or **OFF** to disable Java.</span></span> <span data-ttu-id="2d15c-117">**웹 컨테이너** 옵션을 사용하여 Tomcat 및 Jetty 버전 사이에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-117">Use the **Web Container** option to choose between Tomcat and Jetty versions.</span></span>
* <span data-ttu-id="2d15c-118">**Python**: Python 버전을 설정하거나, Python을 사용하지 않도록 설정하려면 **끄기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-118">**Python**: Select the Python version, or **OFF** to disable Python.</span></span>

<span data-ttu-id="2d15c-119">기술적인 이유로, 앱에 Java를 사용하도록 설정하면 .NET, PHP 및 Python 옵션은 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-119">For technical reasons, enabling Java for your app disables the .NET, PHP, and Python options.</span></span>

<span data-ttu-id="2d15c-120"><a name="platform"></a>
**플랫폼**.</span><span class="sxs-lookup"><span data-stu-id="2d15c-120"><a name="platform"></a>
**Platform**.</span></span> <span data-ttu-id="2d15c-121">응용 프로그램이 32비트 또는 64비트 환경에서 실행되는지 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-121">Selects whether your web app runs in a 32-bit or 64-bit environment.</span></span> <span data-ttu-id="2d15c-122">64비트 환경에는 기본 또는 표준 모드가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-122">The 64-bit environment requires Basic or Standard mode.</span></span> <span data-ttu-id="2d15c-123">무료 및 공유 모드는 항상 32비트 환경에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-123">Free and Shared modes always run in a 32-bit environment.</span></span>

<span data-ttu-id="2d15c-124">**웹 소켓**.</span><span class="sxs-lookup"><span data-stu-id="2d15c-124">**Web Sockets**.</span></span> <span data-ttu-id="2d15c-125">WebSocket 프로토콜을 사용하도록 설정하려면 **켜기**를 설정합니다. 예를 들어 [ASP.NET SignalR] 또는 [socket.io]를 사용하는 경우가 여기에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-125">Set **ON** to enable the WebSocket protocol; for example, if your web app uses [ASP.NET SignalR] or [socket.io].</span></span>

<span data-ttu-id="2d15c-126"><a name="alwayson"></a>
**Always On**.</span><span class="sxs-lookup"><span data-stu-id="2d15c-126"><a name="alwayson"></a>
**Always On**.</span></span> <span data-ttu-id="2d15c-127">기본적으로 웹 앱은 일정 기간 동안 유휴 상태인 경우 언로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-127">By default, web apps are unloaded if they are idle for some period of time.</span></span> <span data-ttu-id="2d15c-128">이를 통해 시스템 리소스가 절약됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-128">This lets the system conserve resources.</span></span> <span data-ttu-id="2d15c-129">기본 또는 표준 모드에서는 **Always On**을 사용하도록 설정하여 앱을 항상 로드된 상태로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-129">In Basic or Standard mode, you can enable **Always On** to keep the app loaded all the time.</span></span> <span data-ttu-id="2d15c-130">앱에서 연속 WebJobs를 실행하거나 CRON 식을 사용하여 트리거되는 WebJobs를 실행하는 경우 **Always On**을 사용하도록 설정해야 합니다. 그러지 않으면 웹 작업이 안정적으로 실행되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-130">If your app runs continuous WebJobs or runs WebJobs triggered using a CRON expression, you should enable **Always On**, or the web jobs may not run reliably.</span></span>

<span data-ttu-id="2d15c-131">**관리되는 파이프라인 버전**.</span><span class="sxs-lookup"><span data-stu-id="2d15c-131">**Managed Pipeline Version**.</span></span> <span data-ttu-id="2d15c-132">IIS [파이프라인 모드]를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-132">Sets the IIS [pipeline mode].</span></span> <span data-ttu-id="2d15c-133">이전 버전의 IIS가 필요한 레거시 앱이 없으면 통합(기본값)으로 설정된 상태로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-133">Leave this set to Integrated (the default) unless you have a legacy app that requires an older version of IIS.</span></span>

<span data-ttu-id="2d15c-134">**자동 교체**.</span><span class="sxs-lookup"><span data-stu-id="2d15c-134">**Auto Swap**.</span></span> <span data-ttu-id="2d15c-135">배포 슬롯에 대한 자동 교체를 사용 하는 경우, 업데이트를 해당 슬롯에 푸시하면 앱 서비스는 자동으로 웹 앱을 프로덕션으로 교체합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-135">If you enable Auto Swap for a deployment slot, App Service will automatically swap the web app into production when you push an update to that slot.</span></span> <span data-ttu-id="2d15c-136">자세한 내용은 [Azure 앱 서비스에서 웹 앱에 대한 스테이징 슬롯에 배포](web-sites-staged-publishing.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d15c-136">For more information, see [Deploy to staging slots for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span>

### <a name="debugging"></a><span data-ttu-id="2d15c-137">디버그</span><span class="sxs-lookup"><span data-stu-id="2d15c-137">Debugging</span></span>
<span data-ttu-id="2d15c-138">**원격 디버깅**.</span><span class="sxs-lookup"><span data-stu-id="2d15c-138">**Remote Debugging**.</span></span> <span data-ttu-id="2d15c-139">원격 디버깅을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-139">Enables remote debugging.</span></span> <span data-ttu-id="2d15c-140">사용하도록 설정되면 Visual Studio에서 원격 디버거를 사용하여 웹 앱에 바로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-140">When enabled, you can use the remote debugger in Visual Studio to connect directly to your web app.</span></span> <span data-ttu-id="2d15c-141">원격 디버깅은 48시간 동안 사용 가능한 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-141">Remote debugging will remain enabled for 48 hours.</span></span> 

### <a name="app-settings"></a><span data-ttu-id="2d15c-142">앱 설정</span><span class="sxs-lookup"><span data-stu-id="2d15c-142">App settings</span></span>
<span data-ttu-id="2d15c-143">이 섹션에는 시작 시 웹 앱이 로드하는 이름/값 쌍을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-143">This section contains name/value pairs that you web app will load on start up.</span></span> 

* <span data-ttu-id="2d15c-144">.NET 앱의 경우, 이 설정은 런타임 시 .NET 구성 `AppSettings`으로 주입되어 기존 설정을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-144">For .NET apps, these settings are injected into your .NET configuration `AppSettings` at runtime, overriding existing settings.</span></span> 
* <span data-ttu-id="2d15c-145">PHP, Python, Java 및 Node 응용 프로그램에서는 런타임에 환경 변수로 이러한 설정에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-145">PHP, Python, Java and Node applications can access these settings as environment variables at runtime.</span></span> <span data-ttu-id="2d15c-146">각 앱 설정에 대해 두 개의 환경 변수가 만들어집니다. 하나는 앱 설정 항목에 의해 이름이 지정되고, 다른 하나는 이름에 APPSETTING_ 접두사가 붙습니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-146">For each app setting, two environment variables are created; one with the name specified by the app setting entry, and another with a prefix of APPSETTING_.</span></span> <span data-ttu-id="2d15c-147">둘 다 같은 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-147">Both contain the same value.</span></span>

### <a name="connection-strings"></a><span data-ttu-id="2d15c-148">연결 문자열</span><span class="sxs-lookup"><span data-stu-id="2d15c-148">Connection strings</span></span>
<span data-ttu-id="2d15c-149">연결된 리소스의 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-149">Connection strings for linked resources.</span></span> 

<span data-ttu-id="2d15c-150">.NET 앱의 경우, 이 연결 문자열이 런타임 시 .NET 구성 `connectionStrings` 설정에 주입되어 키가 연결된 데이터베이스 이름과 같은 기존 항목을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-150">For .NET apps, these connection strings are injected into your .NET configuration `connectionStrings` settings at runtime, overriding existing entries where the key equals the linked database name.</span></span> 

<span data-ttu-id="2d15c-151">PHP, Python, Java 및 Node 응용 프로그램에서는 런타임에 이러한 설정을 환경 변수로 사용할 수 있으며, 환경 변수 앞에는 연결 형식이 옵니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-151">For PHP, Python, Java and Node applications, these settings will be available as environment variables at runtime, prefixed with the connection type.</span></span> <span data-ttu-id="2d15c-152">환경 변수 접두사는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-152">The environment variable prefixes are as follows:</span></span> 

* <span data-ttu-id="2d15c-153">SQL Server: `SQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="2d15c-153">SQL Server: `SQLCONNSTR_`</span></span>
* <span data-ttu-id="2d15c-154">MySQL: `MYSQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="2d15c-154">MySQL: `MYSQLCONNSTR_`</span></span>
* <span data-ttu-id="2d15c-155">SQL 데이터베이스: `SQLAZURECONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="2d15c-155">SQL Database: `SQLAZURECONNSTR_`</span></span>
* <span data-ttu-id="2d15c-156">사용자 지정: `CUSTOMCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="2d15c-156">Custom: `CUSTOMCONNSTR_`</span></span>

<span data-ttu-id="2d15c-157">예를 들어 MySql 연결 문자열 이름이 `connectionstring1`로 지정된 경우 환경 변수 `MYSQLCONNSTR_connectionString1`을 통해 액세스될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-157">For example, if a MySql connection string were named `connectionstring1`, it would be accessed through the environment variable `MYSQLCONNSTR_connectionString1`.</span></span>

### <a name="default-documents"></a><span data-ttu-id="2d15c-158">기본 문서</span><span class="sxs-lookup"><span data-stu-id="2d15c-158">Default documents</span></span>
<span data-ttu-id="2d15c-159">기본 문서는 웹 사이트의 루트 URL에 표시되는 웹 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-159">The default document is the web page that is displayed at the root URL for a website.</span></span>  <span data-ttu-id="2d15c-160">목록에서 첫 번째로 일치되는 파일이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-160">The first matching file in the list is used.</span></span> 

<span data-ttu-id="2d15c-161">웹 앱에서는 정적 콘텐츠를 제공하는 대신 URL을 기반으로 라우팅되는 모듈을 사용할 수 있으며, 이 경우에도 기본 문서는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-161">Web apps might use modules that route based on URL, rather than serving static content, in which case there is no default document as such.</span></span>    

### <a name="handler-mappings"></a><span data-ttu-id="2d15c-162">처리기 매핑</span><span class="sxs-lookup"><span data-stu-id="2d15c-162">Handler mappings</span></span>
<span data-ttu-id="2d15c-163">이 영역을 사용하여 사용자 지정 스크립트 프로세서를 추가해 특정 파일 확장명에 대한 요청을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-163">Use this area to add custom script processors to handle requests for specific file extensions.</span></span> 

* <span data-ttu-id="2d15c-164">**확장명**.</span><span class="sxs-lookup"><span data-stu-id="2d15c-164">**Extension**.</span></span> <span data-ttu-id="2d15c-165">처리할 파일 확장명입니다(예: *.php 또는 handler.fcgi).</span><span class="sxs-lookup"><span data-stu-id="2d15c-165">The file extension to be handled, such as *.php or handler.fcgi.</span></span> 
* <span data-ttu-id="2d15c-166">**스크립트 프로세서 경로**.</span><span class="sxs-lookup"><span data-stu-id="2d15c-166">**Script Processor Path**.</span></span> <span data-ttu-id="2d15c-167">스크립트 프로세서의 절대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-167">The absolute path of the script processor.</span></span> <span data-ttu-id="2d15c-168">파일 확장명과 일치하는 파일에 대한 요청이 스크립트 프로세서에서 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-168">Requests to files that match the file extension will be processed by the script processor.</span></span> <span data-ttu-id="2d15c-169">경로 `D:\home\site\wwwroot` 를 사용하여 앱의 루트 디렉터리를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-169">Use the path `D:\home\site\wwwroot` to refer to your app's root directory.</span></span>
* <span data-ttu-id="2d15c-170">**추가 인수**.</span><span class="sxs-lookup"><span data-stu-id="2d15c-170">**Additional Arguments**.</span></span> <span data-ttu-id="2d15c-171">스크립트 프로세서에 대한 선택적 명령줄 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-171">Optional command-line arguments for the script processor</span></span> 

### <a name="virtual-applications-and-directories"></a><span data-ttu-id="2d15c-172">가상 응용 프로그램 및 디렉터리</span><span class="sxs-lookup"><span data-stu-id="2d15c-172">Virtual applications and directories</span></span>
<span data-ttu-id="2d15c-173">가상 응용 프로그램 및 디렉터리를 구성하려면 각 가상 디렉터리 및 웹 사이트 루트에 상대적인 실제 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-173">To configure virtual applications and directories, specify each virtual directory and its corresponding physical path relative to the website root.</span></span> <span data-ttu-id="2d15c-174">경우에 따라 **응용 프로그램** 확인란을 선택하여 가상 디렉터리를 응용 프로그램으로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-174">Optionally, you can select the **Application** checkbox to mark a virtual directory as an application.</span></span>

## <a name="enabling-diagnostic-logs"></a><span data-ttu-id="2d15c-175">진단 로그를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="2d15c-175">Enabling diagnostic logs</span></span>
<span data-ttu-id="2d15c-176">진단 로그를 사용하도록 설정하려면:</span><span class="sxs-lookup"><span data-stu-id="2d15c-176">To enable diagnostic logs:</span></span>

1. <span data-ttu-id="2d15c-177">웹 앱의 블레이드에서 **모든 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-177">In the blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="2d15c-178">**진단 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-178">Click **Diagnostic logs**.</span></span> 

<span data-ttu-id="2d15c-179">로깅을 지원하는 웹 응용 프로그램의 진단 정보를 기록하는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-179">Options for writing diagnostic logs from a web application that supports logging:</span></span> 

* <span data-ttu-id="2d15c-180">**응용 프로그램 로깅**.</span><span class="sxs-lookup"><span data-stu-id="2d15c-180">**Application Logging**.</span></span> <span data-ttu-id="2d15c-181">파일 시스템에 응용 프로그램 로그를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-181">Writes application logs to the file system.</span></span> <span data-ttu-id="2d15c-182">로깅은 12시간 동안 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-182">Logging lasts for a period of 12 hours.</span></span> 

<span data-ttu-id="2d15c-183">**수준**.</span><span class="sxs-lookup"><span data-stu-id="2d15c-183">**Level**.</span></span> <span data-ttu-id="2d15c-184">응용 프로그램 로깅을 사용하도록 설정하면 이 옵션은 기록될 정보의 양(오류, 경고, 정보 또는 세부 정보 표시)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-184">When application logging is enabled, this option specifies the amount of information that will be recorded (Error, Warning, Information, or Verbose).</span></span>

<span data-ttu-id="2d15c-185">**웹 서버 로깅**.</span><span class="sxs-lookup"><span data-stu-id="2d15c-185">**Web server logging**.</span></span> <span data-ttu-id="2d15c-186">로그는 W3C 확장 로그 파일 형식으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-186">Logs are saved in the W3C extended log file format.</span></span> 

<span data-ttu-id="2d15c-187">**자세한 오류 메시지**.</span><span class="sxs-lookup"><span data-stu-id="2d15c-187">**Detailed error messages**.</span></span> <span data-ttu-id="2d15c-188">자세한 오류 메시지는.htm 파일로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-188">Saves detailed error messages .htm files.</span></span> <span data-ttu-id="2d15c-189">이 파일은 /LogFiles/DetailedErrors 아래 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-189">The files are saved under /LogFiles/DetailedErrors.</span></span> 

<span data-ttu-id="2d15c-190">**실패한 요청 추적**.</span><span class="sxs-lookup"><span data-stu-id="2d15c-190">**Failed request tracing**.</span></span> <span data-ttu-id="2d15c-191">로그는 XML 파일에 대해 요청하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-191">Logs failed requests to XML files.</span></span> <span data-ttu-id="2d15c-192">파일은 /LogFiles/W3SVC*xxx*(여기서 xxx는 고유 식별자) 아래에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-192">The files are saved under /LogFiles/W3SVC*xxx*, where xxx is a unique identifier.</span></span> <span data-ttu-id="2d15c-193">이 폴더에는 하나의 XSL 파일 및 하나 이상의 XML 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-193">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="2d15c-194">XSL 파일은 XML 파일 내용의 서식을 지정하고 필터링하는 기능을 제공하므로 XSL 파일을 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-194">Make sure to download the XSL file, because it provides functionality for formatting and filtering the contents of the XML files.</span></span>

<span data-ttu-id="2d15c-195">로그 파일을 보려면 다음과 같이 FTP 자격 증명을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-195">To view the log files, you must create FTP credentials, as follows:</span></span>

1. <span data-ttu-id="2d15c-196">웹 앱의 블레이드에서 **모든 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-196">In the blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="2d15c-197">**배포 자격 증명**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-197">Click **Deployment credentials**.</span></span>
3. <span data-ttu-id="2d15c-198">사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-198">Enter a user name and password.</span></span>
4. <span data-ttu-id="2d15c-199">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-199">Click **Save**.</span></span>

![배포 자격 증명 설정][configure03]

<span data-ttu-id="2d15c-201">전체 FTP 사용자 이름은 “app\username”이며, 여기서 *app*은 사용자의 웹앱 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-201">The full FTP user name is “app\username” where *app* is the name of your web app.</span></span> <span data-ttu-id="2d15c-202">사용자 이름은 **필수 항목**아래 웹 앱 블레이드에 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-202">The username is listed in the web app blade, under **Essentials**.</span></span>  

![FTP 배포 자격 증명][configure02]

## <a name="other-configuration-tasks"></a><span data-ttu-id="2d15c-204">기타 구성 작업</span><span class="sxs-lookup"><span data-stu-id="2d15c-204">Other configuration tasks</span></span>
### <a name="ssl"></a><span data-ttu-id="2d15c-205">SSL</span><span class="sxs-lookup"><span data-stu-id="2d15c-205">SSL</span></span>
<span data-ttu-id="2d15c-206">기본 또는 표준 모드에서는 사용자 지정 도메인에 대해 SSL 인증서를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-206">In Basic or Standard mode, you can upload SSL certificates for a custom domain.</span></span> <span data-ttu-id="2d15c-207">자세한 내용은 [웹 앱에 대한 HTTPS 사용]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d15c-207">For more information, see [Enable HTTPS for a web app].</span></span> 

<span data-ttu-id="2d15c-208">업로드된 인증서를 보려면 **모든 설정** > **사용자 지정 도메인 및 SSL**을 사용하여 웹앱을 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-208">To view your uploaded certificates, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="domain-names"></a><span data-ttu-id="2d15c-209">도메인 이름</span><span class="sxs-lookup"><span data-stu-id="2d15c-209">Domain names</span></span>
<span data-ttu-id="2d15c-210">웹 앱에 대한 사용자 지정 도메인 이름을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-210">Add custom domain names for your web app.</span></span> <span data-ttu-id="2d15c-211">자세한 내용은 [Azure 앱 서비스에서 웹 앱에 대한 사용자 지정 도메인 이름 구성]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d15c-211">For more information, see [Configure a custom domain name for a web app in Azure App Service].</span></span>

<span data-ttu-id="2d15c-212">도메인 이름을 보려면 **모든 설정** > **사용자 지정 도메인 및 SSL**을 사용하여 웹앱을 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-212">To view your domain names, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="deployments"></a><span data-ttu-id="2d15c-213">배포</span><span class="sxs-lookup"><span data-stu-id="2d15c-213">Deployments</span></span>
* <span data-ttu-id="2d15c-214">연속 배포를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-214">Set up continuous deployment.</span></span> <span data-ttu-id="2d15c-215">[Azure App Service에서 Web Apps 배포를 위해 Git 사용](web-sites-deploy.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d15c-215">See [Using Git to deploy Web Apps in Azure App Service](web-sites-deploy.md).</span></span>
* <span data-ttu-id="2d15c-216">배포 슬롯입니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-216">Deployment slots.</span></span> <span data-ttu-id="2d15c-217">[Azure 앱 서비스에서 웹앱에 대한 스테이징 환경으로 배포]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d15c-217">See [Deploy to Staging Environments for Web Apps in Azure App Service].</span></span>

<span data-ttu-id="2d15c-218">배포 슬롯을 보려면 **모든 설정** > **배포 슬롯**을 사용하여 웹앱을 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-218">To view your deployment slots, click **All Settings** > **Deployment slots**.</span></span>

### <a name="monitoring"></a><span data-ttu-id="2d15c-219">모니터링</span><span class="sxs-lookup"><span data-stu-id="2d15c-219">Monitoring</span></span>
<span data-ttu-id="2d15c-220">기본 또는 표준 모드에서는 지리적으로 분산된 최대 세 곳의 HTTP 또는 HTTPS 끝점에 대한 가용성을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-220">In Basic or Standard mode, you can  test the availability of HTTP or HTTPS endpoints, from up to three geo-distributed locations.</span></span> <span data-ttu-id="2d15c-221">HTTP 응답 코드가 오류(4xx 또는 5xx)이거나 응답에 30초 넘게 걸리는 경우 모니터링 테스트가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-221">A monitoring test fails if the HTTP response code is an error (4xx or 5xx) or the response takes more than 30 seconds.</span></span> <span data-ttu-id="2d15c-222">지정된 모든 위치에서 모니터링 테스트가 성공하는 경우 끝점은 사용 가능한 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-222">An endpoint is considered available if the monitoring tests succeed from all the specified locations.</span></span> 

<span data-ttu-id="2d15c-223">자세한 내용은 [방법: 웹 끝점 모니터링]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d15c-223">For more information, see [How to: Monitor web endpoint status].</span></span>

> [!NOTE]
> <span data-ttu-id="2d15c-224">Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험]으로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-224">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="2d15c-225">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d15c-225">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="2d15c-226">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2d15c-226">Next steps</span></span>
* <span data-ttu-id="2d15c-227">[Azure 앱 서비스에서 사용자 지정 도메인 이름 구성]</span><span class="sxs-lookup"><span data-stu-id="2d15c-227">[Configure a custom domain name in Azure App Service]</span></span>
* <span data-ttu-id="2d15c-228">[Azure 앱 서비스에서 앱에 대한 HTTPS를 사용하도록 설정]</span><span class="sxs-lookup"><span data-stu-id="2d15c-228">[Enable HTTPS for an app in Azure App Service]</span></span>
* <span data-ttu-id="2d15c-229">[Azure 앱 서비스에서 웹 앱 크기 조정]</span><span class="sxs-lookup"><span data-stu-id="2d15c-229">[Scale a web app in Azure App Service]</span></span>
* <span data-ttu-id="2d15c-230">[Azure 앱 서비스에서 웹 앱에 대한 기본 사항 모니터링]</span><span class="sxs-lookup"><span data-stu-id="2d15c-230">[Monitoring basics for Web Apps in Azure App Service]</span></span>

<!-- URL List -->

<span data-ttu-id="2d15c-231">[ASP.NET SignalR]: http://www.asp.net/signalr</span><span class="sxs-lookup"><span data-stu-id="2d15c-231">[ASP.NET SignalR]: http://www.asp.net/signalr</span></span>
<span data-ttu-id="2d15c-232">[Azure Portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="2d15c-232">[Azure Portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="2d15c-233">[Azure 앱 서비스에서 사용자 지정 도메인 이름 구성]: ./app-service-web-tutorial-custom-domain.md</span><span class="sxs-lookup"><span data-stu-id="2d15c-233">[Configure a custom domain name in Azure App Service]: ./app-service-web-tutorial-custom-domain.md</span></span>
<span data-ttu-id="2d15c-234">[Azure 앱 서비스에서 웹앱에 대한 스테이징 환경으로 배포]: ./web-sites-staged-publishing.md</span><span class="sxs-lookup"><span data-stu-id="2d15c-234">[Deploy to Staging Environments for Web Apps in Azure App Service]: ./web-sites-staged-publishing.md</span></span>
<span data-ttu-id="2d15c-235">[Azure 앱 서비스에서 앱에 대한 HTTPS를 사용하도록 설정]: ./app-service-web-tutorial-custom-ssl.md</span><span class="sxs-lookup"><span data-stu-id="2d15c-235">[Enable HTTPS for an app in Azure App Service]: ./app-service-web-tutorial-custom-ssl.md</span></span>
<span data-ttu-id="2d15c-236">[방법: 웹 끝점 모니터링]: http://go.microsoft.com/fwLink/?LinkID=279906</span><span class="sxs-lookup"><span data-stu-id="2d15c-236">[How to: Monitor web endpoint status]: http://go.microsoft.com/fwLink/?LinkID=279906</span></span>
<span data-ttu-id="2d15c-237">[Azure 앱 서비스에서 웹 앱에 대한 기본 사항 모니터링]: ./web-sites-monitor.md</span><span class="sxs-lookup"><span data-stu-id="2d15c-237">[Monitoring basics for Web Apps in Azure App Service]: ./web-sites-monitor.md</span></span>
<span data-ttu-id="2d15c-238">[파이프라인 모드]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application</span><span class="sxs-lookup"><span data-stu-id="2d15c-238">[pipeline mode]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application</span></span>
<span data-ttu-id="2d15c-239">[Azure 앱 서비스에서 웹 앱 크기 조정]: ./web-sites-scale.md</span><span class="sxs-lookup"><span data-stu-id="2d15c-239">[Scale a web app in Azure App Service]: ./web-sites-scale.md</span></span>
<span data-ttu-id="2d15c-240">[socket.io]: ./web-sites-nodejs-chat-app-socketio.md</span><span class="sxs-lookup"><span data-stu-id="2d15c-240">[socket.io]: ./web-sites-nodejs-chat-app-socketio.md</span></span>
<span data-ttu-id="2d15c-241">[App Service 체험]: https://azure.microsoft.com/try/app-service/</span><span class="sxs-lookup"><span data-stu-id="2d15c-241">[Try App Service]: https://azure.microsoft.com/try/app-service/</span></span>

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
