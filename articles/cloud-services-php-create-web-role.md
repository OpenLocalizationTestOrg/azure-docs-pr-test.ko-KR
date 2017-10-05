---
title: "PHP용 Azure 웹 및 작업자 역할 만들기 | Microsoft Docs"
description: "Azure 클라우드 서비스에서 PHP 웹 및 작업자 역할을 만들고 PHP 런타임을 구성하는 방법을 설명하는 가이드입니다."
services: 
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9f7ccda0-bd96-4f7b-a7af-fb279a9e975b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 214fdcfe20f3fa4ebcbe41308404f8b7e7d15310
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-create-php-web-and-worker-roles"></a><span data-ttu-id="e859d-103">PHP 웹 및 작업자 역할을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="e859d-103">How to create PHP web and worker roles</span></span>
## <a name="overview"></a><span data-ttu-id="e859d-104">개요</span><span class="sxs-lookup"><span data-stu-id="e859d-104">Overview</span></span>
<span data-ttu-id="e859d-105">이 가이드는 Windows 개발 환경에서 PHP 웹이나 작업자 역할을 만들고, 사용 가능한 "기본 제공" 버전에서 특정 PHP 버전을 선택하여 PHP 구성을 변경하고, 확장을 사용하고, 마지막으로 Azure에 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-105">This guide will show you how to create PHP web or worker roles in a Windows development environment, choose a specific version of PHP from the "built-in" versions available, change the PHP configuration, enable extensions, and finally, deploy to Azure.</span></span> <span data-ttu-id="e859d-106">또한 사용자 지정 구성 및 확장으로 제공하는 PHP 런타임을 사용하도록 웹 또는 작업자 역할을 구성하는 방법도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-106">It also describes how to configure a web or worker role to use a PHP runtime (with custom configuration and extensions) that you provide.</span></span>

## <a name="what-are-php-web-and-worker-roles"></a><span data-ttu-id="e859d-107">PHP 웹 및 작업자 역할이란?</span><span class="sxs-lookup"><span data-stu-id="e859d-107">What are PHP web and worker roles?</span></span>
<span data-ttu-id="e859d-108">Azure는 응용 프로그램을 실행하기 위한 세 가지 계산 모델인 Azure App Service, Azure 가상 컴퓨터 및 Azure Cloud Services를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-108">Azure provides three compute models for running applications: Azure App Service, Azure Virtual Machines, and Azure Cloud Services.</span></span> <span data-ttu-id="e859d-109">이 세 모델은 모두 PHP를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-109">All three models support PHP.</span></span> <span data-ttu-id="e859d-110">웹 및 작업자 역할을 포함하는 Cloud Services는 *PaaS(Platform as a Service)*를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-110">Cloud Services, which includes web and worker roles, provides *platform as a service (PaaS)*.</span></span> <span data-ttu-id="e859d-111">Cloud Services 안에서 웹 역할은 프런트 엔드 웹 응용 프로그램을 호스팅할 전용 IIS(인터넷 정보 서비스) 웹 서버를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-111">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server to host front-end web applications.</span></span> <span data-ttu-id="e859d-112">작업자 역할은 비동기, 장기 실행 또는 영구 작업을 사용자 조작 또는 입력과 독립적으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-112">A worker role can run asynchronous, long-running or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="e859d-113">이러한 옵션에 대한 자세한 내용은 [Azure에서 제공하는 계산 호스팅 옵션](cloud-services/cloud-services-choose-me.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e859d-113">For more information about these options, see [Compute hosting options provided by Azure](cloud-services/cloud-services-choose-me.md).</span></span>

