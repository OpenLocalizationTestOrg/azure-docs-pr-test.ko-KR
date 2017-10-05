---
title: "클라우드 서비스에 대한 일반적인 시작 작업 | Microsoft Docs"
description: "클라우드 서비스 웹 역할 또는 작업자 역할에서 수행하려는 경우 일반적인 시작 작업의 몇 가지 예를 제공합니다."
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
ms.openlocfilehash: cee23da5b089b02bfc0ef10afd60f0f2272585b1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="common-cloud-service-startup-tasks"></a><span data-ttu-id="45613-103">일반적인 클라우드 서비스 시작 작업</span><span class="sxs-lookup"><span data-stu-id="45613-103">Common Cloud Service startup tasks</span></span>
<span data-ttu-id="45613-104">이 문서에서는 클라우드 서비스에서 수행하려는 경우 일반적인 시작 작업의 몇 가지 예를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-104">This article provides some examples of common startup tasks you may want to perform in your cloud service.</span></span> <span data-ttu-id="45613-105">시작 작업을 사용하여 역할이 시작되기 전에 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-105">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="45613-106">수행하려는 작업은 구성 요소 설치, COM 구성 요소 등록, 레지스트리 키 설정 또는 장기 실행 프로세스를 시작을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-106">Operations that you might want to perform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span> 

<span data-ttu-id="45613-107">[이 문서](cloud-services-startup-tasks.md) 를 참조하여 시작 작업이 작동 하는 방법 및 시작 작업을 정의하는 항목을 만드는 방법을 구체적으로 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-107">See [this article](cloud-services-startup-tasks.md) to understand how startup tasks work, and specifically how to create the entries that define a startup task.</span></span>

> [!NOTE]
> <span data-ttu-id="45613-108">시작 작업은 가상 컴퓨터에 적용되지 않으며 클라우드 서비스 웹 및 작업자 역할에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="45613-108">Startup tasks are not applicable to Virtual Machines, only to Cloud Service Web and Worker roles.</span></span>
> 

## <a name="define-environment-variables-before-a-role-starts"></a><span data-ttu-id="45613-109">역할이 시작되기 전에 환경 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-109">Define environment variables before a role starts</span></span>
<span data-ttu-id="45613-110">특정 태스크에 대해 정의된 환경 변수가 필요한 경우 [태스크] 요소 내부의 [환경] 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-110">If you need environment variables defined for a specific task, use the [Environment] element inside the [Task] element.</span></span>

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

<span data-ttu-id="45613-111">변수는 [유효한 Azure XPath 값](cloud-services-role-config-xpath.md) 을 사용하여 배포에 대한 정보를 참조할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-111">Variables can also use a [valid Azure XPath value](cloud-services-role-config-xpath.md) to reference something about the deployment.</span></span> <span data-ttu-id="45613-112">`value` 특성을 사용하는 대신 [RoleInstanceValue] 자식 요소를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-112">Instead of using the `value` attribute, define a [RoleInstanceValue] child element.</span></span>

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a><span data-ttu-id="45613-113">Appcmd.exe를 사용하여 IIS 시작을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-113">Configure IIS startup with AppCmd.exe</span></span>
<span data-ttu-id="45613-114">[AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) 명령줄 도구는 Azure에서 시작 시 IIS 설정을 관리하는데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-114">The [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) command-line tool can be used to manage IIS settings at startup on Azure.</span></span> <span data-ttu-id="45613-115">*AppCmd.exe* 는 Azure에서 시작 작업에 사용하기 위한 구성 설정에 대한 편리한 명령줄 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-115">*AppCmd.exe* provides convenient, command-line access to configuration settings for use in startup tasks on Azure.</span></span> <span data-ttu-id="45613-116">*AppCmd.exe*를 사용하면 응용 프로그램 및 사이트에 대해 웹사이트 설정을 추가, 수정하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-116">Using *AppCmd.exe*, Website settings can be added, modified, or removed for applications and sites.</span></span>

<span data-ttu-id="45613-117">그러나 시작 작업으로 *AppCmd.exe* 사용에 대해 주의해야 할 사항이 몇 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-117">However, there are a few things to watch out for in the use of *AppCmd.exe* as a startup task:</span></span>

* <span data-ttu-id="45613-118">시작 작업은 재부팅 사이 두 번 이상 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-118">Startup tasks can be run more than once between reboots.</span></span> <span data-ttu-id="45613-119">예를 들어 역할을 재활용하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="45613-119">For instance, when a role recycles.</span></span>
* <span data-ttu-id="45613-120">*AppCmd.exe* 작업이 두 번 이상 수행되는 경우 오류를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-120">If a *AppCmd.exe* action is performed more than once, it may generate an error.</span></span> <span data-ttu-id="45613-121">예를 들어 *Web.config*에 섹션을 두 번 추가하려는 경우 오류가 생성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-121">For example, attempting to add a section to *Web.config* twice could generate an error.</span></span>
* <span data-ttu-id="45613-122">0이 아닌 종료 코드 또는 **errorlevel**을 반환하는 경우 시작 작업이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-122">Startup tasks fail if they return a non-zero exit code or **errorlevel**.</span></span> <span data-ttu-id="45613-123">예를 들어 *AppCmd.exe* 가 오류를 생성하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="45613-123">For example, when *AppCmd.exe* generates an error.</span></span>

