---
title: "aaaCreate Azure 웹 및 작업자 역할에 대 한 PHP | Microsoft Docs"
description: "가이드 toocreating PHP 웹 및 작업자 역할에서 Azure 클라우드 서비스 및 hello PHP 런타임에 구성 합니다."
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
ms.openlocfilehash: 04a6e8c9c379cb0f854645941b6bc7d614bb91f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-php-web-and-worker-roles"></a><span data-ttu-id="ab150-103">어떻게 toocreate PHP 웹 및 작업자 역할</span><span class="sxs-lookup"><span data-stu-id="ab150-103">How toocreate PHP web and worker roles</span></span>
## <a name="overview"></a><span data-ttu-id="ab150-104">개요</span><span class="sxs-lookup"><span data-stu-id="ab150-104">Overview</span></span>
<span data-ttu-id="ab150-105">이 가이드에서는 방법을 toocreate PHP 웹 또는 작업자 역할 Windows 개발 환경에서 사용할 수 있는 버전 "기본" hello에서 PHP의 특정 버전을 선택, 변경 hello PHP 구성을, 확장을 사용 하 고 마지막으로 배포 tooAzure 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-105">This guide will show you how toocreate PHP web or worker roles in a Windows development environment, choose a specific version of PHP from hello "built-in" versions available, change hello PHP configuration, enable extensions, and finally, deploy tooAzure.</span></span> <span data-ttu-id="ab150-106">에 대해서도 설명 방법을 제공 하는 사용자 지정 구성 및 확장) (있음 PHP 런타임에 웹 또는 작업자 역할 toouse tooconfigure 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-106">It also describes how tooconfigure a web or worker role toouse a PHP runtime (with custom configuration and extensions) that you provide.</span></span>

## <a name="what-are-php-web-and-worker-roles"></a><span data-ttu-id="ab150-107">PHP 웹 및 작업자 역할이란?</span><span class="sxs-lookup"><span data-stu-id="ab150-107">What are PHP web and worker roles?</span></span>
<span data-ttu-id="ab150-108">Azure는 응용 프로그램을 실행하기 위한 세 가지 계산 모델인 Azure App Service, Azure 가상 컴퓨터 및 Azure Cloud Services를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-108">Azure provides three compute models for running applications: Azure App Service, Azure Virtual Machines, and Azure Cloud Services.</span></span> <span data-ttu-id="ab150-109">이 세 모델은 모두 PHP를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-109">All three models support PHP.</span></span> <span data-ttu-id="ab150-110">웹 및 작업자 역할을 포함하는 Cloud Services는 *PaaS(Platform as a Service)*를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-110">Cloud Services, which includes web and worker roles, provides *platform as a service (PaaS)*.</span></span> <span data-ttu-id="ab150-111">클라우드 서비스 내에서 웹 역할 서버 toohost 프런트 엔드 웹 응용 프로그램 전용된 인터넷 정보 서비스 (IIS) 웹을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-111">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server toohost front-end web applications.</span></span> <span data-ttu-id="ab150-112">작업자 역할은 비동기, 장기 실행 또는 영구 작업을 사용자 조작 또는 입력과 독립적으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-112">A worker role can run asynchronous, long-running or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="ab150-113">이러한 옵션에 대한 자세한 내용은 [Azure에서 제공하는 계산 호스팅 옵션](cloud-services/cloud-services-choose-me.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ab150-113">For more information about these options, see [Compute hosting options provided by Azure](cloud-services/cloud-services-choose-me.md).</span></span>

