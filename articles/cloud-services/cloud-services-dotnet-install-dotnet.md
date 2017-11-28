---
title: "Azure 클라우드 서비스 역할에.NET aaaInstall | Microsoft Docs"
description: "이 문서에서는 toomanually 클라우드 서비스 웹 및 작업자 역할에 hello.NET Framework를 설치 하는 방법을 설명합니다"
services: cloud-services
documentationcenter: .net
author: thraka
manager: timlt
editor: 
ms.assetid: 8d1243dc-879c-4d1f-9ed0-eecd1f6a6653
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: adegeo
ms.openlocfilehash: 45f0f30221292f98c591511b091b02ebe1c1272c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-net-on-azure-cloud-services-roles"></a><span data-ttu-id="3514a-103">Azure Cloud Services 역할에 .NET 설치</span><span class="sxs-lookup"><span data-stu-id="3514a-103">Install .NET on Azure Cloud Services roles</span></span>
<span data-ttu-id="3514a-104">이 문서에서는 tooinstall 버전의.NET Framework에서 제공 하지 않는 하는 Azure 게스트 OS를 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-104">This article describes how tooinstall versions of .NET Framework that don't come with hello Azure Guest OS.</span></span> <span data-ttu-id="3514a-105">사용할 수 있습니다.NET hello 게스트 OS tooconfigure 클라우드 서비스 웹 및 작업자 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-105">You can use .NET on hello Guest OS tooconfigure your cloud service web and worker roles.</span></span>

<span data-ttu-id="3514a-106">예를 들어 hello.NET 4.6의 모든 릴리스와 함께 제공 되지 게스트 OS 제품군 4에.NET 4.6.1을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-106">For example, you can install .NET 4.6.1 on hello Guest OS family 4, which doesn't come with any release of .NET 4.6.</span></span> <span data-ttu-id="3514a-107">(게스트 OS 제품군 5 hello.NET 4.6과 함께 제공지 않습니다.) Azure 게스트 OS 릴리스 hello hello 대 대 한 최신 정보에 대 한 hello를 참조 하십시오 [Azure 게스트 OS 릴리스 뉴스](cloud-services-guestos-update-matrix.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-107">(hello Guest OS family 5 does come with .NET 4.6.) For hello latest information on hello Azure Guest OS releases, see hello [Azure Guest OS release news](cloud-services-guestos-update-matrix.md).</span></span> 

