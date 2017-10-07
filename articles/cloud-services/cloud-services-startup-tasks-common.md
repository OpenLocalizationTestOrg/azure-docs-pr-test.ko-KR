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
# <a name="common-cloud-service-startup-tasks"></a><span data-ttu-id="76256-103">일반적인 클라우드 서비스 시작 작업</span><span class="sxs-lookup"><span data-stu-id="76256-103">Common Cloud Service startup tasks</span></span>
<span data-ttu-id="76256-104">이 문서는 몇 가지 예에서는 일반적인 시작 작업의 클라우드 서비스에서 tooperform를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-104">This article provides some examples of common startup tasks you may want tooperform in your cloud service.</span></span> <span data-ttu-id="76256-105">역할 시작 되기 전에 시작 작업 tooperform 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-105">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="76256-106">Tooperform 알았으므로 작업에는 구성 요소를 설치, COM 구성 요소를 등록, 레지스트리 키 설정 또는 장기 실행 프로세스 시작 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76256-106">Operations that you might want tooperform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span> 

<span data-ttu-id="76256-107">참조 [이 여기서](cloud-services-startup-tasks.md) toounderstand 시작 작업의 작동 방식 및 방법을 구체적으로 toocreate hello 시작 작업을 정의 하는 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-107">See [this article](cloud-services-startup-tasks.md) toounderstand how startup tasks work, and specifically how toocreate hello entries that define a startup task.</span></span>

> [!NOTE]
> <span data-ttu-id="76256-108">시작 작업은 적용 가능한 tooVirtual 컴퓨터 tooCloud 서비스 웹 및 작업자 역할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-108">Startup tasks are not applicable tooVirtual Machines, only tooCloud Service Web and Worker roles.</span></span>
> 

## <a name="define-environment-variables-before-a-role-starts"></a><span data-ttu-id="76256-109">역할이 시작되기 전에 환경 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-109">Define environment variables before a role starts</span></span>
<span data-ttu-id="76256-110">Hello를 사용 하 여 특정 작업에 대해 정의 된 환경 변수를 필요 하면 [환경] hello 내부 요소 [작업] 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-110">If you need environment variables defined for a specific task, use hello [Environment] element inside hello [Task] element.</span></span>

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

<span data-ttu-id="76256-111">변수를 사용할 수도 [유효한 Azure XPath 값](cloud-services-role-config-xpath.md) hello 배포에 대 한 설명을 tooreference 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-111">Variables can also use a [valid Azure XPath value](cloud-services-role-config-xpath.md) tooreference something about hello deployment.</span></span> <span data-ttu-id="76256-112">Hello를 사용 하는 대신 `value` 특성을 정의 [RoleInstanceValue] 자식 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-112">Instead of using hello `value` attribute, define a [RoleInstanceValue] child element.</span></span>

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a><span data-ttu-id="76256-113">Appcmd.exe를 사용하여 IIS 시작을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-113">Configure IIS startup with AppCmd.exe</span></span>
<span data-ttu-id="76256-114">hello [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) 명령줄 도구는 Azure에서 시작할 때 사용 되는 toomanage IIS 설정 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-114">hello [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) command-line tool can be used toomanage IIS settings at startup on Azure.</span></span> <span data-ttu-id="76256-115">*AppCmd.exe* 편리 하 게, 명령줄 액세스 tooconfiguration 설정을 시작 작업에서 사용 하기 위해 Azure에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-115">*AppCmd.exe* provides convenient, command-line access tooconfiguration settings for use in startup tasks on Azure.</span></span> <span data-ttu-id="76256-116">*AppCmd.exe*를 사용하면 응용 프로그램 및 사이트에 대해 웹사이트 설정을 추가, 수정하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-116">Using *AppCmd.exe*, Website settings can be added, modified, or removed for applications and sites.</span></span>

<span data-ttu-id="76256-117">그러나 여러 가지에 대 한 몇 가지 toowatch 아웃 hello 사용에서 *AppCmd.exe* 시작 작업으로:</span><span class="sxs-lookup"><span data-stu-id="76256-117">However, there are a few things toowatch out for in hello use of *AppCmd.exe* as a startup task:</span></span>

* <span data-ttu-id="76256-118">시작 작업은 재부팅 사이 두 번 이상 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-118">Startup tasks can be run more than once between reboots.</span></span> <span data-ttu-id="76256-119">예를 들어 역할을 재활용하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-119">For instance, when a role recycles.</span></span>
* <span data-ttu-id="76256-120">*AppCmd.exe* 작업이 두 번 이상 수행되는 경우 오류를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-120">If a *AppCmd.exe* action is performed more than once, it may generate an error.</span></span> <span data-ttu-id="76256-121">예를 들어 tooadd 섹션을 너무 시도*Web.config* 두 번는 오류를 생성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-121">For example, attempting tooadd a section too*Web.config* twice could generate an error.</span></span>
* <span data-ttu-id="76256-122">0이 아닌 종료 코드 또는 **errorlevel**을 반환하는 경우 시작 작업이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-122">Startup tasks fail if they return a non-zero exit code or **errorlevel**.</span></span> <span data-ttu-id="76256-123">예를 들어 *AppCmd.exe* 가 오류를 생성하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-123">For example, when *AppCmd.exe* generates an error.</span></span>