## <a name="download-hello-azure-sdk-for-php"></a><span data-ttu-id="ab150-114">PHP 용 hello Azure SDK 다운로드</span><span class="sxs-lookup"><span data-stu-id="ab150-114">Download hello Azure SDK for PHP</span></span>
<span data-ttu-id="ab150-115">hello [PHP 용 Azure SDK] 몇 가지 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-115">hello [Azure SDK for PHP] consists of several components.</span></span> <span data-ttu-id="ab150-116">이 문서는 그 중 두 개 사용 합니다: Azure PowerShell 및 Azure 에뮬레이터 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-116">This article will use two of them: Azure PowerShell and hello Azure emulators.</span></span> <span data-ttu-id="ab150-117">Hello Microsoft 웹 플랫폼 설치 관리자를 통해이 두 구성 요소를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-117">These two components can be installed via hello Microsoft Web Platform Installer.</span></span> <span data-ttu-id="ab150-118">자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-118">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="create-a-cloud-services-project"></a><span data-ttu-id="ab150-119">Cloud Services 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="ab150-119">Create a Cloud Services project</span></span>
<span data-ttu-id="ab150-120">PHP 웹 또는 작업자 역할을 만드는 hello 첫 번째 단계는 toocreate Azure 서비스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-120">hello first step in creating a PHP web or worker role is toocreate an Azure Service project.</span></span> <span data-ttu-id="ab150-121">Azure 서비스 프로젝트 웹 및 작업자 역할에 대 한 논리적 컨테이너로 사용 되 고 hello 프로젝트의 포함 된 [서비스 정의 (.csdef)] 및 [서비스 구성 (.cscfg)] 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-121">an Azure Service project serves as a logical container for web and worker roles, and it contains hello project's [service definition (.csdef)] and [service configuration (.cscfg)] files.</span></span>

<span data-ttu-id="ab150-122">toocreate 새 Azure 서비스 프로젝트를를 관리자로 Azure PowerShell을 실행 하 고 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-122">toocreate a new Azure Service project, run Azure PowerShell as an administrator, and execute hello following command:</span></span>

    PS C:\>New-AzureServiceProject myProject

<span data-ttu-id="ab150-123">이 명령은 새 디렉터리를 만듭니다 (`myProject`) toowhich 웹 및 작업자 역할을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-123">This command will create a new directory (`myProject`) toowhich you can add web and worker roles.</span></span>

## <a name="add-php-web-or-worker-roles"></a><span data-ttu-id="ab150-124">PHP 웹 또는 작업자 역할 추가</span><span class="sxs-lookup"><span data-stu-id="ab150-124">Add PHP web or worker roles</span></span>
<span data-ttu-id="ab150-125">tooadd PHP 웹 역할 tooa 프로젝트에서는 hello 다음 hello 프로젝트의 루트 디렉터리 내에서 명령을 실행 하는 중:</span><span class="sxs-lookup"><span data-stu-id="ab150-125">tooadd a PHP web role tooa project, run hello following command from within hello project's root directory:</span></span>

    PS C:\myProject> Add-AzurePHPWebRole roleName

<span data-ttu-id="ab150-126">작업자 역할의 경우에는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-126">For a worker role, use this command:</span></span>

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> <span data-ttu-id="ab150-127">hello `roleName` 매개 변수는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-127">hello `roleName` parameter is optional.</span></span> <span data-ttu-id="ab150-128">생략 하는 hello 역할 이름이 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-128">If it is omitted, hello role name will be automatically generated.</span></span> <span data-ttu-id="ab150-129">hello 첫 번째 웹 역할이 생성 됩니다 `WebRole1`, hello 둘째 됩니다 `WebRole2`등입니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-129">hello first web role created will be `WebRole1`, hello second will be `WebRole2`, and so on.</span></span> <span data-ttu-id="ab150-130">hello 첫 번째 작업자 역할이 생성 됩니다 `WorkerRole1`, hello 둘째 됩니다 `WorkerRole2`등입니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-130">hello first worker role created will be `WorkerRole1`, hello second will be `WorkerRole2`, and so on.</span></span>
>
>

## <a name="specify-hello-built-in-php-version"></a><span data-ttu-id="ab150-131">Hello 기본 제공 하는 PHP 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-131">Specify hello built-in PHP version</span></span>
<span data-ttu-id="ab150-132">PHP 웹 또는 작업자 역할 tooa 프로젝트에 추가 하면 hello 프로젝트의 구성 파일은 수정 되어 배포 될 때 PHP 응용 프로그램의 웹 또는 작업자 인스턴스마다에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-132">When you add a PHP web or worker role tooa project, hello project's configuration files are modified so that PHP will be installed on each web or worker instance of your application when it is deployed.</span></span> <span data-ttu-id="ab150-133">hello 다음 명령을 실행 합니다. 기본적으로 설치 될 PHP toosee hello 버전:</span><span class="sxs-lookup"><span data-stu-id="ab150-133">toosee hello version of PHP that will be installed by default, run hello following command:</span></span>

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

