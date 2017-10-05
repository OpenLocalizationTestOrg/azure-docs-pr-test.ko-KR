---
title: "Azure App Service Web Apps에서 PHP 구성 | Microsoft Docs"
description: "Azure 앱 서비스의 웹앱에서 기본 PHP 설치를 구성하거나 사용자 지정 PHP 설치를 추가하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 624dd416f37aacdb3d2f6e59afdc2efe646e610b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-php-in-azure-app-service-web-apps"></a><span data-ttu-id="40991-103">Azure 앱 서비스 웹 앱에서 PHP 구성</span><span class="sxs-lookup"><span data-stu-id="40991-103">Configure PHP in Azure App Service Web Apps</span></span>
## <a name="introduction"></a><span data-ttu-id="40991-104">소개</span><span class="sxs-lookup"><span data-stu-id="40991-104">Introduction</span></span>
<span data-ttu-id="40991-105">이 가이드에서는 [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)에서 웹앱에 대한 기본 제공 PHP 런타임을 구성하고 사용자 지정 PHP 런타임을 제공하며 확장을 사용하도록 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="40991-105">This guide will show you how to configure the built-in PHP runtime for Web Apps in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), provide a custom PHP runtime, and enable extensions.</span></span> <span data-ttu-id="40991-106">앱 서비스를 사용하려면 [평가판]에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-106">To use App Service, sign up for the [free trial].</span></span> <span data-ttu-id="40991-107">이 가이드를 최대한 활용하려면 먼저 앱 서비스에서 PHP 웹 앱을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-107">To get the most from this guide, you should first create a PHP web app in App Service.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-the-built-in-php-version"></a><span data-ttu-id="40991-108">방법: 기본 제공 PHP 버전 변경</span><span class="sxs-lookup"><span data-stu-id="40991-108">How to: Change the built-in PHP version</span></span>
<span data-ttu-id="40991-109">기본적으로 PHP 5.5는 앱 서비스 웹 앱을 만들 때 설치하여 바로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40991-109">By default, PHP 5.5 is installed and immediately available for use when you create an App Service web app.</span></span> <span data-ttu-id="40991-110">사용 가능한 릴리스 버전, 관련 기본 구성 및 사용하도록 설정된 확장을 보는 최상의 방법은 [phpinfo()] 함수를 호출하는 스크립트를 배포하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="40991-110">The best way to see the available release revision, its default configuration, and the enabled extensions is to deploy a script that calls the [phpinfo()] function.</span></span>