## <a name="download-the-azure-sdk-for-php"></a><span data-ttu-id="e859d-114">PHP용 Azure SDK 다운로드(영문)</span><span class="sxs-lookup"><span data-stu-id="e859d-114">Download the Azure SDK for PHP</span></span>
<span data-ttu-id="e859d-115">[PHP용 Azure SDK]는 여러 구성 요소로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-115">The [Azure SDK for PHP] consists of several components.</span></span> <span data-ttu-id="e859d-116">이 문서에서는 이러한 구성 요소 중 두 가지인 Azure PowerShell 및 Azure 에뮬레이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-116">This article will use two of them: Azure PowerShell and the Azure emulators.</span></span> <span data-ttu-id="e859d-117">이러한 두 구성 요소는 Microsoft 웹 플랫폼 설치 관리자를 통해 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-117">These two components can be installed via the Microsoft Web Platform Installer.</span></span> <span data-ttu-id="e859d-118">자세한 내용은 [Azure PowerShell을 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e859d-118">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="create-a-cloud-services-project"></a><span data-ttu-id="e859d-119">Cloud Services 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="e859d-119">Create a Cloud Services project</span></span>
<span data-ttu-id="e859d-120">PHP 웹 또는 작업자 역할을 만드는 첫 번째 단계는 Azure 서비스 프로젝트를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-120">The first step in creating a PHP web or worker role is to create an Azure Service project.</span></span> <span data-ttu-id="e859d-121">Azure 서비스 프로젝트는 웹 및 작업자 역할의 논리 컨테이너 역할을 하며 프로젝트의 [서비스 정의(.csdef)] 및 [서비스 구성(.cscfg)] 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-121">an Azure Service project serves as a logical container for web and worker roles, and it contains the project's [service definition (.csdef)] and [service configuration (.cscfg)] files.</span></span>

<span data-ttu-id="e859d-122">새 Azure 서비스 프로젝트를 만들려면 관리자로 Azure PowerShell을 실행하고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-122">To create a new Azure Service project, run Azure PowerShell as an administrator, and execute the following command:</span></span>

    PS C:\>New-AzureServiceProject myProject

<span data-ttu-id="e859d-123">이 명령은 웹 및 작업자 역할을 추가할 수 있는 새 디렉터리(`myProject`)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-123">This command will create a new directory (`myProject`) to which you can add web and worker roles.</span></span>

## <a name="add-php-web-or-worker-roles"></a><span data-ttu-id="e859d-124">PHP 웹 또는 작업자 역할 추가</span><span class="sxs-lookup"><span data-stu-id="e859d-124">Add PHP web or worker roles</span></span>
<span data-ttu-id="e859d-125">PHP 웹 역할을 프로젝트에 추가하려면 프로젝트의 루트 디렉터리에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-125">To add a PHP web role to a project, run the following command from within the project's root directory:</span></span>

    PS C:\myProject> Add-AzurePHPWebRole roleName

<span data-ttu-id="e859d-126">작업자 역할의 경우에는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-126">For a worker role, use this command:</span></span>

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> <span data-ttu-id="e859d-127">`roleName` 매개 변수는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-127">The `roleName` parameter is optional.</span></span> <span data-ttu-id="e859d-128">생략되면 역할 이름이 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-128">If it is omitted, the role name will be automatically generated.</span></span> <span data-ttu-id="e859d-129">첫 번째로 만들어진 웹 역할은 `WebRole1`, 두 번째는 `WebRole2`이 되는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-129">The first web role created will be `WebRole1`, the second will be `WebRole2`, and so on.</span></span> <span data-ttu-id="e859d-130">첫 번째로 만들어진 작업자 역할은 `WorkerRole1`, 두 번째는 `WorkerRole2`이 되는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-130">The first worker role created will be `WorkerRole1`, the second will be `WorkerRole2`, and so on.</span></span>
>
>

## <a name="specify-the-built-in-php-version"></a><span data-ttu-id="e859d-131">기본 제공 PHP 버전 지정</span><span class="sxs-lookup"><span data-stu-id="e859d-131">Specify the built-in PHP version</span></span>
<span data-ttu-id="e859d-132">PHP 웹 또는 작업자 역할을 프로젝트에 추가하면 응용 프로그램이 배포될 때 응용 프로그램의 각 웹 또는 작업자 인스턴스에 PHP가 설치되도록 프로젝트의 구성 파일이 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-132">When you add a PHP web or worker role to a project, the project's configuration files are modified so that PHP will be installed on each web or worker instance of your application when it is deployed.</span></span> <span data-ttu-id="e859d-133">기본적으로 설치되는 PHP 버전을 보려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-133">To see the version of PHP that will be installed by default, run the following command:</span></span>

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

<span data-ttu-id="e859d-134">위 명령은 아래 보이는 것과 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-134">The output from the command above will look similar to what is shown below.</span></span> <span data-ttu-id="e859d-135">이 예제에서 `IsDefault` 플래그는 PHP 5.3.17의 경우 `true`로 설정되어 이 버전이 기본 PHP 버전으로 설치됨을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-135">In this example, the `IsDefault` flag is set to `true` for PHP 5.3.17, indicating that it will be the default PHP version installed.</span></span>