<span data-ttu-id="ab150-134">hello 위의 hello 명령의 출력은 유사 toowhat는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-134">hello output from hello command above will look similar toowhat is shown below.</span></span> <span data-ttu-id="ab150-135">이 예제에서는 hello `IsDefault` 플래그가 설정 너무`true` hello 기본 PHP 버전 설치 하다는 점을 나타내는 5.3.17, PHP에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-135">In this example, hello `IsDefault` flag is set too`true` for PHP 5.3.17, indicating that it will be hello default PHP version installed.</span></span>

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

<span data-ttu-id="ab150-136">나열 된 hello PHP 버전의 PHP 런타임 버전 tooany hello를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-136">You can set hello PHP runtime version tooany of hello PHP versions that are listed.</span></span> <span data-ttu-id="ab150-137">예를 들어 tooset hello PHP 버전 (hello 이름의 역할에 대 한 `roleName`) too5.4.0, 다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="ab150-137">For example, tooset hello PHP version (for a role with hello name `roleName`) too5.4.0, use hello following command:</span></span>

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> <span data-ttu-id="ab150-138">사용 가능한 PHP 버전 hello 나중에 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-138">Available PHP versions may change in hello future.</span></span>
>
>

## <a name="customize-hello-built-in-php-runtime"></a><span data-ttu-id="ab150-139">Hello 기본 제공 PHP 런타임에 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="ab150-139">Customize hello built-in PHP runtime</span></span>
<span data-ttu-id="ab150-140">위의 수정할을 포함 하 여 hello 단계를 수행 하는 경우 설치 된 hello PHP 런타임 hello 구성 완전 하 게 제어할 수 있습니다 `php.ini` 설정과 확장을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-140">You have complete control over hello configuration of hello PHP runtime that is installed when you follow hello steps above, including modification of `php.ini` settings and enabling of extensions.</span></span>

<span data-ttu-id="ab150-141">toocustomize 기본 제공 PHP 런타임에 hello, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-141">toocustomize hello built-in PHP runtime, follow these steps:</span></span>

1. <span data-ttu-id="ab150-142">라는 새 폴더 추가 `php`, toohello `bin` 웹 역할의 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-142">Add a new folder, named `php`, toohello `bin` directory of your web role.</span></span> <span data-ttu-id="ab150-143">작업자 역할에 대 한 루트 디렉터리 toohello 역할을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-143">For a worker role, add it toohello role's root directory.</span></span>
2. <span data-ttu-id="ab150-144">Hello에 `php` 폴더 라고 하는 다른 폴더를 만들고 `ext`합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-144">In hello `php` folder, create another folder called `ext`.</span></span> <span data-ttu-id="ab150-145">모든 배치 `.dll` 확장 파일 (예: `php_mongo.dll`)이이 폴더에 tooenable 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-145">Put any `.dll` extension files (e.g., `php_mongo.dll`) that you want tooenable in this folder.</span></span>
3. <span data-ttu-id="ab150-146">추가 `php.ini` toohello 파일 `php` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-146">Add a `php.ini` file toohello `php` folder.</span></span> <span data-ttu-id="ab150-147">사용자 지정 확장을 사용하도록 설정하고 이 파일에 PHP 지시문을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-147">Enable any custom extensions and set any PHP directives in this file.</span></span> <span data-ttu-id="ab150-148">예를 들어, tooturn 려 `display_errors` 에 hello를 사용 하도록 설정 하 고 `php_mongo.dll` 확장, hello 내용의 프로그램 `php.ini` 파일은 다음과 같을 수:</span><span class="sxs-lookup"><span data-stu-id="ab150-148">For example, if you wanted tooturn `display_errors` on and enable hello `php_mongo.dll` extension, hello contents of your `php.ini` file would be as follows:</span></span>

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> <span data-ttu-id="ab150-149">Hello에 명시적으로 설정 하지 않으면 모든 설정을 `php.ini` 됩니다는 자동으로 제공 하는 파일 tootheir 기본값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-149">Any settings that you don't explicitly set in hello `php.ini` file that you provide will automatically be set tootheir default values.</span></span> <span data-ttu-id="ab150-150">하지만 완전한 `php.ini` 파일을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-150">However, keep in mind that you can add a complete `php.ini` file.</span></span>
>
>

