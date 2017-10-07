---
title: "Azure 앱 서비스 웹 앱에서 PHP aaaConfigure | Microsoft Docs"
description: "Tooconfigure 기본 PHP 설치 hello 또는 PHP 설치를 사용자 지정 Azure 앱 서비스에서 웹 앱에 대 한 추가 방법에 대해 알아봅니다."
services: app-service
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 95c4072b-8570-496b-9c48-ee21a223fb60
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 2e461e4a269a4ce5614f5f05560f38bc53066251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-php-in-azure-app-service-web-apps"></a><span data-ttu-id="d6660-103">Azure 앱 서비스 웹 앱에서 PHP 구성</span><span class="sxs-lookup"><span data-stu-id="d6660-103">Configure PHP in Azure App Service Web Apps</span></span>
## <a name="introduction"></a><span data-ttu-id="d6660-104">소개</span><span class="sxs-lookup"><span data-stu-id="d6660-104">Introduction</span></span>
<span data-ttu-id="d6660-105">이 가이드에서는 설명 어떻게에서 웹 앱에 대 한 기본 제공 PHP 런타임에 hello를 tooconfigure [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714), 제공 된 사용자 지정 PHP 런타임 및 확장을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-105">This guide will show you how tooconfigure hello built-in PHP runtime for Web Apps in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), provide a custom PHP runtime, and enable extensions.</span></span> <span data-ttu-id="d6660-106">앱 서비스 toouse hello에 대 한 등록 [무료 평가판]합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-106">toouse App Service, sign up for hello [free trial].</span></span> <span data-ttu-id="d6660-107">tooget hello 가장이 가이드에서 먼저 만들어야 PHP 웹 응용 프로그램에 앱 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-107">tooget hello most from this guide, you should first create a PHP web app in App Service.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-hello-built-in-php-version"></a><span data-ttu-id="d6660-108">방법: 변경 hello 기본 제공 PHP 버전</span><span class="sxs-lookup"><span data-stu-id="d6660-108">How to: Change hello built-in PHP version</span></span>
<span data-ttu-id="d6660-109">기본적으로 PHP 5.5는 앱 서비스 웹 앱을 만들 때 설치하여 바로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-109">By default, PHP 5.5 is installed and immediately available for use when you create an App Service web app.</span></span> <span data-ttu-id="d6660-110">가장 좋은 방법은 toosee hello 이용할 수 있는 릴리스 수정 버전을 기본 구성 hello 및 hello 사용된 확장은 toodeploy hello를 호출 하는 스크립트 [phpinfo ()] 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-110">hello best way toosee hello available release revision, its default configuration, and hello enabled extensions is toodeploy a script that calls hello [phpinfo()] function.</span></span>

