---
title: "Python 및 Azure 클라우드 서비스 시작: aaaGet | Microsoft Docs"
description: "Python 도구를 사용 하 여 웹 역할과 작업자 역할을 포함 하 여 Visual Studio toocreate Azure 클라우드 서비스에 대해 간략하게 설명 합니다."
services: cloud-services
documentationcenter: python
author: thraka
manager: timlt
editor: 
ms.assetid: 5489405d-6fa9-4b11-a161-609103cbdc18
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: f5fd85e754839f146abe912351c59dc4a148c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a>Python Tools for Visual Studio의 Python 웹 및 작업자 역할

이 문서에서는 [Visual Studio용 Python Tools][Python Tools for Visual Studio]를 사용하여 Python 웹 및 작업자 역할을 사용하는 방법을 간략하게 설명합니다. 자세한 내용은 어떻게 toouse Visual Studio toocreate 및 Python을 사용 하는 기본 클라우드 서비스를 배포 합니다.

## <a name="prerequisites"></a>필수 조건
* [Visual Studio 2013, 2015 또는 2017](https://www.visualstudio.com/)
* [Visual Studio용 Python Tools][Python Tools for Visual Studio](PTVS)
* [VS 2013용 Azure SDK Tools][Azure SDK Tools for VS 2013] 또는  
[VS 2015용 Azure SDK Tools][Azure SDK Tools for VS 2015] 또는  
[VS 2017용 Azure SDK Tools][Azure SDK Tools for VS 2017]
* [Python 2.7 32비트][Python 2.7 32-bit] 또는 [Python 3.5 32비트][Python 3.5 32-bit]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a>Python 웹 및 작업자 역할 정의
Azure는 응용 프로그램을 실행하기 위한 세 가지 컴퓨팅 모델인 [Azure App Service의 Web Apps 기능][execution model-web sites], [Azure Virtual Machines][execution model-vms] 및 [Azure Cloud Services][execution model-cloud services]를 제공합니다. 이 세 모델은 모두 Python을 지원합니다. 웹 및 작업자 역할을 포함하는 Cloud Services는 *PaaS(Platform as a Service)*를 제공합니다. 클라우드 서비스 내에서 웹 역할 제공 하는 전용된 인터넷 정보 서비스 (IIS) 웹 서버 toohost 프런트 엔드 웹 응용 프로그램의 경우 작업자 역할 사용자 상호 작용 및 입력에 관계 없이 비동기, 장기 실행 또는 영구 작업을 실행할 수 합니다.

자세한 내용은 [Cloud Service란?]을 참조하세요.

> [!NOTE]
> *Toobuild 간단한 웹 사이트를 찾고 있습니까?*
> 시나리오는 간단한 웹 사이트 프런트 엔드만 있을 경우에 Azure 앱 서비스의 hello 경량 웹 응용 프로그램 기능을 사용 하는 것이 좋습니다. 웹 사이트 증가 하 고 요구 사항을 변경 하는 대로 tooa 클라우드 서비스를 쉽게 업그레이드할 수 있습니다. Hello 참조 <a href="/develop/python/">Python 개발자 센터</a> hello 웹 응용 프로그램 기능의 Azure 앱 서비스의 개발을 설명 하는 문서에 대 한 합니다.
> <br />
> 
> 

## <a name="project-creation"></a>프로젝트 만들기
Visual Studio에서 선택할 수 있습니다 **Azure 클라우드 서비스** hello에 **새 프로젝트** 대화 상자의 **Python**합니다.

![새 프로젝트 대화 상자](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

Hello Azure 클라우드 서비스 마법사에서 새 웹 및 작업자 역할을 만들 수 있습니다.

![Azure 클라우드 서비스 대화 상자](./media/cloud-services-python-ptvs/new-service-wizard.png)

hello 작업자 역할 템플릿을 상용구 코드 tooconnect tooan Azure 저장소 계정 또는 Azure 서비스 버스 함께 제공 됩니다.

![클라우드 서비스 솔루션](./media/cloud-services-python-ptvs/worker.png)

언제 든 지 웹 또는 작업자 역할 tooan 기존 클라우드 서비스를 추가할 수 있습니다.  솔루션에 tooadd 기존 프로젝트를 선택 하거나 새로 만들 수 있습니다.

![역할 추가 명령](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

클라우드 서비스는 여러 언어로 구현된 역할을 포함할 수 있습니다.  예를 들어 Django로 구현된 Python 웹 역할과 Python 또는 C# 작업자 역할이 포함될 수 있습니다.  서비스 버스 큐 또는 저장소 큐를 사용하면 역할 간에 쉽게 통신할 수 있습니다.

## <a name="install-python-on-hello-cloud-service"></a>Hello 클라우드 서비스에 Python을 설치 합니다.
> [!WARNING]
> hello 설치 스크립트 (이 문서를 마지막으로 수정한 hello 시간)에 설치 된 Visual Studio가 작동 하지 않습니다. 이 섹션에서는 해결 방법을 설명합니다.
> 
> 

hello 설치 스크립트와 hello 큰 문제는 python 설치 하지 마십시오입니다. 먼저 두 개의 정의 [시작 작업](cloud-services-startup-tasks.md) hello에 [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) 파일입니다. hello 첫 번째 작업 (**PrepPython.ps1**) 다운로드 하 고 hello Python 런타임의 설치 합니다. hello 두 번째 작업 (**PipInstaller.ps1**) 실행 pip tooinstall 종속성 할 수 있습니다.

다음 스크립트는 hello Python 3.5를 대상으로 작성 되었습니다. Toouse hello 버전을 원하는 경우 python, 집합 hello의 2.x **PYTHON2** 변수 파일 너무**에** hello 두 시작 작업 및 hello 런타임 작업에 대 한: `<Variable name="PYTHON2" value="<mark>on</mark>" />`합니다.

```xml
<Startup>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>
  </Task>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>

  </Task>

</Startup>
```

hello **PYTHON2** 및 **PYPATH** 변수 toohello 작업자 시작 작업을 추가 해야 합니다. hello **PYPATH** 변수 경우에 사용 hello **PYTHON2** 변수는 너무 설정**에**합니다.

```xml
<Runtime>
  <Environment>
    <Variable name="EMULATED">
      <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
    </Variable>
    <Variable name="PYTHON2" value="off" />
    <Variable name="PYPATH" value="%SystemDrive%\Python27" />
  </Environment>
  <EntryPoint>
    <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
  </EntryPoint>
</Runtime>
```

#### <a name="sample-servicedefinitioncsdef"></a>샘플 ServiceDefinition.csdef
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="AzureCloudServicePython" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRole1" vmsize="Small">
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" />
      <Setting name="Python2" />
    </ConfigurationSettings>
    <Startup>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="EMULATED">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
        </Variable>
        <Variable name="PYTHON2" value="off" />
        <Variable name="PYPATH" value="%SystemDrive%\Python27" />
      </Environment>
      <EntryPoint>
        <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
      </EntryPoint>
    </Runtime>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
  </WorkerRole>
</ServiceDefinition>
```



다음으로 hello를 만듭니다 **PrepPython.ps1** 및 **PipInstaller.ps1** hello에 대 한 파일 **. / b i n** 역할 폴더입니다.

#### <a name="preppythonps1"></a>PrepPython.ps1
이 스크립트는 Python을 설치합니다. 경우 hello **PYTHON2** 환경 변수는 너무 설정**에**, Python 2.7가 설치 되어 다음 그렇지 않은 경우 Python 3.5가 설치 되어 있습니다.

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if python is installed...$nl"
    if ($is_python2) {
        & "${env:SystemDrive}\Python27\python.exe"  -V | Out-Null
    }
    else {
        py -V | Out-Null
    }

    if (-not $?) {

        $url = "https://www.python.org/ftp/python/3.5.2/python-3.5.2-amd64.exe"
        $outFile = "${env:TEMP}\python-3.5.2-amd64.exe"

        if ($is_python2) {
            $url = "https://www.python.org/ftp/python/2.7.12/python-2.7.12.amd64.msi"
            $outFile = "${env:TEMP}\python-2.7.12.amd64.msi"
        }

        Write-Output "Not found, downloading $url too$outFile$nl"
        Invoke-WebRequest $url -OutFile $outFile
        Write-Output "Installing$nl"

        if ($is_python2) {
            Start-Process msiexec.exe -ArgumentList "/q", "/i", "$outFile", "ALLUSERS=1" -Wait
        }
        else {
            Start-Process "$outFile" -ArgumentList "/quiet", "InstallAllUsers=1" -Wait
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Already installed"
    }
}
```

#### <a name="pipinstallerps1"></a>PipInstaller.ps1
이 스크립트는 pip를 호출 하 고 hello에 설치 하는 모든 hello 종속성 **requirements.txt** 파일입니다. 경우 hello **PYTHON2** 환경 변수는 너무 설정**에**, Python 2.7을 사용 하는 다음 Python 3.5 그렇지 않으면 사용 됩니다.

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if requirements.txt exists$nl"
    if (Test-Path ..\requirements.txt) {
        Write-Output "Found. Processing pip$nl"

        if ($is_python2) {
            & "${env:SystemDrive}\Python27\python.exe" -m pip install -r ..\requirements.txt
        }
        else {
            py -m pip install -r ..\requirements.txt
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Not found$nl"
    }
}
```

#### <a name="modify-launchworkerps1"></a>LaunchWorker.ps1 수정
> [!NOTE]
> 경우 hello는 **작업자 역할** 프로젝트 **LauncherWorker.ps1** 파일은 필요한 tooexecute hello 시작 파일. 에 **웹 역할** 프로젝트를 hello 시작 파일 대신에 정의 된 hello 프로젝트 속성입니다.
> 
> 

hello **bin\LaunchWorker.ps1** toodo 준비 작업이 하지만 많은 실제로 작동 하지 않는 원래 만들어진 합니다. 다음 스크립트는 hello로 해당 파일의 내용을 hello를 대체 합니다.

이 스크립트 호출 hello **worker.py** python 프로젝트에서 파일입니다. 경우 hello **PYTHON2** 환경 변수는 너무 설정**에**, Python 2.7을 사용 하는 다음 Python 3.5 그렇지 않으면 사용 됩니다.

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated)
{
    Write-Output "Running worker.py$nl"

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
else
{
    Write-Output "Running (EMULATED) worker.py$nl"

    # Customize tooyour local dev environment

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
```

#### <a name="pscmd"></a>ps.cmd
Visual Studio 템플릿 hello 만들어져 있어야는 **ps.cmd** hello에 대 한 파일 **. / b i n** 폴더입니다. 이 셸 스크립트 래퍼 스크립트가 위의 hello PowerShell 호출를 호출 하는 hello PowerShell 래퍼의 hello 이름에 따라 로깅을 제공 합니다. 이 파일이 생성되지 않은 경우 포함되어야 하는 내용은 다음과 같습니다. 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a>로컬 실행
클라우드 서비스 프로젝트 hello 시작 프로젝트로 설정 하 고 F5 키를 누릅니다 hello 클라우드 서비스는 hello 로컬 Azure 에뮬레이터에서 실행 됩니다.

PTVS 지원 하지만 hello 에뮬레이터, 디버깅 (예: 중단점)에서 시작 작동 하지 않습니다.

toodebug 웹 및 작업자 역할, 역할 프로젝트 hello hello 시작 프로젝트로 설정 하 고 디버그할 수 대신 합니다.  여러 시작 프로젝트를 설정할 수도 있습니다.  Hello 솔루션을 마우스 오른쪽 단추로 클릭 한 다음 선택 **시작 프로젝트 설정**합니다.

![솔루션 시작 프로젝트 속성](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-tooazure"></a>TooAzure 게시
toopublish, hello 솔루션의 hello 클라우드 서비스 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **게시**합니다.

![Microsoft Azure 게시 로그인](./media/cloud-services-python-ptvs/publish-sign-in.png)

Hello 마법사를 따릅니다. 필요한 경우 원격 데스크톱을 사용합니다. 원격 데스크톱 toodebug 대상이 필요 때 유용 합니다.

설정 구성을 완료한 후 **게시**를 클릭합니다.

Hello 출력 창에 표시 되는 일부 진행 한 후 hello Microsoft Azure 활동 로그 창이 표시 됩니다.

![Microsoft Azure 활동 로그 창](./media/cloud-services-python-ptvs/publish-activity-log.png)

배포는 몇 분 toocomplete, 다음 웹 또는 작업자 역할은 Azure에서 실행!

### <a name="investigate-logs"></a>로그 조사
Hello 클라우드 서비스가 가상 컴퓨터 시작 되 고 Python 설치 후 모든 실패 메시지 hello 로그 toofind에서 볼 수 있습니다. 이러한 로그는 hello 아래의 **C:\Resources\Directory\\{역할} \LogFiles** 폴더입니다. **PrepPython.err.txt** hello 스크립트 잠그려고 할 때이 toodetect Python 설치 된 경우에서 오류가 하나 이상 포함 된 및 **PipInstaller.err.txt** 오래 된 버전의 pip는 불만 제기 될 수 있습니다.

## <a name="next-steps"></a>다음 단계
Visual Studio 용 Python 도구에서 웹 및 작업자 역할 사용에 대 한 자세한 내용을 보려면 hello PTVS 설명서를 참조 합니다.

* [Cloud Service 프로젝트][Cloud Service Projects]

Azure 저장소 서비스 또는 서비스 버스를 사용 하는 등 사용자 웹 및 작업자 역할에서 Azure 서비스를 사용 하는 방법에 대 한 자세한 내용은 다음 문서는 hello 참조:

* [Blob Service][Blob Service]
* [Table Service][Table Service]
* [큐 서비스][Queue Service]
* [Service Bus 큐][Service Bus Queues]
* [Service Bus 토픽][Service Bus Topics]

<!--Link references-->

[Cloud Service란?]: cloud-services-choose-me.md
[execution model-web sites]: ../app-service-web/app-service-web-overview.md
[execution model-vms]:../virtual-machines/windows/overview.md
[execution model-cloud services]: cloud-services-choose-me.md
[Python Developer Center]: /develop/python/

[Blob Service]:../storage/blobs/storage-python-how-to-use-blob-storage.md
[Queue Service]: ../storage/queues/storage-python-how-to-use-queue-storage.md
[Table Service]:../cosmos-db/table-storage-how-to-use-python.md
[Service Bus Queues]: ../service-bus-messaging/service-bus-python-how-to-use-queues.md
[Service Bus Topics]: ../service-bus-messaging/service-bus-python-how-to-use-topics-subscriptions.md


<!--External Link references-->

[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs
[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure SDK Tools for VS 2013]: http://go.microsoft.com/fwlink/?LinkId=746482
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=746481
[Azure SDK Tools for VS 2017]: http://go.microsoft.com/fwlink/?LinkId=746483
[Python 2.7 32-bit]: https://www.python.org/downloads/
[Python 3.5 32-bit]: https://www.python.org/downloads/