<span data-ttu-id="76256-124">것이 좋습니다 toocheck hello **errorlevel** 호출한 후 *AppCmd.exe*, 너무 hello 호출을 래핑하는 경우 쉽게 toodo 변수인*AppCmd.exe* 와 *.cmd*  파일입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-124">It is a good practice toocheck hello **errorlevel** after calling *AppCmd.exe*, which is easy toodo if you wrap hello call too*AppCmd.exe* with a *.cmd* file.</span></span> <span data-ttu-id="76256-125">알려진 **errorlevel** 응답을 발견하는 경우 무시하거나 다시 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-125">If you detect a known **errorlevel** response, you can ignore it, or pass it back.</span></span>

<span data-ttu-id="76256-126">반환 되는 errorlevel hello *AppCmd.exe* hello winerror.h 파일에 나열 되어 있으며에 볼 수 있습니다 [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-126">hello errorlevel returned by *AppCmd.exe* are listed in hello winerror.h file, and can also be seen on [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span></span>

### <a name="example-of-managing-hello-error-level"></a><span data-ttu-id="76256-127">Hello 오류 수준 관리 예</span><span class="sxs-lookup"><span data-stu-id="76256-127">Example of managing hello error level</span></span>
<span data-ttu-id="76256-128">이 예제에서는 추가 압축 섹션 및 압축 항목에 대 한 JSON toohello *Web.config* 오류 처리 및 로깅 인 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-128">This example adds a compression section and a compression entry for JSON toohello *Web.config* file, with error handling and logging.</span></span>

<span data-ttu-id="76256-129">관련 섹션의 hello hello [ServiceDefinition.csdef] 파일 여기에 표시 된 hello 설정 등 [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) 너무 특성`elevated` toogive *AppCmd.exe*  hello에서 충분 한 사용 권한 toochange hello 설정을 *Web.config* 파일:</span><span class="sxs-lookup"><span data-stu-id="76256-129">hello relevant sections of hello [ServiceDefinition.csdef] file are shown here, which include setting hello [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) attribute too`elevated` toogive *AppCmd.exe* sufficient permissions toochange hello settings in hello *Web.config* file:</span></span>

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

<span data-ttu-id="76256-130">hello *Startup.cmd* 파일 사용 하 여 일괄 처리 *AppCmd.exe* tooadd 한 압축 섹션 및 압축 항목에 대 한 JSON toohello *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-130">hello *Startup.cmd* batch file uses *AppCmd.exe* tooadd a compression section and a compression entry for JSON toohello *Web.config* file.</span></span> <span data-ttu-id="76256-131">예상 hello **errorlevel** 183 toozero hello 확인을 사용 하 여 설정 됩니다. EXE 명령줄 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-131">hello expected **errorlevel** of 183 is set toozero using hello VERIFY.EXE command-line program.</span></span> <span data-ttu-id="76256-132">예기치 않은 errorlevel tooStartupErrorLog.txt 기록된 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76256-132">Unexpected errorlevels are logged tooStartupErrorLog.txt.</span></span>

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

## <a name="add-firewall-rules"></a><span data-ttu-id="76256-133">방화벽 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="76256-133">Add firewall rules</span></span>
<span data-ttu-id="76256-134">Azure에는 사실상 두 개의 방화벽이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-134">In Azure, there are effectively two firewalls.</span></span> <span data-ttu-id="76256-135">hello 첫 번째 방화벽 hello 가상 컴퓨터와 hello 외부 세계 간의 연결을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-135">hello first firewall controls connections between hello virtual machine and hello outside world.</span></span> <span data-ttu-id="76256-136">이 방화벽을 제어 하 여 hello [끝점] hello 요소 [ServiceDefinition.csdef] 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-136">This firewall is controlled by hello [EndPoints] element in hello [ServiceDefinition.csdef] file.</span></span>

<span data-ttu-id="76256-137">두 번째 방화벽 hello hello 가상 컴퓨터 및 가상 컴퓨터에 있는 hello 프로세스 간의 연결을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-137">hello second firewall controls connections between hello virtual machine and hello processes within that virtual machine.</span></span> <span data-ttu-id="76256-138">이 방화벽 hello를 통해 제어할 수 `netsh advfirewall firewall` 명령줄 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-138">This firewall can be controlled by hello `netsh advfirewall firewall` command-line tool.</span></span>

<span data-ttu-id="76256-139">Azure 역할 내에서 시작 하는 hello 프로세스에 대 한 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76256-139">Azure creates firewall rules for hello processes started within your roles.</span></span> <span data-ttu-id="76256-140">예를 들어, 서비스 또는 프로그램을 시작 하면 Azure 자동으로 만듭니다 hello 필요한 방화벽 규칙 tooallow 해당 서비스 toocommunicate 인터넷 hello로.</span><span class="sxs-lookup"><span data-stu-id="76256-140">For example, when you start a service or program, Azure automatically creates hello necessary firewall rules tooallow that service toocommunicate with hello Internet.</span></span> <span data-ttu-id="76256-141">그러나 (예: COM + 서비스 또는 Windows의 예약 된 작업) 역할 외부의 프로세스에 의해 시작 되는 서비스를 만들면 필요 toomanually 방화벽 규칙 tooallow 액세스 toothat 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76256-141">However, if you create a service that is started by a process outside your role (like a COM+ service or a Windows Scheduled Task), you need toomanually create a firewall rule tooallow access toothat service.</span></span> <span data-ttu-id="76256-142">이러한 방화벽 규칙은 시작 작업을 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-142">These firewall rules can be created by using a startup task.</span></span>

<span data-ttu-id="76256-143">방화벽 규칙을 만드는 시작 작업은 [상승된][작업]  **executionContext**을 반환하는 경우 시작 작업이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-143">A startup task that creates a firewall rule must have an [executionContext][Task] of **elevated**.</span></span> <span data-ttu-id="76256-144">다음 시작 작업 toohello hello 추가 [ServiceDefinition.csdef] 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-144">Add hello following startup task toohello [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="76256-145">tooadd hello 방화벽 규칙을 적절 한 hello를 사용 해야 `netsh advfirewall firewall` 시작 배치 파일에서 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-145">tooadd hello firewall rule, you must use hello appropriate `netsh advfirewall firewall` commands in your startup batch file.</span></span> <span data-ttu-id="76256-146">이 예제에서는 hello 시작 작업 TCP 포트 80에 대 한 보안 및 암호화 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-146">In this example, hello startup task requires security and encryption for TCP port 80.</span></span>

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a><span data-ttu-id="76256-147">특정 IP 주소 차단</span><span class="sxs-lookup"><span data-stu-id="76256-147">Block a specific IP address</span></span>
<span data-ttu-id="76256-148">IIS를 수정 하 여 지정 된 IP 주소는 Azure 웹 역할 액세스 tooa 집합을 제한할 수 있습니다 **web.config** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-148">You can restrict an Azure web role access tooa set of specified IP addresses by modifying your IIS **web.config** file.</span></span> <span data-ttu-id="76256-149">또한 toouse hello의 잠금을 해제 하는 명령 파일을 해야 **ipSecurity** hello 섹션 **ApplicationHost.config** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-149">You also need toouse a command file which unlocks hello **ipSecurity** section of hello **ApplicationHost.config** file.</span></span>

<span data-ttu-id="76256-150">toodo hello를 잠금 해제 **ipSecurity** hello 섹션 **ApplicationHost.config** 파일에서 역할 시작 될 때 실행 되는 명령 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76256-150">toodo unlock hello **ipSecurity** section of hello **ApplicationHost.config** file, create a command file that runs at role start.</span></span> <span data-ttu-id="76256-151">호출 하 여 웹 역할의 hello 루트 수준 폴더를 만듭니다 **시작** 이 폴더 내에서 라는 배치 파일을 작성 하는 고 **startup.cmd**합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-151">Create a folder at hello root level of your web role called **startup** and, within this folder, create a batch file called **startup.cmd**.</span></span> <span data-ttu-id="76256-152">이 파일 tooyour Visual Studio 프로젝트를 추가 하 고 hello 속성을 너무 설정**항상 복사** tooensure 패키지에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76256-152">Add this file tooyour Visual Studio project and set hello properties too**Copy Always** tooensure that it is included in your package.</span></span>

<span data-ttu-id="76256-153">다음 시작 작업 toohello hello 추가 [ServiceDefinition.csdef] 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-153">Add hello following startup task toohello [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="76256-154">이 명령은 toohello 추가 **startup.cmd** 파일:</span><span class="sxs-lookup"><span data-stu-id="76256-154">Add this command toohello **startup.cmd** file:</span></span>

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

<span data-ttu-id="76256-155">이 작업을 수행 하면 hello **startup.cmd** 필요한 해당 hello 보장 hello 웹 역할이 초기화 될 때마다 실행 파일 toobe 배치 **ipSecurity** 잠금을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-155">This task causes hello **startup.cmd** batch file toobe run every time hello web role is initialized, ensuring that hello required **ipSecurity** section is unlocked.</span></span>

<span data-ttu-id="76256-156">Hello를 마지막으로 수정 [system.webServer 섹션이](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) 웹 역할의 **web.config** hello 다음 예제와 같이, 액세스가 허용 된 IP 주소의 목록을 tooadd 파일:</span><span class="sxs-lookup"><span data-stu-id="76256-156">Finally, modify hello [system.webServer section](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) your web role’s **web.config** file tooadd a list of IP addresses that are granted access, as shown in hello following example:</span></span>

<span data-ttu-id="76256-157">이 샘플 구성 **허용** 모든 Ip tooaccess hello 서버 hello 정의 된 두 개의 점을 제외 하 고</span><span class="sxs-lookup"><span data-stu-id="76256-157">This sample config **allows** all IPs tooaccess hello server except hello two defined</span></span>

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

<span data-ttu-id="76256-158">이 샘플 구성 **거부** 모든 Ip hello 두 정의 제외 하 고 hello 서버에 액세스 하지 못하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-158">This sample config **denies** all IPs from accessing hello server except for hello two defined.</span></span>

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

## <a name="create-a-powershell-startup-task"></a><span data-ttu-id="76256-159">PowerShell 시작 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="76256-159">Create a PowerShell startup task</span></span>
<span data-ttu-id="76256-160">Windows PowerShell 스크립트는 hello에서 직접 호출할 수 없습니다 [ServiceDefinition.csdef] 파일인 있지만 시작 배치 파일 내에서 호출 수입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-160">Windows PowerShell scripts cannot be called directly from hello [ServiceDefinition.csdef] file, but they can be invoked from within a startup batch file.</span></span>

<span data-ttu-id="76256-161">PowerShell은 기본적으로 서명되지 않은 스크립트를 실행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-161">PowerShell (by default) does not run unsigned scripts.</span></span> <span data-ttu-id="76256-162">해야 tooconfigure PowerShell 스크립트를 서명 하지 않는 한 서명 되지 않은 스크립트 toorun 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-162">Unless you sign your script, you need tooconfigure PowerShell toorun unsigned scripts.</span></span> <span data-ttu-id="76256-163">toorun 서명 되지 않은 스크립트를 hello **ExecutionPolicy** 너무 설정 되어 있어야**Unrestricted**합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-163">toorun unsigned scripts, hello **ExecutionPolicy** must be set too**Unrestricted**.</span></span> <span data-ttu-id="76256-164">hello **ExecutionPolicy** 설정 사용 하 여 hello 버전의 Windows PowerShell에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-164">hello **ExecutionPolicy** setting that you use is based on hello version of Windows PowerShell.</span></span>

```cmd
REM   Run an unsigned PowerShell script and log hello output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

<span data-ttu-id="76256-165">실행 되는 게스트 OS를 사용 하 여 PowerShell 2.0 또는 1.0 강제로 설정 버전 2 toorun 하 고, 사용할 수 없는 경우 버전 1을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-165">If you're using a Guest OS that is runs PowerShell 2.0 or 1.0 you can force version 2 toorun, and if unavailable, use version 1.</span></span>

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

## <a name="create-files-in-local-storage-from-a-startup-task"></a><span data-ttu-id="76256-166">시작 작업에서 로컬 저장소에 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76256-166">Create files in local storage from a startup task</span></span>
<span data-ttu-id="76256-167">로컬 저장소 리소스 toostore를 사용할 수 있는 응용 프로그램에 나중에 액세스 하는 시작 작업에서 만든 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-167">You can use a local storage resource toostore files created by your startup task that is accessed later by your application.</span></span>

<span data-ttu-id="76256-168">toocreate hello 로컬 저장소 리소스를 추가 [LocalResources] 섹션 toohello [ServiceDefinition.csdef] 파일을 다음 hello 추가 [LocalStorage] 자식 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-168">toocreate hello local storage resource, add a [LocalResources] section toohello [ServiceDefinition.csdef] file and then add hello [LocalStorage] child element.</span></span> <span data-ttu-id="76256-169">시작 작업에 대 한 고유 이름 및 적절 한 크기 hello 로컬 저장소 리소스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-169">Give hello local storage resource a unique name and an appropriate size for your startup task.</span></span>

<span data-ttu-id="76256-170">시작 작업에서 로컬 저장소 리소스 toouse toocreate 환경 변수 tooreference hello 로컬 저장소 리소스 위치 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-170">toouse a local storage resource in your startup task, you need toocreate an environment variable tooreference hello local storage resource location.</span></span> <span data-ttu-id="76256-171">그런 다음 시작 작업을 hello 및 hello 응용 프로그램은 수 tooread 파일 toohello 로컬 저장소 리소스를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-171">Then hello startup task and hello application are able tooread and write files toohello local storage resource.</span></span>

<span data-ttu-id="76256-172">관련 섹션의 hello hello **ServiceDefinition.csdef** 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-172">hello relevant sections of hello **ServiceDefinition.csdef** file are shown here:</span></span>

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

<span data-ttu-id="76256-173">예를 들어이 **Startup.cmd** hello를 사용 하는 배치 파일 **PathToStartupStorage** 환경 변수 toocreate hello 파일 **MyTest.txt** 는 hello 로컬 저장소 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-173">As an example, this **Startup.cmd** batch file uses hello **PathToStartupStorage** environment variable toocreate hello file **MyTest.txt** on hello local storage location.</span></span>

```cmd
REM   Create a simple text file.

ECHO This text will go into hello MyTest.txt file which will be in hello    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed tooby hello PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO hello contents of hello PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit hello batch file with ERRORLEVEL 0.

EXIT /b 0
```

<span data-ttu-id="76256-174">Hello를 사용 하 여 hello Azure SDK에서에서 로컬 저장소 폴더에 액세스할 수 있습니다 [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) 메서드.</span><span class="sxs-lookup"><span data-stu-id="76256-174">You can access local storage folder from hello Azure SDK by using hello [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-hello-emulator-or-cloud"></a><span data-ttu-id="76256-175">Hello 에뮬레이터 또는 클라우드 실행</span><span class="sxs-lookup"><span data-stu-id="76256-175">Run in hello emulator or cloud</span></span>
<span data-ttu-id="76256-176">Hello 계산 에뮬레이터에 hello 비해 클라우드 toowhen에서 작동 하는 경우 서로 다른 단계를 수행 하 여 시작 작업을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-176">You can have your startup task perform different steps when it is operating in hello cloud compared toowhen it is in hello compute emulator.</span></span> <span data-ttu-id="76256-177">예를 들어 hello 에뮬레이터에서 실행 하는 경우에 toouse SQL 데이터의 새 복사본을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-177">For example, you may want toouse a fresh copy of your SQL data only when running in hello emulator.</span></span> <span data-ttu-id="76256-178">또는 toodo hello 클라우드 필요가 없다는 toodo hello 에뮬레이터에서 실행할 때 몇 가지 성능 최적화를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-178">Or you may want toodo some performance optimizations for hello cloud that you don't need toodo when running in hello emulator.</span></span>

<span data-ttu-id="76256-179">이 기능은 tooperform hello에 대 한 작업 계산 에뮬레이터 및 hello 클라우드 hello에서 환경 변수를 만들어 수행할 수 있습니다 다른 [ServiceDefinition.csdef] 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-179">This ability tooperform different actions on hello compute emulator and hello cloud can be accomplished by creating an environment variable in hello [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="76256-180">그런 다음 시작 태스크에서 값의 해당 환경 변수를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-180">You then test that environment variable for a value in your startup task.</span></span>

<span data-ttu-id="76256-181">toocreate hello 환경 변수를 추가 hello [변수]/[RoleInstanceValue] 요소의 XPath 값을 만들고 `/RoleEnvironment/Deployment/@emulated`합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-181">toocreate hello environment variable, add hello [Variable]/[RoleInstanceValue] element and create an XPath value of `/RoleEnvironment/Deployment/@emulated`.</span></span> <span data-ttu-id="76256-182">값의 hello hello **% ComputeEmulatorRunning %** 환경 변수가 `true` hello 계산 에뮬레이터에서 실행 하는 경우 및 `false` hello 클라우드에서 실행 중인 경우.</span><span class="sxs-lookup"><span data-stu-id="76256-182">hello value of hello **%ComputeEmulatorRunning%** environment variable is `true` when running on hello compute emulator, and `false` when running on hello cloud.</span></span>

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

<span data-ttu-id="76256-183">hello 이제 검사할 수 hello **% ComputeEmulatorRunning %** 환경 변수 tooperform 다른 동작에서 hello hello 역할의 실행 여부에 따라 클라우드 또는 에뮬레이터를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-183">hello task can now check hello **%ComputeEmulatorRunning%** environment variable tooperform different actions based on whether hello role is running in hello cloud or hello emulator.</span></span> <span data-ttu-id="76256-184">해당 환경 변수를 검사하는 .cmd 셸 스크립트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-184">Here is a .cmd shell script that checks for that environment variable.</span></span>

```cmd
REM   Check if this task is running on hello compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on hello compute emulator. Perform tasks that must be run only in hello compute emulator.
) ELSE (
    REM   This task is running on hello cloud. Perform tasks that must be run only in hello cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a><span data-ttu-id="76256-185">작업이 이미 실행되었는지 감지</span><span class="sxs-lookup"><span data-stu-id="76256-185">Detect that your task has already run</span></span>
<span data-ttu-id="76256-186">다시 시작 작업 toorun 인해 다시 부팅 하지 않고 hello 역할이 재활용 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-186">hello role may recycle without a reboot causing your startup tasks toorun again.</span></span> <span data-ttu-id="76256-187">작업 hello VM 호스트에서 이미 실행 하는 플래그 tooindicate 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-187">There is no flag tooindicate that a task has already run on hello hosting VM.</span></span> <span data-ttu-id="76256-188">여러 번 실행되는 것과 상관 없는 일부 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-188">You may have some tasks where it doesn't matter that they run multiple times.</span></span> <span data-ttu-id="76256-189">그러나 실행할 수 있습니다 tooprevent 해야 하는 경우에는 작업에서 두 번 이상 실행.</span><span class="sxs-lookup"><span data-stu-id="76256-189">However, you may run into a situation where you need tooprevent a task from running more than once.</span></span>

<span data-ttu-id="76256-190">작업이 이미 실행 하는 hello 가장 간단한 방법은 toodetect toocreate hello에 있는 파일은 **% TEMP %** hello 작업의 시작 부분 hello 작업에 성공할 경우 폴더와 hello에 대 한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-190">hello simplest way toodetect that a task has already run is toocreate a file in hello **%TEMP%** folder when hello task is successful and look for it at hello start of hello task.</span></span> <span data-ttu-id="76256-191">해당 작업을 수행하는 예제 cmd 셸 스크립트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-191">Here is a sample cmd shell script that does that for you.</span></span>

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

## <a name="task-best-practices"></a><span data-ttu-id="76256-192">작업 모범 사례</span><span class="sxs-lookup"><span data-stu-id="76256-192">Task best practices</span></span>
<span data-ttu-id="76256-193">웹 또는 작업자 역할에 대한 작업을 구성할 때 따라야 하는 몇 가지 모범 사례는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-193">Here are some best practices you should follow when configuring task for your web or worker role.</span></span>

### <a name="always-log-startup-activities"></a><span data-ttu-id="76256-194">항상 시작 작업 기록</span><span class="sxs-lookup"><span data-stu-id="76256-194">Always log startup activities</span></span>
<span data-ttu-id="76256-195">Visual Studio 제공 하지 않습니다 디버거 toostep 일괄 처리 파일을 통해 좋은 tooget 이므로 많은 데이터 가능한 배치 파일의 hello 작업.</span><span class="sxs-lookup"><span data-stu-id="76256-195">Visual Studio does not provide a debugger toostep through batch files, so it's good tooget as much data on hello operation of batch files as possible.</span></span> <span data-ttu-id="76256-196">배치 파일의 hello 출력 로깅 모두 **stdout** 및 **stderr**, toodebug 하려고 할 때 중요 한 정보를 제공 하 고 배치 파일을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-196">Logging hello output of batch files, both **stdout** and **stderr**, can give you important information when trying toodebug and fix batch files.</span></span> <span data-ttu-id="76256-197">두 toolog **stdout** 및 **stderr** hello 디렉터리 뾰족한 tooby hello에서 toohello StartupLog.txt 파일 **% TEMP %** 환경 변수 hello 텍스트 추가`>>  "%TEMP%\\StartupLog.txt" 2>&1`특정 toohello 끝 줄 있습니다 사용할 toolog 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-197">toolog both **stdout** and **stderr** toohello StartupLog.txt file in hello directory pointed tooby hello **%TEMP%** environment variable, add hello text `>>  "%TEMP%\\StartupLog.txt" 2>&1` toohello end of specific lines you want toolog.</span></span> <span data-ttu-id="76256-198">예를 들어 tooexecute setup.exe hello에 **% PathToApp1Install %** 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="76256-198">For example, tooexecute setup.exe in hello **%PathToApp1Install%** directory:</span></span>

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

<span data-ttu-id="76256-199">toosimplify xml에 래퍼를 만들 수 있습니다 *cmd* 시작 모두 호출 하는 파일 로깅 함께 작업 및 각 자식 작업 공유 hello 같은 환경 변수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-199">toosimplify your xml, you can create a wrapper *cmd* file that calls all of your startup tasks along with logging and ensures each child-task shares hello same environment variables.</span></span>

<span data-ttu-id="76256-200">하지만 toouse까지 것 `>> "%TEMP%\StartupLog.txt" 2>&1` 각 시작 작업의 hello 끝에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-200">You may find it annoying though toouse `>> "%TEMP%\StartupLog.txt" 2>&1` on hello end of each startup task.</span></span> <span data-ttu-id="76256-201">사용자에 대한 로깅을 처리하는 래퍼를 만들어서 태스크 로깅을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-201">You can enforce task logging by creating a wrapper that handles logging for you.</span></span> <span data-ttu-id="76256-202">이 래퍼 toorun 원하는 hello 실제 배치 파일을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-202">This wrapper calls hello real batch file you want toorun.</span></span> <span data-ttu-id="76256-203">Hello 대상 배치 파일에서 모든 출력에는 리디렉션된 toohello 됩니다 *Startuplog.txt* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-203">Any output from hello target batch file will be redirected toohello *Startuplog.txt* file.</span></span>

<span data-ttu-id="76256-204">다음 예제는 hello tooredirect 모든 시작 배치 파일에서 출력 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="76256-204">hello following example shows how tooredirect all output from a startup batch file.</span></span> <span data-ttu-id="76256-205">이 예제에서는 hello ServerDefinition.csdef 파일은 호출 하는 시작 태스크를 만듭니다 *logwrap.cmd*합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-205">In this example, hello ServerDefinition.csdef file creates a startup task that calls *logwrap.cmd*.</span></span> <span data-ttu-id="76256-206">*logwrap.cmd* 호출 *Startup2.cmd*, 모든 출력을 너무 리디렉션**% TEMP %\\StartupLog.txt**합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-206">*logwrap.cmd* calls *Startup2.cmd*, redirecting all output too**%TEMP%\\StartupLog.txt**.</span></span>

<span data-ttu-id="76256-207">ServiceDefinition.cmd:</span><span class="sxs-lookup"><span data-stu-id="76256-207">ServiceDefinition.cmd:</span></span>

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

<span data-ttu-id="76256-208">**logwrap.cmd:**</span><span class="sxs-lookup"><span data-stu-id="76256-208">**logwrap.cmd:**</span></span>

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

<span data-ttu-id="76256-209">**Startup2.cmd:**</span><span class="sxs-lookup"><span data-stu-id="76256-209">**Startup2.cmd:**</span></span>

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

<span data-ttu-id="76256-210">샘플 출력 hello에 **StartupLog.txt** 파일:</span><span class="sxs-lookup"><span data-stu-id="76256-210">Sample output in hello **StartupLog.txt** file:</span></span>

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> <span data-ttu-id="76256-211">hello **StartupLog.txt** hello 파일은 *C:\Resources\temp\\{역할 식별자} \RoleTemp* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-211">hello **StartupLog.txt** file is located in hello *C:\Resources\temp\\{role identifier}\RoleTemp* folder.</span></span>
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a><span data-ttu-id="76256-212">시작 작업에 적절하게 executionContext 설정</span><span class="sxs-lookup"><span data-stu-id="76256-212">Set executionContext appropriately for startup tasks</span></span>
<span data-ttu-id="76256-213">적절 하 게 hello 시작 작업에 대 한 권한을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-213">Set privileges appropriately for hello startup task.</span></span> <span data-ttu-id="76256-214">경우에 따라 시작 작업 hello 역할이 일반 권한으로 실행 하는 경우에 상승 된 권한으로 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-214">Sometimes startup tasks must run with elevated privileges even though hello role runs with normal privileges.</span></span>

<span data-ttu-id="76256-215">hello [executionContext][작업] hello 시작 작업의 권한 수준을 hello를 설정 하는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-215">hello [executionContext][Task] attribute sets hello privilege level of hello startup task.</span></span> <span data-ttu-id="76256-216">사용 하 여 `executionContext="limited"` 이면 hello 시작 작업에 hello hello 역할과 같은 권한 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-216">Using `executionContext="limited"` means hello startup task has hello same privilege level as hello role.</span></span> <span data-ttu-id="76256-217">사용 하 여 `executionContext="elevated"` hello 시작 작업에 관리자 권한이 수 있는 hello 시작 작업 tooperform 관리자 작업 권한 tooyour 역할 관리자를 제공 하지 않고도 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-217">Using `executionContext="elevated"` means hello startup task has administrator privileges, which allows hello startup task tooperform administrator tasks without giving administrator privileges tooyour role.</span></span>

<span data-ttu-id="76256-218">높은 권한이 필요한 시작 작업의 예로 시작 작업을 사용 하는 **AppCmd.exe** tooconfigure IIS 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-218">An example of a startup task that requires elevated privileges is a startup task that uses **AppCmd.exe** tooconfigure IIS.</span></span> <span data-ttu-id="76256-219">**AppCmd.exe**는 `executionContext="elevated"`이(가) 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-219">**AppCmd.exe** requires `executionContext="elevated"`.</span></span>

### <a name="use-hello-appropriate-tasktype"></a><span data-ttu-id="76256-220">Hello 적절 한 taskType 사용</span><span class="sxs-lookup"><span data-stu-id="76256-220">Use hello appropriate taskType</span></span>
<span data-ttu-id="76256-221">hello [taskType][작업] hello 방식으로 hello 시작 작업이 실행 되는 특성이 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76256-221">hello [taskType][Task] attribute determines hello way hello startup task is executed.</span></span> <span data-ttu-id="76256-222">**간단**, **백그라운드** 및 **포그라운드**의 세 가지 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-222">There are three values: **simple**, **background**, and **foreground**.</span></span> <span data-ttu-id="76256-223">hello background 및 foreground 작업 비동기적으로 시작 되 고 hello 간단한 작업이 동기적으로 실행 되는 한 번에 하나씩 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-223">hello background and foreground tasks are started asynchronously, and then hello simple tasks are executed synchronously one at a time.</span></span>

<span data-ttu-id="76256-224">와 **간단한** 시작 작업 hello ServiceDefinition.csdef 파일에 나열 된 작업 어느 hello의 hello 주문별 hello 작업이 실행 되 hello 순서를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-224">With **simple** startup tasks, you can set hello order in which hello tasks run by hello order in which hello tasks are listed in hello ServiceDefinition.csdef file.</span></span> <span data-ttu-id="76256-225">경우는 **간단한** 작업 끝에 0이 아닌 종료 코드를 hello 시작 프로시저가 중지 하 고 hello 역할이 시작 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76256-225">If a **simple** task ends with a non-zero exit code, then hello startup procedure stops and hello role does not start.</span></span>

<span data-ttu-id="76256-226">차이 hello **배경** 시작 작업 및 **전경** 시작 작업은 **전경** hello까지 hello 역할 실행을 유지 하는 작업  **전경** 작업이 끝날 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-226">hello difference between **background** startup tasks and **foreground** startup tasks is that **foreground** tasks keep hello role running until hello **foreground** task ends.</span></span> <span data-ttu-id="76256-227">또한 즉 hello **전경** 작업 중단 되거나 충돌 hello까지 hello 역할이 재활용 되지 것입니다 **전경** 작업이 강제로 닫힙니다.</span><span class="sxs-lookup"><span data-stu-id="76256-227">This also means that if hello **foreground** task hangs or crashes, hello role will not recycle until hello **foreground** task is forced closed.</span></span> <span data-ttu-id="76256-228">이러한 이유로 **배경** 작업의 hello 기능이 필요 하지 않는 한 비동기 시작 작업에 권장 되 **전경** 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-228">For this reason, **background** tasks are recommended for asynchronous startup tasks unless you need that feature of hello **foreground** task.</span></span>

### <a name="end-batch-files-with-exit-b-0"></a><span data-ttu-id="76256-229">EXIT /B 0를 사용하여 배치 파일 끝내기</span><span class="sxs-lookup"><span data-stu-id="76256-229">End batch files with EXIT /B 0</span></span>
<span data-ttu-id="76256-230">hello 역할은 경우에 시작 hello **errorlevel** 각 simple 시작 작업은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-230">hello role will only start if hello **errorlevel** from each of your simple startup task is zero.</span></span> <span data-ttu-id="76256-231">Hello를 설정 하지 않는 프로그램도 **errorlevel** (종료 코드) 올바르게 하므로 hello 배치 파일 끝나야는 `EXIT /B 0` 모든 항목이 올바르게 실행 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="76256-231">Not all programs set hello **errorlevel** (exit code) correctly, so hello batch file should end with an `EXIT /B 0` if everything ran correctly.</span></span>

<span data-ttu-id="76256-232">누락 된 `EXIT /B 0` hello에서 시작 배치 파일의 끝은 시작 하지 않는 역할의 일반적인 원인입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-232">A missing `EXIT /B 0` at hello end of a startup batch file is a common cause of roles that do not start.</span></span>

> [!NOTE]
> <span data-ttu-id="76256-233">중첩 된 해당 일괄 처리를 발견 했습니다 hello를 사용 하는 경우 파일의 경우에 따라 중지 `/B` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-233">I've noticed that nested batch files sometimes hang when using hello `/B` parameter.</span></span> <span data-ttu-id="76256-234">이 중단 문제가 hello를 사용 하는 경우 다음과 같은 경우 현재 배치 파일을 호출 하는 다른 일괄 처리 파일을 발생 하지 있는지 toomake 할 수 있습니다 [로그 래퍼](#always-log-startup-activities)합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-234">You may want toomake sure that this hang problem does not happen if another batch file calls your current batch file, like if you use hello [log wrapper](#always-log-startup-activities).</span></span> <span data-ttu-id="76256-235">Hello를 생략할 수 `/B` 이 경우 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="76256-235">You can omit hello `/B` parameter in this case.</span></span>
> 
> 

### <a name="expect-startup-tasks-toorun-more-than-once"></a><span data-ttu-id="76256-236">시작 작업 toorun를 두 번 이상 기대</span><span class="sxs-lookup"><span data-stu-id="76256-236">Expect startup tasks toorun more than once</span></span>
<span data-ttu-id="76256-237">모든 역할 재활용은 재부팅을 포함하지 않으므로 모든 역할 재활용은 모든 시작 작업 실행을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-237">Not all role recycles include a reboot, but all role recycles include running all startup tasks.</span></span> <span data-ttu-id="76256-238">이 시작 작업을 여러 번 문제 없이 재부팅 사이 수 toorun 이어야 함을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-238">This means that startup tasks must be able toorun multiple times between reboots without any problems.</span></span> <span data-ttu-id="76256-239">Hello에 설명 되어 있음 [섹션 앞에 오는](#detect-that-your-task-has-already-run)합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-239">This is discussed in hello [preceding section](#detect-that-your-task-has-already-run).</span></span>

### <a name="use-local-storage-toostore-files-that-must-be-accessed-in-hello-role"></a><span data-ttu-id="76256-240">Hello 역할에 액세스 해야 하는 로컬 저장소 toostore 파일 사용</span><span class="sxs-lookup"><span data-stu-id="76256-240">Use local storage toostore files that must be accessed in hello role</span></span>
<span data-ttu-id="76256-241">Toocopy 하거나 시작 작업 중 파일을 만들 경우 액세스할 수 있는 tooyour 역할은 다음 한 다음 해당 파일을 로컬 저장소에 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-241">If you want toocopy or create a file during your startup task that is then accessible tooyour role, then that file must be placed in local storage.</span></span> <span data-ttu-id="76256-242">Hello 참조 [섹션 앞에 오는](#create-files-in-local-storage-from-a-startup-task)합니다.</span><span class="sxs-lookup"><span data-stu-id="76256-242">See hello [preceding section](#create-files-in-local-storage-from-a-startup-task).</span></span>

## <a name="next-steps"></a><span data-ttu-id="76256-243">다음 단계</span><span class="sxs-lookup"><span data-stu-id="76256-243">Next steps</span></span>
<span data-ttu-id="76256-244">Hello 클라우드 검토 [서비스 모델 및 패키지](cloud-services-model-and-package.md)</span><span class="sxs-lookup"><span data-stu-id="76256-244">Review hello cloud [service model and package](cloud-services-model-and-package.md)</span></span>

<span data-ttu-id="76256-245">[작업](cloud-services-startup-tasks.md) 작동 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="76256-245">Learn more about how [Tasks](cloud-services-startup-tasks.md) work.</span></span>

<span data-ttu-id="76256-246">[만들고 배포하세요](cloud-services-how-to-create-deploy-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="76256-246">[Create and deploy](cloud-services-how-to-create-deploy-portal.md) your cloud service package.</span></span>

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
