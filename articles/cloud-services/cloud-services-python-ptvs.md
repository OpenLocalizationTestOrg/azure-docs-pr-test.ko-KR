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
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a><span data-ttu-id="8255e-103">Python Tools for Visual Studio의 Python 웹 및 작업자 역할</span><span class="sxs-lookup"><span data-stu-id="8255e-103">Python web and worker roles with Python Tools for Visual Studio</span></span>

<span data-ttu-id="8255e-104">이 문서에서는 [Visual Studio용 Python Tools][Python Tools for Visual Studio]를 사용하여 Python 웹 및 작업자 역할을 사용하는 방법을 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-104">This article provides an overview of using Python web and worker roles using [Python Tools for Visual Studio][Python Tools for Visual Studio].</span></span> <span data-ttu-id="8255e-105">자세한 내용은 어떻게 toouse Visual Studio toocreate 및 Python을 사용 하는 기본 클라우드 서비스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-105">Learn how toouse Visual Studio toocreate and deploy a basic Cloud Service that uses Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8255e-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8255e-106">Prerequisites</span></span>
* [<span data-ttu-id="8255e-107">Visual Studio 2013, 2015 또는 2017</span><span class="sxs-lookup"><span data-stu-id="8255e-107">Visual Studio 2013, 2015, or 2017</span></span>](https://www.visualstudio.com/)
* <span data-ttu-id="8255e-108">[Visual Studio용 Python Tools][Python Tools for Visual Studio](PTVS)</span><span class="sxs-lookup"><span data-stu-id="8255e-108">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)</span></span>
* <span data-ttu-id="8255e-109">[VS 2013용 Azure SDK Tools][Azure SDK Tools for VS 2013] 또는</span><span class="sxs-lookup"><span data-stu-id="8255e-109">[Azure SDK Tools for VS 2013][Azure SDK Tools for VS 2013] or</span></span>  
<span data-ttu-id="8255e-110">[VS 2015용 Azure SDK Tools][Azure SDK Tools for VS 2015] 또는</span><span class="sxs-lookup"><span data-stu-id="8255e-110">[Azure SDK Tools for VS 2015][Azure SDK Tools for VS 2015] or</span></span>  
<span data-ttu-id="8255e-111">[VS 2017용 Azure SDK Tools][Azure SDK Tools for VS 2017]</span><span class="sxs-lookup"><span data-stu-id="8255e-111">[Azure SDK Tools for VS 2017][Azure SDK Tools for VS 2017]</span></span>
* <span data-ttu-id="8255e-112">[Python 2.7 32비트][Python 2.7 32-bit] 또는 [Python 3.5 32비트][Python 3.5 32-bit]</span><span class="sxs-lookup"><span data-stu-id="8255e-112">[Python 2.7 32-bit][Python 2.7 32-bit] or [Python 3.5 32-bit][Python 3.5 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a><span data-ttu-id="8255e-113">Python 웹 및 작업자 역할 정의</span><span class="sxs-lookup"><span data-stu-id="8255e-113">What are Python web and worker roles?</span></span>
<span data-ttu-id="8255e-114">Azure는 응용 프로그램을 실행하기 위한 세 가지 컴퓨팅 모델인 [Azure App Service의 Web Apps 기능][execution model-web sites], [Azure Virtual Machines][execution model-vms] 및 [Azure Cloud Services][execution model-cloud services]를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-114">Azure provides three compute models for running applications: [Web Apps feature in Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms], and [Azure Cloud Services][execution model-cloud services].</span></span> <span data-ttu-id="8255e-115">이 세 모델은 모두 Python을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-115">All three models support Python.</span></span> <span data-ttu-id="8255e-116">웹 및 작업자 역할을 포함하는 Cloud Services는 *PaaS(Platform as a Service)*를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-116">Cloud Services, which include web and worker roles, provide *Platform as a Service (PaaS)*.</span></span> <span data-ttu-id="8255e-117">클라우드 서비스 내에서 웹 역할 제공 하는 전용된 인터넷 정보 서비스 (IIS) 웹 서버 toohost 프런트 엔드 웹 응용 프로그램의 경우 작업자 역할 사용자 상호 작용 및 입력에 관계 없이 비동기, 장기 실행 또는 영구 작업을 실행할 수 합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-117">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server toohost front end web applications, while a worker role can run asynchronous, long-running, or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="8255e-118">자세한 내용은 [Cloud Service란?]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8255e-118">For more information, see [What is a Cloud Service?].</span></span>

> [!NOTE]
> <span data-ttu-id="8255e-119">*Toobuild 간단한 웹 사이트를 찾고 있습니까?*</span><span class="sxs-lookup"><span data-stu-id="8255e-119">*Looking toobuild a simple website?*</span></span>
> <span data-ttu-id="8255e-120">시나리오는 간단한 웹 사이트 프런트 엔드만 있을 경우에 Azure 앱 서비스의 hello 경량 웹 응용 프로그램 기능을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-120">If your scenario involves just a simple website front end, consider using hello lightweight Web Apps feature in Azure App Service.</span></span> <span data-ttu-id="8255e-121">웹 사이트 증가 하 고 요구 사항을 변경 하는 대로 tooa 클라우드 서비스를 쉽게 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-121">You can easily upgrade tooa Cloud Service as your website grows and your requirements change.</span></span> <span data-ttu-id="8255e-122">Hello 참조 <a href="/develop/python/">Python 개발자 센터</a> hello 웹 응용 프로그램 기능의 Azure 앱 서비스의 개발을 설명 하는 문서에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-122">See hello <a href="/develop/python/">Python Developer Center</a> for articles that cover development of hello Web Apps feature in Azure App Service.</span></span>
> <br />
> 
> 

## <a name="project-creation"></a><span data-ttu-id="8255e-123">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="8255e-123">Project creation</span></span>
<span data-ttu-id="8255e-124">Visual Studio에서 선택할 수 있습니다 **Azure 클라우드 서비스** hello에 **새 프로젝트** 대화 상자의 **Python**합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-124">In Visual Studio, you can select **Azure Cloud Service** in hello **New Project** dialog box, under **Python**.</span></span>

![새 프로젝트 대화 상자](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

<span data-ttu-id="8255e-126">Hello Azure 클라우드 서비스 마법사에서 새 웹 및 작업자 역할을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-126">In hello Azure Cloud Service wizard, you can create new web and worker roles.</span></span>

![Azure 클라우드 서비스 대화 상자](./media/cloud-services-python-ptvs/new-service-wizard.png)

<span data-ttu-id="8255e-128">hello 작업자 역할 템플릿을 상용구 코드 tooconnect tooan Azure 저장소 계정 또는 Azure 서비스 버스 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-128">hello worker role template comes with boilerplate code tooconnect tooan Azure storage account or Azure Service Bus.</span></span>

![클라우드 서비스 솔루션](./media/cloud-services-python-ptvs/worker.png)

<span data-ttu-id="8255e-130">언제 든 지 웹 또는 작업자 역할 tooan 기존 클라우드 서비스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-130">You can add web or worker roles tooan existing cloud service at any time.</span></span>  <span data-ttu-id="8255e-131">솔루션에 tooadd 기존 프로젝트를 선택 하거나 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-131">You can choose tooadd existing projects in your solution, or create new ones.</span></span>

![역할 추가 명령](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

<span data-ttu-id="8255e-133">클라우드 서비스는 여러 언어로 구현된 역할을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-133">Your cloud service can contain roles implemented in different languages.</span></span>  <span data-ttu-id="8255e-134">예를 들어 Django로 구현된 Python 웹 역할과 Python 또는 C# 작업자 역할이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-134">For example, you can have a Python web role implemented using Django, with Python, or with C# worker roles.</span></span>  <span data-ttu-id="8255e-135">서비스 버스 큐 또는 저장소 큐를 사용하면 역할 간에 쉽게 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-135">You can easily communicate between your roles using Service Bus queues or storage queues.</span></span>

## <a name="install-python-on-hello-cloud-service"></a><span data-ttu-id="8255e-136">Hello 클라우드 서비스에 Python을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-136">Install Python on hello cloud service</span></span>
> [!WARNING]
> <span data-ttu-id="8255e-137">hello 설치 스크립트 (이 문서를 마지막으로 수정한 hello 시간)에 설치 된 Visual Studio가 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-137">hello setup scripts that are installed with Visual Studio (at hello time this article was last updated) do not work.</span></span> <span data-ttu-id="8255e-138">이 섹션에서는 해결 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-138">This section describes a workaround.</span></span>
> 
> 

<span data-ttu-id="8255e-139">hello 설치 스크립트와 hello 큰 문제는 python 설치 하지 마십시오입니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-139">hello main problem with hello setup scripts is that they do not install python.</span></span> <span data-ttu-id="8255e-140">먼저 두 개의 정의 [시작 작업](cloud-services-startup-tasks.md) hello에 [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-140">First, define two [startup tasks](cloud-services-startup-tasks.md) in hello [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) file.</span></span> <span data-ttu-id="8255e-141">hello 첫 번째 작업 (**PrepPython.ps1**) 다운로드 하 고 hello Python 런타임의 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-141">hello first task (**PrepPython.ps1**) downloads and installs hello Python runtime.</span></span> <span data-ttu-id="8255e-142">hello 두 번째 작업 (**PipInstaller.ps1**) 실행 pip tooinstall 종속성 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-142">hello second task (**PipInstaller.ps1**) runs pip tooinstall any dependencies you may have.</span></span>

<span data-ttu-id="8255e-143">다음 스크립트는 hello Python 3.5를 대상으로 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-143">hello following scripts were written targeting Python 3.5.</span></span> <span data-ttu-id="8255e-144">Toouse hello 버전을 원하는 경우 python, 집합 hello의 2.x **PYTHON2** 변수 파일 너무**에** hello 두 시작 작업 및 hello 런타임 작업에 대 한: `<Variable name="PYTHON2" value="<mark>on</mark>" />`합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-144">If you want toouse hello version 2.x of python, set hello **PYTHON2** variable file too**on** for hello two startup tasks and hello runtime task: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span></span>

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

<span data-ttu-id="8255e-145">hello **PYTHON2** 및 **PYPATH** 변수 toohello 작업자 시작 작업을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-145">hello **PYTHON2** and **PYPATH** variables must be added toohello worker startup task.</span></span> <span data-ttu-id="8255e-146">hello **PYPATH** 변수 경우에 사용 hello **PYTHON2** 변수는 너무 설정**에**합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-146">hello **PYPATH** variable is only used if hello **PYTHON2** variable is set too**on**.</span></span>

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

#### <a name="sample-servicedefinitioncsdef"></a><span data-ttu-id="8255e-147">샘플 ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="8255e-147">Sample ServiceDefinition.csdef</span></span>
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



<span data-ttu-id="8255e-148">다음으로 hello를 만듭니다 **PrepPython.ps1** 및 **PipInstaller.ps1** hello에 대 한 파일 **. / b i n** 역할 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-148">Next, create hello **PrepPython.ps1** and **PipInstaller.ps1** files in hello **./bin** folder of your role.</span></span>

#### <a name="preppythonps1"></a><span data-ttu-id="8255e-149">PrepPython.ps1</span><span class="sxs-lookup"><span data-stu-id="8255e-149">PrepPython.ps1</span></span>
<span data-ttu-id="8255e-150">이 스크립트는 Python을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-150">This script installs python.</span></span> <span data-ttu-id="8255e-151">경우 hello **PYTHON2** 환경 변수는 너무 설정**에**, Python 2.7가 설치 되어 다음 그렇지 않은 경우 Python 3.5가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-151">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is installed, otherwise Python 3.5 is installed.</span></span>

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

#### <a name="pipinstallerps1"></a><span data-ttu-id="8255e-152">PipInstaller.ps1</span><span class="sxs-lookup"><span data-stu-id="8255e-152">PipInstaller.ps1</span></span>
<span data-ttu-id="8255e-153">이 스크립트는 pip를 호출 하 고 hello에 설치 하는 모든 hello 종속성 **requirements.txt** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-153">This script calls up pip and installs all of hello dependencies in hello **requirements.txt** file.</span></span> <span data-ttu-id="8255e-154">경우 hello **PYTHON2** 환경 변수는 너무 설정**에**, Python 2.7을 사용 하는 다음 Python 3.5 그렇지 않으면 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-154">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

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

#### <a name="modify-launchworkerps1"></a><span data-ttu-id="8255e-155">LaunchWorker.ps1 수정</span><span class="sxs-lookup"><span data-stu-id="8255e-155">Modify LaunchWorker.ps1</span></span>
> [!NOTE]
> <span data-ttu-id="8255e-156">경우 hello는 **작업자 역할** 프로젝트 **LauncherWorker.ps1** 파일은 필요한 tooexecute hello 시작 파일.</span><span class="sxs-lookup"><span data-stu-id="8255e-156">In hello case of a **worker role** project, **LauncherWorker.ps1** file is required tooexecute hello startup file.</span></span> <span data-ttu-id="8255e-157">에 **웹 역할** 프로젝트를 hello 시작 파일 대신에 정의 된 hello 프로젝트 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-157">In a **web role** project, hello startup file is instead defined in hello project properties.</span></span>
> 
> 

<span data-ttu-id="8255e-158">hello **bin\LaunchWorker.ps1** toodo 준비 작업이 하지만 많은 실제로 작동 하지 않는 원래 만들어진 합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-158">hello **bin\LaunchWorker.ps1** was originally created toodo a lot of prep work but it doesn't really work.</span></span> <span data-ttu-id="8255e-159">다음 스크립트는 hello로 해당 파일의 내용을 hello를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-159">Replace hello contents in that file with hello following script.</span></span>

<span data-ttu-id="8255e-160">이 스크립트 호출 hello **worker.py** python 프로젝트에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-160">This script calls hello **worker.py** file from your python project.</span></span> <span data-ttu-id="8255e-161">경우 hello **PYTHON2** 환경 변수는 너무 설정**에**, Python 2.7을 사용 하는 다음 Python 3.5 그렇지 않으면 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-161">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

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

#### <a name="pscmd"></a><span data-ttu-id="8255e-162">ps.cmd</span><span class="sxs-lookup"><span data-stu-id="8255e-162">ps.cmd</span></span>
<span data-ttu-id="8255e-163">Visual Studio 템플릿 hello 만들어져 있어야는 **ps.cmd** hello에 대 한 파일 **. / b i n** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-163">hello Visual Studio templates should have created a **ps.cmd** file in hello **./bin** folder.</span></span> <span data-ttu-id="8255e-164">이 셸 스크립트 래퍼 스크립트가 위의 hello PowerShell 호출를 호출 하는 hello PowerShell 래퍼의 hello 이름에 따라 로깅을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-164">This shell script calls out hello PowerShell wrapper scripts above and provides logging based on hello name of hello PowerShell wrapper called.</span></span> <span data-ttu-id="8255e-165">이 파일이 생성되지 않은 경우 포함되어야 하는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-165">If this file wasn't created, here is what should be in it.</span></span> 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a><span data-ttu-id="8255e-166">로컬 실행</span><span class="sxs-lookup"><span data-stu-id="8255e-166">Run locally</span></span>
<span data-ttu-id="8255e-167">클라우드 서비스 프로젝트 hello 시작 프로젝트로 설정 하 고 F5 키를 누릅니다 hello 클라우드 서비스는 hello 로컬 Azure 에뮬레이터에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-167">If you set your cloud service project as hello startup project and press F5, hello cloud service runs in hello local Azure emulator.</span></span>

<span data-ttu-id="8255e-168">PTVS 지원 하지만 hello 에뮬레이터, 디버깅 (예: 중단점)에서 시작 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-168">Although PTVS supports launching in hello emulator, debugging (for example, breakpoints) does not work.</span></span>

<span data-ttu-id="8255e-169">toodebug 웹 및 작업자 역할, 역할 프로젝트 hello hello 시작 프로젝트로 설정 하 고 디버그할 수 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-169">toodebug your web and worker roles, you can set hello role project as hello startup project and debug that instead.</span></span>  <span data-ttu-id="8255e-170">여러 시작 프로젝트를 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-170">You can also set multiple startup projects.</span></span>  <span data-ttu-id="8255e-171">Hello 솔루션을 마우스 오른쪽 단추로 클릭 한 다음 선택 **시작 프로젝트 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-171">Right-click hello solution and then select **Set StartUp Projects**.</span></span>

![솔루션 시작 프로젝트 속성](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-tooazure"></a><span data-ttu-id="8255e-173">TooAzure 게시</span><span class="sxs-lookup"><span data-stu-id="8255e-173">Publish tooAzure</span></span>
<span data-ttu-id="8255e-174">toopublish, hello 솔루션의 hello 클라우드 서비스 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-174">toopublish, right-click hello cloud service project in hello solution and then select **Publish**.</span></span>

![Microsoft Azure 게시 로그인](./media/cloud-services-python-ptvs/publish-sign-in.png)

<span data-ttu-id="8255e-176">Hello 마법사를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-176">Follow hello wizard.</span></span> <span data-ttu-id="8255e-177">필요한 경우 원격 데스크톱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-177">If you need to, enable remote desktop.</span></span> <span data-ttu-id="8255e-178">원격 데스크톱 toodebug 대상이 필요 때 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-178">Remote desktop is helpful when you need toodebug something.</span></span>

<span data-ttu-id="8255e-179">설정 구성을 완료한 후 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-179">When you are done configuring settings, click **Publish**.</span></span>

<span data-ttu-id="8255e-180">Hello 출력 창에 표시 되는 일부 진행 한 후 hello Microsoft Azure 활동 로그 창이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-180">Some progress appears in hello output window, then you'll see hello Microsoft Azure Activity Log window.</span></span>

![Microsoft Azure 활동 로그 창](./media/cloud-services-python-ptvs/publish-activity-log.png)

<span data-ttu-id="8255e-182">배포는 몇 분 toocomplete, 다음 웹 또는 작업자 역할은 Azure에서 실행!</span><span class="sxs-lookup"><span data-stu-id="8255e-182">Deployment takes several minutes toocomplete, then your web and/or worker roles run on Azure!</span></span>

### <a name="investigate-logs"></a><span data-ttu-id="8255e-183">로그 조사</span><span class="sxs-lookup"><span data-stu-id="8255e-183">Investigate logs</span></span>
<span data-ttu-id="8255e-184">Hello 클라우드 서비스가 가상 컴퓨터 시작 되 고 Python 설치 후 모든 실패 메시지 hello 로그 toofind에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-184">After hello cloud service virtual machine starts up and installs Python, you can look at hello logs toofind any failure messages.</span></span> <span data-ttu-id="8255e-185">이러한 로그는 hello 아래의 **C:\Resources\Directory\\{역할} \LogFiles** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-185">These logs are located in hello **C:\Resources\Directory\\{role}\LogFiles** folder.</span></span> <span data-ttu-id="8255e-186">**PrepPython.err.txt** hello 스크립트 잠그려고 할 때이 toodetect Python 설치 된 경우에서 오류가 하나 이상 포함 된 및 **PipInstaller.err.txt** 오래 된 버전의 pip는 불만 제기 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-186">**PrepPython.err.txt** has at least one error in it from when hello script tries toodetect if Python is installed and **PipInstaller.err.txt** may complain about an outdated version of pip.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8255e-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8255e-187">Next steps</span></span>
<span data-ttu-id="8255e-188">Visual Studio 용 Python 도구에서 웹 및 작업자 역할 사용에 대 한 자세한 내용을 보려면 hello PTVS 설명서를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="8255e-188">For more detailed information about working with web and worker roles in Python Tools for Visual Studio, see hello PTVS documentation:</span></span>

* <span data-ttu-id="8255e-189">[Cloud Service 프로젝트][Cloud Service Projects]</span><span class="sxs-lookup"><span data-stu-id="8255e-189">[Cloud Service Projects][Cloud Service Projects]</span></span>

<span data-ttu-id="8255e-190">Azure 저장소 서비스 또는 서비스 버스를 사용 하는 등 사용자 웹 및 작업자 역할에서 Azure 서비스를 사용 하는 방법에 대 한 자세한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="8255e-190">For more details about using Azure services from your web and worker roles, such as using Azure Storage or Service Bus, see hello following articles:</span></span>

* <span data-ttu-id="8255e-191">[Blob Service][Blob Service]</span><span class="sxs-lookup"><span data-stu-id="8255e-191">[Blob Service][Blob Service]</span></span>
* <span data-ttu-id="8255e-192">[Table Service][Table Service]</span><span class="sxs-lookup"><span data-stu-id="8255e-192">[Table Service][Table Service]</span></span>
* <span data-ttu-id="8255e-193">[큐 서비스][Queue Service]</span><span class="sxs-lookup"><span data-stu-id="8255e-193">[Queue Service][Queue Service]</span></span>
* <span data-ttu-id="8255e-194">[Service Bus 큐][Service Bus Queues]</span><span class="sxs-lookup"><span data-stu-id="8255e-194">[Service Bus Queues][Service Bus Queues]</span></span>
* <span data-ttu-id="8255e-195">[Service Bus 토픽][Service Bus Topics]</span><span class="sxs-lookup"><span data-stu-id="8255e-195">[Service Bus Topics][Service Bus Topics]</span></span>

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
