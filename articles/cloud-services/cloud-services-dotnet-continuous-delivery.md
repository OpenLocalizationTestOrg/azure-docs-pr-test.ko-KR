---
title: "Azure에서 TFS를 사용 하 여 클라우드에 대 한 aaaContinuous 배달 서비스 | Microsoft Docs"
description: "자세한 방법을 tooset Azure에 대 한 지속적인 업데이트를 클라우드 앱입니다. MSBuild 명령줄 문 및 PowerShell 스크립트에 대한 코드 샘플도 제공됩니다."
services: cloud-services
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4f3c93c6-5c82-4779-9d19-7404a01e82ca
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/12/2017
ms.author: kraigb
ms.openlocfilehash: c0e5e72ffbd3c05b84ce1733068e92c528bcc4b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a><span data-ttu-id="80238-104">Azure Cloud Services의 지속적인 전송</span><span class="sxs-lookup"><span data-stu-id="80238-104">Continuous Delivery for Cloud Services in Azure</span></span>
<span data-ttu-id="80238-105">hello이 문서에 설명 된 프로세스에서는 Azure 클라우드 앱에 대 한 지속적인 업데이트를 tooset 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-105">hello process described in this article shows you how tooset up continuous delivery for Azure cloud apps.</span></span> <span data-ttu-id="80238-106">이 프로세스를 사용 하면 자동으로 패키지를 만들고 hello 패키지 tooAzure 모든 코드 체크 인 후에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80238-106">This process enables you to automatically create packages and deploy hello package tooAzure after every code check-in.</span></span> <span data-ttu-id="80238-107">hello이 문서에서 설명 하는 패키지 빌드 프로세스는 해당 toohello **패키지** Visual Studio에서 명령 및 게시 단계는 해당 toohello **게시** Visual Studio에서 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-107">hello package build process described in this article is equivalent toohello **Package** command in Visual Studio, and the publishing steps are equivalent toohello **Publish** command in Visual Studio.</span></span>
<span data-ttu-id="80238-108">MSBuild 명령줄 문 및 Windows PowerShell 스크립트를 toocreate 빌드 서버도 사용 하는 hello 문서에서는 hello 메서드 toooptionally Visual Studio Team Foundation Server-팀 빌드 정의 구성 하는 방법을 보여 줍니다. toouse hello MSBuild 명령 및 PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="80238-108">hello article covers hello methods you would use toocreate a build server with MSBuild command-line statements and Windows PowerShell scripts, and it also demonstrates how toooptionally configure Visual Studio Team Foundation Server - Team Build definitions toouse hello MSBuild commands and PowerShell scripts.</span></span> <span data-ttu-id="80238-109">hello 프로세스는 빌드 환경 및 Azure 대상 환경에 대 한 사용자 지정 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-109">hello process is customizable for your build environment and Azure target environments.</span></span>

<span data-ttu-id="80238-110">Visual Studio Team Services는 tfs 버전을 사용할 수도 있습니다 Azure에서 호스트, toodo이 더 쉽게 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-110">You can also use Visual Studio Team Services, a version of TFS that is hosted in Azure, toodo this more easily.</span></span> 

<span data-ttu-id="80238-111">시작하기 전에 Visual Studio에서 응용 프로그램을 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-111">Before you start, you should publish your application from Visual Studio.</span></span>
<span data-ttu-id="80238-112">이 방법을 사용 하면 모든 hello 리소스가 사용 가능 하 고 초기화 된 인지 tooautomate hello 게시 프로세스를 만들려고 할 때입니다.</span><span class="sxs-lookup"><span data-stu-id="80238-112">This will ensure that all hello resources are available and initialized when you attempt tooautomate hello publication process.</span></span>

## <a name="1-configure-hello-build-server"></a><span data-ttu-id="80238-113">1: hello 빌드 서버 구성</span><span class="sxs-lookup"><span data-stu-id="80238-113">1: Configure hello Build Server</span></span>
<span data-ttu-id="80238-114">MSBuild를 사용 하 여 Azure 패키지를 만들 수 있습니다, 전에 hello 빌드 서버에서 필요한 hello 소프트웨어 및 도구를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-114">Before you can create an Azure package by using MSBuild, you must install hello required software and tools on hello build server.</span></span>

<span data-ttu-id="80238-115">Visual Studio에서 필요한 toobe hello 빌드 서버에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-115">Visual Studio is not required toobe installed on hello build server.</span></span> <span data-ttu-id="80238-116">빌드 서버에 toouse Team Foundation Build Service toomanage을 원하는 경우 hello 지침 hello에 따라 [Team Foundation Build Service] [ Team Foundation Build Service] 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="80238-116">If you want toouse Team Foundation Build Service toomanage your build server, follow hello instructions in hello [Team Foundation Build Service][Team Foundation Build Service] documentation.</span></span>