>[!IMPORTANT]
><span data-ttu-id="3514a-108">Azure SDK 2.9 hello hello 게스트 OS 제품군 4 또는 이전 버전에서.NET 4.6를 배포 하는 방법에 대 한 제한을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-108">hello Azure SDK 2.9 contains a restriction on deploying .NET 4.6 on hello Guest OS family 4 or earlier.</span></span> <span data-ttu-id="3514a-109">Hello 제한에 대 한 수정 hello에 있는 [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-109">A fix for hello restriction is available on hello [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span></span>

<span data-ttu-id="3514a-110">웹 및 작업자 역할에서는.NET tooinstall hello.NET 웹 설치 관리자에서 클라우드 서비스 프로젝트의 일부로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-110">tooinstall .NET on your web and worker roles, include hello .NET web installer as part of your cloud service project.</span></span> <span data-ttu-id="3514a-111">Hello 역할 시작 작업의 일부로 hello 설치 관리자를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-111">Start hello installer as part of hello role's startup tasks.</span></span> 

## <a name="add-hello-net-installer-tooyour-project"></a><span data-ttu-id="3514a-112">Hello.NET 설치 관리자 tooyour 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="3514a-112">Add hello .NET installer tooyour project</span></span>
<span data-ttu-id="3514a-113">.NET Framework hello에 대 한 toodownload hello 웹 설치 관리자 tooinstall hello 버전을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-113">toodownload hello web installer for hello .NET Framework, choose hello version that you want tooinstall:</span></span>

* [<span data-ttu-id="3514a-114">.NET 4.7 웹 설치 관리자</span><span class="sxs-lookup"><span data-stu-id="3514a-114">.NET 4.7 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=825298)
* [<span data-ttu-id="3514a-115">.NET 4.6.1 웹 설치 관리자</span><span class="sxs-lookup"><span data-stu-id="3514a-115">.NET 4.6.1 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=671729)

<span data-ttu-id="3514a-116">에 대 한 tooadd hello 설치 관리자는 *웹* 역할:</span><span class="sxs-lookup"><span data-stu-id="3514a-116">tooadd hello installer for a *web* role:</span></span>
  1. <span data-ttu-id="3514a-117">**솔루션 탐색기** 내 클라우드 서비스 프로젝트의 **역할** 아래에서 *웹* 역할을 마우스 오른쪽 단추로 클릭하고 **추가** > **새 폴더**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-117">In **Solution Explorer**, under **Roles** in your cloud service project, right-click your *web* role and select **Add** > **New Folder**.</span></span> <span data-ttu-id="3514a-118">이름이 **bin**인 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-118">Create a folder named **bin**.</span></span>
  2. <span data-ttu-id="3514a-119">Hello bin 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** > **기존 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-119">Right-click hello bin folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="3514a-120">Hello.NET 설치 관리자를 선택 하 고 toohello bin 폴더에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-120">Select hello .NET installer and add it toohello bin folder.</span></span>
  
<span data-ttu-id="3514a-121">에 대 한 tooadd hello 설치 관리자는 *작업자* 역할:</span><span class="sxs-lookup"><span data-stu-id="3514a-121">tooadd hello installer for a *worker* role:</span></span>
* <span data-ttu-id="3514a-122">*작업자* 역할을 마우스 오른쪽 단추로 클릭하고 **추가** > **기존 항목**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-122">Right-click your *worker* role and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="3514a-123">Hello.NET 설치 관리자를 선택 하 고 toohello 역할을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-123">Select hello .NET installer and add it toohello role.</span></span> 

<span data-ttu-id="3514a-124">이 방식으로 toohello 역할 콘텐츠 폴더에 파일을 추가한 경우 tooyour 클라우드 서비스 패키지 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-124">When files are added in this way toohello role content folder, they're automatically added tooyour cloud service package.</span></span> <span data-ttu-id="3514a-125">hello 파일 됩니다 hello 가상 컴퓨터에 배포 된 tooa 위치를 일관 되 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-125">hello files are then deployed tooa consistent location on hello virtual machine.</span></span> <span data-ttu-id="3514a-126">모든 역할 hello 설치 관리자의 복사본을가지고 않도록 클라우드 서비스에서 각 웹 및 작업자 역할에 대 한이 프로세스를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-126">Repeat this process for each web and worker role in your cloud service so that all roles have a copy of hello installer.</span></span>

> [!NOTE]
> <span data-ttu-id="3514a-127">응용 프로그램이 .NET 4.6을 대상으로 하는 경우 클라우드 서비스 역할에 .NET 4.6.1을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-127">You should install .NET 4.6.1 on your cloud service role even if your application targets .NET 4.6.</span></span> <span data-ttu-id="3514a-128">hello 기술 자료를 포함 하는 게스트 OS hello [업데이트 3098779](https://support.microsoft.com/kb/3098779) 및 [3097997 업데이트](https://support.microsoft.com/kb/3097997)합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-128">hello Guest OS includes hello Knowledge Base [update 3098779](https://support.microsoft.com/kb/3098779) and [update 3097997](https://support.microsoft.com/kb/3097997).</span></span> <span data-ttu-id="3514a-129">.NET 4.6이 hello 기술 자료 업데이트 위에 설치 된 경우.NET 응용 프로그램을 실행 하면 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-129">Issues can occur when you run your .NET applications if .NET 4.6 is installed on top of hello Knowledge Base updates.</span></span> <span data-ttu-id="3514a-130">이러한 문제는 tooavoid 버전 4.6가 아닌.NET 4.6.1 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-130">tooavoid these issues, install .NET 4.6.1 rather than version 4.6.</span></span> <span data-ttu-id="3514a-131">자세한 내용은 참조 hello [기술 자료 문서 3118750](https://support.microsoft.com/kb/3118750)합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-131">For more information, see hello [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
> 
> 

![설치 관리자 파일이 포함된 역할 콘텐츠][1]

## <a name="define-startup-tasks-for-your-roles"></a><span data-ttu-id="3514a-133">사용자 역할에 대한 시작 작업 정의</span><span class="sxs-lookup"><span data-stu-id="3514a-133">Define startup tasks for your roles</span></span>
<span data-ttu-id="3514a-134">역할 시작 되기 전에 시작 작업 tooperform 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-134">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="3514a-135">이 프레임 워크 hello을 보장 하는 hello 시작 작업의 일부 hello.NET Framework를 설치 하면 응용 프로그램 코드를 실행 하기 전에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-135">Installing hello .NET Framework as part of hello startup task ensures that hello framework is installed before any application code is run.</span></span> <span data-ttu-id="3514a-136">시작 작업에 대한 자세한 내용은 [Azure에서 시작 작업 실행](cloud-services-startup-tasks.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3514a-136">For more information on startup tasks, see [Run startup tasks in Azure](cloud-services-startup-tasks.md).</span></span> 

1. <span data-ttu-id="3514a-137">다음 콘텐츠 toohello ServiceDefinition.csdef 파일에서 hello hello 추가 **WebRole** 또는 **WorkerRole** 모든 역할에 대 한 노드:</span><span class="sxs-lookup"><span data-stu-id="3514a-137">Add hello following content toohello ServiceDefinition.csdef file under hello **WebRole** or **WorkerRole** node for all roles:</span></span>
   
    ```xml
    <LocalResources>
      <LocalStorage name="NETFXInstall" sizeInMB="1024" cleanOnRoleRecycle="false" />
    </LocalResources>    
    <Startup>
      <Task commandLine="install.cmd" executionContext="elevated" taskType="simple">
        <Environment>
          <Variable name="PathToNETFXInstall">
            <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='NETFXInstall']/@path" />
          </Variable>
          <Variable name="ComputeEmulatorRunning">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
        </Environment>
      </Task>
    </Startup>
    ```
   
    <span data-ttu-id="3514a-138">hello 앞의 구성 hello 콘솔 명령 실행 `install.cmd` 관리자 권한 tooinstall와.NET Framework hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-138">hello preceding configuration runs hello console command `install.cmd` with administrator privileges tooinstall hello .NET Framework.</span></span> <span data-ttu-id="3514a-139">hello 구성도 만듭니다.는 **LocalStorage** 라는 요소 **NETFXInstall**합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-139">hello configuration also creates a **LocalStorage** element named **NETFXInstall**.</span></span> <span data-ttu-id="3514a-140">hello 시작 스크립트 hello 임시 폴더 toouse이 로컬 저장소 리소스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-140">hello startup script sets hello temp folder toouse this local storage resource.</span></span> 
    
    > [!IMPORTANT]
    > <span data-ttu-id="3514a-141">tooensure hello 프레임 워크의이 리소스 tooat hello 크기 설정의 설치를 최소한 수정 1, 024MB 합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-141">tooensure correct installation of hello framework, set hello size of this resource tooat least 1,024 MB.</span></span>
    
    <span data-ttu-id="3514a-142">시작 작업에 대한 자세한 내용은 [일반적인 Azure Cloud Services 시작 작업](cloud-services-startup-tasks-common.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3514a-142">For more information about startup tasks, see [Common Azure Cloud Services startup tasks](cloud-services-startup-tasks-common.md).</span></span>

2. <span data-ttu-id="3514a-143">라는 파일을 만들어 **install.cmd** hello 다음 설치 스크립트 toohello 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-143">Create a file named **install.cmd** and add hello following install script toohello file.</span></span>

    <span data-ttu-id="3514a-144">hello 스크립트 여부 hello 지정 된 버전의.NET Framework hello에 이미 설치 되어 hello 컴퓨터 hello 레지스트리를 쿼리하여 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-144">hello script checks whether hello specified version of hello .NET Framework is already installed on hello machine by querying hello registry.</span></span> <span data-ttu-id="3514a-145">Hello.NET 버전에 설치 되어 있지 않으면 hello.NET 웹 설치 관리자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-145">If hello .NET version is not installed, then hello .NET web installer is opened.</span></span> <span data-ttu-id="3514a-146">문제를 해결 하는 toohelp, hello 스크립트는 모든 활동 toohello 파일 startuptasklog-(현재 날짜 및 시간).txt에 저장 된 기록 **InstallLogs** 로컬 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-146">toohelp troubleshoot any issues, hello script logs all activity toohello file startuptasklog-(current date and time).txt that is stored in **InstallLogs** local storage.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="3514a-147">Windows 메모장 toocreate hello install.cmd 파일 처럼 기본 텍스트 편집기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-147">Use a basic text editor like Windows Notepad toocreate hello install.cmd file.</span></span> <span data-ttu-id="3514a-148">Visual Studio toocreate 텍스트 파일을 사용 하 여 hello 확장 too.cmd 변경 하는 경우 hello 파일에 u t F-8 바이트 순서 표시를 여전히 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-148">If you use Visual Studio toocreate a text file and change hello extension too.cmd, hello file might still contain a UTF-8 byte order mark.</span></span> <span data-ttu-id="3514a-149">이 표시가 hello hello 스크립트의 첫 번째 줄에서 실행 될 때 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-149">This mark can cause an error when hello first line of hello script is run.</span></span> <span data-ttu-id="3514a-150">tooavoid이이 오류를 hello의 첫 번째 줄 hello hello 바이트 순서 처리에서 생략할 수 있는 REM 문 스크립트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-150">tooavoid this error, make hello first line of hello script a REM statement that can be skipped by hello byte order processing.</span></span> 
    > 
    >
   
    ```cmd
    REM Set hello value of netfx tooinstall appropriate .NET Framework. 
    REM ***** tooinstall .NET 4.5.2 set hello variable netfx too"NDP452" *****
    REM ***** tooinstall .NET 4.6 set hello variable netfx too"NDP46" *****
    REM ***** tooinstall .NET 4.6.1 set hello variable netfx too"NDP461" *****
    REM ***** tooinstall .NET 4.6.2 set hello variable netfx too"NDP462" *****
    REM ***** tooinstall .NET 4.7 set hello variable netfx too"NDP47" *****
    set netfx="NDP47"

    REM ***** Set script start timestamp *****
    set timehour=%time:~0,2%
    set timestamp=%date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2%
    set "log=install.cmd started %timestamp%."

    REM ***** Exit script if running in Emulator *****
    if %ComputeEmulatorRunning%=="true" goto exit

    REM ***** Needed toocorrectly install .NET 4.6.1, otherwise you may see an out of disk space error *****
    set TMP=%PathToNETFXInstall%
    set TEMP=%PathToNETFXInstall%

    REM ***** Setup .NET filenames and registry keys *****
    if %netfx%=="NDP47" goto NDP47
    if %netfx%=="NDP462" goto NDP462
    if %netfx%=="NDP461" goto NDP461
    if %netfx%=="NDP46" goto NDP46
        set "netfxinstallfile=NDP452-KB2901954-Web.exe"
        set netfxregkey="0x5cbf5"
        goto logtimestamp

    :NDP46
    set "netfxinstallfile=NDP46-KB3045560-Web.exe"
    set netfxregkey="0x6004f"
    goto logtimestamp

    :NDP461
    set "netfxinstallfile=NDP461-KB3102438-Web.exe"
    set netfxregkey="0x6040e"
    goto logtimestamp

    :NDP462
    set "netfxinstallfile=NDP462-KB3151802-Web.exe"
    set netfxregkey="0x60632"

    :NDP47
    set "netfxinstallfile=NDP47-KB3186500-Web.exe"
    set netfxregkey="0x707FE"

    :logtimestamp
    REM ***** Setup LogFile with timestamp *****
    md "%PathToNETFXInstall%\log"
    set startuptasklog="%PathToNETFXInstall%log\startuptasklog-%timestamp%.txt"
    set netfxinstallerlog="%PathToNETFXInstall%log\NetFXInstallerLog-%timestamp%"
    echo %log% >> %startuptasklog%
    echo Logfile generated at: %startuptasklog% >> %startuptasklog%
    echo TMP set to: %TMP% >> %startuptasklog%
    echo TEMP set to: %TEMP% >> %startuptasklog%

    REM ***** Check if .NET is installed *****
    echo Checking if .NET (%netfx%) is installed >> %startuptasklog%
    set /A netfxregkeydecimal=%netfxregkey%
    set foundkey=0
    FOR /F "usebackq skip=2 tokens=1,2*" %%A in (`reg query "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full" /v Release 2^>nul`) do @set /A foundkey=%%C
    echo Minimum required key: %netfxregkeydecimal% -- found key: %foundkey% >> %startuptasklog%
    if %foundkey% GEQ %netfxregkeydecimal% goto installed

    REM ***** Installing .NET *****
    echo Installing .NET with commandline: start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog%  /chainingpackage "CloudService Startup Task" >> %startuptasklog%
    start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog% /chainingpackage "CloudService Startup Task" >> %startuptasklog% 2>>&1
    if %ERRORLEVEL%== 0 goto installed
        echo .NET installer exited with code %ERRORLEVEL% >> %startuptasklog%    
        if %ERRORLEVEL%== 3010 goto restart
        if %ERRORLEVEL%== 1641 goto restart
        echo .NET (%netfx%) install failed with Error Code %ERRORLEVEL%. Further logs can be found in %netfxinstallerlog% >> %startuptasklog%

    :restart
    echo Restarting toocomplete .NET (%netfx%) installation >> %startuptasklog%
    EXIT /B %ERRORLEVEL%

    :installed
    echo .NET (%netfx%) is installed >> %startuptasklog%

    :end
    echo install.cmd completed: %date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2% >> %startuptasklog%

    :exit
    EXIT /B 0
    ```
   
   > [!NOTE]
   > <span data-ttu-id="3514a-151">이 스크립트를 보여 줍니다 tooinstall.NET 4.5.2 또는 4.6.NET 4.5.2에 이미 있는 경우에 계속 사용할 수 있도록 버전 hello Azure 게스트 OS에 어떻게 합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-151">This script shows how tooinstall .NET 4.5.2 or version 4.6 for continuity, even though .NET 4.5.2 is already available on hello Azure Guest OS.</span></span> <span data-ttu-id="3514a-152">직접 설치 해야 버전 4.6가 아닌.NET 4.6.1 hello에 설명 된 대로 [기술 자료 문서 3118750](https://support.microsoft.com/kb/3118750)합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-152">You should directly install .NET 4.6.1 rather than version 4.6, as described in hello [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
   > 
   > 

3. <span data-ttu-id="3514a-153">사용 하 여 추가 hello install.cmd 파일 tooeach 역할 **추가** > **기존 항목** 에 **솔루션 탐색기** 이 항목의 앞부분에 설명 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-153">Add hello install.cmd file tooeach role by using **Add** > **Existing Item** in **Solution Explorer** as described earlier in this topic.</span></span> 

    <span data-ttu-id="3514a-154">이 단계를 완료 한 후에 모든 역할 hello install.cmd 파일과 hello.NET 설치 관리자 파일 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-154">After this step is complete, all roles should have hello .NET installer file and hello install.cmd file.</span></span>

   ![모든 파일이 포함된 역할 콘텐츠][2]

## <a name="configure-diagnostics-tootransfer-startup-logs-tooblob-storage"></a><span data-ttu-id="3514a-156">진단 tootransfer 시작 로그 tooBlob 저장소 구성</span><span class="sxs-lookup"><span data-stu-id="3514a-156">Configure Diagnostics tootransfer startup logs tooBlob storage</span></span>
<span data-ttu-id="3514a-157">설치 문제를 해결 하는 toosimplify, Azure 진단을 tootransfer hello 시작에 의해 생성 된 모든 로그 파일을 스크립팅하거나 hello.NET 설치 관리자 tooAzure Blob 저장소를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-157">toosimplify troubleshooting installation issues, you can configure Azure Diagnostics tootransfer any log files generated by hello startup script or hello .NET installer tooAzure Blob storage.</span></span> <span data-ttu-id="3514a-158">이 방법을 사용 하 여 Blob 저장소에서 hello 로그 파일을 다운로드 대신 tooremote 데스크톱 hello 역할을 사용 하 여 hello 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-158">By using this approach, you can view hello logs by downloading hello log files from Blob storage rather than having tooremote desktop into hello role.</span></span>

<span data-ttu-id="3514a-159">tooconfigure 진단 hello diagnostics.wadcfgx 파일을 열고 추가 hello 내용을 따라 hello **디렉터리** 노드:</span><span class="sxs-lookup"><span data-stu-id="3514a-159">tooconfigure Diagnostics, open hello diagnostics.wadcfgx file and add hello following content under hello **Directories** node:</span></span> 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

<span data-ttu-id="3514a-160">이 XML hello에 hello 로그 디렉터리에 진단 tootransfer hello 파일로 구성 **NETFXInstall** 리소스 toohello hello에 진단 저장소 계정 **netfx 설치** blob 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-160">This XML configures Diagnostics tootransfer hello files in hello log directory in hello **NETFXInstall** resource toohello Diagnostics storage account in hello **netfx-install** blob container.</span></span>

## <a name="deploy-your-cloud-service"></a><span data-ttu-id="3514a-161">클라우드 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="3514a-161">Deploy your cloud service</span></span>
<span data-ttu-id="3514a-162">클라우드 서비스를 배포할 때 설치 되어 있지 않은 경우 시작 작업 hello hello.NET Framework를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-162">When you deploy your cloud service, hello startup tasks install hello .NET Framework if it's not already installed.</span></span> <span data-ttu-id="3514a-163">클라우드 서비스 역할 hello 중인 *사용 중* hello 프레임 워크를 설치 하는 동안 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-163">Your cloud service roles are in hello *busy* state while hello framework is being installed.</span></span> <span data-ttu-id="3514a-164">Hello 프레임 워크 설치를 다시 시작이 필요한 경우 hello 서비스 역할 다시 시작 또한 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3514a-164">If hello framework installation requires a restart, hello service roles might also restart.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3514a-165">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="3514a-165">Additional resources</span></span>
* <span data-ttu-id="3514a-166">[Hello.NET Framework 설치][Installing hello .NET Framework]</span><span class="sxs-lookup"><span data-stu-id="3514a-166">[Installing hello .NET Framework][Installing hello .NET Framework]</span></span>
* <span data-ttu-id="3514a-167">[설치된 .NET Framework 버전 확인][How to: Determine Which .NET Framework Versions Are Installed]</span><span class="sxs-lookup"><span data-stu-id="3514a-167">[Determine which .NET Framework versions are installed][How to: Determine Which .NET Framework Versions Are Installed]</span></span>
* <span data-ttu-id="3514a-168">[.NET Framework 설치 문제 해결][Troubleshooting .NET Framework Installations]</span><span class="sxs-lookup"><span data-stu-id="3514a-168">[Troubleshooting .NET Framework installations][Troubleshooting .NET Framework Installations]</span></span>

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing hello .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
