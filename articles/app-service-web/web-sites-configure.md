---
title: "Azure 앱 서비스의 aaaConfigure 웹 응용 프로그램"
description: "어떻게 tooconfigure Azure 앱 서비스의 웹 앱"
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
ms.openlocfilehash: 8697ab6f21cfeb470e11f0d82c68692d43142fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a><span data-ttu-id="69d12-103">Azure 앱 서비스에서 웹 앱 구성</span><span class="sxs-lookup"><span data-stu-id="69d12-103">Configure web apps in Azure App Service</span></span>
<span data-ttu-id="69d12-104">이 항목에서는 방법을 사용 하 여 웹 응용 프로그램 tooconfigure hello 설명 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-104">This topic explains how tooconfigure a web app using hello [Azure Portal].</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a><span data-ttu-id="69d12-105">응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="69d12-105">Application settings</span></span>
1. <span data-ttu-id="69d12-106">Hello에 [Azure 포털]열고 hello 웹 앱에 대 한 hello 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-106">In hello [Azure Portal], open hello blade for hello web app.</span></span>
2. <span data-ttu-id="69d12-107">**모든 설정**을 클릭합니다</span><span class="sxs-lookup"><span data-stu-id="69d12-107">Click **All Settings**.</span></span>
3. <span data-ttu-id="69d12-108">**응용 프로그램 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-108">Click **Application Settings**.</span></span>

![응용 프로그램 설정][configure01]

<span data-ttu-id="69d12-110">hello **응용 프로그램 설정** 블레이드는 여러 범주로 그룹화 된 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-110">hello **Application settings** blade has settings grouped under several categories.</span></span>

### <a name="general-settings"></a><span data-ttu-id="69d12-111">일반 설정</span><span class="sxs-lookup"><span data-stu-id="69d12-111">General settings</span></span>
<span data-ttu-id="69d12-112">**프레임워크 버전**.</span><span class="sxs-lookup"><span data-stu-id="69d12-112">**Framework versions**.</span></span> <span data-ttu-id="69d12-113">앱에서 다음 프레임워크를 사용하는 경우 이러한 옵션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-113">Set these options if your app uses any these frameworks:</span></span> 

* <span data-ttu-id="69d12-114">**.NET framework**: 집합 hello.NET framework 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-114">**.NET Framework**: Set hello .NET framework version.</span></span> 
* <span data-ttu-id="69d12-115">**PHP**: 집합 hello PHP 버전 또는 **OFF** toodisable PHP 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-115">**PHP**: Set hello PHP version, or **OFF** toodisable PHP.</span></span> 
* <span data-ttu-id="69d12-116">**Java**: 선택 hello Java 버전 또는 **OFF** toodisable Java 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-116">**Java**: Select hello Java version or **OFF** toodisable Java.</span></span> <span data-ttu-id="69d12-117">사용 하 여 hello **웹 컨테이너** Tomcat 및 Jetty 버전 간의 toochoose 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-117">Use hello **Web Container** option toochoose between Tomcat and Jetty versions.</span></span>
* <span data-ttu-id="69d12-118">**Python**: 선택 hello Python 버전 또는 **OFF** toodisable Python 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-118">**Python**: Select hello Python version, or **OFF** toodisable Python.</span></span>

<span data-ttu-id="69d12-119">기술적인 이유로 Java 앱에 대 한 사용할 hello.NET, PHP 및 Python 옵션이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-119">For technical reasons, enabling Java for your app disables hello .NET, PHP, and Python options.</span></span>

<span data-ttu-id="69d12-120"><a name="platform"></a>
**플랫폼**.</span><span class="sxs-lookup"><span data-stu-id="69d12-120"><a name="platform"></a>
**Platform**.</span></span> <span data-ttu-id="69d12-121">응용 프로그램이 32비트 또는 64비트 환경에서 실행되는지 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-121">Selects whether your web app runs in a 32-bit or 64-bit environment.</span></span> <span data-ttu-id="69d12-122">hello 64 비트 환경에 기본 또는 표준 모드가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-122">hello 64-bit environment requires Basic or Standard mode.</span></span> <span data-ttu-id="69d12-123">무료 및 공유 모드는 항상 32비트 환경에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-123">Free and Shared modes always run in a 32-bit environment.</span></span>

