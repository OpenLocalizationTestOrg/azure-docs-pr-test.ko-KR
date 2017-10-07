---
title: "클라우드 서비스에 대 한 시작 작업 aaaCommon | Microsoft Docs"
description: "몇 가지 예제 제공 일반적인 시작 작업의 tooperform 클라우드 서비스 웹 역할 또는 작업자 역할을 할 수도 있습니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: a7095dad-1ee7-4141-bc6a-ef19a6e570f1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: c80fac4079439410dfc3795e4bce0fbc07dbbfab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="common-cloud-service-startup-tasks"></a>일반적인 클라우드 서비스 시작 작업
이 문서는 몇 가지 예에서는 일반적인 시작 작업의 클라우드 서비스에서 tooperform를 사용할 수 있습니다. 역할 시작 되기 전에 시작 작업 tooperform 작업을 사용할 수 있습니다. Tooperform 알았으므로 작업에는 구성 요소를 설치, COM 구성 요소를 등록, 레지스트리 키 설정 또는 장기 실행 프로세스 시작 포함 됩니다. 

참조 [이 여기서](cloud-services-startup-tasks.md) toounderstand 시작 작업의 작동 방식 및 방법을 구체적으로 toocreate hello 시작 작업을 정의 하는 항목입니다.

> [!NOTE]
> 시작 작업은 적용 가능한 tooVirtual 컴퓨터 tooCloud 서비스 웹 및 작업자 역할 수 없습니다.
> 

## <a name="define-environment-variables-before-a-role-starts"></a>역할이 시작되기 전에 환경 변수를 정의합니다.
Hello를 사용 하 여 특정 작업에 대해 정의 된 환경 변수를 필요 하면 [환경] hello 내부 요소 [작업] 요소입니다.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
                <Environment>
                    <Variable name="MyEnvironmentVariable" value="MyVariableValue" />
                </Environment>
            </Task>
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

변수를 사용할 수도 [유효한 Azure XPath 값](cloud-services-role-config-xpath.md) hello 배포에 대 한 설명을 tooreference 합니다. Hello를 사용 하는 대신 `value` 특성을 정의 [RoleInstanceValue] 자식 요소입니다.

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a>Appcmd.exe를 사용하여 IIS 시작을 구성합니다.
hello [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) 명령줄 도구는 Azure에서 시작할 때 사용 되는 toomanage IIS 설정 될 수 있습니다. *AppCmd.exe* 편리 하 게, 명령줄 액세스 tooconfiguration 설정을 시작 작업에서 사용 하기 위해 Azure에서 제공 합니다. *AppCmd.exe*를 사용하면 응용 프로그램 및 사이트에 대해 웹사이트 설정을 추가, 수정하거나 제거할 수 있습니다.

그러나 여러 가지에 대 한 몇 가지 toowatch 아웃 hello 사용에서 *AppCmd.exe* 시작 작업으로:

* 시작 작업은 재부팅 사이 두 번 이상 실행할 수 있습니다. 예를 들어 역할을 재활용하는 경우입니다.
* *AppCmd.exe* 작업이 두 번 이상 수행되는 경우 오류를 생성할 수 있습니다. 예를 들어 tooadd 섹션을 너무 시도*Web.config* 두 번는 오류를 생성할 수 없습니다.
* 0이 아닌 종료 코드 또는 **errorlevel**을 반환하는 경우 시작 작업이 실패합니다. 예를 들어 *AppCmd.exe* 가 오류를 생성하는 경우입니다.

것이 좋습니다 toocheck hello **errorlevel** 호출한 후 *AppCmd.exe*, 너무 hello 호출을 래핑하는 경우 쉽게 toodo 변수인*AppCmd.exe* 와 *.cmd*  파일입니다. 알려진 **errorlevel** 응답을 발견하는 경우 무시하거나 다시 전송할 수 있습니다.