```
Runtime Version     PackageUri                      IsDefault
------- -------     ----------                      ---------
Node 0.6.17         http://nodertncu.blob.core...   False
Node 0.6.20         http://nodertncu.blob.core...   True
Node 0.8.4          http://nodertncu.blob.core...   False
IISNode 0.1.21      http://nodertncu.blob.core...   True
Cache 1.8.0         http://nodertncu.blob.core...   True
PHP 5.3.17          http://nodertncu.blob.core...   True
PHP 5.4.0           http://nodertncu.blob.core...   False
```

<span data-ttu-id="e859d-136">나열된 PHP 버전 중 아무 버전에나 PHP 런타임 버전을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-136">You can set the PHP runtime version to any of the PHP versions that are listed.</span></span> <span data-ttu-id="e859d-137">예를 들어 PHP 버전(이름이 `roleName`인 역할의 경우)을 5.4.0에 설정하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-137">For example, to set the PHP version (for a role with the name `roleName`) to 5.4.0, use the following command:</span></span>

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> <span data-ttu-id="e859d-138">사용 가능한 PHP 버전은 나중에 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-138">Available PHP versions may change in the future.</span></span>
>
>

## <a name="customize-the-built-in-php-runtime"></a><span data-ttu-id="e859d-139">기본 제공 PHP 런타임 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="e859d-139">Customize the built-in PHP runtime</span></span>
<span data-ttu-id="e859d-140">`php.ini` 설정 수정 및 확장 사용을 포함하여 위 단계에 따라 설치된 PHP 런타임의 구성을 완전히 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-140">You have complete control over the configuration of the PHP runtime that is installed when you follow the steps above, including modification of `php.ini` settings and enabling of extensions.</span></span>

<span data-ttu-id="e859d-141">기본 제공 PHP 런타임을 사용자 지정하려면 다음 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="e859d-141">To customize the built-in PHP runtime, follow these steps:</span></span>

1. <span data-ttu-id="e859d-142">`php`라는 이름의 새 폴더를 웹 역할의 `bin` 디렉터리에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-142">Add a new folder, named `php`, to the `bin` directory of your web role.</span></span> <span data-ttu-id="e859d-143">작업자 역할의 경우 역할의 루트 디렉터리에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-143">For a worker role, add it to the role's root directory.</span></span>
2. <span data-ttu-id="e859d-144">`php` 폴더에 `ext`라는 다른 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-144">In the `php` folder, create another folder called `ext`.</span></span> <span data-ttu-id="e859d-145">사용하도록 설정할 `.dll` 확장 파일(예: `php_mongo.dll`)을 이 폴더에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-145">Put any `.dll` extension files (e.g., `php_mongo.dll`) that you want to enable in this folder.</span></span>
3. <span data-ttu-id="e859d-146">`php.ini` 파일을 `php` 폴더에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-146">Add a `php.ini` file to the `php` folder.</span></span> <span data-ttu-id="e859d-147">사용자 지정 확장을 사용하도록 설정하고 이 파일에 PHP 지시문을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-147">Enable any custom extensions and set any PHP directives in this file.</span></span> <span data-ttu-id="e859d-148">예를 들어 `display_errors`를 켜고 `php_mongo.dll` 확장을 사용하도록 설정한 경우 `php.ini` 파일의 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-148">For example, if you wanted to turn `display_errors` on and enable the `php_mongo.dll` extension, the contents of your `php.ini` file would be as follows:</span></span>

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> <span data-ttu-id="e859d-149">제공하는 `php.ini` 파일에서 명시적으로 설정하지 않은 설정은 자동으로 기본값으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-149">Any settings that you don't explicitly set in the `php.ini` file that you provide will automatically be set to their default values.</span></span> <span data-ttu-id="e859d-150">하지만 완전한 `php.ini` 파일을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-150">However, keep in mind that you can add a complete `php.ini` file.</span></span>
>
>