<span data-ttu-id="40991-111">PHP 5.6 및 PHP 7.0 버전도 사용할 수 있지만 기본적으로는 사용하도록 설정되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40991-111">PHP 5.6 and PHP 7.0 versions are also available, but not enabled by default.</span></span> <span data-ttu-id="40991-112">PHP 버전을 업데이트하려면 다음 방법 중 하나를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="40991-112">To update the PHP version, follow one of these methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="40991-113">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="40991-113">Azure Portal</span></span>
1. <span data-ttu-id="40991-114">[Azure 포털](https://portal.azure.com) 에서 웹앱을 찾아 **설정** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-114">Browse to your web app in the [Azure Portal](https://portal.azure.com) and click on the **Settings** button.</span></span>
   
    ![저장][settings-button]
2. <span data-ttu-id="40991-116">**설정** 블레이드에서 **응용 프로그램 설정**을 선택하고 새 PHP 버전을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-116">From the **Settings** blade select **Application Settings** and choose the new PHP version.</span></span>
   
    ![응용 프로그램 설정][application-settings]
3. <span data-ttu-id="40991-118">**웹앱 설정** 블레이드의 위쪽에서 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-118">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![구성 설정 저장][save-button]

### <a name="azure-powershell-windows"></a><span data-ttu-id="40991-120">Azure PowerShell(Windows)</span><span class="sxs-lookup"><span data-stu-id="40991-120">Azure PowerShell (Windows)</span></span>
1. <span data-ttu-id="40991-121">Azure PowerShell을 열고 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-121">Open Azure PowerShell, and login to your account:</span></span>
   
        PS C:\> Login-AzureRmAccount
2. <span data-ttu-id="40991-122">웹앱에 대한 PHP 버전을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-122">Set the PHP version for the web app.</span></span>
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. <span data-ttu-id="40991-123">PHP 버전이 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="40991-123">The PHP version is now set.</span></span> <span data-ttu-id="40991-124">이러한 설정을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40991-124">You can confirm these settings:</span></span>
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a><span data-ttu-id="40991-125">Azure 명령줄 인터페이스(Linux, Mac, Windows)</span><span class="sxs-lookup"><span data-stu-id="40991-125">Azure Command-Line Interface (Linux, Mac, Windows)</span></span>
<span data-ttu-id="40991-126">Azure 명령줄 인터페이스를 사용하려면 **Node.js** 를 컴퓨터에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-126">To use the Azure Command-Line Interface, you must have **Node.js** installed on your computer.</span></span>

1. <span data-ttu-id="40991-127">터미널을 열고 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-127">Open Terminal, and login to your account.</span></span>
   
        azure login
2. <span data-ttu-id="40991-128">웹앱에 대한 PHP 버전을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-128">Set the PHP version for the web app.</span></span>
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. <span data-ttu-id="40991-129">PHP 버전이 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="40991-129">The PHP version is now set.</span></span> <span data-ttu-id="40991-130">이러한 설정을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40991-130">You can confirm these settings:</span></span>
   
        azure site show {app-name}

> [!NOTE] 
> <span data-ttu-id="40991-131">위에 해당하는 [Azure CLI 2.0](https://github.com/Azure/azure-cli) 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="40991-131">The [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands that are equivalent to the above are:</span></span>
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-the-built-in-php-configurations"></a><span data-ttu-id="40991-132">방법: 기본 제공 PHP 구성 변경</span><span class="sxs-lookup"><span data-stu-id="40991-132">How to: Change the built-in PHP configurations</span></span>
<span data-ttu-id="40991-133">기본 제공 PHP 런타임에 대해 아래 단계에 따라 구성 옵션을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40991-133">For any built-in PHP runtime, you can change any of the configuration options by following the steps below.</span></span> <span data-ttu-id="40991-134">php.ini 지시문에 대한 자세한 내용은 [php.ini 지시문 목록]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40991-134">(For information about php.ini directives, see [List of php.ini directives].)</span></span>

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a><span data-ttu-id="40991-135">PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL 구성 설정 변경</span><span class="sxs-lookup"><span data-stu-id="40991-135">Changing PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL configuration settings</span></span>
1. <span data-ttu-id="40991-136">[.user.ini] 파일을 루트 디렉터리에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-136">Add a [.user.ini] file to your root directory.</span></span>
2. <span data-ttu-id="40991-137">`php.ini` 파일에 사용한 것과 동일한 구문을 사용하여 구성 설정을 `.user.ini` 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-137">Add configuration settings to the `.user.ini` file using the same syntax you would use in a `php.ini` file.</span></span> <span data-ttu-id="40991-138">예를 들어 `display_errors` 설정을 켜고 `upload_max_filesize` 설정을 10M로 설정하려면 `.user.ini` 파일에 다음 텍스트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-138">For example, if you wanted to turn the `display_errors` setting on and set `upload_max_filesize` setting to 10M, your `.user.ini` file would contain this text:</span></span>
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on to write errors to d:\home\LogFiles\php_errors.log
        ; log_errors=On
3. <span data-ttu-id="40991-139">웹 앱에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-139">Deploy your web app.</span></span>
4. <span data-ttu-id="40991-140">웹 앱을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-140">Restart the web app.</span></span> <span data-ttu-id="40991-141">PHP가 `.user.ini` 파일을 읽는 빈도는 시스템 수준 설정인 `user_ini.cache_ttl` 설정(기본적으로 300초[5분])의 적용을 받으므로 웹앱을 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-141">(Restarting is necessary because the frequency with which PHP reads `.user.ini` files is governed by the `user_ini.cache_ttl` setting, which is a system level setting and is 300 seconds (5 minutes) by default.</span></span> <span data-ttu-id="40991-142">웹앱을 다시 시작하면 PHP가 `.user.ini` 파일에서 새 설정을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="40991-142">Restarting the web app forces PHP to read the new settings in the `.user.ini` file.)</span></span>

<span data-ttu-id="40991-143">`.user.ini` 파일을 사용하는 대신 스크립트에서 [ini_set()] 함수를 사용하여 시스템 수준 지시문이 아닌 구성 옵션을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40991-143">As an alternative to using a `.user.ini` file, you can use the [ini_set()] function in scripts to set configuration options that are not system-level directives.</span></span>

### <a name="changing-phpinisystem-configuration-settings"></a><span data-ttu-id="40991-144">PHP\_INI\_SYSTEM 구성 설정 변경</span><span class="sxs-lookup"><span data-stu-id="40991-144">Changing PHP\_INI\_SYSTEM configuration settings</span></span>
1. <span data-ttu-id="40991-145">`PHP_INI_SCAN_DIR` 키 및 `d:\home\site\ini` 값으로 웹앱에 앱 설정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-145">Add an App Setting to your Web App with the key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
2. <span data-ttu-id="40991-146">Kudu Console(http://&lt;site-name&gt;.scm.azurewebsite.net)을 사용하여 `d:\home\site\ini` 디렉터리에 `settings.ini` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="40991-146">Create an `settings.ini` file using Kudu Console (http://&lt;site-name&gt;.scm.azurewebsite.net) in the `d:\home\site\ini` directory.</span></span>
3. <span data-ttu-id="40991-147">php.ini 파일에서 사용한 것과 동일한 구문을 사용하여 구성 설정을 `settings.ini` 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-147">Add configuration settings to the `settings.ini` file using the same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="40991-148">예를 들어 `curl.cainfo` 설정이 `*.crt` 파일을 가리키고 'wincache.maxfilesize' 설정을 512K로 설정하려면 `settings.ini` 파일에 다음 텍스트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-148">For example, if you wanted to point the `curl.cainfo` setting to a `*.crt` file and set 'wincache.maxfilesize' setting to 512K, your `settings.ini` file would contain this text:</span></span>
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. <span data-ttu-id="40991-149">웹앱을 다시 시작하여 변경 내용을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-149">Restart your Web App to load the changes.</span></span>

## <a name="how-to-enable-extensions-in-the-default-php-runtime"></a><span data-ttu-id="40991-150">방법: 기본 PHP 런타임에서 확장 사용</span><span class="sxs-lookup"><span data-stu-id="40991-150">How to: Enable extensions in the default PHP runtime</span></span>
<span data-ttu-id="40991-151">이전 섹션에 언급된 것처럼 기본 PHP 버전, 관련 기본 구성 및 사용하도록 설정된 확장을 보는 최상의 방법은 [phpinfo()]라는 스크립트를 배포하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="40991-151">As noted in the previous section, the best way to see the default PHP version, its default configuration, and the enabled extensions is to deploy a script that calls [phpinfo()].</span></span> <span data-ttu-id="40991-152">추가 확장을 사용하도록 설정하려면 아래 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="40991-152">To enable additional extensions, follow the steps below:</span></span>

### <a name="configure-via-ini-settings"></a><span data-ttu-id="40991-153">Ini 설정을 통해 구성</span><span class="sxs-lookup"><span data-stu-id="40991-153">Configure via ini settings</span></span>
1. <span data-ttu-id="40991-154">`ext` 디렉터리를 `d:\home\site` 디렉터리에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-154">Add a `ext` directory to the `d:\home\site` directory.</span></span>
2. <span data-ttu-id="40991-155">`.dll` 확장 파일을 `ext` 디렉터리에 둡니다(예: `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="40991-155">Put `.dll` extension files in the `ext` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="40991-156">확장이 기본 버전의 PHP와 호환되며 VC9 및 nts(non-thread-safe)와 호환 가능해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-156">Make sure that the extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="40991-157">`PHP_INI_SCAN_DIR` 키 및 `d:\home\site\ini` 값으로 웹앱에 앱 설정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-157">Add an App Setting to your Web App with the key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
4. <span data-ttu-id="40991-158">`d:\home\site\ini`에 `extensions.ini`라는 `ini` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="40991-158">Create an `ini` file in `d:\home\site\ini` called `extensions.ini`.</span></span>
5. <span data-ttu-id="40991-159">php.ini 파일에서 사용한 것과 동일한 구문을 사용하여 구성 설정을 `extensions.ini` 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-159">Add configuration settings to the `extensions.ini` file using the same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="40991-160">예를 들어 MongoDB 및 XDebug 확장을 사용하려면 `extensions.ini` 파일에 다음 텍스트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-160">For example, if you wanted to enable the MongoDB and XDebug extensions, your `extensions.ini` file would contain this text:</span></span>
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. <span data-ttu-id="40991-161">웹앱을 다시 시작하여 변경 내용을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-161">Restart your Web App to load the changes.</span></span>

### <a name="configure-via-app-setting"></a><span data-ttu-id="40991-162">앱 설정을 통해 구성</span><span class="sxs-lookup"><span data-stu-id="40991-162">Configure via App Setting</span></span>
1. <span data-ttu-id="40991-163">`bin` 디렉터리를 루트 디렉터리에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-163">Add a `bin` directory to the root directory.</span></span>
2. <span data-ttu-id="40991-164">`.dll` 확장 파일을 `bin` 디렉터리에 둡니다(예: `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="40991-164">Put `.dll` extension files in the `bin` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="40991-165">확장이 기본 버전의 PHP와 호환되며 VC9 및 nts(non-thread-safe)와 호환 가능해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-165">Make sure that the extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="40991-166">웹 앱에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-166">Deploy your web app.</span></span>
4. <span data-ttu-id="40991-167">Azure 포털에서 웹앱을 찾아 **설정** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-167">Browse to your web app in the Azure Portal and click on the **Settings** button.</span></span>
   
    ![저장][settings-button]
5. <span data-ttu-id="40991-169">**설정** 블레이드에서 **응용 프로그램 설정**을 선택하고 **앱 설정** 섹션으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-169">From the **Settings** blade select **Application Settings** and scroll to the **App settings** section.</span></span>
6. <span data-ttu-id="40991-170">**앱 설정** 섹션에서 **PHP_EXTENSIONS** 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="40991-170">In the **App settings** section, create a **PHP_EXTENSIONS** key.</span></span> <span data-ttu-id="40991-171">이 키의 값은 웹 사이트 루트 **bin\your-ext-file**에 상대적인 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="40991-171">The value for this key would be a path relative to website root: **bin\your-ext-file**.</span></span>
   
    ![앱 설정의 확장 사용][php-extensions]
7. <span data-ttu-id="40991-173">**웹앱 설정** 블레이드의 위쪽에서 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-173">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![구성 설정 저장][save-button]

<span data-ttu-id="40991-175">**PHP_ZENDEXTENSIONS** 키를 통해 Zend 확장도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="40991-175">Zend extensions are also supported by using a **PHP_ZENDEXTENSIONS** key.</span></span> <span data-ttu-id="40991-176">여러 확장을 사용하려면 앱 설정 값에 `.dll` 파일의 쉼표로 구분된 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-176">To enable multiple extensions, include a comma-separated list of `.dll` files for the app setting value.</span></span>

## <a name="how-to-use-a-custom-php-runtime"></a><span data-ttu-id="40991-177">방법: 사용자 지정 PHP 런타임 사용</span><span class="sxs-lookup"><span data-stu-id="40991-177">How to: Use a custom PHP runtime</span></span>
<span data-ttu-id="40991-178">앱 서비스 웹 앱은 기본 PHP 런타임 대신, 사용자가 PHP 스크립트를 실행하도록 제공한 PHP 런타임을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40991-178">Instead of the default PHP runtime, App Service Web Apps can use a PHP runtime that you provide to execute PHP scripts.</span></span> <span data-ttu-id="40991-179">이러한 런타임은 사용자가 제공한 `php.ini` 파일로 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40991-179">The runtime that you provide can be configured by a `php.ini` file that you also provide.</span></span> <span data-ttu-id="40991-180">웹 앱에 사용자 지정 PHP 런타임을 사용하려면 아래 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="40991-180">To use a custom PHP runtime with Web Apps, follow the steps below.</span></span>

1. <span data-ttu-id="40991-181">스레드로부터 안전하지 않은 VC9 또는 VC11과 호환되는 버전의 Windows용 PHP를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-181">Obtain a non-thread-safe, VC9 or VC11 compatible version of PHP for Windows.</span></span> <span data-ttu-id="40991-182">최신 Windows용 PHP 릴리스는 [http://windows.php.net/download/]에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40991-182">Recent releases of PHP for Windows can be found here: [http://windows.php.net/download/].</span></span> <span data-ttu-id="40991-183">이전 릴리스는 보관 파일 [http://windows.php.net/downloads/releases/archives/]에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40991-183">Older releases can be found in the archive here: [http://windows.php.net/downloads/releases/archives/].</span></span>
2. <span data-ttu-id="40991-184">런타임에 맞게 `php.ini` 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-184">Modify the `php.ini` file for your runtime.</span></span> <span data-ttu-id="40991-185">참고로, 시스템 수준 전용 지시문인 구성 설정은 웹 앱에서 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="40991-185">Note that any configuration settings that are system-level-only directives will be ignored by Web Apps.</span></span> <span data-ttu-id="40991-186">시스템 수준 전용 지시문에 대한 자세한 내용은 [php.ini 지시문 목록](영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40991-186">(For information about system-level-only directives, see [List of php.ini directives]).</span></span>
3. <span data-ttu-id="40991-187">경우에 따라 확장을 PHP 런타임에 추가하고 `php.ini` 파일에서 확장을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-187">Optionally, add extensions to your PHP runtime and enable them in the `php.ini` file.</span></span>
4. <span data-ttu-id="40991-188">루트 디렉터리에 `bin` 디렉터리를 추가하고 PHP 런타임이 포함된 디렉터리(예: `bin\php`)를 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-188">Add a `bin` directory to your root directory, and put the directory that contains your PHP runtime in it (for example, `bin\php`).</span></span>
5. <span data-ttu-id="40991-189">웹 앱에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-189">Deploy your web app.</span></span>
6. <span data-ttu-id="40991-190">Azure 포털에서 웹앱을 찾아 **설정** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-190">Browse to your web app in the Azure Portal and click on the **Settings** button.</span></span>
   
    ![저장][settings-button]
7. <span data-ttu-id="40991-192">**설정** 블레이드에서 **응용 프로그램 설정**을 선택하고 **처리기 매핑** 섹션으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-192">From the **Settings** blade select **Application Settings** and scroll to the **Handler mappings** section.</span></span> <span data-ttu-id="40991-193">`*.php`를 확장 필드에 추가하고 경로를 `php-cgi.exe` 실행 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-193">Add `*.php` to the Extension field and add the path to the `php-cgi.exe` executable.</span></span> <span data-ttu-id="40991-194">PHP 런타임을 응용 프로그램의 루트에 있는 `bin` 디렉터리에 배치하면 경로는 `D:\home\site\wwwroot\bin\php\php-cgi.exe`가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40991-194">If you put your PHP runtime in the `bin` directory in the root of you application, the path will be `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span></span>
   
    ![처리기 매핑에 처리기 지정][handler-mappings]
8. <span data-ttu-id="40991-196">**웹앱 설정** 블레이드의 위쪽에서 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-196">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![구성 설정 저장][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a><span data-ttu-id="40991-198">방법: Azure에서 작성기 자동화를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="40991-198">How to: Enable Composer automation in Azure</span></span>
<span data-ttu-id="40991-199">앱 서비스가 PHP 프로젝트에 있는 경우 기본적으로 composer.json로 작업하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40991-199">By default, App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="40991-200">[Git 배포](app-service-deploy-local-git.md)를 사용하는 경우 작성기 확장을 사용하여 `git push` 중에 composer.json 처리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40991-200">If you use [Git deployment](app-service-deploy-local-git.md), you can enable composer.json processing during `git push` by enabling the Composer extension.</span></span>

> [!NOTE]
> <span data-ttu-id="40991-201">[여기에서 앱 서비스의 최고 수준 작성기 지원에 투표](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40991-201">You can [vote for first-class Composer support in App Service here](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span></span>
> 
> 

1. <span data-ttu-id="40991-202">[Azure Portal](https://portal.azure.com)의 PHP 웹앱의 블레이드에서 **도구** > **확장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-202">In your PHP web app's blade in the [Azure portal](https://portal.azure.com), click **Tools** > **Extensions**.</span></span>
   
    ![Azure에서 작성기를 자동화하도록 설정하기 위한 Azure 포털 설정 블레이드](./media/web-sites-php-configure/composer-extension-settings.png)
2. <span data-ttu-id="40991-204">**추가**를 클릭한 다음 **작성기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-204">Click **Add**, then click **Composer**.</span></span>
   
    ![Azure에서 작성기를 자동화하도록 설정하기 위하여 작성기 확장 추가](./media/web-sites-php-configure/composer-extension-add.png)
3. <span data-ttu-id="40991-206">**확인** 을 클릭하여 약관을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-206">Click **OK** to accept legal terms.</span></span> <span data-ttu-id="40991-207">**확인** 을 다시 클릭하여 확장을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-207">Click **OK** again to add the extension.</span></span>
   
    <span data-ttu-id="40991-208">**설치된 확장** 블레이드에 이제 작성기 확장이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="40991-208">The **Installed extensions** blade will now show the Composer extension.</span></span>  
    <span data-ttu-id="40991-209">![Azure에서 작성기를 자동화하도록 설정하기 위하여 약관에 동의](./media/web-sites-php-configure/composer-extension-view.png)</span><span class="sxs-lookup"><span data-stu-id="40991-209">![Accept legal terms to enable Composer automation in Azure](./media/web-sites-php-configure/composer-extension-view.png)</span></span>
4. <span data-ttu-id="40991-210">이제 `git add`, `git commit` 및 `git push`을 이전 섹션처럼 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="40991-210">Now, perform `git add`, `git commit`, and `git push` like in the previous section.</span></span> <span data-ttu-id="40991-211">이제 작성기가 composer.json에 정의된 종속성을 설치하고 있다고 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="40991-211">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Azure에서 작성기 자동화를 사용하여 GIT 배포](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a><span data-ttu-id="40991-213">다음 단계</span><span class="sxs-lookup"><span data-stu-id="40991-213">Next steps</span></span>
<span data-ttu-id="40991-214">자세한 내용은 [PHP 개발자 센터](/develop/php/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40991-214">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

> [!NOTE]
> <span data-ttu-id="40991-215">Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험](https://azure.microsoft.com/try/app-service/)으로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40991-215">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="40991-216">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40991-216">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="40991-217">[평가판]: https://www.windowsazure.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="40991-217">[free trial]: https://www.windowsazure.com/pricing/free-trial/</span></span>
<span data-ttu-id="40991-218">[phpinfo()]: http://php.net/manual/en/function.phpinfo.php</span><span class="sxs-lookup"><span data-stu-id="40991-218">[phpinfo()]: http://php.net/manual/en/function.phpinfo.php</span></span>
[select-php-version]: ./media/web-sites-php-configure/select-php-version.png
<span data-ttu-id="40991-219">[php.ini 지시문 목록]: http://www.php.net/manual/en/ini.list.php</span><span class="sxs-lookup"><span data-stu-id="40991-219">[List of php.ini directives]: http://www.php.net/manual/en/ini.list.php</span></span>
<span data-ttu-id="40991-220">[.user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php</span><span class="sxs-lookup"><span data-stu-id="40991-220">[.user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php</span></span>
<span data-ttu-id="40991-221">[ini_set()]: http://www.php.net/manual/en/function.ini-set.php</span><span class="sxs-lookup"><span data-stu-id="40991-221">[ini_set()]: http://www.php.net/manual/en/function.ini-set.php</span></span>
[application-settings]: ./media/web-sites-php-configure/application-settings.png
[settings-button]: ./media/web-sites-php-configure/settings-button.png
[save-button]: ./media/web-sites-php-configure/save-button.png
[php-extensions]: ./media/web-sites-php-configure/php-extensions.png
[handler-mappings]: ./media/web-sites-php-configure/handler-mappings.png
<span data-ttu-id="40991-222">[http://windows.php.net/download/]: http://windows.php.net/download/</span><span class="sxs-lookup"><span data-stu-id="40991-222">[http://windows.php.net/download/]: http://windows.php.net/download/</span></span>
<span data-ttu-id="40991-223">[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/</span><span class="sxs-lookup"><span data-stu-id="40991-223">[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/</span></span>
[SETPHPVERCLI]: ./media/web-sites-php-configure/ChangePHPVersion-XPlatCLI.png
[GETPHPVERCLI]: ./media/web-sites-php-configure/ShowPHPVersion-XplatCLI.png
[SETPHPVERPS]: ./media/web-sites-php-configure/ChangePHPVersion-PS.png
[GETPHPVERPS]: ./media/web-sites-php-configure/ShowPHPVersion-PS.png