반환 되는 errorlevel hello *AppCmd.exe* hello winerror.h 파일에 나열 되어 있으며에 볼 수 있습니다 [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx)합니다.

### <a name="example-of-managing-hello-error-level"></a>Hello 오류 수준 관리 예
이 예제에서는 추가 압축 섹션 및 압축 항목에 대 한 JSON toohello *Web.config* 오류 처리 및 로깅 인 파일에 있습니다.

관련 섹션의 hello hello [ServiceDefinition.csdef] 파일 여기에 표시 된 hello 설정 등 [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) 너무 특성`elevated` toogive *AppCmd.exe*  hello에서 충분 한 사용 권한 toochange hello 설정을 *Web.config* 파일:

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="Startup.cmd" executionContext="elevated" taskType="simple" />
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

hello *Startup.cmd* 파일 사용 하 여 일괄 처리 *AppCmd.exe* tooadd 한 압축 섹션 및 압축 항목에 대 한 JSON toohello *Web.config* 파일입니다. 예상 hello **errorlevel** 183 toozero hello 확인을 사용 하 여 설정 됩니다. EXE 명령줄 프로그램입니다. 예기치 않은 errorlevel tooStartupErrorLog.txt 기록된 됩니다.

```cmd
REM   *** Add a compression section toohello Web.config file. ***
%windir%\system32\inetsrv\appcmd set config /section:urlCompression /doDynamicCompression:True /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1

REM   ERRORLEVEL 183 occurs when trying tooadd a section that already exists. This error is expected if this
REM   batch file were executed twice. This can occur and must be accounted for in a Azure startup
REM   task. toohandle this situation, set hello ERRORLEVEL toozero by using hello Verify command. hello Verify
REM   command will safely set hello ERRORLEVEL toozero.
IF %ERRORLEVEL% EQU 183 DO VERIFY > NUL

REM   If hello ERRORLEVEL is not zero at this point, some other error occurred.
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding a compression section toohello Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Add compression for json. ***
%windir%\system32\inetsrv\appcmd set config  -section:system.webServer/httpCompression /+"dynamicTypes.[mimeType='application/json; charset=utf-8',enabled='True']" /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1
IF %ERRORLEVEL% EQU 183 VERIFY > NUL
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding hello JSON compression type toohello Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Exit batch file. ***
EXIT /b 0

REM   *** Log error and exit ***
:ErrorExit
REM   Report hello date, time, and ERRORLEVEL of hello error.
DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
ECHO An error occurred during startup. ERRORLEVEL = %ERRORLEVEL% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT %ERRORLEVEL%
```

## <a name="add-firewall-rules"></a>방화벽 규칙 추가
Azure에는 사실상 두 개의 방화벽이 있습니다. hello 첫 번째 방화벽 hello 가상 컴퓨터와 hello 외부 세계 간의 연결을 제어 합니다. 이 방화벽을 제어 하 여 hello [끝점] hello 요소 [ServiceDefinition.csdef] 파일입니다.

두 번째 방화벽 hello hello 가상 컴퓨터 및 가상 컴퓨터에 있는 hello 프로세스 간의 연결을 제어 합니다. 이 방화벽 hello를 통해 제어할 수 `netsh advfirewall firewall` 명령줄 도구입니다.

Azure 역할 내에서 시작 하는 hello 프로세스에 대 한 방화벽 규칙을 만듭니다. 예를 들어, 서비스 또는 프로그램을 시작 하면 Azure 자동으로 만듭니다 hello 필요한 방화벽 규칙 tooallow 해당 서비스 toocommunicate 인터넷 hello로. 그러나 (예: COM + 서비스 또는 Windows의 예약 된 작업) 역할 외부의 프로세스에 의해 시작 되는 서비스를 만들면 필요 toomanually 방화벽 규칙 tooallow 액세스 toothat 서비스를 만듭니다. 이러한 방화벽 규칙은 시작 작업을 사용하여 만들 수 있습니다.