## <a name="use-your-own-php-runtime"></a><span data-ttu-id="e859d-151">고유 PHP 런타임 사용</span><span class="sxs-lookup"><span data-stu-id="e859d-151">Use your own PHP runtime</span></span>
<span data-ttu-id="e859d-152">기본 제공 PHP 런타임을 선택하여 위 설명대로 구성하는 대신 고유 PHP 런타임을 제공할 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-152">In some cases, instead of selecting a built-in PHP runtime and configuring it as described above, you may want to provide your own PHP runtime.</span></span> <span data-ttu-id="e859d-153">예를 들어, 개발 환경에서 사용하는 웹 또는 작업자 역할에서 동일한 PHP 런타임을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-153">For example, you can use the same PHP runtime in a web or worker role that you use in your development environment.</span></span> <span data-ttu-id="e859d-154">이렇게 하면 더 쉽게 응용 프로그램이 프로덕션 환경에서 동작을 변경하지 않게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-154">This makes it easier to ensure that the application will not change behavior in your production environment.</span></span>

### <a name="configure-a-web-role-to-use-your-own-php-runtime"></a><span data-ttu-id="e859d-155">고유 PHP 런타임을 사용하도록 웹 역할 구성</span><span class="sxs-lookup"><span data-stu-id="e859d-155">Configure a web role to use your own PHP runtime</span></span>
<span data-ttu-id="e859d-156">사용자가 제공하는 PHP 런타임을 사용하도록 웹 역할을 구성하려면 아래 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-156">To configure a web role to use a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="e859d-157">이 항목의 앞부분에서 설명한 대로 Azure 서비스 프로젝트를 만들고 PHP 웹 역할을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-157">Create an Azure Service project and add a PHP web role as described previously in this topic.</span></span>
2. <span data-ttu-id="e859d-158">웹 역할의 루트 디렉터리에 있는 `bin` 폴더에 `php` 폴더를 만든 후 PHP 런타임(모든 바이너리, 구성 파일, 하위 폴더 등)을 `php` 폴더에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-158">Create a `php` folder in the `bin` folder that is in your web role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) to the `php` folder.</span></span>
3. <span data-ttu-id="e859d-159">(선택 사항) PHP 런타임이 [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers]를 사용하면 웹 역할이 프로비전될 때 [SQL Server Native Client 2012][sql native client]를 설치하도록 웹 역할을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-159">(OPTIONAL) If your PHP runtime uses the [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need to configure your web role to install [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="e859d-160">이렇게 하려면 [sqlncli.msi x64 설치 관리자]를 웹 역할의 루트 디렉터리에 있는 `bin` 폴더에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-160">To do this, add the [sqlncli.msi x64 installer] to the `bin` folder in your web role's root directory.</span></span> <span data-ttu-id="e859d-161">다음 단계에 설명되어 있는 시작 스크립트는 역할이 프로비전될 때 설치 관리자를 자동으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-161">The startup script described in the next step will silently run the installer when the role is provisioned.</span></span> <span data-ttu-id="e859d-162">PHP 런타임이 Microsoft Drivers for PHP for SQL Server를 사용하지 않으면 다음 단계의 스크립트에서 다음 줄을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-162">If your PHP runtime does not use the Microsoft Drivers for PHP for SQL Server, you can remove the following line from the script shown in the next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="e859d-163">PHP 런타임을 사용하여 `.php` 페이지에 대한 요청을 처리하도록 [IIS(인터넷 정보 서비스)][iis.net]를 구성하는 시작 작업을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-163">Define a startup task that configures [Internet Information Services (IIS)][iis.net] to use your PHP runtime to handle requests for `.php` pages.</span></span> <span data-ttu-id="e859d-164">이렇게 하려면 텍스트 편집기에서 `setup_web.cmd` 파일(웹 역할 루트 디렉터리의 `bin` 파일에 있음)을 열고 그 내용을 다음 스크립트로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-164">To do this, open the `setup_web.cmd` file (in the `bin` file of your web role's root directory) in a text editor and replace its contents with the following script:</span></span>

    ```cmd
    @ECHO ON
    cd "%~dp0"

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    SET PHP_FULL_PATH=%~dp0php\php-cgi.exe
    SET NEW_PATH=%PATH%;%RoleRoot%\base\x86

    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%',maxInstances='12',idleTimeout='60000',activityTimeout='3600',requestTimeout='60000',instanceMaxRequests='10000',protocol='NamedPipe',flushNamedPipe='False']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PATH',value='%NEW_PATH%']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PHP_FCGI_MAX_REQUESTS',value='10000']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/handlers /+"[name='PHP',path='*.php',verb='GET,HEAD,POST',modules='FastCgiModule',scriptProcessor='%PHP_FULL_PATH%',resourceType='Either',requireAccess='Script']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /"[fullPath='%PHP_FULL_PATH%'].queueLength:50000"
    ```