<span data-ttu-id="d6660-111">PHP 5.6 및 PHP 7.0 버전도 사용할 수 있지만 기본적으로는 사용하도록 설정되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-111">PHP 5.6 and PHP 7.0 versions are also available, but not enabled by default.</span></span> <span data-ttu-id="d6660-112">tooupdate hello PHP 버전을 다음이 방법 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-112">tooupdate hello PHP version, follow one of these methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="d6660-113">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="d6660-113">Azure Portal</span></span>
1. <span data-ttu-id="d6660-114">Hello의 tooyour 웹 앱을 찾아보기 [Azure 포털](https://portal.azure.com) hello에서을 클릭 하 고 **설정을** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-114">Browse tooyour web app in hello [Azure Portal](https://portal.azure.com) and click on hello **Settings** button.</span></span>
   
    ![저장][settings-button]
2. <span data-ttu-id="d6660-116">Hello에서 **설정** 블레이드 선택 **응용 프로그램 설정** hello 새 PHP 버전을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-116">From hello **Settings** blade select **Application Settings** and choose hello new PHP version.</span></span>
   
    ![응용 프로그램 설정][application-settings]
3. <span data-ttu-id="d6660-118">Hello 클릭 **저장** hello hello 위쪽에 단추 **웹 앱 설정** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-118">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![구성 설정 저장][save-button]

### <a name="azure-powershell-windows"></a><span data-ttu-id="d6660-120">Azure PowerShell(Windows)</span><span class="sxs-lookup"><span data-stu-id="d6660-120">Azure PowerShell (Windows)</span></span>
1. <span data-ttu-id="d6660-121">로그인 tooyour 계정 및 Azure PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-121">Open Azure PowerShell, and login tooyour account:</span></span>
   
        PS C:\> Login-AzureRmAccount
2. <span data-ttu-id="d6660-122">Hello 웹 앱에 대 한 hello PHP 버전을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-122">Set hello PHP version for hello web app.</span></span>
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. <span data-ttu-id="d6660-123">hello PHP 버전 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-123">hello PHP version is now set.</span></span> <span data-ttu-id="d6660-124">이러한 설정을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-124">You can confirm these settings:</span></span>
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a><span data-ttu-id="d6660-125">Azure 명령줄 인터페이스(Linux, Mac, Windows)</span><span class="sxs-lookup"><span data-stu-id="d6660-125">Azure Command-Line Interface (Linux, Mac, Windows)</span></span>
<span data-ttu-id="d6660-126">toouse hello Azure 명령줄 인터페이스, 있어야 **Node.js** 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-126">toouse hello Azure Command-Line Interface, you must have **Node.js** installed on your computer.</span></span>

1. <span data-ttu-id="d6660-127">열기 터미널 및 로그인 tooyour 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-127">Open Terminal, and login tooyour account.</span></span>
   
        azure login
2. <span data-ttu-id="d6660-128">Hello 웹 앱에 대 한 hello PHP 버전을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-128">Set hello PHP version for hello web app.</span></span>
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. <span data-ttu-id="d6660-129">hello PHP 버전 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-129">hello PHP version is now set.</span></span> <span data-ttu-id="d6660-130">이러한 설정을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-130">You can confirm these settings:</span></span>
   
        azure site show {app-name}

> [!NOTE] 
> <span data-ttu-id="d6660-131">hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) 위의 해당 toohello는 되는 명령을:</span><span class="sxs-lookup"><span data-stu-id="d6660-131">hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands that are equivalent toohello above are:</span></span>
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-hello-built-in-php-configurations"></a><span data-ttu-id="d6660-132">방법: hello 기본 제공 PHP 구성 변경</span><span class="sxs-lookup"><span data-stu-id="d6660-132">How to: Change hello built-in PHP configurations</span></span>
<span data-ttu-id="d6660-133">모든 기본 제공 PHP 런타임에 대 한 hello 구성 옵션을 다음 hello 단계를 수행 하 여 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-133">For any built-in PHP runtime, you can change any of hello configuration options by following hello steps below.</span></span> <span data-ttu-id="d6660-134">php.ini 지시문에 대한 자세한 내용은 [php.ini 지시문 목록]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6660-134">(For information about php.ini directives, see [List of php.ini directives].)</span></span>

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a><span data-ttu-id="d6660-135">PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL 구성 설정 변경</span><span class="sxs-lookup"><span data-stu-id="d6660-135">Changing PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL configuration settings</span></span>
1. <span data-ttu-id="d6660-136">추가 [. user.ini] 파일 tooyour 루트 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-136">Add a [.user.ini] file tooyour root directory.</span></span>
2. <span data-ttu-id="d6660-137">추가 구성 설정을 toohello `.user.ini` 사용 하 여 파일에 사용 되는 동일한 구문을 hello는 `php.ini` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-137">Add configuration settings toohello `.user.ini` file using hello same syntax you would use in a `php.ini` file.</span></span> <span data-ttu-id="d6660-138">예를 들어, tooturn hello 하려는 경우 `display_errors` 설정 설정 및 설정 `upload_max_filesize` too10M를 설정 하면 `.user.ini` 파일에이 텍스트는 포함:</span><span class="sxs-lookup"><span data-stu-id="d6660-138">For example, if you wanted tooturn hello `display_errors` setting on and set `upload_max_filesize` setting too10M, your `.user.ini` file would contain this text:</span></span>
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on toowrite errors tood:\home\LogFiles\php_errors.log
        ; log_errors=On
3. <span data-ttu-id="d6660-139">웹 앱에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-139">Deploy your web app.</span></span>
4. <span data-ttu-id="d6660-140">Hello 웹 응용 프로그램을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-140">Restart hello web app.</span></span> <span data-ttu-id="d6660-141">(다시 시작 해야만 hello 빈도 PHP 읽기 때문에 `.user.ini` 파일 hello에 의해 제한 `user_ini.cache_ttl` 시스템 수준 설정 이므로 300 초 (5 분) 기본적으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-141">(Restarting is necessary because hello frequency with which PHP reads `.user.ini` files is governed by hello `user_ini.cache_ttl` setting, which is a system level setting and is 300 seconds (5 minutes) by default.</span></span> <span data-ttu-id="d6660-142">Hello 웹 앱을 다시 시작 하면 PHP tooread hello hello에 새 설정이 강제로 `.user.ini` 파일입니다.)</span><span class="sxs-lookup"><span data-stu-id="d6660-142">Restarting hello web app forces PHP tooread hello new settings in hello `.user.ini` file.)</span></span>