<span data-ttu-id="69d12-124">**웹 소켓**.</span><span class="sxs-lookup"><span data-stu-id="69d12-124">**Web Sockets**.</span></span> <span data-ttu-id="69d12-125">설정 **ON** tooenable hello WebSocket 프로토콜 예: 웹 앱을 사용 하는 경우 [ASP.NET SignalR] 또는 [socket.io]합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-125">Set **ON** tooenable hello WebSocket protocol; for example, if your web app uses [ASP.NET SignalR] or [socket.io].</span></span>

<span data-ttu-id="69d12-126"><a name="alwayson"></a>
**Always On**.</span><span class="sxs-lookup"><span data-stu-id="69d12-126"><a name="alwayson"></a>
**Always On**.</span></span> <span data-ttu-id="69d12-127">기본적으로 웹 앱은 일정 기간 동안 유휴 상태인 경우 언로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-127">By default, web apps are unloaded if they are idle for some period of time.</span></span> <span data-ttu-id="69d12-128">Hello 시스템을 리소스를 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-128">This lets hello system conserve resources.</span></span> <span data-ttu-id="69d12-129">기본 또는 표준 모드에서는 사용할 수 있습니다 **Always On** tookeep hello 응용 프로그램이 항상 hello를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-129">In Basic or Standard mode, you can enable **Always On** tookeep hello app loaded all hello time.</span></span> <span data-ttu-id="69d12-130">연속 Webjob을 실행 하는 응용 프로그램 또는 CRON 식을 사용 하 여 WebJobs 실행 발생, 설정 해야 하는 경우 **Always On**, 또는 hello 웹 작업이 안정적으로 실행 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-130">If your app runs continuous WebJobs or runs WebJobs triggered using a CRON expression, you should enable **Always On**, or hello web jobs may not run reliably.</span></span>

<span data-ttu-id="69d12-131">**관리되는 파이프라인 버전**.</span><span class="sxs-lookup"><span data-stu-id="69d12-131">**Managed Pipeline Version**.</span></span> <span data-ttu-id="69d12-132">집합 hello IIS [파이프라인 모드]합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-132">Sets hello IIS [pipeline mode].</span></span> <span data-ttu-id="69d12-133">둡니다 이전 버전의 IIS 필요로 하는 레거시 앱이 있는 경우가 아니면이 tooIntegrated (hello 기본값)를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-133">Leave this set tooIntegrated (hello default) unless you have a legacy app that requires an older version of IIS.</span></span>