<span data-ttu-id="45613-124">*AppCmd.exe*를 호출한 후 **errorlevel**을 확인하는 것이 좋습니다. *.cmd* 파일로 *AppCmd.exe*에 호출을 래핑하는 경우 수행하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-124">It is a good practice to check the **errorlevel** after calling *AppCmd.exe*, which is easy to do if you wrap the call to *AppCmd.exe* with a *.cmd* file.</span></span> <span data-ttu-id="45613-125">알려진 **errorlevel** 응답을 발견하는 경우 무시하거나 다시 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-125">If you detect a known **errorlevel** response, you can ignore it, or pass it back.</span></span>

<span data-ttu-id="45613-126">*AppCmd.exe*로 반환되는 errorlevel은 winerror.h 파일에 나열되어 있으며 [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx)에서 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-126">The errorlevel returned by *AppCmd.exe* are listed in the winerror.h file, and can also be seen on [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span></span>

### <a name="example-of-managing-the-error-level"></a><span data-ttu-id="45613-127">오류 수준 관리 예제</span><span class="sxs-lookup"><span data-stu-id="45613-127">Example of managing the error level</span></span>
<span data-ttu-id="45613-128">이 예에서는 오류 처리 및 로깅으로 JSON에 대한 압축 섹션 및 압축 항목을 *Web.config* 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-128">This example adds a compression section and a compression entry for JSON to the *Web.config* file, with error handling and logging.</span></span>

<span data-ttu-id="45613-129">[ServiceDefinition.csdef] 파일의 관련 섹션은 여기에 표시되어 있으며 *AppCmd.exe*에 *Web.config* 파일에서 설정을 변경할 충분한 권한을 부여하도록 [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) 특성을 `elevated`에 설정하는 것을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-129">The relevant sections of the [ServiceDefinition.csdef] file are shown here, which include setting the [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) attribute to `elevated` to give *AppCmd.exe* sufficient permissions to change the settings in the *Web.config* file:</span></span>

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

<span data-ttu-id="45613-130">*Startup.cmd* 배치 파일은 *AppCmd.exe*를 사용하여 JSON에 대한 압축 섹션 및 압축 항목을 *Web.config* 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-130">The *Startup.cmd* batch file uses *AppCmd.exe* to add a compression section and a compression entry for JSON to the *Web.config* file.</span></span> <span data-ttu-id="45613-131">예상된 183의 **errorlevel** 은 VERIFY.EXE 명령줄 프로그램을 사용하여 0으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="45613-131">The expected **errorlevel** of 183 is set to zero using the VERIFY.EXE command-line program.</span></span> <span data-ttu-id="45613-132">예기치 않은 errorlevel은 StartupErrorLog.txt에 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="45613-132">Unexpected errorlevels are logged to StartupErrorLog.txt.</span></span>

```cmd
REM   *** Add a compression section to the Web.config file. ***
%windir%\system32\inetsrv\appcmd set config /section:urlCompression /doDynamicCompression:True /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1

REM   ERRORLEVEL 183 occurs when trying to add a section that already exists. This error is expected if this
REM   batch file were executed twice. This can occur and must be accounted for in a Azure startup
REM   task. To handle this situation, set the ERRORLEVEL to zero by using the Verify command. The Verify
REM   command will safely set the ERRORLEVEL to zero.
IF %ERRORLEVEL% EQU 183 DO VERIFY > NUL

REM   If the ERRORLEVEL is not zero at this point, some other error occurred.
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding a compression section to the Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Add compression for json. ***
%windir%\system32\inetsrv\appcmd set config  -section:system.webServer/httpCompression /+"dynamicTypes.[mimeType='application/json; charset=utf-8',enabled='True']" /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1
IF %ERRORLEVEL% EQU 183 VERIFY > NUL
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding the JSON compression type to the Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Exit batch file. ***
EXIT /b 0

REM   *** Log error and exit ***
:ErrorExit
REM   Report the date, time, and ERRORLEVEL of the error.
DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
ECHO An error occurred during startup. ERRORLEVEL = %ERRORLEVEL% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT %ERRORLEVEL%
```

## <a name="add-firewall-rules"></a><span data-ttu-id="45613-133">방화벽 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="45613-133">Add firewall rules</span></span>
<span data-ttu-id="45613-134">Azure에는 사실상 두 개의 방화벽이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-134">In Azure, there are effectively two firewalls.</span></span> <span data-ttu-id="45613-135">첫 번째 방화벽은 가상 컴퓨터와 외부 세계 간의 연결을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-135">The first firewall controls connections between the virtual machine and the outside world.</span></span> <span data-ttu-id="45613-136">이 방화벽은 [ServiceDefinition.csdef] 파일의 [끝점] 요소에 의해 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="45613-136">This firewall is controlled by the [EndPoints] element in the [ServiceDefinition.csdef] file.</span></span>

<span data-ttu-id="45613-137">두 번째 방화벽은 가상 컴퓨터와 해당 가상 컴퓨터 내의 프로세스 간의 연결을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-137">The second firewall controls connections between the virtual machine and the processes within that virtual machine.</span></span> <span data-ttu-id="45613-138">이 방화벽은 `netsh advfirewall firewall` 명령줄 도구를 통해 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-138">This firewall can be controlled by the `netsh advfirewall firewall` command-line tool.</span></span>