방화벽 규칙을 만드는 시작 작업은 [상승된][작업]  **executionContext**을 반환하는 경우 시작 작업이 실패합니다. 다음 시작 작업 toohello hello 추가 [ServiceDefinition.csdef] 파일입니다.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="AddFirewallRules.cmd" executionContext="elevated" taskType="simple" />
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

tooadd hello 방화벽 규칙을 적절 한 hello를 사용 해야 `netsh advfirewall firewall` 시작 배치 파일에서 명령을 합니다. 이 예제에서는 hello 시작 작업 TCP 포트 80에 대 한 보안 및 암호화 해야합니다.

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a>특정 IP 주소 차단
IIS를 수정 하 여 지정 된 IP 주소는 Azure 웹 역할 액세스 tooa 집합을 제한할 수 있습니다 **web.config** 파일입니다. 또한 toouse hello의 잠금을 해제 하는 명령 파일을 해야 **ipSecurity** hello 섹션 **ApplicationHost.config** 파일입니다.

toodo hello를 잠금 해제 **ipSecurity** hello 섹션 **ApplicationHost.config** 파일에서 역할 시작 될 때 실행 되는 명령 파일을 만듭니다. 호출 하 여 웹 역할의 hello 루트 수준 폴더를 만듭니다 **시작** 이 폴더 내에서 라는 배치 파일을 작성 하는 고 **startup.cmd**합니다. 이 파일 tooyour Visual Studio 프로젝트를 추가 하 고 hello 속성을 너무 설정**항상 복사** tooensure 패키지에 포함 됩니다.

다음 시작 작업 toohello hello 추가 [ServiceDefinition.csdef] 파일입니다.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WebRole name="WebRole1">
        ...
        <Startup>
            <Task commandLine="startup.cmd" executionContext="elevated" />
        </Startup>
    </WebRole>
</ServiceDefinition>
```

이 명령은 toohello 추가 **startup.cmd** 파일:

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

이 작업을 수행 하면 hello **startup.cmd** 필요한 해당 hello 보장 hello 웹 역할이 초기화 될 때마다 실행 파일 toobe 배치 **ipSecurity** 잠금을 해제 합니다.

Hello를 마지막으로 수정 [system.webServer 섹션이](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) 웹 역할의 **web.config** hello 다음 예제와 같이, 액세스가 허용 된 IP 주소의 목록을 tooadd 파일:

이 샘플 구성 **허용** 모든 Ip tooaccess hello 서버 hello 정의 된 두 개의 점을 제외 하 고

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are granted access-->
    <ipSecurity>
        <!--hello following IP addresses are denied access-->
        <add allowed="false" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="false" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

이 샘플 구성 **거부** 모든 Ip hello 두 정의 제외 하 고 hello 서버에 액세스 하지 못하도록 합니다.

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are denied access-->
    <ipSecurity allowUnlisted="false">
        <!--hello following IP addresses are granted access-->
        <add allowed="true" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="true" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

## <a name="create-a-powershell-startup-task"></a>PowerShell 시작 작업 만들기
Windows PowerShell 스크립트는 hello에서 직접 호출할 수 없습니다 [ServiceDefinition.csdef] 파일인 있지만 시작 배치 파일 내에서 호출 수입니다.

PowerShell은 기본적으로 서명되지 않은 스크립트를 실행하지 않습니다. 해야 tooconfigure PowerShell 스크립트를 서명 하지 않는 한 서명 되지 않은 스크립트 toorun 합니다. toorun 서명 되지 않은 스크립트를 hello **ExecutionPolicy** 너무 설정 되어 있어야**Unrestricted**합니다. hello **ExecutionPolicy** 설정 사용 하 여 hello 버전의 Windows PowerShell에 기반 합니다.

```cmd
REM   Run an unsigned PowerShell script and log hello output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