5. <span data-ttu-id="e859d-165">응용 프로그램 파일을 웹 역할의 루트 디렉터리에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-165">Add your application files to your web role's root directory.</span></span> <span data-ttu-id="e859d-166">그러면 웹 서버의 루트 디렉터리가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-166">This will be the web server's root directory.</span></span>
6. <span data-ttu-id="e859d-167">아래 [응용 프로그램 게시](#publish-your-application) 섹션에 설명된 대로 응용 프로그램을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-167">Publish your application as described in the [Publish your application](#publish-your-application) section below.</span></span>

> [!NOTE]
> <span data-ttu-id="e859d-168">`download.ps1` 스크립트(웹 역할 루트 디렉터리의 `bin` 폴더에 있음)는 고유 PHP 런타임을 사용하기 위해 위에 설명된 단계를 따른 후에 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-168">The `download.ps1` script (in the `bin` folder of the web role's root directory) can be deleted after you follow the steps described above for using your own PHP runtime.</span></span>
>
>

### <a name="configure-a-worker-role-to-use-your-own-php-runtime"></a><span data-ttu-id="e859d-169">고유 PHP 런타임을 사용하도록 작업자 역할 구성</span><span class="sxs-lookup"><span data-stu-id="e859d-169">Configure a worker role to use your own PHP runtime</span></span>
<span data-ttu-id="e859d-170">제공하는 PHP 런타임을 사용하도록 작업자 역할을 구성하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="e859d-170">To configure a worker role to use a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="e859d-171">이 항목의 앞부분에서 설명한 대로 Azure 서비스 프로젝트를 만들고 PHP 작업자 역할을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-171">Create an Azure Service project and add a PHP worker role as described previously in this topic.</span></span>
2. <span data-ttu-id="e859d-172">작업자 역할의 루트 디렉터리에 `php` 폴더를 만든 후 PHP 런타임(모든 바이너리, 구성 파일, 하위 폴더 등)을 `php` 폴더에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-172">Create a `php` folder in the worker role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) to the `php` folder.</span></span>
3. <span data-ttu-id="e859d-173">(선택 사항) PHP 런타임이 [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers]를 사용하면 작업자 역할이 프로비전될 때 [SQL Server Native Client 2012][sql native client]를 설치하도록 작업자 역할을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-173">(OPTIONAL) If your PHP runtime uses [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need to configure your worker role to install [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="e859d-174">이렇게 하려면 [sqlncli.msi x64 설치 관리자]를 작업자 역할의 루트 디렉터리에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-174">To do this, add the [sqlncli.msi x64 installer] to the worker role's root directory.</span></span> <span data-ttu-id="e859d-175">다음 단계에 설명되어 있는 시작 스크립트는 역할이 프로비전될 때 설치 관리자를 자동으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-175">The startup script described in the next step will silently run the installer when the role is provisioned.</span></span> <span data-ttu-id="e859d-176">PHP 런타임이 Microsoft Drivers for PHP for SQL Server를 사용하지 않으면 다음 단계의 스크립트에서 다음 줄을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-176">If your PHP runtime does not use the Microsoft Drivers for PHP for SQL Server, you can remove the following line from the script shown in the next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="e859d-177">역할이 프로비전될 때 `php.exe` 실행 파일을 작업자 역할의 PATH 환경 변수에 추가하는 시작 작업을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-177">Define a startup task that adds your `php.exe` executable to the worker role's PATH environment variable when the role is provisioned.</span></span> <span data-ttu-id="e859d-178">이렇게 하려면 텍스트 편집기에서 `setup_worker.cmd` 파일(작업자 역할의 루트 디렉터리에 있음)을 열고 그 내용을 다음 스크립트로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-178">To do this, open the `setup_worker.cmd` file (in the worker role's root directory) in a text editor and replace its contents with the following script:</span></span>

    ```cmd
    @echo on

    cd "%~dp0"

    echo Granting permissions for Network Service to the web root directory...
    icacls ..\ /grant "Network Service":(OI)(CI)W
    if %ERRORLEVEL% neq 0 goto error
    echo OK

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    setx Path "%PATH%;%~dp0php" /M

    if %ERRORLEVEL% neq 0 goto error

    echo SUCCESS
    exit /b 0

    :error

    echo FAILED
    exit /b -1
    ```
5. <span data-ttu-id="e859d-179">응용 프로그램 파일을 작업자 역할의 루트 디렉터리에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-179">Add your application files to your worker role's root directory.</span></span>
6. <span data-ttu-id="e859d-180">아래 [응용 프로그램 게시](#publish-your-application) 섹션에 설명된 대로 응용 프로그램을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-180">Publish your application as described in the [Publish your application](#publish-your-application) section below.</span></span>

## <a name="run-your-application-in-the-compute-and-storage-emulators"></a><span data-ttu-id="e859d-181">계산 및 저장소 에뮬레이터에서 응용 프로그램 실행 </span><span class="sxs-lookup"><span data-stu-id="e859d-181">Run your application in the compute and storage emulators</span></span>
<span data-ttu-id="e859d-182">Azure 에뮬레이터는 클라우드에 배포하기 전에 Azure 응용 프로그램을 테스트할 수 있는 로컬 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-182">The Azure emulators provide a local environment in which you can test your Azure application before you deploy it to the cloud.</span></span> <span data-ttu-id="e859d-183">에뮬레이터와 Azure 환경 사이에는 약간의 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-183">There are some differences between the emulators and the Azure environment.</span></span> <span data-ttu-id="e859d-184">이해하기 쉽도록 [개발 및 테스트에 Azure Storage 에뮬레이터 사용](storage/common/storage-use-emulator.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e859d-184">To understand this better, see [Use the Azure storage emulator for development and testing](storage/common/storage-use-emulator.md).</span></span>

<span data-ttu-id="e859d-185">계산 에뮬레이터를 사용하려면 PHP를 로컬로 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-185">Note that you must have PHP installed locally to use the compute emulator.</span></span> <span data-ttu-id="e859d-186">계산 에뮬레이터는 로컬 PHP 설치를 사용하여 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-186">The compute emulator will use your local PHP installation to run your application.</span></span>

<span data-ttu-id="e859d-187">에뮬레이터에서 프로젝트를 실행하려면 프로젝트의 루트 디렉터리에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-187">To run your project in the emulators, execute the following command from your project's root directory:</span></span>

    PS C:\MyProject> Start-AzureEmulator

<span data-ttu-id="e859d-188">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-188">You will see output similar to this:</span></span>

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

<span data-ttu-id="e859d-189">웹 브라우저를 열고 출력에 표시된 로컬 주소(위 예제 출력의 `http://127.0.0.1:81`)로 이동하면 에뮬레이터에서 실행 중인 응용 프로그램을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-189">You can see your application running in the emulator by opening a web browser and browsing to the local address shown in the output (`http://127.0.0.1:81` in the example output above).</span></span>

<span data-ttu-id="e859d-190">에뮬레이터를 중지하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-190">To stop the emulators, execute this command:</span></span>

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a><span data-ttu-id="e859d-191">응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="e859d-191">Publish your application</span></span>
<span data-ttu-id="e859d-192">응용 프로그램을 게시하려면 먼저 [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet을 사용하여 게시 설정을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-192">To publish your application, you need to first import your publish settings by using the [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet.</span></span> <span data-ttu-id="e859d-193">그런 다음 [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet을 사용하여 응용 프로그램을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="e859d-193">Then you can publish your application by using the [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet.</span></span> <span data-ttu-id="e859d-194">로그인에 대한 자세한 내용은 [Azure PowerShell을 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e859d-194">For information about signing in, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e859d-195">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e859d-195">Next steps</span></span>
<span data-ttu-id="e859d-196">자세한 내용은 [PHP 개발자 센터](/develop/php/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e859d-196">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

[PHP용 Azure SDK]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[서비스 정의(.csdef)]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[서비스 구성(.cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[sqlncli.msi x64 설치 관리자]: http://go.microsoft.com/fwlink/?LinkID=239648