1. <span data-ttu-id="80238-117">Hello 빌드 서버에서 설치 hello [.NET Framework 4.5.2][.NET Framework 4.5.2], MSBuild가 포함 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-117">On hello build server, install hello [.NET Framework 4.5.2][.NET Framework 4.5.2], which includes MSBuild.</span></span>
2. <span data-ttu-id="80238-118">Hello 최신 설치 [.NET 용 Azure Authoring Tools](https://azure.microsoft.com/develop/net/)합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-118">Install hello latest [Azure Authoring Tools for .NET](https://azure.microsoft.com/develop/net/).</span></span>
3. <span data-ttu-id="80238-119">Hello 설치 [Azure Libraries for.NET](http://go.microsoft.com/fwlink/?LinkId=623519)합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-119">Install hello [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span></span>
4. <span data-ttu-id="80238-120">빌드 서버를 Visual Studio 설치 toohello로 hello Microsoft.WebApplication.targets 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-120">Copy hello Microsoft.WebApplication.targets file from a Visual Studio installation toohello build server.</span></span>

   <span data-ttu-id="80238-121">Visual Studio가 설치 된 컴퓨터에서이 파일은 hello 디렉터리 c:\\Program files (x86)\\MSBuild\\Microsoft\\VisualStudio\\v 14.0\\WebApplications 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-121">On a computer with Visual Studio installed, this file is located in hello directory C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span></span> <span data-ttu-id="80238-122">Toohello 복사 해야 hello 빌드 서버의 동일한 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80238-122">You should copy it toohello same directory on hello build server.</span></span>
5. <span data-ttu-id="80238-123">Hello 설치 [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-123">Install hello [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span></span>

## <a name="2-build-a-package-using-msbuild-commands"></a><span data-ttu-id="80238-124">2: MSBuild 명령을 사용하여 패키지 빌드</span><span class="sxs-lookup"><span data-stu-id="80238-124">2: Build a Package using MSBuild Commands</span></span>
<span data-ttu-id="80238-125">이 단원의 내용은 방법을 tooconstruct는 MSBuild 명령 하는 Azure 패키지를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-125">This section describes how tooconstruct an MSBuild command that builds an Azure package.</span></span> <span data-ttu-id="80238-126">Toodo hello 빌드 서버 tooverify 모든 항목이 올바르게 구성 되 고 hello MSBuild 명령이 수행 하려는 작업에이 단계를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-126">Run this step on hello build server tooverify that everything is configured correctly and that hello MSBuild command does what you want it toodo.</span></span> <span data-ttu-id="80238-127">Hello 다음 섹션에 설명 된 대로이 명령줄 tooexisting hello 빌드 서버에서 스크립트를 작성 하거나 hello 명령줄 TFS 빌드 정의에서 사용할 수 있습니다 하거나 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80238-127">You can either add this command line tooexisting build scripts on hello build server, or you can use hello command line in a TFS Build Definition, as described in hello next section.</span></span> <span data-ttu-id="80238-128">명령줄 매개 변수 및 MSBuild에 대한 자세한 내용은 [MSBuild 명령줄 참조](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80238-128">For more information about command-line parameters and MSBuild, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>

1. <span data-ttu-id="80238-129">Visual Studio가 hello 빌드 서버에 설치를 찾아 선택 **Visual Studio 명령 프롬프트** hello에 **Visual Studio Tools** Windows 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="80238-129">If Visual Studio is installed on hello build server, locate and choose **Visual Studio Command Prompt** in hello **Visual Studio Tools** folder in Windows.</span></span>

   <span data-ttu-id="80238-130">Visual Studio hello 빌드 서버에 설치 되어 있지는 명령 프롬프트를 열고 및 MSBuild.exe 경로에 액세스할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-130">If Visual Studio is not installed on hello build server, open a command prompt and make sure that MSBuild.exe is accessible on the path.</span></span> <span data-ttu-id="80238-131">MSBuild는 hello 경로 % WINDIR %에 hello.NET Framework와 함께 설치\\Microsoft.NET\\프레임 워크\\*버전*합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-131">MSBuild is installed with hello .NET Framework in hello path %WINDIR%\\Microsoft.NET\\Framework\\*Version*.</span></span> <span data-ttu-id="80238-132">예를 들어.NET Framework 4가 설치 되어 있는 경우 MSBuild.exe toohello PATH 환경 변수를 추가 하려면 hello 다음 hello 명령 프롬프트에서 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-132">For example, to add MSBuild.exe toohello PATH environment variable when you have .NET Framework 4 installed, type hello following command at hello command prompt:</span></span>

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. <span data-ttu-id="80238-133">Hello 명령 프롬프트에서 원하는 toobuild Azure 프로젝트 파일이 있는 toohello 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-133">At hello command prompt, navigate toohello folder containing the Azure project file that you want toobuild.</span></span>
3. <span data-ttu-id="80238-134">Hello /target으로 MSBuild를 실행: 게시 hello 다음 예제와 같이 옵션:</span><span class="sxs-lookup"><span data-stu-id="80238-134">Run MSBuild with hello /target:Publish option as in hello following example:</span></span>

       MSBuild /target:Publish

   <span data-ttu-id="80238-135">이 옵션은 /t:Publish로 간략하게 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80238-135">This option can be abbreviated as /t:Publish.</span></span> <span data-ttu-id="80238-136">Visual Studio에서 사용할 수 있는 hello 게시 명령 hello Azure SDK가 설치 되어 있는 경우 MSBuild의 hello /t:Publish 옵션 혼동 될 안 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-136">hello /t:Publish option in MSBuild should not be confused with hello Publish commands available in Visual Studio when you have hello Azure SDK installed.</span></span> <span data-ttu-id="80238-137">hello /t: 빌드 hello Azure 패키지에만 게시 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="80238-137">hello /t:Publish option only builds hello Azure packages.</span></span> <span data-ttu-id="80238-138">Visual Studio에서 게시 명령을 hello와 마찬가지로 hello 패키지는 배포 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="80238-138">It does not deploy hello packages as hello Publish commands in Visual Studio do.</span></span>

   <span data-ttu-id="80238-139">필요에 따라 hello 프로젝트 이름을 MSBuild 매개 변수로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80238-139">Optionally, you can specify hello project name as an MSBuild parameter.</span></span> <span data-ttu-id="80238-140">지정 하지 않으면 hello 현재 디렉터리가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80238-140">If not specified, hello current directory is used.</span></span> <span data-ttu-id="80238-141">MSBuild 명령줄 옵션에 대한 자세한 내용은 [MSBuild 명령줄 참조](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80238-141">For more information about MSBuild command line options, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>
4. <span data-ttu-id="80238-142">Hello 출력을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="80238-142">Locate hello output.</span></span> <span data-ttu-id="80238-143">기본적으로이 명령은 디렉터리에에서 만듭니다 hello 프로젝트에 대 한 관계 toohello 루트 폴더와 같은 *ProjectDir*\\bin\\*구성* \\ app.publish\\합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-143">By default, this command creates a directory in relation toohello root folder for hello project, such as *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span></span> <span data-ttu-id="80238-144">Azure 프로젝트를 빌드할 때 두 개의 파일, hello 패키지 파일 자체와 hello 함께 나타날 구성 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-144">When you build an Azure project, you generate two files, hello package file itself and hello accompanying configuration file:</span></span>

   * <span data-ttu-id="80238-145">Project.cspkg</span><span class="sxs-lookup"><span data-stu-id="80238-145">Project.cspkg</span></span>
   * <span data-ttu-id="80238-146">ServiceConfiguration.*TargetProfile*.cscfg</span><span class="sxs-lookup"><span data-stu-id="80238-146">ServiceConfiguration.*TargetProfile*.cscfg</span></span>

   <span data-ttu-id="80238-147">기본적으로 각 Azure 프로젝트에는 로컬(디버깅) 빌드용 서비스 구성 파일(.cscfg 파일) 하나와 클라우드(스테이징 또는 프로덕션) 빌드용 서비스 구성 파일 하나가 포함되지만 필요에 따라 서비스 구성 파일을 추가하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80238-147">By default, each Azure project includes one service configuration file (.cscfg file) for local (debugging) builds and another for cloud (staging or production) builds, but you can add or remove service configuration files as needed.</span></span> <span data-ttu-id="80238-148">Visual Studio 내에서 패키지를 빌드할 때 hello 패키지와 함께 어떤 서비스 구성 파일 tooinclude를 묻는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80238-148">When you build a package within Visual Studio, you will be asked which service configuration file tooinclude alongside hello package.</span></span>
5. <span data-ttu-id="80238-149">Hello 서비스 구성 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-149">Specify hello service configuration file.</span></span> <span data-ttu-id="80238-150">MSBuild를 사용 하 여 패키지를 빌드할 때 hello 로컬 서비스 구성 파일은 기본적으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80238-150">When you build a package by using MSBuild, hello local service configuration file is included by default.</span></span> <span data-ttu-id="80238-151">tooinclude 다른 서비스 구성 파일을 hello 다음 예제와 같이 hello MSBuild 명령의 TargetProfile 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-151">tooinclude a different service configuration file, set the TargetProfile property of hello MSBuild command, as in hello following example:</span></span>

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. <span data-ttu-id="80238-152">Hello 출력을 위한 hello 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-152">Specify hello location for hello output.</span></span> <span data-ttu-id="80238-153">/p:PublishDir를 사용 하 여 hello 경로 설정 =*디렉터리* \\ hello 후행 hello 다음 예제와 같이 백슬래시 구분 기호를 포함 하 여 옵션:</span><span class="sxs-lookup"><span data-stu-id="80238-153">Set hello path by using the /p:PublishDir=*Directory*\\ option, including hello trailing backslash separator, as in hello following example:</span></span>

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   <span data-ttu-id="80238-154">생성 하 고 테스트 한 후 적절 한 MSBuild 명령 줄 toobuild 프로젝트 및 Azure 패키지에 결합 합니다,이 명령줄 tooyour 빌드 스크립트를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80238-154">Once you've constructed and tested an appropriate MSBuild command line toobuild your projects and combine them into an Azure package, you can add this command line tooyour build scripts.</span></span> <span data-ttu-id="80238-155">빌드 서버에서 사용자 지정 스크립트를 사용하는 경우 이 프로세스는 사용자 지정 빌드 프로세스의 세부 사항에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="80238-155">If your build server uses custom scripts, this process will depend on the specifics of your custom build process.</span></span> <span data-ttu-id="80238-156">TFS 빌드 환경으로를 사용 하는 hello 다음 단계 tooadd hello Azure 패키지 빌드 tooyour 빌드 프로세스의 hello 지침에 따라 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80238-156">If you are using TFS as a build environment, then you can follow hello instructions in hello next step tooadd hello Azure package build tooyour build process.</span></span>

## <a name="3-build-a-package-using-tfs-team-build"></a><span data-ttu-id="80238-157">3: TFS 팀 빌드를 사용하여 패키지 빌드</span><span class="sxs-lookup"><span data-stu-id="80238-157">3: Build a Package using TFS Team Build</span></span>
<span data-ttu-id="80238-158">있는 경우 Team Foundation Server (TFS) 빌드 컨트롤러와 hello 빌드 서버에 따라 설정할 TFS 빌드 컴퓨터로 설정 후 Azure 패키지에 대 한 자동화 된 빌드를 필요에 따라 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80238-158">If you have Team Foundation Server (TFS) set up as a build controller and hello build server set up as a TFS build machine, then you can optionally set up an automated build for your Azure package.</span></span> <span data-ttu-id="80238-159">tooset 및 Team Foundation server 사용 하 여 빌드 시스템으로 참조 하는 방법에 대 한 내용은 [확장 빌드 시스템][Scale out your build system]합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-159">For information on how tooset up and use Team Foundation server as a build system, see [Scale out your build system][Scale out your build system].</span></span> <span data-ttu-id="80238-160">특히, 다음 절차에 설명 된 대로 빌드 서버를 구성 있을 것을 전제로 [배포 빌드 서버를 구성 하 고][Deploy and configure a build server], 및 팀 프로젝트를 만든 클라우드를 만든 상태 hello 팀 프로젝트에서 서비스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="80238-160">In particular, the following procedure assumes that you have configured your build server as described in [Deploy and configure a build server][Deploy and configure a build server], and that you have created a team project, created a cloud service project in hello team project.</span></span>

<span data-ttu-id="80238-161">tooconfigure TFS toobuild Azure 패키지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-161">tooconfigure TFS toobuild Azure packages, perform hello following steps:</span></span>

1. <span data-ttu-id="80238-162">Hello 보기 메뉴에 개발 컴퓨터에 Visual Studio에서 선택 **팀 탐색기**, Ctrl + 선택 또는\\, Ctrl + M입니다.</span><span class="sxs-lookup"><span data-stu-id="80238-162">In Visual Studio on your development computer, on hello View menu, choose **Team Explorer**, or choose Ctrl+\\, Ctrl+M.</span></span> <span data-ttu-id="80238-163">팀 탐색기 창에서 확장 hello **빌드** 노드 hello를 선택 하거나 **빌드** 선택한 페이지 **새 빌드 정의**합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-163">In the Team Explorer window, expand hello **Builds** node or choose hello **Builds** page, and choose **New Build Definition**.</span></span>

   ![새 빌드 정의 옵션][0]
2. <span data-ttu-id="80238-165">Hello 선택 **트리거** 탭을 하려는 경우에 대 한 조건을 작성 하는 패키지 toobe hello hello 원하는 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-165">Choose hello **Trigger** tab, and specify hello desired conditions for when you want hello package toobe built.</span></span> <span data-ttu-id="80238-166">예를 들어 지정 **연속 통합** toobuild hello 패키지는 소스 제어에서 체크 인 될 때마다 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-166">For example, specify **Continuous Integration** toobuild hello package whenever a source control check-in occurs.</span></span>
3. <span data-ttu-id="80238-167">Hello 선택 **소스 설정** 탭을 프로젝트 폴더는 hello에 나열 되는지 확인 **소스 제어 폴더** 열, 그리고 hello 상태가 **활성**합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-167">Choose hello **Source Settings** tab, and make sure your project folder is listed in hello **Source Control Folder** column, and hello status is **Active**.</span></span>
4. <span data-ttu-id="80238-168">Hello 선택 **빌드 기본값** 탭을 빌드 컨트롤러에서 빌드 서버 hello hello 이름을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-168">Choose hello **Build Defaults** tab, and under Build controller, verify hello name of hello build server.</span></span>  <span data-ttu-id="80238-169">도 hello 옵션을 선택 **복사 빌드 출력 toohello 다음 저장 폴더** 원하는 hello 저장 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-169">Also, choose hello option **Copy build output toohello following drop folder** and specify hello desired drop location.</span></span>
5. <span data-ttu-id="80238-170">Hello 선택 **프로세스** 탭 합니다. Hello 프로세스 탭에서 선택 hello 기본 서식 파일에서 **빌드**을 아직 선택 하지 않은 경우 hello 확장 hello 프로젝트를 선택 **고급** hello 섹션인 **빌드**hello 눈금의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="80238-170">Choose hello **Process** tab. On hello Process tab, choose hello default template, under **Build**, choose hello project if it is not already selected, and expand hello **Advanced** section in hello **Build** section of hello grid.</span></span>
6. <span data-ttu-id="80238-171">선택 **MSBuild 인수**, 위의 2 단계에에서 설명 된 대로 hello 적절 한 MSBuild 명령줄 인수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-171">Choose **MSBuild Arguments**, and set hello appropriate MSBuild command line arguments as described in Step 2 above.</span></span> <span data-ttu-id="80238-172">예를 들어 입력 **/t: /p:PublishDir 게시 =\\\\myserver\\삭제\\**  toobuild 패키지 및 복사 hello 패키지 파일 toohello 위치 \\ \\myserver\\삭제\\:</span><span class="sxs-lookup"><span data-stu-id="80238-172">For example, enter **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** toobuild a package and copy hello package files toohello location \\\\myserver\\drops\\:</span></span>

   ![MSBuild Arguments][2]

   > [!NOTE]
   > <span data-ttu-id="80238-174">Hello 파일 tooa 복사 공유 사용 하면 보다 쉽게 toomanually 개발 컴퓨터에서 hello 패키지를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-174">Copying hello files tooa public share makes it easier toomanually deploy hello packages from your development computer.</span></span>
7. <span data-ttu-id="80238-175">새 빌드를 큐 또는 tooyour 프로젝트 변경에서에서 확인 하 여 빌드 단계의 hello 성공 여부를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-175">Test hello success of your build step by checking in a change tooyour project, or queue up a new build.</span></span> <span data-ttu-id="80238-176">팀 탐색기에서 새 빌드를 tooqueue 마우스 오른쪽 단추로 클릭 **모든 빌드 정의** 선택한 후 **새 빌드 큐 대기**합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-176">tooqueue up a new build, in the Team Explorer, right-click **All Build Definitions,** and then choose **Queue New Build**.</span></span>

## <a name="4-publish-a-package-using-a-powershell-script"></a><span data-ttu-id="80238-177">4: PowerShell 스크립트를 사용하여 패키지 게시</span><span class="sxs-lookup"><span data-stu-id="80238-177">4: Publish a Package using a PowerShell Script</span></span>
<span data-ttu-id="80238-178">이 섹션에서는 tooconstruct hello 클라우드 응용 프로그램 패키지를 게시 하는 Windows PowerShell 스크립트에서 선택적 매개 변수를 사용 하 여 tooAzure를 출력 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-178">This section describes how tooconstruct a Windows PowerShell script that will publish hello Cloud app package output tooAzure using optional parameters.</span></span> <span data-ttu-id="80238-179">사용자 지정 빌드 자동화에서 hello 빌드 단계 후에이 스크립트를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80238-179">This script can be called after hello build step in your custom build automation.</span></span> <span data-ttu-id="80238-180">Visual Studio TFS 팀 빌드의 프로세스 템플릿 워크플로 작업에서 호출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80238-180">It can also be called from Process Template workflow activities in Visual Studio TFS Team Build.</span></span>

1. <span data-ttu-id="80238-181">Hello 설치 [Azure PowerShell cmdlet] [ Azure PowerShell cmdlets] (v0.6.1 또는 이상)입니다.</span><span class="sxs-lookup"><span data-stu-id="80238-181">Install hello [Azure PowerShell cmdlets][Azure PowerShell cmdlets] (v0.6.1 or higher).</span></span>
   <span data-ttu-id="80238-182">Hello cmdlet 설치 단계 동안 tooinstall 스냅인으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-182">During hello cmdlet setup phase, choose tooinstall as a snap-in.</span></span> <span data-ttu-id="80238-183">Note hello 이전 버전 번호 2.x.x 있지만이 공식적으로 지원 되는 버전 CodePlex를 통해 제공 되는 hello 이전 버전을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-183">Note that this officially supported version replaces hello older version offered through CodePlex, although hello previous versions were numbered 2.x.x.</span></span>
2. <span data-ttu-id="80238-184">Hello 시작 메뉴 또는 시작 페이지를 사용 하 여 Azure PowerShell을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-184">Start Azure PowerShell using hello Start menu or Start page.</span></span> <span data-ttu-id="80238-185">이러한 방식으로 시작 하는 경우 hello Azure PowerShell cmdlet이 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80238-185">If you start in this way, hello Azure PowerShell cmdlets will be loaded.</span></span>
3. <span data-ttu-id="80238-186">Hello 부분 명령을 입력 하 여 hello PowerShell cmdlet가 로드 되었는지 확인 hello PowerShell 프롬프트에서 `Get-Azure` 문 완성을 위해 Tab 키를 hello 다음 키를 눌러 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80238-186">At hello PowerShell prompt, verify that hello PowerShell cmdlets are loaded by entering hello partial command `Get-Azure` and then pressing hello Tab key for statement completion.</span></span>

   <span data-ttu-id="80238-187">반복 해 서 hello Tab 키를 누를 경우 다양 한 Azure PowerShell 명령을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-187">If you press hello Tab key repeatedly, you should see various Azure PowerShell commands.</span></span>
4. <span data-ttu-id="80238-188">Hello.publishsettings 파일에서 구독 정보를 가져와서 tooyour Azure 구독을 연결할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-188">Verify that you can connect tooyour Azure subscription by importing your subscription information from hello .publishsettings file.</span></span>

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   <span data-ttu-id="80238-189">다음 명령을 실행 hello</span><span class="sxs-lookup"><span data-stu-id="80238-189">Then enter hello command</span></span>

   `Get-AzureSubscription`

   <span data-ttu-id="80238-190">그러면 구독에 대한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="80238-190">This shows information about your subscription.</span></span> <span data-ttu-id="80238-191">모든 정보가 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-191">Verify that everything is correct.</span></span>
5. <span data-ttu-id="80238-192">Hello c: \로 스크립트 폴더에이 문서의 뒷부분에서 제공 하는 hello 스크립트 템플릿을 저장\\스크립트\\WindowsAzure\\**PublishCloudService.ps1**합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-192">Save hello script template provided at hello end of this article to your scripts folder as c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span></span>
6. <span data-ttu-id="80238-193">Hello 스크립트의 hello 매개 변수 섹션을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-193">Review hello parameters section of hello script.</span></span> <span data-ttu-id="80238-194">기본값을 추가하거나 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-194">Add or modify any default values.</span></span> <span data-ttu-id="80238-195">이러한 값은 명시적 매개 변수를 전달하여 언제든지 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80238-195">These values can always be overridden by passing in explicit parameters.</span></span>
7. <span data-ttu-id="80238-196">유효한 클라우드 서비스는 hello에서 대상이 될 수 있는 구독에 생성 된 저장소 계정 게시 스크립트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-196">Ensure there are valid cloud service and storage accounts created in your subscription that can be targeted by hello publish script.</span></span> <span data-ttu-id="80238-197">저장소 계정 (blob storage) 사용 하는 tooupload 되며 일시적으로 배포를 만드는 동안 hello 배포 패키지 및 config 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-197">The storage account (blob storage) will be used tooupload and temporarily store hello deployment package and config file while the deployment is being created.</span></span>

   * <span data-ttu-id="80238-198">새 클라우드 서비스 toocreate이 스크립트 또는 사용 하 여 hello를 호출할 수 있습니다 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-198">toocreate a new cloud service, you can call this script or use hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="80238-199">hello 클라우드 서비스 이름 접두사에 정규화 된 도메인 이름으로 사용 됩니다 하 고 따라서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-199">hello cloud service name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span>

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * <span data-ttu-id="80238-200">새 저장소 계정을 toocreate이 스크립트 또는 사용 하 여 hello를 호출할 수 있습니다 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-200">toocreate a new storage account, you can call this script or use hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="80238-201">hello 저장소 계정 이름 접두사에 정규화 된 도메인 이름으로 사용 됩니다 하 고 따라서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-201">hello storage account name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span> <span data-ttu-id="80238-202">클라우드 서비스 이름과 같은 이름을 hello를 사용 하 여 작업을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80238-202">You can try using hello same name as the cloud service.</span></span>

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. <span data-ttu-id="80238-203">Azure PowerShell에서 직접 hello 스크립트를 호출 하거나 hello 패키지 빌드 후이 스크립트 tooyour 호스트 빌드 자동화 toooccur를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-203">Call hello script directly from Azure PowerShell, or wire up this script tooyour host build automation toooccur after hello package build.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="80238-204">hello 스크립트 항상 검색 되는 경우 기본적으로 기존 배포를 교체 또는 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80238-204">hello script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="80238-205">사용자에게 확인할 수 없는 경우 자동화에서 지속적인 전송을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-205">This is necessary to enable continuous delivery from automation where no user prompting is possible.</span></span>
   >
   >

   <span data-ttu-id="80238-206">**예제 시나리오 1:** 연속 배포 toohello 서비스의 환경을 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-206">**Example scenario 1:** continuous deployment toohello staging environment of a service:</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="80238-207">그런 다음 일반적으로 테스트 실행 검증 및 VIP 교환이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="80238-207">This is typically followed up by test run verification and a VIP swap.</span></span> <span data-ttu-id="80238-208">hello 통해 hello VIP 교체를 수행할 수 있습니다 [Azure 포털](https://portal.azure.com) 또는 hello 이동 배포 cmdlet을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-208">hello VIP swap can be done via hello [Azure portal](https://portal.azure.com) or by using hello Move-Deployment cmdlet.</span></span>

   <span data-ttu-id="80238-209">**예제 시나리오 2:** 전용된 테스트 서비스의 연속 배포 toohello 프로덕션 환경</span><span class="sxs-lookup"><span data-stu-id="80238-209">**Example scenario 2:** continuous deployment toohello production environment of a dedicated test service</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="80238-210">**원격 데스크톱:**</span><span class="sxs-lookup"><span data-stu-id="80238-210">**Remote Desktop:**</span></span>

   <span data-ttu-id="80238-211">Azure 프로젝트에서 원격 데스크톱이 활성화 되어 tooperform 추가 일회성 단계 tooensure hello 올바른 클라우드 서비스 인증서가이 스크립트의 대상 tooall 클라우드 서비스를 업로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-211">If Remote Desktop is enabled in your Azure project you will need tooperform additional one-time steps tooensure hello correct Cloud Service Certificate is uploaded tooall cloud services targeted by this script.</span></span>

   <span data-ttu-id="80238-212">역할에 필요한 hello 인증서 지문 값을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="80238-212">Locate hello certificate thumbprint values expected by your roles.</span></span> <span data-ttu-id="80238-213">지문 값 클라우드 구성 파일 (즉, ServiceConfiguration.Cloud.cscfg)의 hello 인증서 섹션에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80238-213">The thumbprint values are visible in hello Certificates section of the cloud config file (i.e. ServiceConfiguration.Cloud.cscfg).</span></span> <span data-ttu-id="80238-214">인증서를 선택 하면 옵션 표시 및 보기 hello에도 Visual Studio의 hello 원격 데스크톱 구성 대화 상자에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80238-214">It is also visible in hello Remote Desktop Configuration dialog in Visual Studio when you Show Options and view hello selected certificate.</span></span>

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   <span data-ttu-id="80238-215">일회 설치 단계로 cmdlet 스크립트를 다음 hello를 사용 하 여 원격 데스크톱 인증서를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-215">Upload Remote Desktop certificates as a one-time setup step using hello following cmdlet script:</span></span>

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   <span data-ttu-id="80238-216">예:</span><span class="sxs-lookup"><span data-stu-id="80238-216">For example:</span></span>

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   <span data-ttu-id="80238-217">또는 개인 키 및 업로드 인증서 tooeach 대상 클라우드 서비스를 사용 하 여 hello 인증서 파일 PFX를 내보낼 수는 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-217">Alternatively you can export hello certificate file PFX with private key and upload certificates tooeach target cloud service using the [Azure portal](https://portal.azure.com).</span></span>

   <!---
   Fixing broken links for Azure content migration from ACOM tooDOCS. I'm unable toofind a replacement links, so I'm commenting out this reference for now. hello author can investigate in hello future. "Read hello following article toolearn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   <span data-ttu-id="80238-218">**배포 업그레이드 및 배포 삭제 -\> 새 배포**</span><span class="sxs-lookup"><span data-stu-id="80238-218">**Upgrade Deployment vs. Delete Deployment -\> New Deployment**</span></span>

   <span data-ttu-id="80238-219">hello 스크립트는 기본적으로 수행 업그레이드 배포 ($enableDeploymentUpgrade = 1) 경우 매개 변수가 전달 또는 1 값이 명시적으로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80238-219">hello script will by default perform an Upgrade Deployment ($enableDeploymentUpgrade = 1) when no parameter is passed in or the value 1 is passed explicitly.</span></span> <span data-ttu-id="80238-220">단일 인스턴스인 경우 전체 배포보다 시간이 적게 걸린다는 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80238-220">For single instances this has the advantage of taking less time than a full deployment.</span></span> <span data-ttu-id="80238-221">에 대해 고가용성이도 이점이 hello 다른 실행 중인 경우에 따라 유지 해야 하는 인스턴스 업그레이드 (업데이트 도메인 walking) 뿐 아니라 VIP를 삭제 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="80238-221">For instances that require high availability this also has hello advantage of leaving some instances running while others are upgraded (walking your update domain), plus your VIP will not be deleted.</span></span>

   <span data-ttu-id="80238-222">Hello 스크립트에서 업그레이드 배포를 해제할 수 있습니다 ($enableDeploymentUpgrade = 0) 또는 전달 하 여 *-enableDeploymentUpgrade 0* 를 매개 변수로 스크립트 동작 toofirst 삭제 모든 기존 배포를 변경한 다음 만듭니다는 새 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-222">Upgrade Deployment can be disabled in hello script ($enableDeploymentUpgrade = 0) or by passing *-enableDeploymentUpgrade 0* as a parameter, which alters the script behavior toofirst delete any existing deployment and then create a new deployment.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="80238-223">hello 스크립트 항상 검색 되는 경우 기본적으로 기존 배포를 교체 또는 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80238-223">hello script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="80238-224">사용자에게 확인할 수 없는 경우 자동화에서 지속적인 전송을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-224">This is necessary to enable continuous delivery from automation where no user/operator prompting is possible.</span></span>
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a><span data-ttu-id="80238-225">5: TFS 팀 빌드를 사용하여 패키지 게시</span><span class="sxs-lookup"><span data-stu-id="80238-225">5: Publish a Package using TFS Team Build</span></span>
<span data-ttu-id="80238-226">이 선택적 단계 TFS 팀 빌드 toohello 스크립트 4 단계에서 만든 hello 패키지 빌드 tooAzure의 게시를 처리 하는 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-226">This optional step connects TFS Team Build toohello script created in step 4, which handles publishing of hello package build tooAzure.</span></span> <span data-ttu-id="80238-227">게시 작업 hello 워크플로의 hello 끝에 실행 되도록 빌드 정의에서 사용 하는 프로세스 템플릿을 수정 하 고 hello을 수반 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-227">This entails modifying hello Process Template used by your build definition so that it runs a Publish activity at hello end of hello workflow.</span></span> <span data-ttu-id="80238-228">hello 게시 활동에는 hello 빌드에서 매개 변수에 전달 하면 PowerShell 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-228">hello Publish activity will execute your PowerShell command passing in parameters from hello build.</span></span> <span data-ttu-id="80238-229">Hello 표준 빌드 출력으로 hello MSBuild 대상 및 게시 스크립트의 출력을 콘솔로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-229">Output of hello MSBuild targets and publish script will be piped into hello standard build output.</span></span>

1. <span data-ttu-id="80238-230">Hello에 대 한 책임 빌드 정의 편집 연속 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-230">Edit hello Build Definition responsible for continuous deploy.</span></span>
2. <span data-ttu-id="80238-231">선택 hello **프로세스** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-231">Select hello **Process** tab.</span></span>
3. <span data-ttu-id="80238-232">에 따라 [이러한 지침](http://msdn.microsoft.com/library/dd647551.aspx) tooadd hello에 대 한 활동 프로젝트 빌드 프로세스 템플릿 다운로드 hello 기본 서식 파일, hello 프로젝트에 추가 하 여 체크 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-232">Follow [these instructions](http://msdn.microsoft.com/library/dd647551.aspx) tooadd an Activity project for hello build process template, download hello default template, add it to hello project and check it in.</span></span> <span data-ttu-id="80238-233">Hello 빌드 프로세스 템플릿을 AzureBuildProcessTemplate 같은 새 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-233">Give hello build process template a new name, such as AzureBuildProcessTemplate.</span></span>
4. <span data-ttu-id="80238-234">Toohello 반환 **프로세스** 탭을 사용 하 여 **자세한 정보 표시** tooshow 사용 가능한 빌드 프로세스 템플릿의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="80238-234">Return toohello **Process** tab, and use **Show Details** tooshow a list of available build process templates.</span></span> <span data-ttu-id="80238-235">Hello 선택 **새로 만들기...**  단추를 선택한 toohello 프로젝트 방금 추가 하 고 체크 인을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-235">Choose hello **New...** button, and navigate toohello project you just added and checked in.</span></span> <span data-ttu-id="80238-236">방금 만든 hello 템플릿을 찾아 선택 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-236">Locate hello template you just created and choose **OK**.</span></span>
5. <span data-ttu-id="80238-237">열기 hello 편집 프로세스 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-237">Open hello selected Process Template for editing.</span></span> <span data-ttu-id="80238-238">또는 XAML hello로 hello XML 편집기 toowork hello 워크플로 디자이너에서 직접 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80238-238">You can open directly in hello Workflow designer or in hello XML editor toowork with hello XAML.</span></span>
6. <span data-ttu-id="80238-239">Hello 워크플로 디자이너의 hello 인수 탭에서 별도 줄 항목으로 새 인수 목록을 따르는 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-239">Add hello following list of new arguments as separate line items in hello arguments tab of hello workflow designer.</span></span> <span data-ttu-id="80238-240">모든 인수는 direction=In 및 type=String이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-240">All arguments should have direction=In and type=String.</span></span> <span data-ttu-id="80238-241">이러한 게시 스크립트는 다음 get 사용 되는 toocall hello hello 워크플로에 hello 빌드 정의의 매개 변수를 사용 하는 tooflow 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80238-241">These will be used tooflow parameters from hello build definition into hello workflow, which then get used toocall hello publish script.</span></span>

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![인수 목록][3]

   <span data-ttu-id="80238-243">hello 해당 XAML은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="80238-243">hello corresponding XAML looks like this:</span></span>

       <Activity  _ />
         <x:Members>
           <x:Property Name="BuildSettings" Type="InArgument(mtbwa:BuildSettings)" />
           <x:Property Name="TestSpecs" Type="InArgument(mtbwa:TestSpecList)" />
           <x:Property Name="BuildNumberFormat" Type="InArgument(x:String)" />
           <x:Property Name="CleanWorkspace" Type="InArgument(mtbwa:CleanWorkspaceOption)" />
           <x:Property Name="RunCodeAnalysis" Type="InArgument(mtbwa:CodeAnalysisOption)" />
           <x:Property Name="SourceAndSymbolServerSettings" Type="InArgument(mtbwa:SourceAndSymbolServerSettings)" />
           <x:Property Name="AgentSettings" Type="InArgument(mtbwa:AgentSettings)" />
           <x:Property Name="AssociateChangesetsAndWorkItems" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateWorkItem" Type="InArgument(x:Boolean)" />
           <x:Property Name="DropBuild" Type="InArgument(x:Boolean)" />
           <x:Property Name="MSBuildArguments" Type="InArgument(x:String)" />
           <x:Property Name="MSBuildPlatform" Type="InArgument(mtbwa:ToolPlatform)" />
           <x:Property Name="PerformTestImpactAnalysis" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateLabel" Type="InArgument(x:Boolean)" />
           <x:Property Name="DisableTests" Type="InArgument(x:Boolean)" />
           <x:Property Name="GetVersion" Type="InArgument(x:String)" />
           <x:Property Name="PrivateDropLocation" Type="InArgument(x:String)" />
           <x:Property Name="Verbosity" Type="InArgument(mtbw:BuildVerbosity)" />
           <x:Property Name="Metadata" Type="mtbw:ProcessParameterMetadataCollection" />
           <x:Property Name="SupportedReasons" Type="mtbc:BuildReason" />
           <x:Property Name="SubscriptionName" Type="InArgument(x:String)" />
           <x:Property Name="StorageAccountName" Type="InArgument(x:String)" />
           <x:Property Name="CloudConfigLocation" Type="InArgument(x:String)" />
           <x:Property Name="PackageLocation" Type="InArgument(x:String)" />
           <x:Property Name="Environment" Type="InArgument(x:String)" />
           <x:Property Name="SubscriptionDataFileLocation" Type="InArgument(x:String)" />
           <x:Property Name="PublishScriptLocation" Type="InArgument(x:String)" />
           <x:Property Name="ServiceName" Type="InArgument(x:String)" />
         </x:Members>

         <this:Process.MSBuildArguments>
7. <span data-ttu-id="80238-244">에이전트에서 실행의 hello 끝에 새 시퀀스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-244">Add a new sequence at hello end of Run On Agent:</span></span>

   1. <span data-ttu-id="80238-245">If 문을 활동 toocheck 유효한 스크립트 파일에 대 한 추가 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-245">Start by adding an If Statement activity toocheck for a valid script file.</span></span> <span data-ttu-id="80238-246">Hello 조건 toothis 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-246">Set hello condition toothis value:</span></span>

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. <span data-ttu-id="80238-247">다음의 대/소문자 hello If 문을 hello에 새 시퀀스 활동을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-247">In hello Then case of hello If Statement, add a new Sequence activity.</span></span> <span data-ttu-id="80238-248">집합 hello 표시 이름 too'Start 게시 '</span><span class="sxs-lookup"><span data-stu-id="80238-248">Set hello display name too'Start publish'</span></span>
   3. <span data-ttu-id="80238-249">시작 시퀀스 선택 된 상태를 게시 하는 hello로 hello 워크플로 디자이너의 변수 탭에서 별도 줄 항목으로 다음과 같은 새 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-249">With hello Start publish sequence still selected, add the following list of new variables as separate line items in the variables tab of hello workflow designer.</span></span> <span data-ttu-id="80238-250">모든 변수의 변수 유형은 문자열이고 범위는 Start publish여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-250">All variables should have Variable type =String and Scope=Start publish.</span></span> <span data-ttu-id="80238-251">이 다음 get 사용 되는 toocall hello 게시 스크립트 워크플로에 hello 빌드 정의에서 매개 변수 사용된 tooflow 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80238-251">These will be used tooflow parameters from hello build definition into the workflow, which then get used toocall hello publish script.</span></span>

      * <span data-ttu-id="80238-252">SubscriptionDataFilePath, 문자열 유형</span><span class="sxs-lookup"><span data-stu-id="80238-252">SubscriptionDataFilePath, of type String</span></span>
      * <span data-ttu-id="80238-253">PublishScriptFilePath, 문자열 유형</span><span class="sxs-lookup"><span data-stu-id="80238-253">PublishScriptFilePath, of type String</span></span>

        ![새 변수][4]
   4. <span data-ttu-id="80238-255">이전 버전에서의 hello 시작 부분에서 ConvertWorkspaceItem 활동을 추가 또는 TFS 2012를 사용 하는 경우 새 시퀀스를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-255">If you are using TFS 2012 or earlier, add a ConvertWorkspaceItem activity at hello beginning of hello new Sequence.</span></span> <span data-ttu-id="80238-256">TFS 2013 이상를 사용 하는 경우 hello 새 시퀀스의 hello 시작 부분에서 GetLocalPath 활동을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-256">If you are using TFS 2013 or later, add a GetLocalPath activity at hello beginning of hello new sequence.</span></span> <span data-ttu-id="80238-257">ConvertWorkspaceItem에 대 한 hello 속성을 다음과 같이 설정: 방향 ServerToLocal, DisplayName = = 'Convert 게시 스크립트 파일 이름' 입력 'PublishScriptLocation', 결과 = 작업 영역 ' PublishScriptFilePath' = = '작업 영역'.</span><span class="sxs-lookup"><span data-stu-id="80238-257">For a ConvertWorkspaceItem, set hello properties as follows: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="80238-258">Hello 속성 IncomingPath too'PublishScriptLocation 설정 GetLocalPath 활동에 대 한 ', 결과 too'PublishScriptFilePath hello 및 '.</span><span class="sxs-lookup"><span data-stu-id="80238-258">For a GetLocalPath activity, set hello property IncomingPath too'PublishScriptLocation', and hello Result too'PublishScriptFilePath'.</span></span> <span data-ttu-id="80238-259">이 활동으로 변환 hello 경로 toohello (있는 경우) TFS 서버 위치에서 스크립트를 게시 tooa 표준 로컬 디스크 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="80238-259">This activity converts hello path toohello publish script from TFS server locations (if applicable) tooa standard local disk path.</span></span>
   5. <span data-ttu-id="80238-260">이전 버전에서의 hello 끝에 다른 ConvertWorkspaceItem 활동을 추가 또는 TFS 2012를 사용 하는 경우 새 시퀀스를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-260">If you are using TFS 2012 or earlier, add another ConvertWorkspaceItem activity at hello end of hello new Sequence.</span></span> <span data-ttu-id="80238-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span><span class="sxs-lookup"><span data-stu-id="80238-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="80238-262">TFS 2013 이상을 사용하고 있으면 또 다른 GetLocalPath를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-262">If you are using TFS 2013 or later, add another GetLocalPath.</span></span> <span data-ttu-id="80238-263">IncomingPath='SubscriptionDataFileLocation' 및 Result='SubscriptionDataFilePath'입니다.</span><span class="sxs-lookup"><span data-stu-id="80238-263">IncomingPath='SubscriptionDataFileLocation', and Result='SubscriptionDataFilePath.'</span></span>
   6. <span data-ttu-id="80238-264">Hello hello 끝나기 전에 InvokeProcess 활동을 추가할 새 시퀀스입니다.</span><span class="sxs-lookup"><span data-stu-id="80238-264">Add an InvokeProcess activity at hello end of hello new Sequence.</span></span>
      <span data-ttu-id="80238-265">Hello 인수를 사용 하 여이 활동 PowerShell.exe 호출에 의해 전달 된 hello 빌드 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-265">This activity calls PowerShell.exe with hello arguments passed in by hello Build Definition.</span></span>

      + <span data-ttu-id="80238-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span><span class="sxs-lookup"><span data-stu-id="80238-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span></span>
      + <span data-ttu-id="80238-267">DisplayName = Execute publish script</span><span class="sxs-lookup"><span data-stu-id="80238-267">DisplayName = Execute publish script</span></span>
      + <span data-ttu-id="80238-268">파일 이름 = "PowerShell" (hello 따옴표 포함)</span><span class="sxs-lookup"><span data-stu-id="80238-268">FileName = "PowerShell" (include hello quotes)</span></span>
      + <span data-ttu-id="80238-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span><span class="sxs-lookup"><span data-stu-id="80238-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span></span>
   7. <span data-ttu-id="80238-270">Hello에 **표준 출력 처리** 는 InvokeProcess의 텍스트 상자를 섹션을 hello textbox 값 too'data 설정 '.</span><span class="sxs-lookup"><span data-stu-id="80238-270">In hello **Handle Standard Output** section textbox of the InvokeProcess, set hello textbox value too'data'.</span></span> <span data-ttu-id="80238-271">변수 toostore hello 표준 출력 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="80238-271">This is a variable toostore hello standard output data.</span></span>
   8. <span data-ttu-id="80238-272">Hello 바로 아래에 된 WriteBuildMessage 활동 추가 **표준 출력 처리** 섹션.</span><span class="sxs-lookup"><span data-stu-id="80238-272">Add a WriteBuildMessage activity just below hello **Handle Standard Output** section.</span></span> <span data-ttu-id="80238-273">Hello 중요도 설정 = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' 및 hello 메시지 = 'data'.</span><span class="sxs-lookup"><span data-stu-id="80238-273">Set hello Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' and hello Message='data'.</span></span> <span data-ttu-id="80238-274">이렇게 하면 스크립트의 표준 출력 hello toohello 빌드 출력이 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80238-274">This ensures hello standard output of the script will get written toohello build output.</span></span>
   9. <span data-ttu-id="80238-275">Hello에 **오류 출력 처리** 는 InvokeProcess의 텍스트 상자를 섹션을 hello textbox 값 too'data 설정 '.</span><span class="sxs-lookup"><span data-stu-id="80238-275">In hello **Handle Error Output** section textbox of the InvokeProcess, set hello textbox value too'data'.</span></span> <span data-ttu-id="80238-276">변수 toostore hello 표준 오류 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="80238-276">This is a variable toostore hello standard error data.</span></span>
   10. <span data-ttu-id="80238-277">Hello 바로 아래에 WriteBuildError 활동 추가 **오류 출력 처리** 섹션.</span><span class="sxs-lookup"><span data-stu-id="80238-277">Add a WriteBuildError activity just below hello **Handle Error Output** section.</span></span> <span data-ttu-id="80238-278">Hello 메시지 설정 = 'data'.</span><span class="sxs-lookup"><span data-stu-id="80238-278">Set hello Message='data'.</span></span> <span data-ttu-id="80238-279">이렇게 하면 hello 스크립트의 표준 오류 hello toohello 빌드 오류 출력이 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80238-279">This ensures hello standard errors of hello script will get written toohello build error output.</span></span>
   11. <span data-ttu-id="80238-280">파란색 느낌표가 표시된 오류를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-280">Correct any errors, indicated by blue exclamation marks.</span></span> <span data-ttu-id="80238-281">위로 마우스를 가져가고 느낌표 tooget hello 오류에 대 한 힌트입니다.</span><span class="sxs-lookup"><span data-stu-id="80238-281">Hover over the exclamation marks tooget a hint about hello error.</span></span> <span data-ttu-id="80238-282">오류를 지우려면 hello 워크플로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-282">Save hello workflow to clear errors.</span></span>

   <span data-ttu-id="80238-283">hello hello의 최종 결과 게시 워크플로 활동 hello 디자이너에서 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80238-283">hello final result of hello publish workflow activities will look like this in hello designer:</span></span>

   ![워크플로 작업][5]

   <span data-ttu-id="80238-285">hello hello의 최종 결과 게시 워크플로 활동은 XAML에서 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80238-285">hello final result of hello publish workflow activities will look like this in XAML:</span></span>

       <If Condition="[Not String.IsNullOrEmpty(PublishScriptLocation)]" sap2010:WorkflowViewState.IdRef="If_1">
           <If.Then>
             <Sequence DisplayName="Start Publish" sap2010:WorkflowViewState.IdRef="Sequence_4">
               <Sequence.Variables>
                 <Variable x:TypeArguments="x:String" Name="SubscriptionDataFilePath" />
                 <Variable x:TypeArguments="x:String" Name="PublishScriptFilePath" />
               </Sequence.Variables>
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert publish script filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_1" Input="[PublishScriptLocation]" Result="[PublishScriptFilePath]" Workspace="[Workspace]" />
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert subscription filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_2" Input="[SubscriptionDataFileLocation]" Result="[SubscriptionDataFilePath]" Workspace="[Workspace]" />
               <mtbwa:InvokeProcess Arguments="[String.Format(&quot; -File &quot;&quot;{0}&quot;&quot; -serviceName {1}&#xD;&#xA;            -storageAccountName {2} -packageLocation &quot;&quot;{3}&quot;&quot;&#xD;&#xA;            -cloudConfigLocation &quot;&quot;{4}&quot;&quot; -subscriptionDataFile &quot;&quot;{5}&quot;&quot;&#xD;&#xA;            -selectedSubscription {6} -environment &quot;&quot;{7}&quot;&quot;&quot;,&#xD;&#xA;            PublishScriptFilePath, ServiceName, StorageAccountName,&#xD;&#xA;            PackageLocation, CloudConfigLocation,&#xD;&#xA;            SubscriptionDataFilePath, SubscriptionName, Environment)]" DisplayName="'Execute Publish Script'" FileName="[PowerShell]" sap2010:WorkflowViewState.IdRef="InvokeProcess_1">
                 <mtbwa:InvokeProcess.ErrorDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildError Message="{x:Null}" sap2010:WorkflowViewState.IdRef="WriteBuildError_1" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.ErrorDataReceived>
                 <mtbwa:InvokeProcess.OutputDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildMessage sap2010:WorkflowViewState.IdRef="WriteBuildMessage_2" Importance="[Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High]" Message="[data]" mva:VisualBasic.Settings="Assembly references and imported namespaces serialized as XML namespaces" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.OutputDataReceived>
               </mtbwa:InvokeProcess>
             </Sequence>
           </If.Then>
         </If>
       </Sequence>
8. <span data-ttu-id="80238-286">Hello 빌드 프로세스 템플릿 워크플로 및 체크 인이 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-286">Save hello build process template workflow and Check In this file.</span></span>
9. <span data-ttu-id="80238-287">Hello 빌드 정의 편집 (닫으려면 이미 열려 있으면) 및 선택 hello **새로** hello hello 프로세스 템플릿 목록에 새 템플릿이 아직 표시 되지 않으면 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="80238-287">Edit hello build definition (close it if it is already open), and select hello **New** button if you do not yet see hello new template in hello list of Process Templates.</span></span>
10. <span data-ttu-id="80238-288">다음과 같이 hello 기타 섹션에서에서 hello 매개 변수 속성 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-288">Set hello parameter property values in hello Misc section as follows:</span></span>

    1. <span data-ttu-id="80238-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *이 값의 파생 위치: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span><span class="sxs-lookup"><span data-stu-id="80238-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *This value is derived from: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span></span>
    2. <span data-ttu-id="80238-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *이 값의 파생 위치: ($PublishDir)($ProjectName).cspkg*</span><span class="sxs-lookup"><span data-stu-id="80238-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *This value is derived from: ($PublishDir)($ProjectName).cspkg*</span></span>
    3. <span data-ttu-id="80238-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span><span class="sxs-lookup"><span data-stu-id="80238-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span></span>
    4. <span data-ttu-id="80238-292">ServiceName = 'mycloudservicename' *hello 적절 한 클라우드 서비스 이름 사용 여기*</span><span class="sxs-lookup"><span data-stu-id="80238-292">ServiceName = 'mycloudservicename' *Use hello appropriate cloud service name here*</span></span>
    5. <span data-ttu-id="80238-293">Environment = 'Staging'</span><span class="sxs-lookup"><span data-stu-id="80238-293">Environment = 'Staging'</span></span>
    6. <span data-ttu-id="80238-294">StorageAccountName 'mystorageaccountname' = *사용 하 여 hello 적절 한 저장소 계정 이름을 여기*</span><span class="sxs-lookup"><span data-stu-id="80238-294">StorageAccountName = 'mystorageaccountname' *Use hello appropriate storage account name here*</span></span>
    7. <span data-ttu-id="80238-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span><span class="sxs-lookup"><span data-stu-id="80238-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span></span>
    8. <span data-ttu-id="80238-296">SubscriptionName = 'default'</span><span class="sxs-lookup"><span data-stu-id="80238-296">SubscriptionName = 'default'</span></span>

    ![매개 변수 속성 값][6]
11. <span data-ttu-id="80238-298">Hello 변경 toohello 빌드 정의 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-298">Save hello changes toohello Build Definition.</span></span>
12. <span data-ttu-id="80238-299">패키지 빌드 hello와 게시를 모두 빌드 tooexecute 큐에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="80238-299">Queue a Build tooexecute both hello package build and publish.</span></span> <span data-ttu-id="80238-300">TooContinuous 통합을 설정 하는 트리거를 사용 하도록 설정한 경우 모든 체크 인에이 동작을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-300">If you have a trigger set tooContinuous Integration, you will execute this behavior on every check-in.</span></span>

### <a name="publishcloudserviceps1-script-template"></a><span data-ttu-id="80238-301">PublishCloudService.ps1 스크립트 템플릿</span><span class="sxs-lookup"><span data-stu-id="80238-301">PublishCloudService.ps1 script template</span></span>
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy too$servicename",
        $timeStampFormat = "g",
        $alwaysDeleteExistingDeployments = 1,
        $enableDeploymentUpgrade = 1,
        $selectedsubscription = "default",
        $subscriptionDataFile = ""
     )


function Publish()
{
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot -ErrorVariable a -ErrorAction silentlycontinue
    if ($a[0] -ne $null)
    {
        Write-Output "$(Get-Date -f $timeStampFormat) - No deployment is detected. Creating a new deployment. "
    }
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according too$alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
    if ($deployment.Name -ne $null)
    {
        switch ($alwaysDeleteExistingDeployments)
        {
            1
            {
                switch ($enableDeploymentUpgrade)
                {
                    1  #Update deployment inplace (usually faster, cheaper, won't destroy VIP)
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Upgrading deployment."
                        UpgradeDeployment
                    }
                    0  #Delete then create new deployment
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Deleting deployment."
                        DeleteDeployment
                        CreateNewDeployment

                    }
                } # switch ($enableDeploymentUpgrade)
            }
            0
            {
                Write-Output "$(Get-Date -f $timeStampFormat) - ERROR: Deployment exists in $servicename.  Script execution cancelled."
                exit
            }
        } #switch ($alwaysDeleteExistingDeployments)
    } else {
            CreateNewDeployment
    }
}

function CreateNewDeployment()
{
    write-progress -id 3 -activity "Creating New Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: In progress"

    $opstat = New-AzureDeployment -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Creating New Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: Complete, Deployment ID: $completeDeploymentID"

    StartInstances
}

function UpgradeDeployment()
{
    write-progress -id 3 -activity "Upgrading Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: In progress"

    # perform Update-Deployment
    $setdeployment = Set-AzureDeployment -Upgrade -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName -Force

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Upgrading Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: Complete, Deployment ID: $completeDeploymentID"
}

function DeleteDeployment()
{

    write-progress -id 2 -activity "Deleting Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: In progress"

    #WARNING - always deletes with force
    $removeDeployment = Remove-AzureDeployment -Slot $slot -ServiceName $serviceName -Force

    write-progress -id 2 -activity "Deleting Deployment: Complete" -completed -Status $removeDeployment
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: Complete"

}

function StartInstances()
{
    write-progress -id 4 -activity "Starting Instances" -status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: In progress"

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $runstatus = $deployment.Status

    if ($runstatus -ne 'Running')
    {
        $run = Set-AzureDeployment -Slot $slot -ServiceName $serviceName -Status Running
    }
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $oldStatusStr = @("") * $deployment.RoleInstanceList.Count

    while (-not(AllInstancesRunning($deployment.RoleInstanceList)))
    {
        $i = 1
        foreach ($roleInstance in $deployment.RoleInstanceList)
        {
            $instanceName = $roleInstance.InstanceName
            $instanceStatus = $roleInstance.InstanceStatus

            if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
            {
                $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
                Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
            }

            write-progress -id (4 + $i) -activity "Starting Instance '$instanceName'" -status "$instanceStatus"
            $i = $i + 1
        }

        sleep -Seconds 1

        $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    }

    $i = 1
    foreach ($roleInstance in $deployment.RoleInstanceList)
    {
        $instanceName = $roleInstance.InstanceName
        $instanceStatus = $roleInstance.InstanceStatus

        if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
        {
            $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
            Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
        }

        $i = $i + 1
    }

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $opstat = $deployment.Status

    write-progress -id 4 -activity "Starting Instances" -completed -status $opstat
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: $opstat"
}

function AllInstancesRunning($roleInstanceList)
{
    foreach ($roleInstance in $roleInstanceList)
    {
        if ($roleInstance.InstanceStatus -ne "ReadyRole")
        {
            return $false
        }
    }

    return $true
}

#configure powershell with Azure 1.7 modules
Import-Module Azure

#configure powershell with publishsettings for your subscription
$pubsettings = $subscriptionDataFile
Import-AzurePublishSettingsFile $pubsettings
Set-AzureSubscription -CurrentStorageAccountName $storageAccountName -SubscriptionName $selectedsubscription
Select-AzureSubscription $selectedsubscription

#set remaining environment variables for Azure cmdlets
$subscription = Get-AzureSubscription $selectedsubscription
$subscriptionname = $subscription.subscriptionname
$subscriptionid = $subscription.subscriptionid
$slot = $environment

#main driver - publish & write progress tooactivity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a><span data-ttu-id="80238-302">다음 단계</span><span class="sxs-lookup"><span data-stu-id="80238-302">Next steps</span></span>
<span data-ttu-id="80238-303">참조 지속적인 업데이트를 사용 하 여 tooenable 원격 디버깅 [toopublish tooAzure 지속적인 업데이트를 사용 하는 경우 원격 디버깅을 활성화](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="80238-303">tooenable remote debugging when using continuous delivery, see [Enable remote debugging when using continuous delivery toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span></span>

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[hello .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