<span data-ttu-id="45613-139">Azure는 역할 내에서 시작되는 프로세스에 대한 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45613-139">Azure creates firewall rules for the processes started within your roles.</span></span> <span data-ttu-id="45613-140">예를 들어 서비스 또는 프로그램을 시작하면 Azure는 필요한 방화벽 규칙을 만들어 해당 서비스가 인터넷과 통신할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-140">For example, when you start a service or program, Azure automatically creates the necessary firewall rules to allow that service to communicate with the Internet.</span></span> <span data-ttu-id="45613-141">그러나 사용자의 역할(예: COM + 서비스 또는 Windows 예약된 태스크) 외부 프로세스에 의해 시작되는 서비스를 만드는 경우 해당 서비스에 대한 액세스를 허용하는 방화벽 규칙을 수동으로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-141">However, if you create a service that is started by a process outside your role (like a COM+ service or a Windows Scheduled Task), you need to manually create a firewall rule to allow access to that service.</span></span> <span data-ttu-id="45613-142">이러한 방화벽 규칙은 시작 작업을 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-142">These firewall rules can be created by using a startup task.</span></span>

<span data-ttu-id="45613-143">방화벽 규칙을 만드는 시작 작업은 [상승된][태스크]  **executionContext**을 반환하는 경우 시작 작업이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-143">A startup task that creates a firewall rule must have an [executionContext][Task] of **elevated**.</span></span> <span data-ttu-id="45613-144">다음 시작 작업을 [ServiceDefinition.csdef] 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-144">Add the following startup task to the [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="45613-145">방화벽 규칙을 추가하려면 시작 배치 파일에서 적절한 `netsh advfirewall firewall` 명령을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-145">To add the firewall rule, you must use the appropriate `netsh advfirewall firewall` commands in your startup batch file.</span></span> <span data-ttu-id="45613-146">이 예에서는 시작 작업은 TCP 포트 80에 대한 보안 및 암호화가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-146">In this example, the startup task requires security and encryption for TCP port 80.</span></span>

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a><span data-ttu-id="45613-147">특정 IP 주소 차단</span><span class="sxs-lookup"><span data-stu-id="45613-147">Block a specific IP address</span></span>
<span data-ttu-id="45613-148">IIS **web.config** 파일을 수정하여 일련의 지정된 IP 주소에 대한 Azure 웹 역할 액세스를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-148">You can restrict an Azure web role access to a set of specified IP addresses by modifying your IIS **web.config** file.</span></span> <span data-ttu-id="45613-149">또한 **ApplicationHost.config** 파일의 **ipSecurity** 섹션의 차단을 해제하는 명령 파일을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-149">You also need to use a command file which unlocks the **ipSecurity** section of the **ApplicationHost.config** file.</span></span>

<span data-ttu-id="45613-150">**ApplicationHost.config** 파일의 **ipSecurity** 섹션의 차단을 해제하려면 역할 시작 시 실행하는 명령 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45613-150">To do unlock the **ipSecurity** section of the **ApplicationHost.config** file, create a command file that runs at role start.</span></span> <span data-ttu-id="45613-151">웹 역할의 루트 수준에서 **startup**이라는 폴더를 만들고 이 폴더 내에서 **startup.cmd**라는 배치 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45613-151">Create a folder at the root level of your web role called **startup** and, within this folder, create a batch file called **startup.cmd**.</span></span> <span data-ttu-id="45613-152">Visual Studio 프로젝트에 이 파일을 추가하고 속성을 **항상 복사**로 설정하여 패키지에 포함되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-152">Add this file to your Visual Studio project and set the properties to **Copy Always** to ensure that it is included in your package.</span></span>

<span data-ttu-id="45613-153">다음 시작 작업을 [ServiceDefinition.csdef] 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-153">Add the following startup task to the [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="45613-154">이 명령을 **startup.cmd** 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-154">Add this command to the **startup.cmd** file:</span></span>

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

<span data-ttu-id="45613-155">이 태스크를 통해 **startup.cmd** 배치 파일이 웹 역할이 초기화될 때마다 실행되어 필요한 **ipSecurity** 섹션이 잠금 해제되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-155">This task causes the **startup.cmd** batch file to be run every time the web role is initialized, ensuring that the required **ipSecurity** section is unlocked.</span></span>

<span data-ttu-id="45613-156">마지막으로 웹 역할의 [web.config](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) 파일의 **system.webServer 섹션** 을 수정하여 다음 예와 같이 액세스 권한이 부여된 IP 주소의 목록을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-156">Finally, modify the [system.webServer section](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) your web role’s **web.config** file to add a list of IP addresses that are granted access, as shown in the following example:</span></span>

<span data-ttu-id="45613-157">이 샘플 구성은 모든 IP가 두 정의를 제외하고 서버에 액세스하도록 **허용** 합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-157">This sample config **allows** all IPs to access the server except the two defined</span></span>

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are granted access-->
    <ipSecurity>
        <!--The following IP addresses are denied access-->
        <add allowed="false" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="false" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

<span data-ttu-id="45613-158">이 샘플 구성은 모든 IP가 두 정의를 제외하고 서버에 액세스하는 것을 **거부** 합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-158">This sample config **denies** all IPs from accessing the server except for the two defined.</span></span>

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are denied access-->
    <ipSecurity allowUnlisted="false">
        <!--The following IP addresses are granted access-->
        <add allowed="true" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="true" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

## <a name="create-a-powershell-startup-task"></a><span data-ttu-id="45613-159">PowerShell 시작 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="45613-159">Create a PowerShell startup task</span></span>
<span data-ttu-id="45613-160">Windows PowerShell 스크립트는 [ServiceDefinition.csdef] 파일에서 직접 호출할 수 없지만 시작 배치 파일 내에서 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-160">Windows PowerShell scripts cannot be called directly from the [ServiceDefinition.csdef] file, but they can be invoked from within a startup batch file.</span></span>

<span data-ttu-id="45613-161">PowerShell은 기본적으로 서명되지 않은 스크립트를 실행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-161">PowerShell (by default) does not run unsigned scripts.</span></span> <span data-ttu-id="45613-162">스크립트를 서명하지 않으면 서명되지 않은 스크립트를 실행하도록 PowerShell을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-162">Unless you sign your script, you need to configure PowerShell to run unsigned scripts.</span></span> <span data-ttu-id="45613-163">서명되지 않은 스크립트를 실행하려면 **ExecutionPolicy**을 **제한 없음**으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-163">To run unsigned scripts, the **ExecutionPolicy** must be set to **Unrestricted**.</span></span> <span data-ttu-id="45613-164">사용하는 **ExecutionPolicy** 설정은 Windows PowerShell의 버전에 기반합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-164">The **ExecutionPolicy** setting that you use is based on the version of Windows PowerShell.</span></span>

```cmd
REM   Run an unsigned PowerShell script and log the output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

<span data-ttu-id="45613-165">PowerShell 2.0 또는 1.0을 실행하는 게스트 OS를 사용하는 경우 버전 2를 강제로 실행할 수 있으며 사용할 수 없는 경우 버전 1을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-165">If you're using a Guest OS that is runs PowerShell 2.0 or 1.0 you can force version 2 to run, and if unavailable, use version 1.</span></span>

```cmd
REM   Attempt to set the execution policy by using PowerShell version 2.0 syntax.
PowerShell -Version 2.0 -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If PowerShell version 2.0 isn't available. Set the execution policy by using the PowerShell
IF %ERRORLEVEL% EQU -393216 (
   PowerShell -Command "Set-ExecutionPolicy Unrestricted" >> "%TEMP%\StartupLog.txt" 2>&1
   PowerShell .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1
)

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

## <a name="create-files-in-local-storage-from-a-startup-task"></a><span data-ttu-id="45613-166">시작 작업에서 로컬 저장소에 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45613-166">Create files in local storage from a startup task</span></span>
<span data-ttu-id="45613-167">로컬 저장소 리소스를 사용하여 응용 프로그램에 의해 나중에 액세스하는 시작 태스크에서 만든 파일을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-167">You can use a local storage resource to store files created by your startup task that is accessed later by your application.</span></span>

<span data-ttu-id="45613-168">로컬 저장소 리소스를 만들려면 [LocalResources] 섹션을 [ServiceDefinition.csdef] 파일에 추가한 다음 [LocalStorage] 자식 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-168">To create the local storage resource, add a [LocalResources] section to the [ServiceDefinition.csdef] file and then add the [LocalStorage] child element.</span></span> <span data-ttu-id="45613-169">로컬 저장소 리소스에 고유한 이름을 부여하고 시작 작업에 대한 적절한 크기를 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-169">Give the local storage resource a unique name and an appropriate size for your startup task.</span></span>

<span data-ttu-id="45613-170">시작 작업에서 로컬 저장소 리소스를 사용하려면 로컬 저장소 리소스 위치를 참조하는 환경 변수를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-170">To use a local storage resource in your startup task, you need to create an environment variable to reference the local storage resource location.</span></span> <span data-ttu-id="45613-171">그러면 시작 태스크 및 응용 프로그램이 로컬 저장소 리소스에 파일을 읽고 쓸 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45613-171">Then the startup task and the application are able to read and write files to the local storage resource.</span></span>

<span data-ttu-id="45613-172">**ServiceDefinition.csdef** 파일의 관련 섹션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-172">The relevant sections of the **ServiceDefinition.csdef** file are shown here:</span></span>

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

<span data-ttu-id="45613-173">한 예로 이 **Startup.cmd** 배치 파일은 **PathToStartupStorage** 환경 변수를 사용하여 로컬 저장소 위치에 파일 **MyTest.txt**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45613-173">As an example, this **Startup.cmd** batch file uses the **PathToStartupStorage** environment variable to create the file **MyTest.txt** on the local storage location.</span></span>

```cmd
REM   Create a simple text file.

ECHO This text will go into the MyTest.txt file which will be in the    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed to by the PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO The contents of the PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit the batch file with ERRORLEVEL 0.

EXIT /b 0
```

<span data-ttu-id="45613-174">[GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) 메서드를 사용하여 Azure SDK에서 로컬 저장소 폴더에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-174">You can access local storage folder from the Azure SDK by using the [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-the-emulator-or-cloud"></a><span data-ttu-id="45613-175">에뮬레이터 또는 클라우드에서 실행</span><span class="sxs-lookup"><span data-stu-id="45613-175">Run in the emulator or cloud</span></span>
<span data-ttu-id="45613-176">계산 에뮬레이터에 있을 때에 비해 클라우드에서 작동하는 경우 시작 작업이 다른 단계를 수행하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-176">You can have your startup task perform different steps when it is operating in the cloud compared to when it is in the compute emulator.</span></span> <span data-ttu-id="45613-177">예를 들어 에뮬레이터에서 실행하는 경우 SQL 데이터의 새 복사본을 사용하려고 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-177">For example, you may want to use a fresh copy of your SQL data only when running in the emulator.</span></span> <span data-ttu-id="45613-178">또는 에뮬레이터에서 실행하는 경우 수행할 필요가 없는 클라우드에 대한 성능 최적화를 수행하려고 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-178">Or you may want to do some performance optimizations for the cloud that you don't need to do when running in the emulator.</span></span>

<span data-ttu-id="45613-179">계산 에뮬레이터와 클라우드에서 서로 다른 동작을 수행하도록 하는 이 기능은 [ServiceDefinition.csdef] 파일에서 환경 변수를 만들어서 수행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-179">This ability to perform different actions on the compute emulator and the cloud can be accomplished by creating an environment variable in the [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="45613-180">그런 다음 시작 태스크에서 값의 해당 환경 변수를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-180">You then test that environment variable for a value in your startup task.</span></span>

<span data-ttu-id="45613-181">환경 변수를 만들려면 [변수]/[RoleInstanceValue] 요소를 추가하고 `/RoleEnvironment/Deployment/@emulated`의 XPath 값을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45613-181">To create the environment variable, add the [Variable]/[RoleInstanceValue] element and create an XPath value of `/RoleEnvironment/Deployment/@emulated`.</span></span> <span data-ttu-id="45613-182">**%ComputeEmulatorRunning%** 환경 변수의 값은 계산 에뮬레이터에서 실행 되는 경우 `true`이(가) 되고 클라우드에서 실행 되는 경우 `false`이(가) 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45613-182">The value of the **%ComputeEmulatorRunning%** environment variable is `true` when running on the compute emulator, and `false` when running on the cloud.</span></span>

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

<span data-ttu-id="45613-183">태스크는 이제 **%ComputeEmulatorRunning%** 환경 변수를 확인하여 역할이 클라우드 또는 에뮬레이터에서 실행되는지 여부에 따라 다른 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-183">The task can now check the **%ComputeEmulatorRunning%** environment variable to perform different actions based on whether the role is running in the cloud or the emulator.</span></span> <span data-ttu-id="45613-184">해당 환경 변수를 검사하는 .cmd 셸 스크립트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-184">Here is a .cmd shell script that checks for that environment variable.</span></span>

```cmd
REM   Check if this task is running on the compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on the compute emulator. Perform tasks that must be run only in the compute emulator.
) ELSE (
    REM   This task is running on the cloud. Perform tasks that must be run only in the cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a><span data-ttu-id="45613-185">작업이 이미 실행되었는지 감지</span><span class="sxs-lookup"><span data-stu-id="45613-185">Detect that your task has already run</span></span>
<span data-ttu-id="45613-186">재부팅 없이 역할이 재활용되어 시작 작업이 다시 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-186">The role may recycle without a reboot causing your startup tasks to run again.</span></span> <span data-ttu-id="45613-187">호스팅 VM에서 이미 실행된 태스크를 나타내는 플래그가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-187">There is no flag to indicate that a task has already run on the hosting VM.</span></span> <span data-ttu-id="45613-188">여러 번 실행되는 것과 상관 없는 일부 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-188">You may have some tasks where it doesn't matter that they run multiple times.</span></span> <span data-ttu-id="45613-189">그러나 태스크가 두 번 이상 실행되지 않도록 해야 하는 상황에 직면할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-189">However, you may run into a situation where you need to prevent a task from running more than once.</span></span>

<span data-ttu-id="45613-190">작업이 이미 실행되었는지 감지하는 가장 간단한 방법은 작업이 성공하고 작업 시작 시 검색할 경우 **%TEMP%** 폴더에 파일을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="45613-190">The simplest way to detect that a task has already run is to create a file in the **%TEMP%** folder when the task is successful and look for it at the start of the task.</span></span> <span data-ttu-id="45613-191">해당 작업을 수행하는 예제 cmd 셸 스크립트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-191">Here is a sample cmd shell script that does that for you.</span></span>

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
  REM   The application installed without error. Create a file to indicate that the task
  REM   does not need to be run again.

  ECHO This line will create a file to indicate that Application 1 installed correctly. > "%RoleRoot%\Task1_Success.txt"

) ELSE (
  REM   An error occurred. Log the error and exit with the error code.

  DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
  TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
  ECHO  An error occurred running task 1. Errorlevel = %ERRORLEVEL%. >> "%TEMP%\StartupLog.txt" 2>&1

  EXIT %ERRORLEVEL%
)

:Finish

REM   Exit normally.
EXIT /B 0
```

## <a name="task-best-practices"></a><span data-ttu-id="45613-192">작업 모범 사례</span><span class="sxs-lookup"><span data-stu-id="45613-192">Task best practices</span></span>
<span data-ttu-id="45613-193">웹 또는 작업자 역할에 대한 작업을 구성할 때 따라야 하는 몇 가지 모범 사례는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-193">Here are some best practices you should follow when configuring task for your web or worker role.</span></span>

### <a name="always-log-startup-activities"></a><span data-ttu-id="45613-194">항상 시작 작업 기록</span><span class="sxs-lookup"><span data-stu-id="45613-194">Always log startup activities</span></span>
<span data-ttu-id="45613-195">Visual Studio는 배치 파일을 통해 단계에 디버거를 제공하지 않으므로 배치 파일 작업 시 가능한 많은 데이터를 가져오는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-195">Visual Studio does not provide a debugger to step through batch files, so it's good to get as much data on the operation of batch files as possible.</span></span> <span data-ttu-id="45613-196">**stdout** 및 **stderr** 배치 파일의 출력 로깅은 배치 파일을 디버깅하고 수정하려고 할 때 중요한 정보를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-196">Logging the output of batch files, both **stdout** and **stderr**, can give you important information when trying to debug and fix batch files.</span></span> <span data-ttu-id="45613-197">**stdout** 및 **stderr** 모두를 **%TEMP%** 환경 변수가 가리킨 디렉터리의 StartupLog.txt 파일에 로깅하려면 텍스트 `>>  "%TEMP%\\StartupLog.txt" 2>&1`을 로깅하려면 특정 줄의 끝에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-197">To log both **stdout** and **stderr** to the StartupLog.txt file in the directory pointed to by the **%TEMP%** environment variable, add the text `>>  "%TEMP%\\StartupLog.txt" 2>&1` to the end of specific lines you want to log.</span></span> <span data-ttu-id="45613-198">예를 들어 **%PathToApp1Install%** 디렉터리의 setup.exe를 실행하려면:</span><span class="sxs-lookup"><span data-stu-id="45613-198">For example, to execute setup.exe in the **%PathToApp1Install%** directory:</span></span>

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

<span data-ttu-id="45613-199">xml을 단순화하기 위해 로깅과 함께 모든 시작 태스크를 호출하는 래퍼 *cmd* 파일을 만들고 동일한 환경 변수를 공유하는 각 하위 태스크를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-199">To simplify your xml, you can create a wrapper *cmd* file that calls all of your startup tasks along with logging and ensures each child-task shares the same environment variables.</span></span>

<span data-ttu-id="45613-200">각 시작 태스크의 끝에 `>> "%TEMP%\StartupLog.txt" 2>&1`을 사용하지 않으려 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-200">You may find it annoying though to use `>> "%TEMP%\StartupLog.txt" 2>&1` on the end of each startup task.</span></span> <span data-ttu-id="45613-201">사용자에 대한 로깅을 처리하는 래퍼를 만들어서 태스크 로깅을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-201">You can enforce task logging by creating a wrapper that handles logging for you.</span></span> <span data-ttu-id="45613-202">이 래퍼는 실행하려는 실제 배치 파일을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-202">This wrapper calls the real batch file you want to run.</span></span> <span data-ttu-id="45613-203">대상 배치 파일의 모든 출력은 *Startuplog.txt* 파일로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="45613-203">Any output from the target batch file will be redirected to the *Startuplog.txt* file.</span></span>

<span data-ttu-id="45613-204">다음 예제는 시작 배치 파일의 모든 출력을 리디렉션하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="45613-204">The following example shows how to redirect all output from a startup batch file.</span></span> <span data-ttu-id="45613-205">이 예에서 ServerDefinition.csdef 파일은 *logwrap.cmd*를 호출하는 시작 태스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45613-205">In this example, the ServerDefinition.csdef file creates a startup task that calls *logwrap.cmd*.</span></span> <span data-ttu-id="45613-206">*logwrap.cmd*는 *Startup2.cmd*를 호출하여 모든 출력을 **%TEMP%\\StartupLog.txt**로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-206">*logwrap.cmd* calls *Startup2.cmd*, redirecting all output to **%TEMP%\\StartupLog.txt**.</span></span>

<span data-ttu-id="45613-207">ServiceDefinition.cmd:</span><span class="sxs-lookup"><span data-stu-id="45613-207">ServiceDefinition.cmd:</span></span>

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

<span data-ttu-id="45613-208">**logwrap.cmd:**</span><span class="sxs-lookup"><span data-stu-id="45613-208">**logwrap.cmd:**</span></span>

```cmd
@ECHO OFF

REM   logwrap.cmd calls passed in batch file, redirecting all output to the StartupLog.txt log file.

ECHO [%date% %time%] == START logwrap.cmd ============================================== >> "%TEMP%\StartupLog.txt" 2>&1
ECHO [%date% %time%] Running %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Call the child command batch file, redirecting all output to the StartupLog.txt log file.
START /B /WAIT %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Log the completion of child command.
ECHO [%date% %time%] Done >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (

   REM   No errors occurred. Exit logwrap.cmd normally.
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B 0

) ELSE (

   REM   Log the error.
   ECHO [%date% %time%] An error occurred. The ERRORLEVEL = %ERRORLEVEL%.  >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B %ERRORLEVEL%

)
```

<span data-ttu-id="45613-209">**Startup2.cmd:**</span><span class="sxs-lookup"><span data-stu-id="45613-209">**Startup2.cmd:**</span></span>

```cmd
@ECHO OFF

REM   This is the batch file where the startup steps should be performed. Because of the
REM   way Startup2.cmd was called, all commands and their outputs will be stored in the
REM   StartupLog.txt file in the directory pointed to by the TEMP environment variable.

REM   If an error occurs, the following command will pass the ERRORLEVEL back to the
REM   calling batch file.

ECHO [%date% %time%] Some log information about this task
ECHO [%date% %time%] Some more log information about this task

EXIT %ERRORLEVEL%
```

<span data-ttu-id="45613-210">**StartupLog.txt** 파일의 샘플 출력:</span><span class="sxs-lookup"><span data-stu-id="45613-210">Sample output in the **StartupLog.txt** file:</span></span>

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> <span data-ttu-id="45613-211">**StartupLog.txt** 파일은 *C:\Resources\temp\\{role identifier}\RoleTemp* 폴더에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-211">The **StartupLog.txt** file is located in the *C:\Resources\temp\\{role identifier}\RoleTemp* folder.</span></span>
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a><span data-ttu-id="45613-212">시작 작업에 적절하게 executionContext 설정</span><span class="sxs-lookup"><span data-stu-id="45613-212">Set executionContext appropriately for startup tasks</span></span>
<span data-ttu-id="45613-213">시작 작업에 대한 권한을 적절하게 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-213">Set privileges appropriately for the startup task.</span></span> <span data-ttu-id="45613-214">경우에 따라 역할이 일반 권한으로 실행되더라도 시작 작업을 상승된 권한으로 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-214">Sometimes startup tasks must run with elevated privileges even though the role runs with normal privileges.</span></span>

<span data-ttu-id="45613-215">[상승된][태스크] 특성은 시작 작업의 권한 수준을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-215">The [executionContext][Task] attribute sets the privilege level of the startup task.</span></span> <span data-ttu-id="45613-216">`executionContext="limited"`을 사용하는 것은 시작 태스크가 역할과 동일한 권한 수준을 갖는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-216">Using `executionContext="limited"` means the startup task has the same privilege level as the role.</span></span> <span data-ttu-id="45613-217">`executionContext="elevated"`을 사용하면 시작 태스크가 관리자 권한을 갖게 되므로 역할에 관리자 권한을 부여하지 않고 시작 태스크가 관리자 태스크를 수행하도록 하는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-217">Using `executionContext="elevated"` means the startup task has administrator privileges, which allows the startup task to perform administrator tasks without giving administrator privileges to your role.</span></span>

<span data-ttu-id="45613-218">상승된 권한이 필요한 시작 작업의 예로 **AppCmd.exe** 를 사용하여 IIS를 구성하는 시작 작업을 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-218">An example of a startup task that requires elevated privileges is a startup task that uses **AppCmd.exe** to configure IIS.</span></span> <span data-ttu-id="45613-219">**AppCmd.exe**는 `executionContext="elevated"`이(가) 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-219">**AppCmd.exe** requires `executionContext="elevated"`.</span></span>

### <a name="use-the-appropriate-tasktype"></a><span data-ttu-id="45613-220">적절한 taskType 사용</span><span class="sxs-lookup"><span data-stu-id="45613-220">Use the appropriate taskType</span></span>
<span data-ttu-id="45613-221">[taskType][태스크] 특성은 시작 태스크가 실행되는 방식을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-221">The [taskType][Task] attribute determines the way the startup task is executed.</span></span> <span data-ttu-id="45613-222">**간단**, **백그라운드** 및 **포그라운드**의 세 가지 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-222">There are three values: **simple**, **background**, and **foreground**.</span></span> <span data-ttu-id="45613-223">백그라운드 및 포그라운드 작업은 비동기적으로 시작된 다음 간단 작업이 한 번에 하나씩 동기적으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="45613-223">The background and foreground tasks are started asynchronously, and then the simple tasks are executed synchronously one at a time.</span></span>

<span data-ttu-id="45613-224">**간단** 시작 태스크의 경우 ServiceDefinition.csdef 파일에 나열된 태스크의 순서에 따라 태스크를 실행할 순서를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-224">With **simple** startup tasks, you can set the order in which the tasks run by the order in which the tasks are listed in the ServiceDefinition.csdef file.</span></span> <span data-ttu-id="45613-225">**간단** 태스크가 0이 아닌 종료 코드로 끝나는 경우 시작 절차가 중지되고 역할이 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-225">If a **simple** task ends with a non-zero exit code, then the startup procedure stops and the role does not start.</span></span>

<span data-ttu-id="45613-226">**백그라운드** 시작 태스크와 **포그라운드** 시작 태스크의 차이는 **포그라운드** 태스크는 **포그라운드** 태스크가 끝날 때까지 역할이 실행되도록 유지하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="45613-226">The difference between **background** startup tasks and **foreground** startup tasks is that **foreground** tasks keep the role running until the **foreground** task ends.</span></span> <span data-ttu-id="45613-227">또한 **포그라운드** 태스크가 중단되거나 충돌되는 경우 **포그라운드** 태스크가 강제로 닫힐 때까지 역할이 재활용되지 않는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-227">This also means that if the **foreground** task hangs or crashes, the role will not recycle until the **foreground** task is forced closed.</span></span> <span data-ttu-id="45613-228">이러한 이유로 **백그라운드** 태스크는 **포그라운드** 태스크의 해당 기능이 필요하지 않는 경우 비동기적 시작 태스크에 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-228">For this reason, **background** tasks are recommended for asynchronous startup tasks unless you need that feature of the **foreground** task.</span></span>

### <a name="end-batch-files-with-exit-b-0"></a><span data-ttu-id="45613-229">EXIT /B 0를 사용하여 배치 파일 끝내기</span><span class="sxs-lookup"><span data-stu-id="45613-229">End batch files with EXIT /B 0</span></span>
<span data-ttu-id="45613-230">각 간단 시작 작업에서 **errorlevel** 이 0인 경우 역할이 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-230">The role will only start if the **errorlevel** from each of your simple startup task is zero.</span></span> <span data-ttu-id="45613-231">모든 프로그램이 **errorlevel**(종료 코드)을 올바르게 설정하지 않으므로 모든 항목이 올바르게 실행된 경우 배치 파일은 `EXIT /B 0`으로 끝나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-231">Not all programs set the **errorlevel** (exit code) correctly, so the batch file should end with an `EXIT /B 0` if everything ran correctly.</span></span>

<span data-ttu-id="45613-232">시작 배치 파일의 끝에 누락된 `EXIT /B 0` 은(는) 시작하지 않는 역할의 일반적인 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="45613-232">A missing `EXIT /B 0` at the end of a startup batch file is a common cause of roles that do not start.</span></span>

> [!NOTE]
> <span data-ttu-id="45613-233">중첩된 배치 파일은 `/B` 매개 변수를 사용하는 경우 때로는 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="45613-233">I've noticed that nested batch files sometimes hang when using the `/B` parameter.</span></span> <span data-ttu-id="45613-234">[로그 래퍼](#always-log-startup-activities)를 사용하는 경우와 같이 다른 배치 파일에서 현재 배치 파일을 호출하는 경우 이 중단 문제가 발생하지 않는지 확인하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-234">You may want to make sure that this hang problem does not happen if another batch file calls your current batch file, like if you use the [log wrapper](#always-log-startup-activities).</span></span> <span data-ttu-id="45613-235">이 경우에 `/B` 매개 변수를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45613-235">You can omit the `/B` parameter in this case.</span></span>
> 
> 

### <a name="expect-startup-tasks-to-run-more-than-once"></a><span data-ttu-id="45613-236">시작 작업이 두 번 이상 실행되도록 예상</span><span class="sxs-lookup"><span data-stu-id="45613-236">Expect startup tasks to run more than once</span></span>
<span data-ttu-id="45613-237">모든 역할 재활용은 재부팅을 포함하지 않으므로 모든 역할 재활용은 모든 시작 작업 실행을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-237">Not all role recycles include a reboot, but all role recycles include running all startup tasks.</span></span> <span data-ttu-id="45613-238">이는 시작 작업이 문제 없이 재부팅 사이 여러 번 실행될 수 있어야 함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-238">This means that startup tasks must be able to run multiple times between reboots without any problems.</span></span> <span data-ttu-id="45613-239">이에 대해서는 [앞의 섹션](#detect-that-your-task-has-already-run)에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-239">This is discussed in the [preceding section](#detect-that-your-task-has-already-run).</span></span>

### <a name="use-local-storage-to-store-files-that-must-be-accessed-in-the-role"></a><span data-ttu-id="45613-240">로컬 저장소를 사용하여 역할에 액세스할 수 있어야 하는 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-240">Use local storage to store files that must be accessed in the role</span></span>
<span data-ttu-id="45613-241">그런 다음 역할에 액세스할 수 있는 시작 작업 중 파일을 복사하거나 만들려는 경우 해당 파일이 로컬 저장소에 배치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45613-241">If you want to copy or create a file during your startup task that is then accessible to your role, then that file must be placed in local storage.</span></span> <span data-ttu-id="45613-242">[앞의 섹션](#create-files-in-local-storage-from-a-startup-task)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45613-242">See the [preceding section](#create-files-in-local-storage-from-a-startup-task).</span></span>

## <a name="next-steps"></a><span data-ttu-id="45613-243">다음 단계</span><span class="sxs-lookup"><span data-stu-id="45613-243">Next steps</span></span>
<span data-ttu-id="45613-244">클라우드 [서비스 모델 및 패키지](cloud-services-model-and-package.md)</span><span class="sxs-lookup"><span data-stu-id="45613-244">Review the cloud [service model and package](cloud-services-model-and-package.md)</span></span>

<span data-ttu-id="45613-245">[작업](cloud-services-startup-tasks.md) 작동 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="45613-245">Learn more about how [Tasks](cloud-services-startup-tasks.md) work.</span></span>

<span data-ttu-id="45613-246">[만들고 배포하세요](cloud-services-how-to-create-deploy-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="45613-246">[Create and deploy](cloud-services-how-to-create-deploy-portal.md) your cloud service package.</span></span>

<span data-ttu-id="45613-247">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span><span class="sxs-lookup"><span data-stu-id="45613-247">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span></span>
<span data-ttu-id="45613-248">[태스크]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span><span class="sxs-lookup"><span data-stu-id="45613-248">[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span></span>
[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
<span data-ttu-id="45613-249">[환경]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span><span class="sxs-lookup"><span data-stu-id="45613-249">[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span></span>
<span data-ttu-id="45613-250">[변수]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span><span class="sxs-lookup"><span data-stu-id="45613-250">[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span></span>
<span data-ttu-id="45613-251">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span><span class="sxs-lookup"><span data-stu-id="45613-251">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span></span>
[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
<span data-ttu-id="45613-252">[끝점]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints</span><span class="sxs-lookup"><span data-stu-id="45613-252">[Endpoints]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints</span></span>
<span data-ttu-id="45613-253">[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage</span><span class="sxs-lookup"><span data-stu-id="45613-253">[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage</span></span>
<span data-ttu-id="45613-254">[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources</span><span class="sxs-lookup"><span data-stu-id="45613-254">[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources</span></span>
<span data-ttu-id="45613-255">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span><span class="sxs-lookup"><span data-stu-id="45613-255">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span></span>
