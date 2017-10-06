---
title: "aaaUsing tooPublish tooDev Windows PowerShell 스크립트 및 테스트 환경 | Microsoft Docs"
description: "Visual Studio toopublish toodevelopment 및 테스트 환경에서 Windows PowerShell toouse 스크립트 하는 방법에 대해 알아봅니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5fff1301-5469-4d97-be88-c85c30f837c1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 491a058f96255576afa74f6156f20ae9559bb9f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-powershell-scripts-toopublish-toodev-and-test-environments"></a>Windows PowerShell을 사용 하 여 스크립트를 toopublish toodev 및 테스트 환경
Visual Studio에서 웹 응용 프로그램을 만들 때 웹 사이트 tooAzure의 뒷부분에 나오는 tooautomate hello 게시를 사용 하면 Azure 앱 서비스 또는 가상 컴퓨터에서 웹 응용 프로그램으로 Windows PowerShell 스크립트를 생성할 수 있습니다. 편집 하 hello Visual Studio 편집기 toosuit에서 Windows PowerShell 스크립트를 hello 요구 사항, 확장 또는 기존 빌드, 테스트 및 게시 스크립트와 hello 스크립트를 통합할 수 있습니다.

이러한 스크립트를 사용하면 일시적으로 사용할 사이트의 사용자 지정 버전(개발 및 테스트 환경이라고도 함)을 프로비저닝할 수 있습니다. 예를 들어 있습니다 수 설정 웹 사이트의 특정 버전 슬롯에서 웹 사이트 toorun hello 또는 Azure 가상 컴퓨터에서 테스트 도구 모음, 버그를 재현, 버그 수정을, 평가판 제안된 된 변경 내용을 테스트 또는 데모 또는 프레젠테이션을 위한 사용자 지정 환경을 설정 합니다. 프로젝트를 게시 하는 스크립트를 만든 후 필요에 따라 다시 hello 스크립트를 실행 하 여 동일한 환경을 다시 또는 테스트에 대 한 사용자 지정 환경을 웹 응용 프로그램 toocreate 직접 빌드할 hello 스크립트를 실행할 수 있습니다.