실행 되는 게스트 OS를 사용 하 여 PowerShell 2.0 또는 1.0 강제로 설정 버전 2 toorun 하 고, 사용할 수 없는 경우 버전 1을 사용 합니다.

```cmd
REM   Attempt tooset hello execution policy by using PowerShell version 2.0 syntax.
PowerShell -Version 2.0 -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If PowerShell version 2.0 isn't available. Set hello execution policy by using hello PowerShell
IF %ERRORLEVEL% EQU -393216 (
   PowerShell -Command "Set-ExecutionPolicy Unrestricted" >> "%TEMP%\StartupLog.txt" 2>&1
   PowerShell .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1
)

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="create-files-in-local-storage-from-a-startup-task"></a>시작 작업에서 로컬 저장소에 파일을 만듭니다.
로컬 저장소 리소스 toostore를 사용할 수 있는 응용 프로그램에 나중에 액세스 하는 시작 작업에서 만든 파일입니다.

toocreate hello 로컬 저장소 리소스를 추가 [LocalResources] 섹션 toohello [ServiceDefinition.csdef] 파일을 다음 hello 추가 [LocalStorage] 자식 요소입니다. 시작 작업에 대 한 고유 이름 및 적절 한 크기 hello 로컬 저장소 리소스를 제공 합니다.

시작 작업에서 로컬 저장소 리소스 toouse toocreate 환경 변수 tooreference hello 로컬 저장소 리소스 위치 해야합니다. 그런 다음 시작 작업을 hello 및 hello 응용 프로그램은 수 tooread 파일 toohello 로컬 저장소 리소스를 작성 합니다.

관련 섹션의 hello hello **ServiceDefinition.csdef** 파일은 다음과 같습니다.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WorkerRole name="WorkerRole1">
    ...

    <LocalResources>
      <LocalStorage name="StartupLocalStorage" sizeInMB="5"/>
    </LocalResources>

    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>
          <Variable name="PathToStartupStorage">
            <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
          </Variable>
        </Environment>
      </Task>
    </Startup>
  </WorkerRole>
</ServiceDefinition>
```

예를 들어이 **Startup.cmd** hello를 사용 하는 배치 파일 **PathToStartupStorage** 환경 변수 toocreate hello 파일 **MyTest.txt** 는 hello 로컬 저장소 위치입니다.

```cmd
REM   Create a simple text file.

ECHO This text will go into hello MyTest.txt file which will be in hello    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed tooby hello PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO hello contents of hello PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit hello batch file with ERRORLEVEL 0.

EXIT /b 0
```

Hello를 사용 하 여 hello Azure SDK에서에서 로컬 저장소 폴더에 액세스할 수 있습니다 [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) 메서드.

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-hello-emulator-or-cloud"></a>Hello 에뮬레이터 또는 클라우드 실행
Hello 계산 에뮬레이터에 hello 비해 클라우드 toowhen에서 작동 하는 경우 서로 다른 단계를 수행 하 여 시작 작업을 할 수 있습니다. 예를 들어 hello 에뮬레이터에서 실행 하는 경우에 toouse SQL 데이터의 새 복사본을 사용할 수 있습니다. 또는 toodo hello 클라우드 필요가 없다는 toodo hello 에뮬레이터에서 실행할 때 몇 가지 성능 최적화를 할 수 있습니다.

이 기능은 tooperform hello에 대 한 작업 계산 에뮬레이터 및 hello 클라우드 hello에서 환경 변수를 만들어 수행할 수 있습니다 다른 [ServiceDefinition.csdef] 파일입니다. 그런 다음 시작 태스크에서 값의 해당 환경 변수를 테스트합니다.

toocreate hello 환경 변수를 추가 hello [변수]/[RoleInstanceValue] 요소의 XPath 값을 만들고 `/RoleEnvironment/Deployment/@emulated`합니다. 값의 hello hello **% ComputeEmulatorRunning %** 환경 변수가 `true` hello 계산 에뮬레이터에서 실행 하는 경우 및 `false` hello 클라우드에서 실행 중인 경우.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WorkerRole name="WorkerRole1">

    ...

    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>
          <Variable name="ComputeEmulatorRunning">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
        </Environment>
      </Task>
    </Startup>

  </WorkerRole>
