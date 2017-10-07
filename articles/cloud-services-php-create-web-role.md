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
# <a name="how-toocreate-php-web-and-worker-roles"></a>어떻게 toocreate PHP 웹 및 작업자 역할
## <a name="overview"></a>개요
이 가이드에서는 방법을 toocreate PHP 웹 또는 작업자 역할 Windows 개발 환경에서 사용할 수 있는 버전 "기본" hello에서 PHP의 특정 버전을 선택, 변경 hello PHP 구성을, 확장을 사용 하 고 마지막으로 배포 tooAzure 설명 합니다. 에 대해서도 설명 방법을 제공 하는 사용자 지정 구성 및 확장) (있음 PHP 런타임에 웹 또는 작업자 역할 toouse tooconfigure 합니다.

## <a name="what-are-php-web-and-worker-roles"></a>PHP 웹 및 작업자 역할이란?
Azure는 응용 프로그램을 실행하기 위한 세 가지 계산 모델인 Azure App Service, Azure 가상 컴퓨터 및 Azure Cloud Services를 제공합니다. 이 세 모델은 모두 PHP를 지원합니다. 웹 및 작업자 역할을 포함하는 Cloud Services는 *PaaS(Platform as a Service)*를 제공합니다. 클라우드 서비스 내에서 웹 역할 서버 toohost 프런트 엔드 웹 응용 프로그램 전용된 인터넷 정보 서비스 (IIS) 웹을 제공합니다. 작업자 역할은 비동기, 장기 실행 또는 영구 작업을 사용자 조작 또는 입력과 독립적으로 실행할 수 있습니다.

이러한 옵션에 대한 자세한 내용은 [Azure에서 제공하는 계산 호스팅 옵션](cloud-services/cloud-services-choose-me.md)을 참조하세요.

## <a name="download-hello-azure-sdk-for-php"></a>PHP 용 hello Azure SDK 다운로드
hello [PHP 용 Azure SDK] 몇 가지 구성 요소로 이루어져 있습니다. 이 문서는 그 중 두 개 사용 합니다: Azure PowerShell 및 Azure 에뮬레이터 hello 합니다. Hello Microsoft 웹 플랫폼 설치 관리자를 통해이 두 구성 요소를 설치할 수 있습니다. 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

## <a name="create-a-cloud-services-project"></a>Cloud Services 프로젝트 만들기
PHP 웹 또는 작업자 역할을 만드는 hello 첫 번째 단계는 toocreate Azure 서비스 프로젝트입니다. Azure 서비스 프로젝트 웹 및 작업자 역할에 대 한 논리적 컨테이너로 사용 되 고 hello 프로젝트의 포함 된 [서비스 정의 (.csdef)] 및 [서비스 구성 (.cscfg)] 파일입니다.

toocreate 새 Azure 서비스 프로젝트를를 관리자로 Azure PowerShell을 실행 하 고 hello 다음 명령을 실행 합니다.

    PS C:\>New-AzureServiceProject myProject

이 명령은 새 디렉터리를 만듭니다 (`myProject`) toowhich 웹 및 작업자 역할을 추가할 수 있습니다.

## <a name="add-php-web-or-worker-roles"></a>PHP 웹 또는 작업자 역할 추가
tooadd PHP 웹 역할 tooa 프로젝트에서는 hello 다음 hello 프로젝트의 루트 디렉터리 내에서 명령을 실행 하는 중:

    PS C:\myProject> Add-AzurePHPWebRole roleName

작업자 역할의 경우에는 다음 명령을 사용합니다.

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> hello `roleName` 매개 변수는 선택 사항입니다. 생략 하는 hello 역할 이름이 자동으로 생성 됩니다. hello 첫 번째 웹 역할이 생성 됩니다 `WebRole1`, hello 둘째 됩니다 `WebRole2`등입니다. hello 첫 번째 작업자 역할이 생성 됩니다 `WorkerRole1`, hello 둘째 됩니다 `WorkerRole2`등입니다.
>
>

## <a name="specify-hello-built-in-php-version"></a>Hello 기본 제공 하는 PHP 버전을 지정 합니다.
PHP 웹 또는 작업자 역할 tooa 프로젝트에 추가 하면 hello 프로젝트의 구성 파일은 수정 되어 배포 될 때 PHP 응용 프로그램의 웹 또는 작업자 인스턴스마다에 설치 됩니다. hello 다음 명령을 실행 합니다. 기본적으로 설치 될 PHP toosee hello 버전:

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

hello 위의 hello 명령의 출력은 유사 toowhat는 다음과 같습니다. 이 예제에서는 hello `IsDefault` 플래그가 설정 너무`true` hello 기본 PHP 버전 설치 하다는 점을 나타내는 5.3.17, PHP에 대 한 합니다.

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

나열 된 hello PHP 버전의 PHP 런타임 버전 tooany hello를 설정할 수 있습니다. 예를 들어 tooset hello PHP 버전 (hello 이름의 역할에 대 한 `roleName`) too5.4.0, 다음 명령을 사용 하 여 hello:

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> 사용 가능한 PHP 버전 hello 나중에 변경할 수 있습니다.
>
>

## <a name="customize-hello-built-in-php-runtime"></a>Hello 기본 제공 PHP 런타임에 사용자 지정
위의 수정할을 포함 하 여 hello 단계를 수행 하는 경우 설치 된 hello PHP 런타임 hello 구성 완전 하 게 제어할 수 있습니다 `php.ini` 설정과 확장을 사용 하도록 설정 합니다.

toocustomize 기본 제공 PHP 런타임에 hello, 다음이 단계를 수행 합니다.

1. 라는 새 폴더 추가 `php`, toohello `bin` 웹 역할의 디렉터리입니다. 작업자 역할에 대 한 루트 디렉터리 toohello 역할을 추가 합니다.
2. Hello에 `php` 폴더 라고 하는 다른 폴더를 만들고 `ext`합니다. 모든 배치 `.dll` 확장 파일 (예: `php_mongo.dll`)이이 폴더에 tooenable 되도록 합니다.
3. 추가 `php.ini` toohello 파일 `php` 폴더입니다. 사용자 지정 확장을 사용하도록 설정하고 이 파일에 PHP 지시문을 설정합니다. 예를 들어, tooturn 려 `display_errors` 에 hello를 사용 하도록 설정 하 고 `php_mongo.dll` 확장, hello 내용의 프로그램 `php.ini` 파일은 다음과 같을 수:

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> Hello에 명시적으로 설정 하지 않으면 모든 설정을 `php.ini` 됩니다는 자동으로 제공 하는 파일 tootheir 기본값을 설정할 수 있습니다. 하지만 완전한 `php.ini` 파일을 추가할 수 있습니다.
>
>

## <a name="use-your-own-php-runtime"></a>고유 PHP 런타임 사용
경우에 따라 기본 제공 PHP 런타임에 선택 하 고 위에서 설명한 대로를 구성 하는 대신 좋습니다 tooprovide 고유한 PHP 런타임. 사용할 수는 예를 들어 개발 환경에서 사용 하는 웹 또는 작업자 역할에서 PHP 런타임에 동일한 hello 합니다. 이렇게 하면 보다 쉽게 tooensure hello 응용 프로그램이 프로덕션 환경에서 동작을 변경 되지 것입니다.

### <a name="configure-a-web-role-toouse-your-own-php-runtime"></a>웹 역할 toouse 고유한 PHP 런타임 구성
웹 역할 toouse 제공 하는 PHP 런타임에 tooconfigure 다음이 단계를 따르십시오.

1. 이 항목의 앞부분에서 설명한 대로 Azure 서비스 프로젝트를 만들고 PHP 웹 역할을 추가합니다.
2. 만들기는 `php` 폴더 hello에 `bin` 웹 역할의 루트 디렉터리에는 다음 PHP 런타임 (모든 이진 파일, 구성 파일, 하위 폴더, 등) toohello 추가 폴더 `php` 폴더입니다.
3. (선택 사항) PHP 런타임에 hello를 사용 하는 경우 [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], 해야 tooconfigure 웹 역할 tooinstall [SQL Server Native Client 2012] [ sql native client] 프로 비전 된 경우. toodo이 hello 추가 [sqlncli.msi x64 설치 관리자] toohello `bin` 웹 역할의 루트 디렉터리의 폴더입니다. 자동으로 hello 다음 단계에 설명 된 hello 시작 스크립트는 hello 역할 프로 비전 될 때 hello 설치 관리자를 실행 해야 합니다. PHP 런타임에 hello Microsoft Drivers for PHP for SQL Server 사용 하지 않는 경우에 hello hello 다음 단계에 표시 된 hello 스크립트에서 다음 줄을 제거할 수 있습니다.

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. 구성 하는 시작 작업 정의 [인터넷 정보 서비스 (IIS)] [ iis.net] PHP 런타임 toohandle에 대 한 요청 toouse `.php` 페이지입니다. toodo이, 열기 hello `setup_web.cmd` 파일 (hello에 `bin` 웹 역할의 루트 디렉터리의 파일) 텍스트 편집기 및 그 내용을 스크립트 다음 hello 바꾸기:

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
5. 응용 프로그램 파일 tooyour 웹 역할의 루트 디렉터리를 추가 합니다. Hello 웹 서버의 루트 디렉터리 사용 됩니다.
6. Hello에 설명 된 대로 응용 프로그램을 게시 [응용 프로그램을 게시](#publish-your-application) 아래 섹션.

> [!NOTE]
> hello `download.ps1` 스크립트 (hello에 `bin` hello 웹 역할의 루트 디렉터리의 폴더) 고유한 PHP 런타임에 사용 하 여 앞서 설명한 hello 단계를 수행한 후에 삭제할 수 있습니다.
>
>

### <a name="configure-a-worker-role-toouse-your-own-php-runtime"></a>작업자 역할 toouse 고유한 PHP 런타임 구성
작업자 역할 toouse 제공 하는 PHP 런타임에 tooconfigure 다음이 단계를 따르십시오.

1. 이 항목의 앞부분에서 설명한 대로 Azure 서비스 프로젝트를 만들고 PHP 작업자 역할을 추가합니다.
2. 만들기는 `php` hello 작업자 역할의 루트 디렉터리에 폴더가 다음 PHP 런타임 (모든 이진 파일, 구성 파일, 하위 폴더, 등) toohello 추가 `php` 폴더입니다.
3. (선택 사항) PHP 런타임에 사용 하는 경우 [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], 해야 tooconfigure 작업자 역할 tooinstall [SQL Server Native Client 2012] [ sql native client] 프로 비전 된 경우. toodo이 hello 추가 [sqlncli.msi x64 설치 관리자] toohello 작업자 역할의 루트 디렉터리입니다. 자동으로 hello 다음 단계에 설명 된 hello 시작 스크립트는 hello 역할 프로 비전 될 때 hello 설치 관리자를 실행 해야 합니다. PHP 런타임에 hello Microsoft Drivers for PHP for SQL Server 사용 하지 않는 경우에 hello hello 다음 단계에 표시 된 hello 스크립트에서 다음 줄을 제거할 수 있습니다.

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. 추가 하는 시작 작업을 정의 하면 `php.exe` hello 역할 프로 비전 될 때 실행 toohello 작업자 역할의 PATH 환경 변수입니다. toodo이, 열기 hello `setup_worker.cmd` 텍스트 편집기에서 hello 작업자 역할의 루트 디렉터리에 파일을 hello 다음 스크립트의 내용을 바꿉니다.

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
5. 응용 프로그램 파일 tooyour 작업자 역할의 루트 디렉터리를 추가 합니다.
6. Hello에 설명 된 대로 응용 프로그램을 게시 [응용 프로그램을 게시](#publish-your-application) 아래 섹션.

## <a name="run-your-application-in-hello-compute-and-storage-emulators"></a>계산 및 저장소 에뮬레이터의 hello 응용 프로그램을 실행합니다
hello Azure 에뮬레이터는 로컬 환경을 제공를 테스트할 수 toohello 클라우드 배포 하기 전에 Azure 응용 프로그램입니다. Hello 에뮬레이터와 Azure 환경 hello 간의 차이가 있습니다. 을 더 잘 참조 toounderstand [hello Azure 저장소 에뮬레이터를 사용 하 여 개발 및 테스트에 대 한](storage/common/storage-use-emulator.md)합니다.

PHP을 해야 toouse hello 계산 에뮬레이터를 로컬로 설치 합니다. hello 계산 에뮬레이터는 응용 프로그램 사용자 로컬 PHP 설치 toorun 사용 합니다.

toorun hello 에뮬레이터에서 프로젝트 실행 다음 프로젝트의 루트 디렉터리에서 명령을 hello:

    PS C:\MyProject> Start-AzureEmulator

출력 유사한 toothis를 표시 됩니다.

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

웹 브라우저를 열고 hello 출력에 표시 된 toohello 로컬 주소를 검색 하 여 hello 에뮬레이터에서 실행 중인 응용 프로그램을 볼 수 있습니다 (`http://127.0.0.1:81` 위의 hello 예제 출력에서).

toostop hello 에뮬레이터,이 명령을 실행 합니다.

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a>응용 프로그램 게시
toopublish 응용 프로그램 toofirst 가져오기 필요 하면 hello를 사용 하 여 게시 설정 [Import-azurepublishsettingsfile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet. Hello를 사용 하 여 응용 프로그램을 게시할 수 있습니다 다음 [게시 AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet. 로그인 하는 방법에 대 한 정보를 참조 하십시오. [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

## <a name="next-steps"></a>다음 단계
자세한 내용은 참조 hello [PHP 개발자 센터](/develop/php/)합니다.

[PHP 용 Azure SDK]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[서비스 정의 (.csdef)]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[서비스 구성 (.cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[sqlncli.msi x64 설치 관리자]: http://go.microsoft.com/fwlink/?LinkID=239648