## <a name="what-you-need"></a>필요한 항목
* Azure SDK 2.3 이상 자세한 내용은 [Visual Studio 다운로드](http://go.microsoft.com/fwlink/?LinkID=624384)를 참조하세요.

웹 프로젝트에 대 한 hello Azure SDK toogenerate hello 스크립트 필요가 없습니다. 이 기능은 클라우드 서비스의 웹 역할이 아닌 웹 프로젝트용입니다.

* Azure PowerShell 0.7.4 이상 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 자세한 정보에 대 한 합니다.
* [Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) 이상

## <a name="additional-tools"></a>추가 도구
Azure 개발 시 Visual Studio에서 PowerShell을 사용하기 위한 추가 도구와 리소스를 사용할 수 있습니다. [Visual Studio용 PowerShell](http://go.microsoft.com/fwlink/?LinkId=404012)을 참조하세요.

## <a name="generating-hello-publish-scripts"></a>게시 스크립트 생성이 hello
Hello를 생성할 수에 따라 새 프로젝트를 만들 때 웹 사이트를 호스팅하는 가상 컴퓨터에 대 한 스크립트를 게시 [이러한 지침](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다. 또한 [Azure App Service에서 웹앱용 게시 스크립트를 생성](app-service-web/app-service-web-get-started-dotnet.md)할 수도 있습니다.

## <a name="scripts-that-visual-studio-generates"></a>Visual Studio에서 생성하는 스크립트
Visual Studio에서 호출 하는 솔루션 수준의 폴더 생성 **PublishScripts** 두 개의 Windows PowerShell 파일을 포함 하 여 가상 컴퓨터 또는 웹 사이트 및 hello에 사용할 수 있는 함수가 포함 된 모듈에 대 한 게시 스크립트 스크립트입니다. Visual Studio는 배포 하는 hello 프로젝트의 hello 세부 정보를 지정 하는 hello JSON 형식의 파일을 생성 합니다.

### <a name="windows-powershell-publish-script"></a>Windows PowerShell 게시 스크립트
게시 스크립트를 hello 특정 포함 tooa 웹 사이트 또는 가상 컴퓨터를 배포 하기 위한 단계를 게시 합니다. Visual Studio는 Windows PowerShell 배포를 위한 구문 색 지정을 제공합니다. Hello 함수를 사용할 수 있습니다 자유롭게 hello 함수를에서 편집할 수 hello 스크립트 toosuit 변경 요구 사항에 대 한 도움말입니다.

### <a name="windows-powershell-module"></a>Windows PowerShell 모듈
hello Visual Studio에서 생성 하는 모듈 hello 하는 함수를 포함 하는 Windows PowerShell 스크립트 사용 하 여 게시 합니다. 이 Azure PowerShell 함수로 되며 의도 한 toobe 수정 없습니다. 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 자세한 정보에 대 한 합니다.

### <a name="json-configuration-file"></a>JSON 구성 파일
hello에 hello JSON 파일을 만들지 **구성을** 폴더 및 어떤 리소스 toodeploy tooAzure 정확 하 게 지정 하는 구성 데이터를 포함 합니다. hello Visual Studio에서 생성 하는 hello 파일 이름은 프로젝트-이름-w a w S-dev.json 가상 컴퓨터를 만든 경우 웹 사이트 또는 프로젝트 이름 VM dev.json를 만든 경우. 다음은 웹 사이트를 만들 때 생성된 JSON 구성 파일의 예입니다. Hello 값의 대부분은 자체 설명입니다. hello 웹 사이트 이름은 프로젝트 이름과 일치 하지 않을 수 있으므로 Azure에서 생성 됩니다.

```json
{
    "environmentSettings": {
        "webSite": {
            "name": "WebApplication26632",
            "location": "West US"
        },
        "databases": [{
            "connectionStringName": "DefaultConnection",
            "databaseName": "WebApplication26632_db",
            "serverName": "YourDatabaseServerName",
            "user": "sqluser2",
            "password": "",
            "edition": "",
            "size": "",
            "collation": "",
            "location": "West US"
        }]
    }
}
```
가상 컴퓨터를 만들 때 hello JSON 구성 파일에 비슷한 toohello 다음 찾습니다. 만들어진 클라우드 서비스는 hello 가상 컴퓨터에 대 한 컨테이너로 참고 합니다. hello 가상 컴퓨터에는 HTTP 및 HTTPS를 통한 웹 액세스용 일반 끝점과 hello 뿐만 아니라 로컬 컴퓨터, 원격 데스크톱 및 Windows PowerShell에서 toohello 웹 사이트를 게시할 수 있는 웹 배포에 대 한 끝점 포함 되어 있습니다.

```json
{
    "environmentSettings": {
        "cloudService": {
            "name": "myusernamevm1",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myusernamevm1",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Win2K8R2SP1-Datacenter-201403.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [{
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [{
            "connectionStringName": "",
            "databaseName": "",
            "serverName": "",
            "user": "",
            "password": ""
        }],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

Hello를 실행 하는 경우 JSON 구성 toochange hello 편집할 수 스크립트를 게시 합니다. hello `cloudService` 및 `virtualMachine` 섹션이 모두 필요, 되지만 hello를 삭제할 수 있습니다 `databases` 필요 하지 않으면 섹션. Visual Studio에서 생성 하는 hello 기본 구성 파일에서 비어 있는 hello 속성은 선택 사항입니다. 값이 있는 hello 기본 구성 파일에는 필요 합니다.

Azure에서 단일 프로덕션 사이트 대신 여러 배포 환경 (슬롯 이라고 함)가 있는 웹 사이트를 설정한 경우 hello JSON 구성 파일의 hello 웹 사이트의 hello 이름에 hello 슬롯 이름을 포함할 수 있습니다. 예를 들어, 명명 된 웹 사이트가 있는 경우 **mysite** 및 명명 된 것에 대 한 슬롯 **테스트** hello URI는 mysite-test.cloudapp.net 이지만 hello 구성 파일에 올바른 이름을 toouse hello 인 한 다음 . 수만 이렇게 하면 hello 웹 사이트와 슬롯이 이미 구독에 있는 경우. 없는 경우 hello 슬롯을 지정 하지 않고 hello 스크립트를 실행 하 여 hello 웹 사이트를 만든 다음 만듭니다 hello의 hello 슬롯 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885), 그 후 hello 수정한 웹 사이트 이름으로 hello 스크립트를 실행 합니다. 웹앱의 배포 슬롯에 대한 자세한 내용은 [Azure App Service에서 웹앱에 대한 스테이징 환경 설정](app-service-web/web-sites-staged-publishing.md)을 참조하세요.

## <a name="how-toorun-hello-publish-scripts"></a>Toorun hello 스크립트를 게시 하는 방법
하기 전에 Windows PowerShell 스크립트를 실행 하지 않아도 hello 실행 정책 tooenable 스크립트 toorun 먼저 설정 해야 합니다. 취약 한 toomalware 또는 스크립트 실행과 관련이 있는 바이러스 인 경우 Windows PowerShell 스크립트 실행에서 보안 기능 tooprevent 사용자입니다.

### <a name="run-hello-script"></a>Hello 스크립트 실행
1. 프로젝트에 대 한 hello 웹 배포 패키지를 만듭니다. 웹 배포 패키지는 toocopy tooyour 웹 사이트 또는 가상 컴퓨터 파일이 있는 압축된 보관 (.zip 파일). Visual Studio에서 모든 웹 응용 프로그램에 사용할 웹 배포 패키지를 만들 수 있습니다.

![웹 배포 패키지 만들기](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

자세한 내용은 [방법: Visual Studio에서 웹 배포 패키지 만들기](https://msdn.microsoft.com/library/dd465323.aspx)를 참조하세요. Hello 섹션에 설명 된 대로 웹 배포 패키지의 hello 만들기를 자동화할 수도 있습니다 **사용자 지정 및 확장 hello에 대 한 게시 스크립트** 이 항목의 뒷부분에 나오는 합니다.

1. **솔루션 탐색기**를 hello 스크립트에 대 한 hello 상황에 맞는 메뉴를 열고 다음 선택 **PowerShell ISE로 열기**합니다.
2. 인 경우 hello이이 컴퓨터에서 Windows PowerShell 스크립트를 실행 하는 처음으로 관리자 권한 및 형식 hello 다음 명령을 사용 하 여 명령 프롬프트 창을 엽니다.

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. 다음 명령을 hello를 사용 하 여 tooAzure에 로그인 합니다.

    ```powershell
    Add-AzureAccount
    ```

    메시지가 표시되면 사용자 이름과 암호를 입력합니다.

    Note hello 스크립트 자동화 하면 Azure 자격 증명을 제공이 방법을 작동 하지 않습니다. 대신, hello.publishsettings 파일 tooprovide 자격 증명을 사용 해야 합니다. 한 번만 명령을 사용 하면 hello **Get-azurepublishsettingsfile** toodownload hello azure에서 파일을 사용 하 여 이후 **Import-azurepublishsettingsfile** tooimport hello 파일입니다. 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

4. (선택 사항) Azure toocreate 하려는 경우 hello 가상 컴퓨터, 데이터베이스 및 웹 응용 프로그램을 게시 하지 않고 웹 사이트와 같은 리소스 사용 hello **Publish-webapplication.ps1** hello로 명령을 **-구성** 인수 toohello JSON 구성 파일을 설정 합니다. 이 명령줄 어떤 리소스 toocreate JSON 구성 파일 toodetermine hello를 사용합니다. 다른 명령줄 인수에 대 한 기본 설정을 hello를 사용 하기 때문에 hello 리소스를 만들지만 웹 응용 프로그램을 게시 하지는 않습니다. hello-Verbose 옵션 자세한 정보를 제공 하는 상황에 대 한 합니다.

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. 사용 하 여 hello **Publish-webapplication.ps1** hello 예제 tooinvoke hello 스크립트를 다음 중 하나에 표시 된 것 처럼 명령 및 웹 응용 프로그램을 게시 합니다. 필요한 경우 toooverride hello 기본 설정을 hello에 대 한 hello 구독 이름 등의 다른 인수 패키지 이름, 가상 컴퓨터 자격 증명 또는 데이터베이스 서버 자격 증명을 게시 합니다. 이러한 매개 변수를 지정할 수 있습니다. 사용 하 여 hello **– Verbose** toosee hello 게시 프로세스의 hello 진행률에 대 한 자세한 내용은 옵션입니다.

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    가상 컴퓨터를 만드는 경우 hello 명령 hello 다음과 같습니다. 이 예제에서는 또한 toospecify hello 여러 데이터베이스에 대 한 자격 증명 하는 방법을 보여 줍니다. 이러한 스크립트로 만드는 hello 가상 컴퓨터에 대 한 hello SSL 인증서가 신뢰할 수 있는 루트 기관에서. 따라서 toouse hello **– AllowUntrusted** 옵션입니다.

    ```powershell
    Publish-WebApplication.ps1 `
    -Configuration C:\Path\ADVM-VM-test.json `
    -SubscriptionName Contoso `
    -WebDeployPackage C:\Path\ADVM.zip `
    -AllowUntrusted `
    -VMPassword @{name = "vmUserName"; password = "YourPasswordHere"} `
    -DatabaseServerPassword @{Name="server1";Password="adminPassword1"}, @{Name="server2";Password="adminPassword2"} `
    -Verbose
    ```

    hello 스크립트에 데이터베이스를 만들 수 있지만 데이터베이스 서버를 만들지는 않습니다. Hello toocreate 데이터베이스 서버를 원하는 경우 사용할 수 있습니다 **New-azuresqldatabaseserver** hello Azure 모듈의에서 함수입니다.

## <a name="customizing-and-extending-hello-publish-scripts"></a>사용자 지정 및 확장 hello에 대 한 게시 스크립트
Hello를 사용자 지정할 수 있습니다 스크립트 및 JSON 구성 파일을 게시 합니다. hello Windows PowerShell 모듈의 함수 hello **AzureWebAppPublishModule.psm1** 의도 한 toobe 수정 되지 않습니다. 다른 데이터베이스 toospecify 방금 싶거나 hello 가상 컴퓨터의 hello 속성의 일부 변경 hello JSON 구성 파일을 편집 합니다. 에 함수 스텁을 구현 하면 hello 스크립트 tooautomate 빌드 및 테스트 프로젝트의 tooextend hello 기능을 사용 하려면 **Publish-webapplication.ps1**합니다.

너무 MSBuild를 호출 하는 코드를 추가 하는 프로젝트를 빌드하지 tooautomate`New-WebDeployPackage` 이 코드 예제와 같이 합니다. hello 경로 toohello MSBuild 명령을 설치한 Visual Studio의 hello 버전에 따라 다릅니다. tooget hello 올바른 경로 hello 함수를 사용할 수 있습니다 **Get-msbuildcmd**이 예제에 나온 것 처럼 합니다.

### <a name="tooautomate-building-your-project"></a>프로젝트 빌드를 tooautomate
1. Hello 추가 `$ProjectFile` hello 전역 param 섹션에서 매개 변수입니다.

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. Copy 함수 hello `Get-MSBuildCmd` 스크립트 파일에 있습니다.

    ```powershell
    function Get-MSBuildCmd
    {
            process
    {

                $path =  Get-ChildItem "HKLM:\SOFTWARE\Microsoft\MSBuild\ToolsVersions\" |
                                    Sort-Object {[double]$_.PSChildName} -Descending |
                                    Select-Object -First 1 |
                                    Get-ItemProperty -Name MSBuildToolsPath |
                                    Select -ExpandProperty MSBuildToolsPath

                $path = (Join-Path -Path $path -ChildPath 'msbuild.exe')

            return Get-Item $path
        }
    }
    ```

3. 대체 `New-WebDeployPackage` 다음 코드로 바꾸고 줄 생성 hello에 hello 자리 표시자를 대체 하는 hello로 `$msbuildCmd`합니다. 이 코드는 Visual Studio 2015용입니다. Visual Studio 2013을 사용 하는 경우 변경 hello **VisualStudioVersion** 속성 아래 너무`12.0`합니다.

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function toobuild and package your web application
    ```

    toobuild 프로그램 웹 응용 프로그램을 MsBuild.exe를 사용 합니다. 도움말은 [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)에서 MSBuild 명령줄을 참조하세요.

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-hello-build-command"></a>Hello 빌드 명령 실행 시작

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain hello project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct hello path tooweb deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get hello full path for hello web deploy zip package. This is required for MSDeploy toowork
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. Hello 호출 `New-WebDeployPackage` 이 줄 앞 함수: `$Config = Read-ConfigFile $Configuration` 는 웹 응용 프로그램 또는 `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` 가상 컴퓨터에 대 한 합니다.

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. 사용자 지정 하는 hello 스크립트 전달 hello를 사용 하 여 명령줄에서 호출할 `$Project` hello 다음 예에서는 명령 줄에서와 같이 인수입니다.

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    코드를 너무 추가 응용 프로그램의 테스트 tooautomate`Test-WebApplication`합니다. 수 있는지 toouncomment hello 줄에 **Publish-webapplication.ps1** 이러한 함수 호출 됩니다. 구현을 제공 하지 않으면 수동으로 Visual Studio를 사용 하 여 프로젝트를 빌드할 수 있습니다 및 다음 실행된 hello 게시 스크립트 toopublish tooAzure 합니다.

## <a name="publishing-function-summary"></a>게시 함수 요약
hello Windows PowerShell 명령 프롬프트에서 사용 가능한 함수에 대 한 도움말 tooget hello 명령을 사용 하 여 `Get-Help function-name`합니다. hello 도움말에는 매개 변수 도움말과 예제가 포함 되어 있습니다. 동일한 도움말 텍스트는 hello 스크립트 원본 파일에도 hello **AzureWebAppPublishModule.psm1** 및 **Publish-webapplication.ps1**합니다. hello 스크립트와 도움말은 Visual Studio 언어로 지역화 됩니다.

**AzureWebAppPublishModule**

| 함수 이름 | 설명 |
| --- | --- |
| Add-AzureSQLDatabase |새 Azure SQL 데이터베이스를 만듭니다. |
| Add-AzureSQLDatabases |Visual Studio에서 생성 하는 hello JSON 구성 파일의 hello 값에서 Azure SQL 데이터베이스를 만듭니다. |
| Add-AzureVM |Azure 가상 컴퓨터를 만들고 hello의 hello URL VM 배포를 반환 합니다. hello 함수를 설정 hello 필수 조건 및 호출 hello **New-azurevm** (Azure 모듈) toocreate 새 가상 컴퓨터를 작동 합니다. |
| Add-AzureVMEndpoints |새 입력된 끝점 tooa 가상 컴퓨터를 추가 하 고 hello 새 끝점이 있는 hello 가상 컴퓨터를 반환 합니다. |
| Add-AzureVMStorage |Hello 현재 구독에서 새 Azure 저장소 계정을 만듭니다. hello 계정의 hello 이름을 다음 고유한 영숫자 문자열 "devtest"로 시작 합니다. hello 함수 hello hello 새 저장소 계정의 이름으로 반환합니다. 위치 또는 hello 새 저장소 계정에 대 한 선호도 그룹을 지정 해야 합니다. |
| Add-AzureWebsite |Hello 지정 된 이름 및 위치와 웹 사이트를 만듭니다. 이 함수 호출 hello **New-azurewebsite** hello Azure 모듈의에서 함수입니다. Hello 구독 된 hello 지정 된 이름의 웹 사이트가 아직 없는, 하는 경우이 함수는 hello 웹 사이트를 만들고 웹 사이트 개체를 반환 합니다. 그렇지 않으면 `$null`를 반환합니다. |
| 백업-구독 |저장 hello hello에 현재 Azure 구독 `$Script:originalSubscription` 스크립트 범위에서 변수입니다. Hello 현재 Azure 구독을 저장 하는이 함수 (여 얻어지는 `Get-AzureSubscription -Current`) 및 해당 저장소 계정과,이 스크립트에 의해 변경 된 hello 구독 (hello 변수에 저장 된 `$UserSpecifiedSubscription`) 및 해당 저장소 계정을 스크립트 범위에 있습니다. Hello 값으로 저장 하 여 사용할 수 있습니다는 함수 같은 `Restore-Subscription`, toorestore hello 원래 현재 구독과 저장소 계정 toocurrent 상태 hello 현재 상태가 변경 된 경우. |
| Find-AzureVM |Azure 가상 컴퓨터를 지정 하는 hello 가져옵니다. |
| Format-DevTestMessageWithTime |Hello 날짜 및 시간 tooa 메시지 앞에 추가 합니다. 이 함수는 toohello 오류 및 자세한 정보 스트림에 기록 된 메시지에 대 한 설계 되었습니다. |
| Get-AzureSQLDatabaseConnectionString |연결 문자열 tooconnect tooan Azure SQL 데이터베이스를 어셈블합니다. |
| Get-AzureVMStorage |반환 hello hello 이름 패턴 hello 첫 번째 저장소 계정의 이름을 "devtest*" (대/소문자 구분) hello 지정 된 위치 또는 선호도 그룹에서. 경우 hello "devtest*" hello 위치 또는 선호도 그룹에 저장소 계정 일치 하지 않습니다, hello 함수가를 무시 합니다. 위치 또는 선호도 그룹을 지정해야 합니다. |
| Get-MSDeployCmd |명령 toorun hello MsDeploy.exe 도구를 반환합니다. |
| New-AzureVMEnvironment |찾거나 hello JSON 구성 파일의 hello 값과 일치 하는 hello 구독에서 가상 컴퓨터를 만듭니다. |
| Publish-WebPackage |사용 하 여 MsDeploy.exe 및 웹 게시 패키지 합니다. Zip 파일 toodeploy 리소스 tooa 웹 사이트입니다. 이 함수는 출력을 생성하지 않습니다. Hello 호출 tooMSDeploy.exe 실패 hello 함수에서 예외가 발생 합니다. tooget 자세한 출력을 사용 하 여 hello **-Verbose** 옵션입니다. |
| Publish-WebPackageToVM |Hello 매개 변수 값을 확인 한 다음 호출 하는 hello **Publish-webpackage** 함수입니다. |
| Read-ConfigFile |Hello JSON 구성 파일의 유효성을 검사 하 고 선택한 값의 해시 테이블을 반환 합니다. |
| Restore-Subscription |Hello 현재 구독 toohello 원래 구독을 다시 설정합니다. |
| Test-AzureModule |반환 `$true` 경우 hello 설치 된 Azure 모듈 버전이 0.7.4 이상. 반환 `$false` 경우 hello 모듈이 설치 되지 않았거나 이전 버전입니다. 이 함수에는 매개 변수가 없습니다. |
| Test-AzureModuleVersion |반환 `$true` 경우 hello hello Azure 모듈 버전이 0.7.4 이상. 반환 `$false` 경우 hello 모듈이 설치 되지 않았거나 이전 버전입니다. 이 함수에는 매개 변수가 없습니다. |
| Test-HttpsUrl |Hello 입력된 URL tooa System.Uri 개체로 변환합니다. 반환 `$True` hello URL이 절대 주소이 고 스키마가 https 경우. 반환 `$false` 경우 hello URL은 상대의 구성표가 HTTPS가 아니거나 입력된 문자열 hello 변환된 tooa URL 일 수 없습니다. |
| Test-Member |반환 `$true` 메서드나 속성에 hello 개체의 멤버 이면 합니다. 그렇지 않으면 `$false`을(를) 반환합니다. |
| Write-ErrorWithTime |Hello로 현재 시간을 접두사로 한 오류 메시지를 씁니다. 이 함수 호출 hello **Format-devtestmessagewithtime** hello 메시지 toohello 오류 스트림에 쓰기 전에 함수 tooprepend hello 시간입니다. |
| Write-HostWithTime |메시지 toohello 호스트 프로그램 씁니다 (**Write-host**) 접두사로 hello 현재 시간입니다. hello toohello 호스트 프로그램을 작성 효과 달라 집니다. 대부분의 프로그램 Windows PowerShell을 호스팅하는 이러한 메시지에 기록 toostandard 출력 합니다. |
| Write-VerboseWithTime |Hello로 현재 시간을 접두사로 한 자세한 메시지를 씁니다. 호출 하므로 **Write-verbose**, hello 메시지 hello 스크립트를 실행할 때만 hello로 표시 됩니다. **Verbose** 매개 변수 또는 때 환영 **VerbosePreference** 기본 설정이입니다 도**계속**합니다. |

**Publish-WebApplication**

| 함수 이름 | 설명 |
| --- | --- |
| New-AzureWebApplicationEnvironment |웹 사이트, 가상 컴퓨터와 같은 Azure 리소스를 만듭니다. |
| New-WebDeployPackage |이 함수는 구현되지 않았습니다. 추가할 수 있습니다 명령에서이 함수 toobuild 프로젝트. |
| Publish-AzureWebApplication |웹 응용 프로그램 tooAzure를 게시합니다. |
| Publish-WebApplication |Visual Studio 웹 프로젝트를 위한 웹 앱, 가상 컴퓨터, SQL 데이터베이스, 저장소 계정을 만들고 배포합니다. |
| Test-WebApplication |이 함수는 구현되지 않았습니다. 있습니다 수에 명령을 추가 함수 tootest이 응용 프로그램. |

## <a name="next-steps"></a>다음 단계
참조 하 여 PowerShell 스크립트에 대 한 자세한 [Windows PowerShell과 함께 스크립팅](https://technet.microsoft.com/library/bb978526.aspx) hello에서 다른 Azure PowerShell 스크립트를 참조 하 고 [스크립트 센터](https://azure.microsoft.com/documentation/scripts/)합니다.