## <a name="use-your-own-php-runtime"></a><span data-ttu-id="ab150-151">고유 PHP 런타임 사용</span><span class="sxs-lookup"><span data-stu-id="ab150-151">Use your own PHP runtime</span></span>
<span data-ttu-id="ab150-152">경우에 따라 기본 제공 PHP 런타임에 선택 하 고 위에서 설명한 대로를 구성 하는 대신 좋습니다 tooprovide 고유한 PHP 런타임.</span><span class="sxs-lookup"><span data-stu-id="ab150-152">In some cases, instead of selecting a built-in PHP runtime and configuring it as described above, you may want tooprovide your own PHP runtime.</span></span> <span data-ttu-id="ab150-153">사용할 수는 예를 들어 개발 환경에서 사용 하는 웹 또는 작업자 역할에서 PHP 런타임에 동일한 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-153">For example, you can use hello same PHP runtime in a web or worker role that you use in your development environment.</span></span> <span data-ttu-id="ab150-154">이렇게 하면 보다 쉽게 tooensure hello 응용 프로그램이 프로덕션 환경에서 동작을 변경 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-154">This makes it easier tooensure that hello application will not change behavior in your production environment.</span></span>

### <a name="configure-a-web-role-toouse-your-own-php-runtime"></a><span data-ttu-id="ab150-155">웹 역할 toouse 고유한 PHP 런타임 구성</span><span class="sxs-lookup"><span data-stu-id="ab150-155">Configure a web role toouse your own PHP runtime</span></span>
<span data-ttu-id="ab150-156">웹 역할 toouse 제공 하는 PHP 런타임에 tooconfigure 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="ab150-156">tooconfigure a web role toouse a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="ab150-157">이 항목의 앞부분에서 설명한 대로 Azure 서비스 프로젝트를 만들고 PHP 웹 역할을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-157">Create an Azure Service project and add a PHP web role as described previously in this topic.</span></span>
2. <span data-ttu-id="ab150-158">만들기는 `php` 폴더 hello에 `bin` 웹 역할의 루트 디렉터리에는 다음 PHP 런타임 (모든 이진 파일, 구성 파일, 하위 폴더, 등) toohello 추가 폴더 `php` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-158">Create a `php` folder in hello `bin` folder that is in your web role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) toohello `php` folder.</span></span>
3. <span data-ttu-id="ab150-159">(선택 사항) PHP 런타임에 hello를 사용 하는 경우 [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], 해야 tooconfigure 웹 역할 tooinstall [SQL Server Native Client 2012] [ sql native client] 프로 비전 된 경우.</span><span class="sxs-lookup"><span data-stu-id="ab150-159">(OPTIONAL) If your PHP runtime uses hello [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need tooconfigure your web role tooinstall [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="ab150-160">toodo이 hello 추가 [sqlncli.msi x64 설치 관리자] toohello `bin` 웹 역할의 루트 디렉터리의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-160">toodo this, add hello [sqlncli.msi x64 installer] toohello `bin` folder in your web role's root directory.</span></span> <span data-ttu-id="ab150-161">자동으로 hello 다음 단계에 설명 된 hello 시작 스크립트는 hello 역할 프로 비전 될 때 hello 설치 관리자를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-161">hello startup script described in hello next step will silently run hello installer when hello role is provisioned.</span></span> <span data-ttu-id="ab150-162">PHP 런타임에 hello Microsoft Drivers for PHP for SQL Server 사용 하지 않는 경우에 hello hello 다음 단계에 표시 된 hello 스크립트에서 다음 줄을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-162">If your PHP runtime does not use hello Microsoft Drivers for PHP for SQL Server, you can remove hello following line from hello script shown in hello next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="ab150-163">구성 하는 시작 작업 정의 [인터넷 정보 서비스 (IIS)] [ iis.net] PHP 런타임 toohandle에 대 한 요청 toouse `.php` 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-163">Define a startup task that configures [Internet Information Services (IIS)][iis.net] toouse your PHP runtime toohandle requests for `.php` pages.</span></span> <span data-ttu-id="ab150-164">toodo이, 열기 hello `setup_web.cmd` 파일 (hello에 `bin` 웹 역할의 루트 디렉터리의 파일) 텍스트 편집기 및 그 내용을 스크립트 다음 hello 바꾸기:</span><span class="sxs-lookup"><span data-stu-id="ab150-164">toodo this, open hello `setup_web.cmd` file (in hello `bin` file of your web role's root directory) in a text editor and replace its contents with hello following script:</span></span>

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
5. <span data-ttu-id="ab150-165">응용 프로그램 파일 tooyour 웹 역할의 루트 디렉터리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-165">Add your application files tooyour web role's root directory.</span></span> <span data-ttu-id="ab150-166">Hello 웹 서버의 루트 디렉터리 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-166">This will be hello web server's root directory.</span></span>
6. <span data-ttu-id="ab150-167">Hello에 설명 된 대로 응용 프로그램을 게시 [응용 프로그램을 게시](#publish-your-application) 아래 섹션.</span><span class="sxs-lookup"><span data-stu-id="ab150-167">Publish your application as described in hello [Publish your application](#publish-your-application) section below.</span></span>

> [!NOTE]
> <span data-ttu-id="ab150-168">hello `download.ps1` 스크립트 (hello에 `bin` hello 웹 역할의 루트 디렉터리의 폴더) 고유한 PHP 런타임에 사용 하 여 앞서 설명한 hello 단계를 수행한 후에 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-168">hello `download.ps1` script (in hello `bin` folder of hello web role's root directory) can be deleted after you follow hello steps described above for using your own PHP runtime.</span></span>
>
>

### <a name="configure-a-worker-role-toouse-your-own-php-runtime"></a><span data-ttu-id="ab150-169">작업자 역할 toouse 고유한 PHP 런타임 구성</span><span class="sxs-lookup"><span data-stu-id="ab150-169">Configure a worker role toouse your own PHP runtime</span></span>
<span data-ttu-id="ab150-170">작업자 역할 toouse 제공 하는 PHP 런타임에 tooconfigure 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="ab150-170">tooconfigure a worker role toouse a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="ab150-171">이 항목의 앞부분에서 설명한 대로 Azure 서비스 프로젝트를 만들고 PHP 작업자 역할을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-171">Create an Azure Service project and add a PHP worker role as described previously in this topic.</span></span>
2. <span data-ttu-id="ab150-172">만들기는 `php` hello 작업자 역할의 루트 디렉터리에 폴더가 다음 PHP 런타임 (모든 이진 파일, 구성 파일, 하위 폴더, 등) toohello 추가 `php` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-172">Create a `php` folder in hello worker role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) toohello `php` folder.</span></span>
3. <span data-ttu-id="ab150-173">(선택 사항) PHP 런타임에 사용 하는 경우 [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], 해야 tooconfigure 작업자 역할 tooinstall [SQL Server Native Client 2012] [ sql native client] 프로 비전 된 경우.</span><span class="sxs-lookup"><span data-stu-id="ab150-173">(OPTIONAL) If your PHP runtime uses [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need tooconfigure your worker role tooinstall [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="ab150-174">toodo이 hello 추가 [sqlncli.msi x64 설치 관리자] toohello 작업자 역할의 루트 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-174">toodo this, add hello [sqlncli.msi x64 installer] toohello worker role's root directory.</span></span> <span data-ttu-id="ab150-175">자동으로 hello 다음 단계에 설명 된 hello 시작 스크립트는 hello 역할 프로 비전 될 때 hello 설치 관리자를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-175">hello startup script described in hello next step will silently run hello installer when hello role is provisioned.</span></span> <span data-ttu-id="ab150-176">PHP 런타임에 hello Microsoft Drivers for PHP for SQL Server 사용 하지 않는 경우에 hello hello 다음 단계에 표시 된 hello 스크립트에서 다음 줄을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-176">If your PHP runtime does not use hello Microsoft Drivers for PHP for SQL Server, you can remove hello following line from hello script shown in hello next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="ab150-177">추가 하는 시작 작업을 정의 하면 `php.exe` hello 역할 프로 비전 될 때 실행 toohello 작업자 역할의 PATH 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-177">Define a startup task that adds your `php.exe` executable toohello worker role's PATH environment variable when hello role is provisioned.</span></span> <span data-ttu-id="ab150-178">toodo이, 열기 hello `setup_worker.cmd` 텍스트 편집기에서 hello 작업자 역할의 루트 디렉터리에 파일을 hello 다음 스크립트의 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-178">toodo this, open hello `setup_worker.cmd` file (in hello worker role's root directory) in a text editor and replace its contents with hello following script:</span></span>

    ```cmd
    @echo on

    cd "%~dp0"

    echo Granting permissions for Network Service toohello web root directory...
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
5. <span data-ttu-id="ab150-179">응용 프로그램 파일 tooyour 작업자 역할의 루트 디렉터리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-179">Add your application files tooyour worker role's root directory.</span></span>
6. <span data-ttu-id="ab150-180">Hello에 설명 된 대로 응용 프로그램을 게시 [응용 프로그램을 게시](#publish-your-application) 아래 섹션.</span><span class="sxs-lookup"><span data-stu-id="ab150-180">Publish your application as described in hello [Publish your application](#publish-your-application) section below.</span></span>

## <a name="run-your-application-in-hello-compute-and-storage-emulators"></a><span data-ttu-id="ab150-181">계산 및 저장소 에뮬레이터의 hello 응용 프로그램을 실행합니다</span><span class="sxs-lookup"><span data-stu-id="ab150-181">Run your application in hello compute and storage emulators</span></span>
<span data-ttu-id="ab150-182">hello Azure 에뮬레이터는 로컬 환경을 제공를 테스트할 수 toohello 클라우드 배포 하기 전에 Azure 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-182">hello Azure emulators provide a local environment in which you can test your Azure application before you deploy it toohello cloud.</span></span> <span data-ttu-id="ab150-183">Hello 에뮬레이터와 Azure 환경 hello 간의 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-183">There are some differences between hello emulators and hello Azure environment.</span></span> <span data-ttu-id="ab150-184">을 더 잘 참조 toounderstand [hello Azure 저장소 에뮬레이터를 사용 하 여 개발 및 테스트에 대 한](storage/common/storage-use-emulator.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-184">toounderstand this better, see [Use hello Azure storage emulator for development and testing](storage/common/storage-use-emulator.md).</span></span>

<span data-ttu-id="ab150-185">PHP을 해야 toouse hello 계산 에뮬레이터를 로컬로 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-185">Note that you must have PHP installed locally toouse hello compute emulator.</span></span> <span data-ttu-id="ab150-186">hello 계산 에뮬레이터는 응용 프로그램 사용자 로컬 PHP 설치 toorun 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-186">hello compute emulator will use your local PHP installation toorun your application.</span></span>

<span data-ttu-id="ab150-187">toorun hello 에뮬레이터에서 프로젝트 실행 다음 프로젝트의 루트 디렉터리에서 명령을 hello:</span><span class="sxs-lookup"><span data-stu-id="ab150-187">toorun your project in hello emulators, execute hello following command from your project's root directory:</span></span>

    PS C:\MyProject> Start-AzureEmulator

<span data-ttu-id="ab150-188">출력 유사한 toothis를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-188">You will see output similar toothis:</span></span>

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

<span data-ttu-id="ab150-189">웹 브라우저를 열고 hello 출력에 표시 된 toohello 로컬 주소를 검색 하 여 hello 에뮬레이터에서 실행 중인 응용 프로그램을 볼 수 있습니다 (`http://127.0.0.1:81` 위의 hello 예제 출력에서).</span><span class="sxs-lookup"><span data-stu-id="ab150-189">You can see your application running in hello emulator by opening a web browser and browsing toohello local address shown in hello output (`http://127.0.0.1:81` in hello example output above).</span></span>

<span data-ttu-id="ab150-190">toostop hello 에뮬레이터,이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-190">toostop hello emulators, execute this command:</span></span>

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a><span data-ttu-id="ab150-191">응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="ab150-191">Publish your application</span></span>
<span data-ttu-id="ab150-192">toopublish 응용 프로그램 toofirst 가져오기 필요 하면 hello를 사용 하 여 게시 설정 [Import-azurepublishsettingsfile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ab150-192">toopublish your application, you need toofirst import your publish settings by using hello [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet.</span></span> <span data-ttu-id="ab150-193">Hello를 사용 하 여 응용 프로그램을 게시할 수 있습니다 다음 [게시 AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ab150-193">Then you can publish your application by using hello [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet.</span></span> <span data-ttu-id="ab150-194">로그인 하는 방법에 대 한 정보를 참조 하십시오. [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-194">For information about signing in, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab150-195">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ab150-195">Next steps</span></span>
<span data-ttu-id="ab150-196">자세한 내용은 참조 hello [PHP 개발자 센터](/develop/php/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ab150-196">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

[PHP 용 Azure SDK]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[서비스 정의 (.csdef)]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[서비스 구성 (.cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[sqlncli.msi x64 설치 관리자]: http://go.microsoft.com/fwlink/?LinkID=239648