<span data-ttu-id="d6660-143">대체 toousing으로는 `.user.ini` 파일인 hello를 사용할 수 있습니다 [ini_set()] 시스템 수준 지시문 없는 스크립트 tooset 구성 옵션에는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-143">As an alternative toousing a `.user.ini` file, you can use hello [ini_set()] function in scripts tooset configuration options that are not system-level directives.</span></span>

### <a name="changing-phpinisystem-configuration-settings"></a><span data-ttu-id="d6660-144">PHP\_INI\_SYSTEM 구성 설정 변경</span><span class="sxs-lookup"><span data-stu-id="d6660-144">Changing PHP\_INI\_SYSTEM configuration settings</span></span>
1. <span data-ttu-id="d6660-145">Hello 키와 앱 설정 tooyour 웹 응용 프로그램 추가 `PHP_INI_SCAN_DIR` 및 값`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="d6660-145">Add an App Setting tooyour Web App with hello key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
2. <span data-ttu-id="d6660-146">만들기는 `settings.ini` Kudu 콘솔을 사용 하 여 파일 (http://&lt;사이트 이름&gt;. scm.azurewebsite.net) hello에 `d:\home\site\ini` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-146">Create an `settings.ini` file using Kudu Console (http://&lt;site-name&gt;.scm.azurewebsite.net) in hello `d:\home\site\ini` directory.</span></span>
3. <span data-ttu-id="d6660-147">추가 구성 설정을 toohello `settings.ini` 사용 하 여 파일 hello 동일한 구문을 php.ini 파일에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-147">Add configuration settings toohello `settings.ini` file using hello same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="d6660-148">예를 들어, toopoint hello 려 `curl.cainfo` tooa 설정 `*.crt` 파일을 'wincache.maxfilesize' too512K, 설정 설정 프로그램 `settings.ini` 파일에이 텍스트는 포함:</span><span class="sxs-lookup"><span data-stu-id="d6660-148">For example, if you wanted toopoint hello `curl.cainfo` setting tooa `*.crt` file and set 'wincache.maxfilesize' setting too512K, your `settings.ini` file would contain this text:</span></span>
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. <span data-ttu-id="d6660-149">웹 앱 tooload hello 변경 내용을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-149">Restart your Web App tooload hello changes.</span></span>

## <a name="how-to-enable-extensions-in-hello-default-php-runtime"></a><span data-ttu-id="d6660-150">방법: hello 기본 PHP 런타임에서 확장 사용</span><span class="sxs-lookup"><span data-stu-id="d6660-150">How to: Enable extensions in hello default PHP runtime</span></span>
<span data-ttu-id="d6660-151">Extensions toodeploy 호출 하는 스크립트는 hello 이전 섹션, hello 가장 좋은 방법은 toosee hello 기본 PHP 버전, 해당 기본 구성 및 사용 하도록 설정 하는 hello에서 설명한 것 처럼 [phpinfo ()]합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-151">As noted in hello previous section, hello best way toosee hello default PHP version, its default configuration, and hello enabled extensions is toodeploy a script that calls [phpinfo()].</span></span> <span data-ttu-id="d6660-152">아래의 hello 단계를 수행 하는 tooenable 추가 확장:</span><span class="sxs-lookup"><span data-stu-id="d6660-152">tooenable additional extensions, follow hello steps below:</span></span>

### <a name="configure-via-ini-settings"></a><span data-ttu-id="d6660-153">Ini 설정을 통해 구성</span><span class="sxs-lookup"><span data-stu-id="d6660-153">Configure via ini settings</span></span>
1. <span data-ttu-id="d6660-154">추가 `ext` 디렉터리 toohello `d:\home\site` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-154">Add a `ext` directory toohello `d:\home\site` directory.</span></span>
2. <span data-ttu-id="d6660-155">배치 `.dll` hello에서 확장 파일 `ext` 디렉터리 (예를 들어 `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="d6660-155">Put `.dll` extension files in hello `ext` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="d6660-156">Hello 확장 기본 버전의 PHP 및 VC9 및 호환 되는 비-스레드로부터 안전한 (nts)와 호환 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-156">Make sure that hello extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="d6660-157">Hello 키와 앱 설정 tooyour 웹 응용 프로그램 추가 `PHP_INI_SCAN_DIR` 및 값`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="d6660-157">Add an App Setting tooyour Web App with hello key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
4. <span data-ttu-id="d6660-158">`d:\home\site\ini`에 `extensions.ini`라는 `ini` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-158">Create an `ini` file in `d:\home\site\ini` called `extensions.ini`.</span></span>
5. <span data-ttu-id="d6660-159">추가 구성 설정을 toohello `extensions.ini` 사용 하 여 파일 hello 동일한 구문을 php.ini 파일에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-159">Add configuration settings toohello `extensions.ini` file using hello same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="d6660-160">예를 들어, tooenable hello MongoDB 및 XDebug 확장 하려는 경우 사용자 `extensions.ini` 파일에는이 텍스트 포함:</span><span class="sxs-lookup"><span data-stu-id="d6660-160">For example, if you wanted tooenable hello MongoDB and XDebug extensions, your `extensions.ini` file would contain this text:</span></span>
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. <span data-ttu-id="d6660-161">웹 앱 tooload hello 변경 내용을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-161">Restart your Web App tooload hello changes.</span></span>