</ServiceDefinition>
```

hello 이제 검사할 수 hello **% ComputeEmulatorRunning %** 환경 변수 tooperform 다른 동작에서 hello hello 역할의 실행 여부에 따라 클라우드 또는 에뮬레이터를 환영 합니다. 해당 환경 변수를 검사하는 .cmd 셸 스크립트는 다음과 같습니다.

```cmd
REM   Check if this task is running on hello compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on hello compute emulator. Perform tasks that must be run only in hello compute emulator.
) ELSE (
    REM   This task is running on hello cloud. Perform tasks that must be run only in hello cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a>작업이 이미 실행되었는지 감지
다시 시작 작업 toorun 인해 다시 부팅 하지 않고 hello 역할이 재활용 될 수 있습니다. 작업 hello VM 호스트에서 이미 실행 하는 플래그 tooindicate 되지 않습니다. 여러 번 실행되는 것과 상관 없는 일부 작업이 있을 수 있습니다. 그러나 실행할 수 있습니다 tooprevent 해야 하는 경우에는 작업에서 두 번 이상 실행.

작업이 이미 실행 하는 hello 가장 간단한 방법은 toodetect toocreate hello에 있는 파일은 **% TEMP %** hello 작업의 시작 부분 hello 작업에 성공할 경우 폴더와 hello에 대 한 참조입니다. 해당 작업을 수행하는 예제 cmd 셸 스크립트는 다음과 같습니다.

```cmd
REM   If Task1_Success.txt exists, then Application 1 is already installed.
IF EXIST "%RoleRoot%\Task1_Success.txt" (
  ECHO Application 1 is already installed. Exiting. >> "%TEMP%\StartupLog.txt" 2>&1
  GOTO Finish
)

REM   Run your real exe task
ECHO Running XYZ >> "%TEMP%\StartupLog.txt" 2>&1
"%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (
  REM   hello application installed without error. Create a file tooindicate that hello task
  REM   does not need toobe run again.

  ECHO This line will create a file tooindicate that Application 1 installed correctly. > "%RoleRoot%\Task1_Success.txt"

) ELSE (
  REM   An error occurred. Log hello error and exit with hello error code.

  DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
  TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
  ECHO  An error occurred running task 1. Errorlevel = %ERRORLEVEL%. >> "%TEMP%\StartupLog.txt" 2>&1

  EXIT %ERRORLEVEL%
)

:Finish

REM   Exit normally.
EXIT /B 0
```

## <a name="task-best-practices"></a>작업 모범 사례
웹 또는 작업자 역할에 대한 작업을 구성할 때 따라야 하는 몇 가지 모범 사례는 다음과 같습니다.

### <a name="always-log-startup-activities"></a>항상 시작 작업 기록
Visual Studio 제공 하지 않습니다 디버거 toostep 일괄 처리 파일을 통해 좋은 tooget 이므로 많은 데이터 가능한 배치 파일의 hello 작업. 배치 파일의 hello 출력 로깅 모두 **stdout** 및 **stderr**, toodebug 하려고 할 때 중요 한 정보를 제공 하 고 배치 파일을 수정할 수 있습니다. 두 toolog **stdout** 및 **stderr** hello 디렉터리 뾰족한 tooby hello에서 toohello StartupLog.txt 파일 **% TEMP %** 환경 변수 hello 텍스트 추가`>>  "%TEMP%\\StartupLog.txt" 2>&1`특정 toohello 끝 줄 있습니다 사용할 toolog 합니다. 예를 들어 tooexecute setup.exe hello에 **% PathToApp1Install %** 디렉터리:

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

toosimplify xml에 래퍼를 만들 수 있습니다 *cmd* 시작 모두 호출 하는 파일 로깅 함께 작업 및 각 자식 작업 공유 hello 같은 환경 변수를 확인 합니다.

하지만 toouse까지 것 `>> "%TEMP%\StartupLog.txt" 2>&1` 각 시작 작업의 hello 끝에 있습니다. 사용자에 대한 로깅을 처리하는 래퍼를 만들어서 태스크 로깅을 적용할 수 있습니다. 이 래퍼 toorun 원하는 hello 실제 배치 파일을 호출 합니다. Hello 대상 배치 파일에서 모든 출력에는 리디렉션된 toohello 됩니다 *Startuplog.txt* 파일입니다.

다음 예제는 hello tooredirect 모든 시작 배치 파일에서 출력 하는 방법을 보여 줍니다. 이 예제에서는 hello ServerDefinition.csdef 파일은 호출 하는 시작 태스크를 만듭니다 *logwrap.cmd*합니다. *logwrap.cmd* 호출 *Startup2.cmd*, 모든 출력을 너무 리디렉션**% TEMP %\\StartupLog.txt**합니다.

ServiceDefinition.cmd:

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

**logwrap.cmd:**

```cmd
@ECHO OFF

REM   logwrap.cmd calls passed in batch file, redirecting all output toohello StartupLog.txt log file.

ECHO [%date% %time%] == START logwrap.cmd ============================================== >> "%TEMP%\StartupLog.txt" 2>&1
ECHO [%date% %time%] Running %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Call hello child command batch file, redirecting all output toohello StartupLog.txt log file.
START /B /WAIT %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Log hello completion of child command.
ECHO [%date% %time%] Done >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (

   REM   No errors occurred. Exit logwrap.cmd normally.
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B 0

) ELSE (

   REM   Log hello error.
   ECHO [%date% %time%] An error occurred. hello ERRORLEVEL = %ERRORLEVEL%.  >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B %ERRORLEVEL%

)
```

**Startup2.cmd:**

```cmd
@ECHO OFF

REM   This is hello batch file where hello startup steps should be performed. Because of the
REM   way Startup2.cmd was called, all commands and their outputs will be stored in the
REM   StartupLog.txt file in hello directory pointed tooby hello TEMP environment variable.

REM   If an error occurs, hello following command will pass hello ERRORLEVEL back toothe
REM   calling batch file.

ECHO [%date% %time%] Some log information about this task
ECHO [%date% %time%] Some more log information about this task

EXIT %ERRORLEVEL%
```

샘플 출력 hello에 **StartupLog.txt** 파일:

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> hello **StartupLog.txt** hello 파일은 *C:\Resources\temp\\{역할 식별자} \RoleTemp* 폴더입니다.
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a>시작 작업에 적절하게 executionContext 설정
적절 하 게 hello 시작 작업에 대 한 권한을 설정 합니다. 경우에 따라 시작 작업 hello 역할이 일반 권한으로 실행 하는 경우에 상승 된 권한으로 실행 해야 합니다.

hello [executionContext][작업] hello 시작 작업의 권한 수준을 hello를 설정 하는 특성입니다. 사용 하 여 `executionContext="limited"` 이면 hello 시작 작업에 hello hello 역할과 같은 권한 수준입니다. 사용 하 여 `executionContext="elevated"` hello 시작 작업에 관리자 권한이 수 있는 hello 시작 작업 tooperform 관리자 작업 권한 tooyour 역할 관리자를 제공 하지 않고도 것을 의미 합니다.

높은 권한이 필요한 시작 작업의 예로 시작 작업을 사용 하는 **AppCmd.exe** tooconfigure IIS 합니다. **AppCmd.exe**는 `executionContext="elevated"`이(가) 필요합니다.

### <a name="use-hello-appropriate-tasktype"></a>Hello 적절 한 taskType 사용
hello [taskType][작업] hello 방식으로 hello 시작 작업이 실행 되는 특성이 결정 됩니다. **간단**, **백그라운드** 및 **포그라운드**의 세 가지 값이 있습니다. hello background 및 foreground 작업 비동기적으로 시작 되 고 hello 간단한 작업이 동기적으로 실행 되는 한 번에 하나씩 있습니다.

와 **간단한** 시작 작업 hello ServiceDefinition.csdef 파일에 나열 된 작업 어느 hello의 hello 주문별 hello 작업이 실행 되 hello 순서를 설정할 수 있습니다. 경우는 **간단한** 작업 끝에 0이 아닌 종료 코드를 hello 시작 프로시저가 중지 하 고 hello 역할이 시작 되지 않습니다.

차이 hello **배경** 시작 작업 및 **전경** 시작 작업은 **전경** hello까지 hello 역할 실행을 유지 하는 작업  **전경** 작업이 끝날 합니다. 또한 즉 hello **전경** 작업 중단 되거나 충돌 hello까지 hello 역할이 재활용 되지 것입니다 **전경** 작업이 강제로 닫힙니다. 이러한 이유로 **배경** 작업의 hello 기능이 필요 하지 않는 한 비동기 시작 작업에 권장 되 **전경** 작업 합니다.

### <a name="end-batch-files-with-exit-b-0"></a>EXIT /B 0를 사용하여 배치 파일 끝내기
hello 역할은 경우에 시작 hello **errorlevel** 각 simple 시작 작업은 0입니다. Hello를 설정 하지 않는 프로그램도 **errorlevel** (종료 코드) 올바르게 하므로 hello 배치 파일 끝나야는 `EXIT /B 0` 모든 항목이 올바르게 실행 하는 경우.

누락 된 `EXIT /B 0` hello에서 시작 배치 파일의 끝은 시작 하지 않는 역할의 일반적인 원인입니다.

> [!NOTE]
> 중첩 된 해당 일괄 처리를 발견 했습니다 hello를 사용 하는 경우 파일의 경우에 따라 중지 `/B` 매개 변수입니다. 이 중단 문제가 hello를 사용 하는 경우 다음과 같은 경우 현재 배치 파일을 호출 하는 다른 일괄 처리 파일을 발생 하지 있는지 toomake 할 수 있습니다 [로그 래퍼](#always-log-startup-activities)합니다. Hello를 생략할 수 `/B` 이 경우 매개 변수입니다.
> 
> 

### <a name="expect-startup-tasks-toorun-more-than-once"></a>시작 작업 toorun를 두 번 이상 기대
모든 역할 재활용은 재부팅을 포함하지 않으므로 모든 역할 재활용은 모든 시작 작업 실행을 포함합니다. 이 시작 작업을 여러 번 문제 없이 재부팅 사이 수 toorun 이어야 함을 의미 합니다. Hello에 설명 되어 있음 [섹션 앞에 오는](#detect-that-your-task-has-already-run)합니다.

### <a name="use-local-storage-toostore-files-that-must-be-accessed-in-hello-role"></a>Hello 역할에 액세스 해야 하는 로컬 저장소 toostore 파일 사용
Toocopy 하거나 시작 작업 중 파일을 만들 경우 액세스할 수 있는 tooyour 역할은 다음 한 다음 해당 파일을 로컬 저장소에 배치 해야 합니다. Hello 참조 [섹션 앞에 오는](#create-files-in-local-storage-from-a-startup-task)합니다.

## <a name="next-steps"></a>다음 단계
Hello 클라우드 검토 [서비스 모델 및 패키지](cloud-services-model-and-package.md)

[작업](cloud-services-startup-tasks.md) 작동 방법에 대해 자세히 알아보세요.

[만들고 배포하세요](cloud-services-how-to-create-deploy-portal.md) .

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[작업]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[환경]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[변수]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
[끝점]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints
[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage
[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