<span data-ttu-id="69d12-134">**자동 교체**.</span><span class="sxs-lookup"><span data-stu-id="69d12-134">**Auto Swap**.</span></span> <span data-ttu-id="69d12-135">배포 슬롯에 대 한 자동 전환을 사용 하도록 설정 하면 앱 서비스를 자동으로 바꾸어 hello 웹 응용 프로그램 프로덕션 환경으로 업데이트 toothat 슬롯을 푸시할 때 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-135">If you enable Auto Swap for a deployment slot, App Service will automatically swap hello web app into production when you push an update toothat slot.</span></span> <span data-ttu-id="69d12-136">자세한 내용은 참조 [toostaging 슬롯 Azure 앱 서비스의 웹 앱에 대 한 배포](web-sites-staged-publishing.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-136">For more information, see [Deploy toostaging slots for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span>

### <a name="debugging"></a><span data-ttu-id="69d12-137">디버그</span><span class="sxs-lookup"><span data-stu-id="69d12-137">Debugging</span></span>
<span data-ttu-id="69d12-138">**원격 디버깅**.</span><span class="sxs-lookup"><span data-stu-id="69d12-138">**Remote Debugging**.</span></span> <span data-ttu-id="69d12-139">원격 디버깅을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-139">Enables remote debugging.</span></span> <span data-ttu-id="69d12-140">Hello 원격 디버거 tooyour 웹 앱을 직접 사용 하도록 설정 하면 Visual Studio tooconnect에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-140">When enabled, you can use hello remote debugger in Visual Studio tooconnect directly tooyour web app.</span></span> <span data-ttu-id="69d12-141">원격 디버깅은 48시간 동안 사용 가능한 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-141">Remote debugging will remain enabled for 48 hours.</span></span> 

### <a name="app-settings"></a><span data-ttu-id="69d12-142">앱 설정</span><span class="sxs-lookup"><span data-stu-id="69d12-142">App settings</span></span>
<span data-ttu-id="69d12-143">이 섹션에는 시작 시 웹 앱이 로드하는 이름/값 쌍을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-143">This section contains name/value pairs that you web app will load on start up.</span></span> 

* <span data-ttu-id="69d12-144">.NET 앱의 경우, 이 설정은 런타임 시 .NET 구성 `AppSettings`으로 주입되어 기존 설정을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-144">For .NET apps, these settings are injected into your .NET configuration `AppSettings` at runtime, overriding existing settings.</span></span> 
* <span data-ttu-id="69d12-145">PHP, Python, Java 및 Node 응용 프로그램에서는 런타임에 환경 변수로 이러한 설정에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-145">PHP, Python, Java and Node applications can access these settings as environment variables at runtime.</span></span> <span data-ttu-id="69d12-146">각 응용 프로그램 설정에 대해 두 개의 환경 변수 만들어집니다. hello 지정 된 이름의 hello 응용 프로그램 설정 항목 및 APPSETTING_의 접두사와 함께 다른 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-146">For each app setting, two environment variables are created; one with hello name specified by hello app setting entry, and another with a prefix of APPSETTING_.</span></span> <span data-ttu-id="69d12-147">둘 다 포함 hello 동일한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-147">Both contain hello same value.</span></span>

### <a name="connection-strings"></a><span data-ttu-id="69d12-148">연결 문자열</span><span class="sxs-lookup"><span data-stu-id="69d12-148">Connection strings</span></span>
<span data-ttu-id="69d12-149">연결된 리소스의 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-149">Connection strings for linked resources.</span></span> 

<span data-ttu-id="69d12-150">.NET 응용 프로그램에 대 한이 연결 문자열은.NET 구성에 삽입 `connectionStrings` hello 키가 동일한 기존 항목을 재정의 하는 런타임 시 설정 hello 연결 된 데이터베이스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-150">For .NET apps, these connection strings are injected into your .NET configuration `connectionStrings` settings at runtime, overriding existing entries where hello key equals hello linked database name.</span></span> 

<span data-ttu-id="69d12-151">PHP, Python, Java 및 노드 응용 프로그램의 경우 이러한 설정이 hello 연결 유형 접두사로 런타임 시 환경 변수로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-151">For PHP, Python, Java and Node applications, these settings will be available as environment variables at runtime, prefixed with hello connection type.</span></span> <span data-ttu-id="69d12-152">hello 환경 변수 접두사는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-152">hello environment variable prefixes are as follows:</span></span> 

* <span data-ttu-id="69d12-153">SQL Server: `SQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="69d12-153">SQL Server: `SQLCONNSTR_`</span></span>
* <span data-ttu-id="69d12-154">MySQL: `MYSQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="69d12-154">MySQL: `MYSQLCONNSTR_`</span></span>
* <span data-ttu-id="69d12-155">SQL 데이터베이스: `SQLAZURECONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="69d12-155">SQL Database: `SQLAZURECONNSTR_`</span></span>
* <span data-ttu-id="69d12-156">사용자 지정: `CUSTOMCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="69d12-156">Custom: `CUSTOMCONNSTR_`</span></span>

<span data-ttu-id="69d12-157">MySql 연결 문자열 이름이 지정 된 경우 등 `connectionstring1`, hello 환경 변수를 통해 액세스 됩니다 `MYSQLCONNSTR_connectionString1`합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-157">For example, if a MySql connection string were named `connectionstring1`, it would be accessed through hello environment variable `MYSQLCONNSTR_connectionString1`.</span></span>

### <a name="default-documents"></a><span data-ttu-id="69d12-158">기본 문서</span><span class="sxs-lookup"><span data-stu-id="69d12-158">Default documents</span></span>
<span data-ttu-id="69d12-159">hello 기본 문서는 웹 사이트에 대 한 hello 루트 URL에 표시 되는 hello 웹 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-159">hello default document is hello web page that is displayed at hello root URL for a website.</span></span>  <span data-ttu-id="69d12-160">hello hello 목록에서 첫 번째 일치 하는 파일 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-160">hello first matching file in hello list is used.</span></span> 

<span data-ttu-id="69d12-161">웹 앱에서는 정적 콘텐츠를 제공하는 대신 URL을 기반으로 라우팅되는 모듈을 사용할 수 있으며, 이 경우에도 기본 문서는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-161">Web apps might use modules that route based on URL, rather than serving static content, in which case there is no default document as such.</span></span>    

### <a name="handler-mappings"></a><span data-ttu-id="69d12-162">처리기 매핑</span><span class="sxs-lookup"><span data-stu-id="69d12-162">Handler mappings</span></span>
<span data-ttu-id="69d12-163">이 영역 tooadd 사용자 지정 스크립트 프로세서 toohandle 요청을 사용 하 여 특정 파일 확장명에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-163">Use this area tooadd custom script processors toohandle requests for specific file extensions.</span></span> 

* <span data-ttu-id="69d12-164">**확장명**.</span><span class="sxs-lookup"><span data-stu-id="69d12-164">**Extension**.</span></span> <span data-ttu-id="69d12-165">예: *.php 또는 handler.fcgi hello 파일 확장명 toobe 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-165">hello file extension toobe handled, such as *.php or handler.fcgi.</span></span> 
* <span data-ttu-id="69d12-166">**스크립트 프로세서 경로**.</span><span class="sxs-lookup"><span data-stu-id="69d12-166">**Script Processor Path**.</span></span> <span data-ttu-id="69d12-167">hello hello 스크립트 프로세서의 절대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-167">hello absolute path of hello script processor.</span></span> <span data-ttu-id="69d12-168">Hello 파일 확장명과 일치 하는 요청 toofiles hello 스크립트 프로세서에 의해 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-168">Requests toofiles that match hello file extension will be processed by hello script processor.</span></span> <span data-ttu-id="69d12-169">Hello 경로 사용 `D:\home\site\wwwroot` toorefer tooyour 응용 프로그램의 루트 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-169">Use hello path `D:\home\site\wwwroot` toorefer tooyour app's root directory.</span></span>
* <span data-ttu-id="69d12-170">**추가 인수**.</span><span class="sxs-lookup"><span data-stu-id="69d12-170">**Additional Arguments**.</span></span> <span data-ttu-id="69d12-171">Hello 스크립트 프로세서에 대 한 선택적인 명령줄 인수</span><span class="sxs-lookup"><span data-stu-id="69d12-171">Optional command-line arguments for hello script processor</span></span> 

### <a name="virtual-applications-and-directories"></a><span data-ttu-id="69d12-172">가상 응용 프로그램 및 디렉터리</span><span class="sxs-lookup"><span data-stu-id="69d12-172">Virtual applications and directories</span></span>
<span data-ttu-id="69d12-173">tooconfigure 가상 응용 프로그램 및 디렉터리의 경우 각 가상 디렉터리와 그에 해당 하는 실제 경로 상대 toohello 웹 사이트 루트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-173">tooconfigure virtual applications and directories, specify each virtual directory and its corresponding physical path relative toohello website root.</span></span> <span data-ttu-id="69d12-174">필요에 따라 hello를 선택할 수 있습니다 **응용 프로그램** 확인란 toomark 응용 프로그램으로 가상 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-174">Optionally, you can select hello **Application** checkbox toomark a virtual directory as an application.</span></span>

## <a name="enabling-diagnostic-logs"></a><span data-ttu-id="69d12-175">진단 로그를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="69d12-175">Enabling diagnostic logs</span></span>
<span data-ttu-id="69d12-176">tooenable 진단 로그:</span><span class="sxs-lookup"><span data-stu-id="69d12-176">tooenable diagnostic logs:</span></span>

1. <span data-ttu-id="69d12-177">웹 앱에 대 한 hello 블레이드에서 클릭 **모든 설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-177">In hello blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="69d12-178">**진단 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-178">Click **Diagnostic logs**.</span></span> 

<span data-ttu-id="69d12-179">로깅을 지원하는 웹 응용 프로그램의 진단 정보를 기록하는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-179">Options for writing diagnostic logs from a web application that supports logging:</span></span> 

* <span data-ttu-id="69d12-180">**응용 프로그램 로깅**.</span><span class="sxs-lookup"><span data-stu-id="69d12-180">**Application Logging**.</span></span> <span data-ttu-id="69d12-181">Toohello 파일 시스템 응용 프로그램 로그를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-181">Writes application logs toohello file system.</span></span> <span data-ttu-id="69d12-182">로깅은 12시간 동안 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-182">Logging lasts for a period of 12 hours.</span></span> 

<span data-ttu-id="69d12-183">**수준**.</span><span class="sxs-lookup"><span data-stu-id="69d12-183">**Level**.</span></span> <span data-ttu-id="69d12-184">응용 프로그램 로깅을 사용 하는 경우이 옵션 hello 기록 된 (오류, 경고, 정보 또는 Verbose) 되는 정보의 양을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-184">When application logging is enabled, this option specifies hello amount of information that will be recorded (Error, Warning, Information, or Verbose).</span></span>

<span data-ttu-id="69d12-185">**웹 서버 로깅**.</span><span class="sxs-lookup"><span data-stu-id="69d12-185">**Web server logging**.</span></span> <span data-ttu-id="69d12-186">로그는 hello W3C 확장된 로그 파일 형식에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-186">Logs are saved in hello W3C extended log file format.</span></span> 

<span data-ttu-id="69d12-187">**자세한 오류 메시지**.</span><span class="sxs-lookup"><span data-stu-id="69d12-187">**Detailed error messages**.</span></span> <span data-ttu-id="69d12-188">자세한 오류 메시지는.htm 파일로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-188">Saves detailed error messages .htm files.</span></span> <span data-ttu-id="69d12-189">hello 파일 /LogFiles/DetailedErrors 아래 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-189">hello files are saved under /LogFiles/DetailedErrors.</span></span> 

<span data-ttu-id="69d12-190">**실패한 요청 추적**.</span><span class="sxs-lookup"><span data-stu-id="69d12-190">**Failed request tracing**.</span></span> <span data-ttu-id="69d12-191">로그 요청 tooXML 파일에 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-191">Logs failed requests tooXML files.</span></span> <span data-ttu-id="69d12-192">hello 파일 저장 된/로그 파일이/W3SVC*xxx*여기서 xxx는 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-192">hello files are saved under /LogFiles/W3SVC*xxx*, where xxx is a unique identifier.</span></span> <span data-ttu-id="69d12-193">이 폴더에는 하나의 XSL 파일 및 하나 이상의 XML 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-193">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="69d12-194">서식을 지정 하 고 hello XML 파일의 내용을 hello 필터링 기능을 제공 하기 때문에 있는지 toodownload hello XSL 파일을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-194">Make sure toodownload hello XSL file, because it provides functionality for formatting and filtering hello contents of hello XML files.</span></span>

<span data-ttu-id="69d12-195">tooview hello 로그 파일을 만들어야 합니다 FTP 자격 증명 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-195">tooview hello log files, you must create FTP credentials, as follows:</span></span>

1. <span data-ttu-id="69d12-196">웹 앱에 대 한 hello 블레이드에서 클릭 **모든 설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-196">In hello blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="69d12-197">**배포 자격 증명**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-197">Click **Deployment credentials**.</span></span>
3. <span data-ttu-id="69d12-198">사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-198">Enter a user name and password.</span></span>
4. <span data-ttu-id="69d12-199">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-199">Click **Save**.</span></span>

![배포 자격 증명 설정][configure03]

<span data-ttu-id="69d12-201">hello 전체 FTP 사용자 이름이 "app\username" 여기서 *앱* hello 웹 응용 프로그램 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-201">hello full FTP user name is “app\username” where *app* is hello name of your web app.</span></span> <span data-ttu-id="69d12-202">hello 사용자 이름에에서 나열 된 hello 웹 앱 블레이드 아래 **Essentials**합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-202">hello username is listed in hello web app blade, under **Essentials**.</span></span>  

![FTP 배포 자격 증명][configure02]

## <a name="other-configuration-tasks"></a><span data-ttu-id="69d12-204">기타 구성 작업</span><span class="sxs-lookup"><span data-stu-id="69d12-204">Other configuration tasks</span></span>
### <a name="ssl"></a><span data-ttu-id="69d12-205">SSL</span><span class="sxs-lookup"><span data-stu-id="69d12-205">SSL</span></span>
<span data-ttu-id="69d12-206">기본 또는 표준 모드에서는 사용자 지정 도메인에 대해 SSL 인증서를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-206">In Basic or Standard mode, you can upload SSL certificates for a custom domain.</span></span> <span data-ttu-id="69d12-207">자세한 내용은 [웹 앱에 대한 HTTPS 사용]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69d12-207">For more information, see [Enable HTTPS for a web app].</span></span> 

<span data-ttu-id="69d12-208">tooview 업로드 된 인증서를 클릭 하 여 **모든 설정을** > **사용자 지정 도메인 및 SSL**합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-208">tooview your uploaded certificates, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="domain-names"></a><span data-ttu-id="69d12-209">도메인 이름</span><span class="sxs-lookup"><span data-stu-id="69d12-209">Domain names</span></span>
<span data-ttu-id="69d12-210">웹 앱에 대한 사용자 지정 도메인 이름을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-210">Add custom domain names for your web app.</span></span> <span data-ttu-id="69d12-211">자세한 내용은 [Azure 앱 서비스에서 웹 앱에 대한 사용자 지정 도메인 이름 구성]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69d12-211">For more information, see [Configure a custom domain name for a web app in Azure App Service].</span></span>

<span data-ttu-id="69d12-212">tooview 도메인 이름, 클릭 **모든 설정을** > **사용자 지정 도메인 및 SSL**합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-212">tooview your domain names, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="deployments"></a><span data-ttu-id="69d12-213">배포</span><span class="sxs-lookup"><span data-stu-id="69d12-213">Deployments</span></span>
* <span data-ttu-id="69d12-214">연속 배포를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-214">Set up continuous deployment.</span></span> <span data-ttu-id="69d12-215">참조 [Git를 사용 하 여 toodeploy Azure 앱 서비스에서 웹 앱](web-sites-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-215">See [Using Git toodeploy Web Apps in Azure App Service](web-sites-deploy.md).</span></span>
* <span data-ttu-id="69d12-216">배포 슬롯입니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-216">Deployment slots.</span></span> <span data-ttu-id="69d12-217">참조 [tooStaging 환경을 Azure 앱 서비스의 웹 앱에 대 한 배포]합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-217">See [Deploy tooStaging Environments for Web Apps in Azure App Service].</span></span>

<span data-ttu-id="69d12-218">tooview 배포 슬롯을 클릭 하 여 **모든 설정을** > **배포 슬롯**합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-218">tooview your deployment slots, click **All Settings** > **Deployment slots**.</span></span>

### <a name="monitoring"></a><span data-ttu-id="69d12-219">모니터링</span><span class="sxs-lookup"><span data-stu-id="69d12-219">Monitoring</span></span>
<span data-ttu-id="69d12-220">기본 또는 표준 모드에서 HTTP 또는 HTTPS 끝점의 가용성을 hello toothree 지리적으로 분산 된 위치를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-220">In Basic or Standard mode, you can  test hello availability of HTTP or HTTPS endpoints, from up toothree geo-distributed locations.</span></span> <span data-ttu-id="69d12-221">Hello HTTP 응답 코드는 오류 (4xx 또는 5xx) 이거나 hello 응답 하는 데 30 초 이상 모니터링 테스트가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-221">A monitoring test fails if hello HTTP response code is an error (4xx or 5xx) or hello response takes more than 30 seconds.</span></span> <span data-ttu-id="69d12-222">끝점에서 모든 hello 모니터링 테스트가 성공 하는 경우 사용할 수 있는 것으로 간주 됩니다 hello 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-222">An endpoint is considered available if hello monitoring tests succeed from all hello specified locations.</span></span> 

<span data-ttu-id="69d12-223">자세한 내용은 [방법: 웹 끝점 모니터링]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69d12-223">For more information, see [How to: Monitor web endpoint status].</span></span>

> [!NOTE]
> <span data-ttu-id="69d12-224">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도]앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-224">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="69d12-225">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69d12-225">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="69d12-226">다음 단계</span><span class="sxs-lookup"><span data-stu-id="69d12-226">Next steps</span></span>
* <span data-ttu-id="69d12-227">[Azure 앱 서비스에서 사용자 지정 도메인 이름 구성]</span><span class="sxs-lookup"><span data-stu-id="69d12-227">[Configure a custom domain name in Azure App Service]</span></span>
* <span data-ttu-id="69d12-228">[Azure 앱 서비스에서 앱에 대한 HTTPS를 사용하도록 설정]</span><span class="sxs-lookup"><span data-stu-id="69d12-228">[Enable HTTPS for an app in Azure App Service]</span></span>
* <span data-ttu-id="69d12-229">[Azure 앱 서비스에서 웹 앱 크기 조정]</span><span class="sxs-lookup"><span data-stu-id="69d12-229">[Scale a web app in Azure App Service]</span></span>
* <span data-ttu-id="69d12-230">[Azure 앱 서비스에서 웹 앱에 대한 기본 사항 모니터링]</span><span class="sxs-lookup"><span data-stu-id="69d12-230">[Monitoring basics for Web Apps in Azure App Service]</span></span>

<!-- URL List -->

[ASP.NET SignalR]: http://www.asp.net/signalr
[Azure 포털]: https://portal.azure.com/
[Azure 앱 서비스에서 사용자 지정 도메인 이름 구성]: ./app-service-web-tutorial-custom-domain.md
[tooStaging 환경을 Azure 앱 서비스의 웹 앱에 대 한 배포]: ./web-sites-staged-publishing.md
[Azure 앱 서비스에서 앱에 대한 HTTPS를 사용하도록 설정]: ./app-service-web-tutorial-custom-ssl.md
[방법: 웹 끝점 모니터링]: http://go.microsoft.com/fwLink/?LinkID=279906
[Azure 앱 서비스에서 웹 앱에 대한 기본 사항 모니터링]: ./web-sites-monitor.md
[파이프라인 모드]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application
[Azure 앱 서비스에서 웹 앱 크기 조정]: ./web-sites-scale.md
[socket.io]: ./web-sites-nodejs-chat-app-socketio.md
[앱 서비스 시도]: https://azure.microsoft.com/try/app-service/

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