### <a name="configure-via-app-setting"></a><span data-ttu-id="d6660-162">앱 설정을 통해 구성</span><span class="sxs-lookup"><span data-stu-id="d6660-162">Configure via App Setting</span></span>
1. <span data-ttu-id="d6660-163">추가 `bin` 디렉터리 toohello 루트 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-163">Add a `bin` directory toohello root directory.</span></span>
2. <span data-ttu-id="d6660-164">배치 `.dll` hello에서 확장 파일 `bin` 디렉터리 (예를 들어 `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="d6660-164">Put `.dll` extension files in hello `bin` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="d6660-165">Hello 확장 기본 버전의 PHP 및 VC9 및 호환 되는 비-스레드로부터 안전한 (nts)와 호환 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-165">Make sure that hello extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="d6660-166">웹 앱에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-166">Deploy your web app.</span></span>
4. <span data-ttu-id="d6660-167">Hello Azure 포털의에서 tooyour 웹 앱을 찾아 hello 클릭 **설정을** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-167">Browse tooyour web app in hello Azure Portal and click on hello **Settings** button.</span></span>
   
    ![저장][settings-button]
5. <span data-ttu-id="d6660-169">Hello에서 **설정** 블레이드 선택 **응용 프로그램 설정** toohello 스크롤하여 **앱 설정** 섹션.</span><span class="sxs-lookup"><span data-stu-id="d6660-169">From hello **Settings** blade select **Application Settings** and scroll toohello **App settings** section.</span></span>
6. <span data-ttu-id="d6660-170">Hello에 **앱 설정** 섹션을 만듭니다는 **PHP_EXTENSIONS** 키입니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-170">In hello **App settings** section, create a **PHP_EXTENSIONS** key.</span></span> <span data-ttu-id="d6660-171">이 키에 대 한 값과 hello 경로 상대 toowebsite 루트 수: **bin\your ext 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-171">hello value for this key would be a path relative toowebsite root: **bin\your-ext-file**.</span></span>
   
    ![앱 설정의 확장 사용][php-extensions]
7. <span data-ttu-id="d6660-173">Hello 클릭 **저장** hello hello 위쪽에 단추 **웹 앱 설정** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-173">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![구성 설정 저장][save-button]

<span data-ttu-id="d6660-175">**PHP_ZENDEXTENSIONS** 키를 통해 Zend 확장도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-175">Zend extensions are also supported by using a **PHP_ZENDEXTENSIONS** key.</span></span> <span data-ttu-id="d6660-176">tooenable 여러 확장명을 쉼표로 구분 된 목록이 포함 `.dll` hello 응용 프로그램 설정 값에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-176">tooenable multiple extensions, include a comma-separated list of `.dll` files for hello app setting value.</span></span>

## <a name="how-to-use-a-custom-php-runtime"></a><span data-ttu-id="d6660-177">방법: 사용자 지정 PHP 런타임 사용</span><span class="sxs-lookup"><span data-stu-id="d6660-177">How to: Use a custom PHP runtime</span></span>
<span data-ttu-id="d6660-178">Hello 기본 PHP 런타임 대신 앱 서비스 웹 앱 제공 하는 tooexecute PHP 스크립트 PHP 런타임에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-178">Instead of hello default PHP runtime, App Service Web Apps can use a PHP runtime that you provide tooexecute PHP scripts.</span></span> <span data-ttu-id="d6660-179">가 제공 하는 hello 런타임을 구성할 수 있습니다는 `php.ini` 도 제공 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-179">hello runtime that you provide can be configured by a `php.ini` file that you also provide.</span></span> <span data-ttu-id="d6660-180">웹 앱을 사용자 지정 PHP 런타임 toouse 아래 hello 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-180">toouse a custom PHP runtime with Web Apps, follow hello steps below.</span></span>

1. <span data-ttu-id="d6660-181">스레드로부터 안전하지 않은 VC9 또는 VC11과 호환되는 버전의 Windows용 PHP를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-181">Obtain a non-thread-safe, VC9 or VC11 compatible version of PHP for Windows.</span></span> <span data-ttu-id="d6660-182">최신 Windows용 PHP 릴리스는 [http://windows.php.net/download/]에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-182">Recent releases of PHP for Windows can be found here: [http://windows.php.net/download/].</span></span> <span data-ttu-id="d6660-183">이전 릴리스에서 hello 보관 여기에서 확인할 수 있습니다: [http://windows.php.net/downloads/releases/archives/]합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-183">Older releases can be found in hello archive here: [http://windows.php.net/downloads/releases/archives/].</span></span>
2. <span data-ttu-id="d6660-184">Hello 수정 `php.ini` 프로그램 런타임의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-184">Modify hello `php.ini` file for your runtime.</span></span> <span data-ttu-id="d6660-185">참고로, 시스템 수준 전용 지시문인 구성 설정은 웹 앱에서 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-185">Note that any configuration settings that are system-level-only directives will be ignored by Web Apps.</span></span> <span data-ttu-id="d6660-186">시스템 수준 전용 지시문에 대한 자세한 내용은 [php.ini 지시문 목록](영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6660-186">(For information about system-level-only directives, see [List of php.ini directives]).</span></span>
3. <span data-ttu-id="d6660-187">필요에 따라 tooyour PHP 런타임에 확장을 추가 하 고 hello에 사용할 수 있도록 `php.ini` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-187">Optionally, add extensions tooyour PHP runtime and enable them in hello `php.ini` file.</span></span>
4. <span data-ttu-id="d6660-188">추가 `bin` 디렉터리 tooyour 루트 디렉터리와 그 안에 프로그램 PHP 런타임에 포함 된 put hello 디렉터리 (예를 들어 `bin\php`).</span><span class="sxs-lookup"><span data-stu-id="d6660-188">Add a `bin` directory tooyour root directory, and put hello directory that contains your PHP runtime in it (for example, `bin\php`).</span></span>
5. <span data-ttu-id="d6660-189">웹 앱에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-189">Deploy your web app.</span></span>
6. <span data-ttu-id="d6660-190">Hello Azure 포털의에서 tooyour 웹 앱을 찾아 hello 클릭 **설정을** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-190">Browse tooyour web app in hello Azure Portal and click on hello **Settings** button.</span></span>
   
    ![저장][settings-button]
7. <span data-ttu-id="d6660-192">Hello에서 **설정** 블레이드 선택 **응용 프로그램 설정** toohello 스크롤하여 **처리기 매핑** 섹션.</span><span class="sxs-lookup"><span data-stu-id="d6660-192">From hello **Settings** blade select **Application Settings** and scroll toohello **Handler mappings** section.</span></span> <span data-ttu-id="d6660-193">추가 `*.php` toohello 확장 필드 및 hello 경로 toohello 추가 `php-cgi.exe` 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-193">Add `*.php` toohello Extension field and add hello path toohello `php-cgi.exe` executable.</span></span> <span data-ttu-id="d6660-194">PHP 런타임에 hello에 두면 `bin` hello 경로으로 응용 프로그램의 hello 루트에서 디렉터리 `D:\home\site\wwwroot\bin\php\php-cgi.exe`합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-194">If you put your PHP runtime in hello `bin` directory in hello root of you application, hello path will be `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span></span>
   
    ![처리기 매핑에 처리기 지정][handler-mappings]
8. <span data-ttu-id="d6660-196">Hello 클릭 **저장** hello hello 위쪽에 단추 **웹 앱 설정** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-196">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![구성 설정 저장][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a><span data-ttu-id="d6660-198">방법: Azure에서 작성기 자동화를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="d6660-198">How to: Enable Composer automation in Azure</span></span>
<span data-ttu-id="d6660-199">앱 서비스가 PHP 프로젝트에 있는 경우 기본적으로 composer.json로 작업하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-199">By default, App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="d6660-200">사용 하는 경우 [Git 배포](app-service-deploy-local-git.md), composer.json 중 처리를 사용 하도록 설정할 수 `git push` hello 작성기 확장을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-200">If you use [Git deployment](app-service-deploy-local-git.md), you can enable composer.json processing during `git push` by enabling hello Composer extension.</span></span>

> [!NOTE]
> <span data-ttu-id="d6660-201">[여기에서 앱 서비스의 최고 수준 작성기 지원에 투표](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-201">You can [vote for first-class Composer support in App Service here](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span></span>
> 
> 

1. <span data-ttu-id="d6660-202">웹 응용 프로그램의 블레이드 hello에 프로그램 PHP에 [Azure 포털](https://portal.azure.com), 클릭 **도구** > **확장**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-202">In your PHP web app's blade in hello [Azure portal](https://portal.azure.com), click **Tools** > **Extensions**.</span></span>
   
    ![Azure 포털 설정 블레이드에서 tooenable Azure에서 작성기 자동화](./media/web-sites-php-configure/composer-extension-settings.png)
2. <span data-ttu-id="d6660-204">**추가**를 클릭한 다음 **작성기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-204">Click **Add**, then click **Composer**.</span></span>
   
    ![Azure의 작성기 확장 tooenable 작성기 자동화를 추가 합니다.](./media/web-sites-php-configure/composer-extension-add.png)
3. <span data-ttu-id="d6660-206">클릭 **확인** tooaccept 약관 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-206">Click **OK** tooaccept legal terms.</span></span> <span data-ttu-id="d6660-207">클릭 **확인** 다시 tooadd hello 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-207">Click **OK** again tooadd hello extension.</span></span>
   
    <span data-ttu-id="d6660-208">hello **설치 된 확장** 블레이드 hello 작성기 확장 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-208">hello **Installed extensions** blade will now show hello Composer extension.</span></span>  
    <span data-ttu-id="d6660-209">![Azure에서 tooenable 작성기 자동화 약관에 동의](./media/web-sites-php-configure/composer-extension-view.png)</span><span class="sxs-lookup"><span data-stu-id="d6660-209">![Accept legal terms tooenable Composer automation in Azure](./media/web-sites-php-configure/composer-extension-view.png)</span></span>
4. <span data-ttu-id="d6660-210">이제 수행 `git add`, `git commit`, 및 `git push` hello 이전 섹션에서와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-210">Now, perform `git add`, `git commit`, and `git push` like in hello previous section.</span></span> <span data-ttu-id="d6660-211">이제 작성기가 composer.json에 정의된 종속성을 설치하고 있다고 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-211">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Azure에서 작성기 자동화를 사용하여 GIT 배포](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a><span data-ttu-id="d6660-213">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d6660-213">Next steps</span></span>
<span data-ttu-id="d6660-214">자세한 내용은 참조 hello [PHP 개발자 센터](/develop/php/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-214">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

> [!NOTE]
> <span data-ttu-id="d6660-215">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-215">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d6660-216">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d6660-216">No credit cards required; no commitments.</span></span>
> 
> 

[무료 평가판]: https://www.windowsazure.com/pricing/free-trial/
[phpinfo ()]: http://php.net/manual/en/function.phpinfo.php
[select-php-version]: ./media/web-sites-php-configure/select-php-version.png
[php.ini 지시문 목록]: http://www.php.net/manual/en/ini.list.php
[. user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php
[ini_set()]: http://www.php.net/manual/en/function.ini-set.php
[application-settings]: ./media/web-sites-php-configure/application-settings.png
[settings-button]: ./media/web-sites-php-configure/settings-button.png
[save-button]: ./media/web-sites-php-configure/save-button.png
[php-extensions]: ./media/web-sites-php-configure/php-extensions.png
[handler-mappings]: ./media/web-sites-php-configure/handler-mappings.png
[http://windows.php.net/download/]: http://windows.php.net/download/
[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/
[SETPHPVERCLI]: ./media/web-sites-php-configure/ChangePHPVersion-XPlatCLI.png
[GETPHPVERCLI]: ./media/web-sites-php-configure/ShowPHPVersion-XplatCLI.png
[SETPHPVERPS]: ./media/web-sites-php-configure/ChangePHPVersion-PS.png
[GETPHPVERPS]: ./media/web-sites-php-configure/ShowPHPVersion-PS.png

