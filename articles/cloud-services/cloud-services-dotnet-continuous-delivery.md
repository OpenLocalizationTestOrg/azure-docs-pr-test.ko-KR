---
title: "Azure의 TFS를 사용한 Cloud Services의 지속적인 전송 | Microsoft Docs"
description: "Azure 클라우드 앱에 대해 지속적인 전송을 설정하는 방법에 대해 알아봅니다. MSBuild 명령줄 문 및 PowerShell 스크립트에 대한 코드 샘플도 제공됩니다."
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
ms.openlocfilehash: 0979722b9ec715e91825c7aba74657451df6e83f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a><span data-ttu-id="49b76-104">Azure Cloud Services의 지속적인 전송</span><span class="sxs-lookup"><span data-stu-id="49b76-104">Continuous Delivery for Cloud Services in Azure</span></span>
<span data-ttu-id="49b76-105">이 문서에서 설명하는 프로세스에서는 Azure 클라우드 앱에 대해 지속적인 전송을 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-105">The process described in this article shows you how to set up continuous delivery for Azure cloud apps.</span></span> <span data-ttu-id="49b76-106">이 프로세스를 통해 각 코드 체크 인 이후에 자동으로 패키지를 만들어 Azure에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-106">This process enables you to automatically create packages and deploy the package to Azure after every code check-in.</span></span> <span data-ttu-id="49b76-107">이 문서에서 설명하는 패키지 빌드 프로세스는 Visual Studio의 **패키지** 명령과 동일하며 게시 단계는 Visual Studio의 **게시** 명령과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-107">The package build process described in this article is equivalent to the **Package** command in Visual Studio, and the publishing steps are equivalent to the **Publish** command in Visual Studio.</span></span>
<span data-ttu-id="49b76-108">이 문서에서는 MSBuild 명령줄 문과 Windows PowerShell 스크립트를 사용하여 빌드 서버를 만드는 데 사용하는 메서드에 대해 설명하고, MSBuild 명령 및 PowerShell 스크립트를 사용하도록 선택적으로 Visual Studio Team Foundation Server - 팀 빌드 정의를 구성하는 방법도 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-108">The article covers the methods you would use to create a build server with MSBuild command-line statements and Windows PowerShell scripts, and it also demonstrates how to optionally configure Visual Studio Team Foundation Server - Team Build definitions to use the MSBuild commands and PowerShell scripts.</span></span> <span data-ttu-id="49b76-109">이 프로세스는 빌드 환경 및 Azure 대상 환경에 맞게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-109">The process is customizable for your build environment and Azure target environments.</span></span>

<span data-ttu-id="49b76-110">또한 Azure에서 호스트되는 TFS 버전인 Visual Studio Team Services를 사용하면 이 작업을 보다 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-110">You can also use Visual Studio Team Services, a version of TFS that is hosted in Azure, to do this more easily.</span></span> 

<span data-ttu-id="49b76-111">시작하기 전에 Visual Studio에서 응용 프로그램을 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-111">Before you start, you should publish your application from Visual Studio.</span></span>
<span data-ttu-id="49b76-112">그러면 게시 프로세스를 자동화하려고 할 때 모든 리소스가 사용 가능하며 초기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-112">This will ensure that all the resources are available and initialized when you attempt to automate the publication process.</span></span>

## <a name="1-configure-the-build-server"></a><span data-ttu-id="49b76-113">1: 빌드 서버 구성</span><span class="sxs-lookup"><span data-stu-id="49b76-113">1: Configure the Build Server</span></span>
<span data-ttu-id="49b76-114">MSBuild를 사용하여 Azure 패키지를 만들려면 먼저 필요한 소프트웨어 및 도구를 빌드 서버에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-114">Before you can create an Azure package by using MSBuild, you must install the required software and tools on the build server.</span></span>

<span data-ttu-id="49b76-115">Visual Studio는 빌드 서버에 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-115">Visual Studio is not required to be installed on the build server.</span></span> <span data-ttu-id="49b76-116">Team Foundation Build 서비스를 사용하여 빌드 서버를 관리하려면 [Team Foundation Build Service][Team Foundation Build Service](영문) 설명서의 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="49b76-116">If you want to use Team Foundation Build Service to manage your build server, follow the instructions in the [Team Foundation Build Service][Team Foundation Build Service] documentation.</span></span>

1. <span data-ttu-id="49b76-117">빌드 서버에 MSBuild가 포함된 [.NET Framework 4.5.2][.NET Framework 4.5.2]를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-117">On the build server, install the [.NET Framework 4.5.2][.NET Framework 4.5.2], which includes MSBuild.</span></span>
2. <span data-ttu-id="49b76-118">최신 [.NET용 Azure 작성 도구](https://azure.microsoft.com/develop/net/)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-118">Install the latest [Azure Authoring Tools for .NET](https://azure.microsoft.com/develop/net/).</span></span>
3. <span data-ttu-id="49b76-119">[.NET용 Azure 라이브러리](http://go.microsoft.com/fwlink/?LinkId=623519)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-119">Install the [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span></span>
4. <span data-ttu-id="49b76-120">Visual Studio 설치에서 Microsoft.WebApplication.targets 파일을 빌드 서버에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-120">Copy the Microsoft.WebApplication.targets file from a Visual Studio installation to the build server.</span></span>

   <span data-ttu-id="49b76-121">Visual Studio가 설치된 컴퓨터에서 이 파일은 디렉터리 C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-121">On a computer with Visual Studio installed, this file is located in the directory C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span></span> <span data-ttu-id="49b76-122">빌드 서버의 동일한 디렉터리에 해당 파일을 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-122">You should copy it to the same directory on the build server.</span></span>
5. <span data-ttu-id="49b76-123">[Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-123">Install the [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span></span>

## <a name="2-build-a-package-using-msbuild-commands"></a><span data-ttu-id="49b76-124">2: MSBuild 명령을 사용하여 패키지 빌드</span><span class="sxs-lookup"><span data-stu-id="49b76-124">2: Build a Package using MSBuild Commands</span></span>
<span data-ttu-id="49b76-125">이 섹션에서는 Azure 패키지를 빌드하는 MSBuild 명령 구성 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-125">This section describes how to construct an MSBuild command that builds an Azure package.</span></span> <span data-ttu-id="49b76-126">빌드 서버에서 이 단계를 실행하여 모든 항목이 제대로 구성되어 있고 MSBuild 명령이 원하는 대로 수행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-126">Run this step on the build server to verify that everything is configured correctly and that the MSBuild command does what you want it to do.</span></span> <span data-ttu-id="49b76-127">다음 섹션에 설명된 대로 이 명령줄을 빌드 서버의 기존 빌드 스크립트에 추가하거나 TFS 빌드 정의에서 명령줄을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-127">You can either add this command line to existing build scripts on the build server, or you can use the command line in a TFS Build Definition, as described in the next section.</span></span> <span data-ttu-id="49b76-128">명령줄 매개 변수 및 MSBuild에 대한 자세한 내용은 [MSBuild 명령줄 참조](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49b76-128">For more information about command-line parameters and MSBuild, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>

1. <span data-ttu-id="49b76-129">Visual Studio가 빌드 서버에 설치되어 있는 경우 Windows의 **Visual Studio Tools** 폴더에서 **Visual Studio 명령 프롬프트**를 찾아서 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-129">If Visual Studio is installed on the build server, locate and choose **Visual Studio Command Prompt** in the **Visual Studio Tools** folder in Windows.</span></span>

   <span data-ttu-id="49b76-130">Visual Studio가 빌드 서버에 설치되어 있지 않으면 명령 프롬프트를 열고 해당 경로에서 MSBuild.exe에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-130">If Visual Studio is not installed on the build server, open a command prompt and make sure that MSBuild.exe is accessible on the path.</span></span> <span data-ttu-id="49b76-131">MSBuild는 .NET Framework와 함께 %WINDIR%\\Microsoft.NET\\Framework\\*Version* 경로에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-131">MSBuild is installed with the .NET Framework in the path %WINDIR%\\Microsoft.NET\\Framework\\*Version*.</span></span> <span data-ttu-id="49b76-132">예를 들어 .NET Framework 4를 설치한 경우 PATH 환경 변수에 MSBuild.exe를 추가하려면 명령 프롬프트에서 다음 명령을 입력하세요.</span><span class="sxs-lookup"><span data-stu-id="49b76-132">For example, to add MSBuild.exe to the PATH environment variable when you have .NET Framework 4 installed, type the following command at the command prompt:</span></span>

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. <span data-ttu-id="49b76-133">명령 프롬프트에서 빌드할 Azure 프로젝트 파일이 포함된 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-133">At the command prompt, navigate to the folder containing the Azure project file that you want to build.</span></span>
3. <span data-ttu-id="49b76-134">다음 예제와 /target:Publish 옵션을 사용하여 MSBuild를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-134">Run MSBuild with the /target:Publish option as in the following example:</span></span>

       MSBuild /target:Publish

   <span data-ttu-id="49b76-135">이 옵션은 /t:Publish로 간략하게 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-135">This option can be abbreviated as /t:Publish.</span></span> <span data-ttu-id="49b76-136">MSBuild의 /t:Publish 옵션을 Azure SDK를 설치한 경우 Visual Studio에서 제공되는 게시 명령과 혼동해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-136">The /t:Publish option in MSBuild should not be confused with the Publish commands available in Visual Studio when you have the Azure SDK installed.</span></span> <span data-ttu-id="49b76-137">/t:Publish 옵션은 Azure 패키지를 빌드만 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-137">The /t:Publish option only builds the Azure packages.</span></span> <span data-ttu-id="49b76-138">Visual Studio의 게시 명령처럼 패키지를 배포하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-138">It does not deploy the packages as the Publish commands in Visual Studio do.</span></span>

   <span data-ttu-id="49b76-139">선택적으로 프로젝트 이름을 MSBuild 매개 변수로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-139">Optionally, you can specify the project name as an MSBuild parameter.</span></span> <span data-ttu-id="49b76-140">지정하지 않으면 현재 디렉터리가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-140">If not specified, the current directory is used.</span></span> <span data-ttu-id="49b76-141">MSBuild 명령줄 옵션에 대한 자세한 내용은 [MSBuild 명령줄 참조](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49b76-141">For more information about MSBuild command line options, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>
4. <span data-ttu-id="49b76-142">출력을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-142">Locate the output.</span></span> <span data-ttu-id="49b76-143">기본적으로 이 명령은 프로젝트의 루트 폴더를 기준으로 디렉터리를 만듭니다(예: *ProjectDir*\\bin\\*Configuration*\\app.publish\\).</span><span class="sxs-lookup"><span data-stu-id="49b76-143">By default, this command creates a directory in relation to the root folder for the project, such as *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span></span> <span data-ttu-id="49b76-144">Azure 프로젝트를 빌드하면 패키지 파일 자체와 함께 제공되는 구성 파일의 두 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-144">When you build an Azure project, you generate two files, the package file itself and the accompanying configuration file:</span></span>

   * <span data-ttu-id="49b76-145">Project.cspkg</span><span class="sxs-lookup"><span data-stu-id="49b76-145">Project.cspkg</span></span>
   * <span data-ttu-id="49b76-146">ServiceConfiguration.*TargetProfile*.cscfg</span><span class="sxs-lookup"><span data-stu-id="49b76-146">ServiceConfiguration.*TargetProfile*.cscfg</span></span>

   <span data-ttu-id="49b76-147">기본적으로 각 Azure 프로젝트에는 로컬(디버깅) 빌드용 서비스 구성 파일(.cscfg 파일) 하나와 클라우드(스테이징 또는 프로덕션) 빌드용 서비스 구성 파일 하나가 포함되지만 필요에 따라 서비스 구성 파일을 추가하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-147">By default, each Azure project includes one service configuration file (.cscfg file) for local (debugging) builds and another for cloud (staging or production) builds, but you can add or remove service configuration files as needed.</span></span> <span data-ttu-id="49b76-148">Visual Studio 내에서 패키지를 빌드하면 패키지와 함께 포함할 서비스 구성 파일을 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-148">When you build a package within Visual Studio, you will be asked which service configuration file to include alongside the package.</span></span>
5. <span data-ttu-id="49b76-149">서비스 구성 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-149">Specify the service configuration file.</span></span> <span data-ttu-id="49b76-150">MSBuild를 사용하여 패키지를 빌드하면 로컬 서비스 구성 파일이 기본적으로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-150">When you build a package by using MSBuild, the local service configuration file is included by default.</span></span> <span data-ttu-id="49b76-151">다른 서비스 구성 파일을 포함하려면 다음 예제와 같이 MSBuild 명령의 TargetProfile 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-151">To include a different service configuration file, set the TargetProfile property of the MSBuild command, as in the following example:</span></span>

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. <span data-ttu-id="49b76-152">출력의 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-152">Specify the location for the output.</span></span> <span data-ttu-id="49b76-153">다음 예제와 같이 뒤에 오는 백슬래시 구분 기호를 포함하는 /p:PublishDir=*Directory*\\ 옵션을 사용하여 경로를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-153">Set the path by using the /p:PublishDir=*Directory*\\ option, including the trailing backslash separator, as in the following example:</span></span>

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   <span data-ttu-id="49b76-154">적절한 MSBuild 명령줄을 구성하고 테스트하여 프로젝트를 빌드하고 Azure 패키지로 결합했으면 이 명령줄을 빌드 스크립트에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-154">Once you've constructed and tested an appropriate MSBuild command line to build your projects and combine them into an Azure package, you can add this command line to your build scripts.</span></span> <span data-ttu-id="49b76-155">빌드 서버에서 사용자 지정 스크립트를 사용하는 경우 이 프로세스는 사용자 지정 빌드 프로세스의 세부 사항에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-155">If your build server uses custom scripts, this process will depend on the specifics of your custom build process.</span></span> <span data-ttu-id="49b76-156">TFS를 빌드 환경으로 사용하는 경우 다음 단계의 지침에 따라 Azure 패키지 빌드를 빌드 프로세스에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-156">If you are using TFS as a build environment, then you can follow the instructions in the next step to add the Azure package build to your build process.</span></span>

## <a name="3-build-a-package-using-tfs-team-build"></a><span data-ttu-id="49b76-157">3: TFS 팀 빌드를 사용하여 패키지 빌드</span><span class="sxs-lookup"><span data-stu-id="49b76-157">3: Build a Package using TFS Team Build</span></span>
<span data-ttu-id="49b76-158">TFS(Team Foundation Server)를 빌드 컨트롤러로 설정하고 빌드 서버를 TFS 빌드 컴퓨터로 설정한 경우 Azure 패키지에 대해 자동화된 빌드를 선택적으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-158">If you have Team Foundation Server (TFS) set up as a build controller and the build server set up as a TFS build machine, then you can optionally set up an automated build for your Azure package.</span></span> <span data-ttu-id="49b76-159">Team Foundation Server를 빌드 시스템으로 설정하고 사용하는 방법에 대한 자세한 내용은 [빌드 시스템 확장][Scale out your build system]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49b76-159">For information on how to set up and use Team Foundation server as a build system, see [Scale out your build system][Scale out your build system].</span></span> <span data-ttu-id="49b76-160">특히 다음 절차에서는 빌드 서버를 [빌드 서버 배포 및 구성][Deploy and configure a build server]에 설명된 대로 구성했고, 팀 프로젝트를 만들고 팀 프로젝트에 클라우드 서비스를 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-160">In particular, the following procedure assumes that you have configured your build server as described in [Deploy and configure a build server][Deploy and configure a build server], and that you have created a team project, created a cloud service project in the team project.</span></span>

<span data-ttu-id="49b76-161">Azure 패키지를 빌드하도록 TFS를 구성하려면 다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="49b76-161">To configure TFS to build Azure packages, perform the following steps:</span></span>

1. <span data-ttu-id="49b76-162">개발 컴퓨터의 Visual Studio 보기 메뉴에서 **팀 Explorer**를 선택하거나 Ctrl+\\, Ctrl+M을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-162">In Visual Studio on your development computer, on the View menu, choose **Team Explorer**, or choose Ctrl+\\, Ctrl+M.</span></span> <span data-ttu-id="49b76-163">팀 Explorer 창에서 **빌드** 노드를 확장하거나 **빌드** 페이지를 선택하고 **새 빌드 정의**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-163">In the Team Explorer window, expand the **Builds** node or choose the **Builds** page, and choose **New Build Definition**.</span></span>

   ![새 빌드 정의 옵션][0]
2. <span data-ttu-id="49b76-165">**트리거** 탭을 선택하고 패키지를 빌드하려는 경우에 원하는 조건을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-165">Choose the **Trigger** tab, and specify the desired conditions for when you want the package to be built.</span></span> <span data-ttu-id="49b76-166">예를 들어 소스 제어 체크 인이 발생할 때마다 패키지를 빌드하려면 **연속 통합**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-166">For example, specify **Continuous Integration** to build the package whenever a source control check-in occurs.</span></span>
3. <span data-ttu-id="49b76-167">**소스 설정** 탭을 선택하고 프로젝트 폴더가 **소스 제어 폴더** 열에 나열되고 상태가 **활성**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-167">Choose the **Source Settings** tab, and make sure your project folder is listed in the **Source Control Folder** column, and the status is **Active**.</span></span>
4. <span data-ttu-id="49b76-168">**빌드 기본값** 탭을 선택하고 빌드 컨트롤러에서 빌드 서버의 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-168">Choose the **Build Defaults** tab, and under Build controller, verify the name of the build server.</span></span>  <span data-ttu-id="49b76-169">또한 **다음 저장 폴더에 빌드 출력 복사** 옵션을 선택하고 원하는 저장 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-169">Also, choose the option **Copy build output to the following drop folder** and specify the desired drop location.</span></span>
5. <span data-ttu-id="49b76-170">**프로세스** 탭을 선택합니다. 프로세스 탭에서 기본 템플릿을 선택하고 **빌드**에서 프로젝트를 선택한 다음(선택되지 않은 경우) 표의 **빌드** 섹션에서 **고급** 섹션을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-170">Choose the **Process** tab. On the Process tab, choose the default template, under **Build**, choose the project if it is not already selected, and expand the **Advanced** section in the **Build** section of the grid.</span></span>
6. <span data-ttu-id="49b76-171">**MSBuild Arguments**를 선택하고 위의 2단계에서 설명한 대로 적절한 MSBuild 명령줄 인수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-171">Choose **MSBuild Arguments**, and set the appropriate MSBuild command line arguments as described in Step 2 above.</span></span> <span data-ttu-id="49b76-172">예를 들어 패키지를 빌드하고 패키지 파일을 \\\\myserver\\drops\\ 위치에 복사하려면 **/t:Publish /p:PublishDir=\\\\myserver\\drops\\**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-172">For example, enter **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** to build a package and copy the package files to the location \\\\myserver\\drops\\:</span></span>

   ![MSBuild Arguments][2]

   > [!NOTE]
   > <span data-ttu-id="49b76-174">파일을 공용 공유 위치에 복사하면 개발 컴퓨터에서 패키지를 수동으로 배포하기가 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-174">Copying the files to a public share makes it easier to manually deploy the packages from your development computer.</span></span>
7. <span data-ttu-id="49b76-175">프로젝트의 변경 내용을 체크 인하여 빌드 단계의 성공 여부를 테스트하거나 새 빌드를 큐에 대기시킵니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-175">Test the success of your build step by checking in a change to your project, or queue up a new build.</span></span> <span data-ttu-id="49b76-176">새 빌드를 큐에 대기시키려면 팀 Explorer에서 **모든 빌드 정의**를 마우스 오른쪽 단추로 클릭한 다음 **새 빌드 큐 대기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-176">To queue up a new build, in the Team Explorer, right-click **All Build Definitions,** and then choose **Queue New Build**.</span></span>

## <a name="4-publish-a-package-using-a-powershell-script"></a><span data-ttu-id="49b76-177">4: PowerShell 스크립트를 사용하여 패키지 게시</span><span class="sxs-lookup"><span data-stu-id="49b76-177">4: Publish a Package using a PowerShell Script</span></span>
<span data-ttu-id="49b76-178">이 섹션에서는 선택적 매개 변수를 사용하여 클라우드 앱 패키지 출력을 Azure에 게시할 Windows PowerShell 스크립트를 구성하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-178">This section describes how to construct a Windows PowerShell script that will publish the Cloud app package output to Azure using optional parameters.</span></span> <span data-ttu-id="49b76-179">이 스크립트는 사용자 지정 빌드 자동화의 빌드 단계 후에 호출할 수 있으며,</span><span class="sxs-lookup"><span data-stu-id="49b76-179">This script can be called after the build step in your custom build automation.</span></span> <span data-ttu-id="49b76-180">Visual Studio TFS 팀 빌드의 프로세스 템플릿 워크플로 작업에서 호출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-180">It can also be called from Process Template workflow activities in Visual Studio TFS Team Build.</span></span>

1. <span data-ttu-id="49b76-181">[Azure PowerShell cmdlet][Azure PowerShell cmdlets](v0.6.1 이상)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-181">Install the [Azure PowerShell cmdlets][Azure PowerShell cmdlets] (v0.6.1 or higher).</span></span>
   <span data-ttu-id="49b76-182">cmdlet 설치 단계 중 스냅인으로 설치하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-182">During the cmdlet setup phase, choose to install as a snap-in.</span></span> <span data-ttu-id="49b76-183">이전 버전의 번호는 2.x.x로 지정되었지만 공식적으로 지원되는 이 버전이 CodePlex를 통해 제공된 이전 버전을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-183">Note that this officially supported version replaces the older version offered through CodePlex, although the previous versions were numbered 2.x.x.</span></span>
2. <span data-ttu-id="49b76-184">시작 메뉴나 시작 페이지를 사용하여 Azure PowerShell을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-184">Start Azure PowerShell using the Start menu or Start page.</span></span> <span data-ttu-id="49b76-185">이런 방식으로 시작하면 Azure PowerShell cmdlet이 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-185">If you start in this way, the Azure PowerShell cmdlets will be loaded.</span></span>
3. <span data-ttu-id="49b76-186">PowerShell 프롬프트에서 부분 명령 `Get-Azure`를 입력한 다음 문 완성에 대한 Tab 키를 눌러 PowerShell cmdlet가 로드되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-186">At the PowerShell prompt, verify that the PowerShell cmdlets are loaded by entering the partial command `Get-Azure` and then pressing the Tab key for statement completion.</span></span>

   <span data-ttu-id="49b76-187">Tab 키를 반복해서 누르면 다양한 Azure PowerShell 명령이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-187">If you press the Tab key repeatedly, you should see various Azure PowerShell commands.</span></span>
4. <span data-ttu-id="49b76-188">.publishsettings 파일에서 구독 정보를 가져와 Azure 구독에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-188">Verify that you can connect to your Azure subscription by importing your subscription information from the .publishsettings file.</span></span>

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   <span data-ttu-id="49b76-189">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-189">Then enter the command</span></span>

   `Get-AzureSubscription`

   <span data-ttu-id="49b76-190">그러면 구독에 대한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-190">This shows information about your subscription.</span></span> <span data-ttu-id="49b76-191">모든 정보가 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-191">Verify that everything is correct.</span></span>
5. <span data-ttu-id="49b76-192">이 문서의 끝에 제공된 스크립트 템플릿을 c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**로 스크립트 폴더에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-192">Save the script template provided at the end of this article to your scripts folder as c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span></span>
6. <span data-ttu-id="49b76-193">스크립트의 매개 변수 섹션을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-193">Review the parameters section of the script.</span></span> <span data-ttu-id="49b76-194">기본값을 추가하거나 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-194">Add or modify any default values.</span></span> <span data-ttu-id="49b76-195">이러한 값은 명시적 매개 변수를 전달하여 언제든지 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-195">These values can always be overridden by passing in explicit parameters.</span></span>
7. <span data-ttu-id="49b76-196">게시 스크립트에서 대상으로 지정할 수 있는 유효한 클라우드 서비스 및 저장소 계정이 구독에 만들어져 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-196">Ensure there are valid cloud service and storage accounts created in your subscription that can be targeted by the publish script.</span></span> <span data-ttu-id="49b76-197">저장소 계정(Blob Storage)은 배포를 만드는 동안 배포 패키지 및 구성 파일을 업로드하고 일시적으로 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-197">The storage account (blob storage) will be used to upload and temporarily store the deployment package and config file while the deployment is being created.</span></span>

   * <span data-ttu-id="49b76-198">새 클라우드 서비스를 만들려면 다음 스크립트를 호출하거나 [Azure Portal](https://portal.azure.com)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-198">To create a new cloud service, you can call this script or use the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="49b76-199">클라우드 서비스 이름은 정규화된 도메인 이름의 접두사로 사용되므로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-199">The cloud service name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span>

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * <span data-ttu-id="49b76-200">새 저장소 계정을 만들려면 다음 스크립트를 호출하거나 [Azure Portal](https://portal.azure.com)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-200">To create a new storage account, you can call this script or use the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="49b76-201">저장소 계정 이름은 정규화된 도메인 이름의 접두사로 사용되므로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-201">The storage account name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span> <span data-ttu-id="49b76-202">클라우드 서비스와 같은 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-202">You can try using the same name as the cloud service.</span></span>

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. <span data-ttu-id="49b76-203">Azure PowerShell에서 직접 스크립트를 호출하거나 패키지 빌드 후 수행되도록 호스트 빌드 자동화에 이 스크립트를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-203">Call the script directly from Azure PowerShell, or wire up this script to your host build automation to occur after the package build.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="49b76-204">스크립트는 기존 배포가 검색될 경우 기본적으로 항상 삭제하거나 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-204">The script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="49b76-205">사용자에게 확인할 수 없는 경우 자동화에서 지속적인 전송을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-205">This is necessary to enable continuous delivery from automation where no user prompting is possible.</span></span>
   >
   >

   <span data-ttu-id="49b76-206">**예제 시나리오 1:** 서비스의 스테이징 환경에 지속적인 배포:</span><span class="sxs-lookup"><span data-stu-id="49b76-206">**Example scenario 1:** continuous deployment to the staging environment of a service:</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="49b76-207">그런 다음 일반적으로 테스트 실행 검증 및 VIP 교환이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-207">This is typically followed up by test run verification and a VIP swap.</span></span> <span data-ttu-id="49b76-208">VIP 교환은 [Azure Portal](https://portal.azure.com)이나 Move-Deployment cmdlet을 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-208">The VIP swap can be done via the [Azure portal](https://portal.azure.com) or by using the Move-Deployment cmdlet.</span></span>

   <span data-ttu-id="49b76-209">**예제 시나리오 2:** 전용 테스트 서비스의 프로덕션 환경에 지속적인 배포</span><span class="sxs-lookup"><span data-stu-id="49b76-209">**Example scenario 2:** continuous deployment to the production environment of a dedicated test service</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="49b76-210">**원격 데스크톱:**</span><span class="sxs-lookup"><span data-stu-id="49b76-210">**Remote Desktop:**</span></span>

   <span data-ttu-id="49b76-211">Azure 프로젝트에서 원격 데스크톱을 사용하는 경우 일회성 단계를 추가로 수행하여 이 스크립트의 대상이 되는 모든 Cloud Services에 올바른 클라우드 서비스 인증서가 업로드되었는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-211">If Remote Desktop is enabled in your Azure project you will need to perform additional one-time steps to ensure the correct Cloud Service Certificate is uploaded to all cloud services targeted by this script.</span></span>

   <span data-ttu-id="49b76-212">역할에 필요한 인증서 지문 값을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-212">Locate the certificate thumbprint values expected by your roles.</span></span> <span data-ttu-id="49b76-213">지문 값은 클라우드 config 파일(예: ServiceConfiguration.Cloud.cscfg)의 Certificates 섹션에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-213">The thumbprint values are visible in the Certificates section of the cloud config file (i.e. ServiceConfiguration.Cloud.cscfg).</span></span> <span data-ttu-id="49b76-214">옵션 표시를 선택하고 선택한 인증서를 보면 Visual Studio의 원격 데스크톱 구성 대화 상자에도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-214">It is also visible in the Remote Desktop Configuration dialog in Visual Studio when you Show Options and view the selected certificate.</span></span>

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   <span data-ttu-id="49b76-215">다음 cmdlet 스크립트를 사용하여 원격 데스크톱 인증서를 일회성 설치 단계로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-215">Upload Remote Desktop certificates as a one-time setup step using the following cmdlet script:</span></span>

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   <span data-ttu-id="49b76-216">예:</span><span class="sxs-lookup"><span data-stu-id="49b76-216">For example:</span></span>

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   <span data-ttu-id="49b76-217">또는 개인 키로 인증서 파일 PFX를 내보내고 [Azure Portal](https://portal.azure.com)을 사용하여 각 대상 클라우드 서비스에 인증서를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-217">Alternatively you can export the certificate file PFX with private key and upload certificates to each target cloud service using the [Azure portal](https://portal.azure.com).</span></span>

   <!---
   Fixing broken links for Azure content migration from ACOM to DOCS. I'm unable to find a replacement links, so I'm commenting out this reference for now. The author can investigate in the future. "Read the following article to learn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   <span data-ttu-id="49b76-218">**배포 업그레이드 및 배포 삭제 -\> 새 배포**</span><span class="sxs-lookup"><span data-stu-id="49b76-218">**Upgrade Deployment vs. Delete Deployment -\> New Deployment**</span></span>

   <span data-ttu-id="49b76-219">매개 변수가 전달되지 않거나 값 1이 명시적으로 전달되는 경우 스크립트는 기본적으로 배포 업그레이드($enableDeploymentUpgrade = 1)를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-219">The script will by default perform an Upgrade Deployment ($enableDeploymentUpgrade = 1) when no parameter is passed in or the value 1 is passed explicitly.</span></span> <span data-ttu-id="49b76-220">단일 인스턴스인 경우 전체 배포보다 시간이 적게 걸린다는 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-220">For single instances this has the advantage of taking less time than a full deployment.</span></span> <span data-ttu-id="49b76-221">고가용성이 필요한 인스턴스의 경우 일부 인스턴스가 업그레이드(업데이트 도메인 이동)되는 동안 다른 인스턴스가 계속 실행되며 VIP가 삭제되지 않는다는 장점도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-221">For instances that require high availability this also has the advantage of leaving some instances running while others are upgraded (walking your update domain), plus your VIP will not be deleted.</span></span>

   <span data-ttu-id="49b76-222">배포 업그레이드는 스크립트에서($enableDeploymentUpgrade = 0) 또는 *-enableDeploymentUpgrade 0* 을 매개 변수로 전달하여 사용하지 않도록 설정함으로써 기존 배포를 먼저 삭제한 다음 새 배포를 만들도록 스크립트 동작을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-222">Upgrade Deployment can be disabled in the script ($enableDeploymentUpgrade = 0) or by passing *-enableDeploymentUpgrade 0* as a parameter, which alters the script behavior to first delete any existing deployment and then create a new deployment.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="49b76-223">스크립트는 기존 배포가 검색될 경우 기본적으로 항상 삭제하거나 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-223">The script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="49b76-224">사용자에게 확인할 수 없는 경우 자동화에서 지속적인 전송을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-224">This is necessary to enable continuous delivery from automation where no user/operator prompting is possible.</span></span>
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a><span data-ttu-id="49b76-225">5: TFS 팀 빌드를 사용하여 패키지 게시</span><span class="sxs-lookup"><span data-stu-id="49b76-225">5: Publish a Package using TFS Team Build</span></span>
<span data-ttu-id="49b76-226">이 선택적 단계에서는 TFS 팀 빌드를 4단계에서 만든 스크립트에 연결하여 Azure에 패키지 빌드 게시를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-226">This optional step connects TFS Team Build to the script created in step 4, which handles publishing of the package build to Azure.</span></span> <span data-ttu-id="49b76-227">그런 다음 빌드 정의에서 사용하는 프로세스 템플릿을 수정하여 워크플로가 끝날 때 게시 작업이 실행되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-227">This entails modifying the Process Template used by your build definition so that it runs a Publish activity at the end of the workflow.</span></span> <span data-ttu-id="49b76-228">게시 작업에서는 빌드에서 매개 변수를 전달하는 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-228">The Publish activity will execute your PowerShell command passing in parameters from the build.</span></span> <span data-ttu-id="49b76-229">MSBuild 대상 및 게시 스크립트의 출력은 표준 빌드 출력에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-229">Output of the MSBuild targets and publish script will be piped into the standard build output.</span></span>

1. <span data-ttu-id="49b76-230">지속적인 배포를 담당하는 빌드 정의를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-230">Edit the Build Definition responsible for continuous deploy.</span></span>
2. <span data-ttu-id="49b76-231">**프로세스** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-231">Select the **Process** tab.</span></span>
3. <span data-ttu-id="49b76-232">[다음 지침](http://msdn.microsoft.com/library/dd647551.aspx)에 따라 빌드 프로세스 템플릿에 대한 작업 프로젝트를 추가하고, 기본 템플릿을 다운로드하여 프로젝트에 추가하고, 체크 인합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-232">Follow [these instructions](http://msdn.microsoft.com/library/dd647551.aspx) to add an Activity project for the build process template, download the default template, add it to the project and check it in.</span></span> <span data-ttu-id="49b76-233">빌드 프로세스 템플릿에 새 이름을 지정합니다(예: AzureBuildProcessTemplate).</span><span class="sxs-lookup"><span data-stu-id="49b76-233">Give the build process template a new name, such as AzureBuildProcessTemplate.</span></span>
4. <span data-ttu-id="49b76-234">**프로세스** 탭으로 돌아가서 **자세한 정보 표시**를 사용하여 사용 가능한 빌드 프로세스 템플릿 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-234">Return to the **Process** tab, and use **Show Details** to show a list of available build process templates.</span></span> <span data-ttu-id="49b76-235">**새로 만들기...** 단추를 선택하고 방금 추가하고 체크 인한 프로젝트로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-235">Choose the **New...** button, and navigate to the project you just added and checked in.</span></span> <span data-ttu-id="49b76-236">방금 만든 템플릿을 찾은 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-236">Locate the template you just created and choose **OK**.</span></span>
5. <span data-ttu-id="49b76-237">선택한 프로세스 템플릿을 열어 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-237">Open the selected Process Template for editing.</span></span> <span data-ttu-id="49b76-238">Workflow Designer에서 직접 열거나 XML 편집기에서 열어 XAML로 작업합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-238">You can open directly in the Workflow designer or in the XML editor to work with the XAML.</span></span>
6. <span data-ttu-id="49b76-239">다음 새 인수 목록을 별도의 라인 항목으로 Workflow Designer의 인수 탭에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-239">Add the following list of new arguments as separate line items in the arguments tab of the workflow designer.</span></span> <span data-ttu-id="49b76-240">모든 인수는 direction=In 및 type=String이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-240">All arguments should have direction=In and type=String.</span></span> <span data-ttu-id="49b76-241">이러한 값은 빌드 정의에서 워크플로로 매개 변수가 흐르는 데 사용된 다음 게시 스크립트를 호출하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-241">These will be used to flow parameters from the build definition into the workflow, which then get used to call the publish script.</span></span>

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![인수 목록][3]

   <span data-ttu-id="49b76-243">해당 XAML은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-243">The corresponding XAML looks like this:</span></span>

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
7. <span data-ttu-id="49b76-244">에이전트에서 실행이 끝나면 새 시퀀스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-244">Add a new sequence at the end of Run On Agent:</span></span>

   1. <span data-ttu-id="49b76-245">유효한 스크립트 파일을 확인하는 If 문 작업을 추가하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-245">Start by adding an If Statement activity to check for a valid script file.</span></span> <span data-ttu-id="49b76-246">조건을 다음 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-246">Set the condition to this value:</span></span>

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. <span data-ttu-id="49b76-247">If 문의 Then 케이스에서 새 시퀀스 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-247">In the Then case of the If Statement, add a new Sequence activity.</span></span> <span data-ttu-id="49b76-248">표시 이름을 'Start publish'로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-248">Set the display name to 'Start publish'</span></span>
   3. <span data-ttu-id="49b76-249">Start publish 시퀀스를 선택한 상태에서 다음 새 변수 목록을 별도의 라인 항목으로 Workflow Designer의 변수 탭에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-249">With the Start publish sequence still selected, add the following list of new variables as separate line items in the variables tab of the workflow designer.</span></span> <span data-ttu-id="49b76-250">모든 변수의 변수 유형은 문자열이고 범위는 Start publish여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-250">All variables should have Variable type =String and Scope=Start publish.</span></span> <span data-ttu-id="49b76-251">이러한 값은 빌드 정의에서 워크플로로 매개 변수가 흐르는 데 사용된 다음 게시 스크립트를 호출하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-251">These will be used to flow parameters from the build definition into the workflow, which then get used to call the publish script.</span></span>

      * <span data-ttu-id="49b76-252">SubscriptionDataFilePath, 문자열 유형</span><span class="sxs-lookup"><span data-stu-id="49b76-252">SubscriptionDataFilePath, of type String</span></span>
      * <span data-ttu-id="49b76-253">PublishScriptFilePath, 문자열 유형</span><span class="sxs-lookup"><span data-stu-id="49b76-253">PublishScriptFilePath, of type String</span></span>

        ![새 변수][4]
   4. <span data-ttu-id="49b76-255">TFS 2012 이하를 사용하고 있으면 새 시퀀스의 시작 부분에 ConvertWorkspaceItem 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-255">If you are using TFS 2012 or earlier, add a ConvertWorkspaceItem activity at the beginning of the new Sequence.</span></span> <span data-ttu-id="49b76-256">TFS 2013 이상을 사용하고 있으면 새 시퀀스의 시작 부분에 GetLocalPath 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-256">If you are using TFS 2013 or later, add a GetLocalPath activity at the beginning of the new sequence.</span></span> <span data-ttu-id="49b76-257">ConvertWorkspaceItem의 경우 다음과 같이 속성을 설정합니다. Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span><span class="sxs-lookup"><span data-stu-id="49b76-257">For a ConvertWorkspaceItem, set the properties as follows: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="49b76-258">GetLocalPath 작업의 경우 IncomingPath 속성을 'PublishScriptLocation'으로 설정하고 Result를 'PublishScriptFilePath'로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-258">For a GetLocalPath activity, set the property IncomingPath to 'PublishScriptLocation', and the Result to 'PublishScriptFilePath'.</span></span> <span data-ttu-id="49b76-259">이 작업은 TFS 서버 위치(해당되는 경우)의 게시 스크립트 경로를 표준 로컬 디스크 경로로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-259">This activity converts the path to the publish script from TFS server locations (if applicable) to a standard local disk path.</span></span>
   5. <span data-ttu-id="49b76-260">TFS 2012 이하를 사용하고 있으면 새 시퀀스의 끝 부분에 또 다른 ConvertWorkspaceItem 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-260">If you are using TFS 2012 or earlier, add another ConvertWorkspaceItem activity at the end of the new Sequence.</span></span> <span data-ttu-id="49b76-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span><span class="sxs-lookup"><span data-stu-id="49b76-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="49b76-262">TFS 2013 이상을 사용하고 있으면 또 다른 GetLocalPath를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-262">If you are using TFS 2013 or later, add another GetLocalPath.</span></span> <span data-ttu-id="49b76-263">IncomingPath='SubscriptionDataFileLocation' 및 Result='SubscriptionDataFilePath'입니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-263">IncomingPath='SubscriptionDataFileLocation', and Result='SubscriptionDataFilePath.'</span></span>
   6. <span data-ttu-id="49b76-264">새 시퀀스의 끝 부분에 InvokeProcess 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-264">Add an InvokeProcess activity at the end of the new Sequence.</span></span>
      <span data-ttu-id="49b76-265">이 작업은 빌드 정의에 의해 전달된 인수를 사용하여 PowerShell.exe를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-265">This activity calls PowerShell.exe with the arguments passed in by the Build Definition.</span></span>

      + <span data-ttu-id="49b76-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span><span class="sxs-lookup"><span data-stu-id="49b76-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span></span>
      + <span data-ttu-id="49b76-267">DisplayName = Execute publish script</span><span class="sxs-lookup"><span data-stu-id="49b76-267">DisplayName = Execute publish script</span></span>
      + <span data-ttu-id="49b76-268">FileName = "PowerShell"(따옴표 포함)</span><span class="sxs-lookup"><span data-stu-id="49b76-268">FileName = "PowerShell" (include the quotes)</span></span>
      + <span data-ttu-id="49b76-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span><span class="sxs-lookup"><span data-stu-id="49b76-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span></span>
   7. <span data-ttu-id="49b76-270">InvokeProcess의 **표준 출력 처리** 섹션 텍스트 상자에서 텍스트 상자 값을 'data'로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-270">In the **Handle Standard Output** section textbox of the InvokeProcess, set the textbox value to 'data'.</span></span> <span data-ttu-id="49b76-271">이 값은 표준 출력 데이터를 저장하는 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-271">This is a variable to store the standard output data.</span></span>
   8. <span data-ttu-id="49b76-272">**표준 출력 처리** 섹션 바로 아래에 WriteBuildMessage 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-272">Add a WriteBuildMessage activity just below the **Handle Standard Output** section.</span></span> <span data-ttu-id="49b76-273">Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' 및 Message='data'로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-273">Set the Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' and the Message='data'.</span></span> <span data-ttu-id="49b76-274">그러면 스크립트의 표준 출력이 빌드 출력에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-274">This ensures the standard output of the script will get written to the build output.</span></span>
   9. <span data-ttu-id="49b76-275">InvokeProcess의 **오류 출력 처리** 섹션 텍스트 상자에서 텍스트 상자 값을 'data'로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-275">In the **Handle Error Output** section textbox of the InvokeProcess, set the textbox value to 'data'.</span></span> <span data-ttu-id="49b76-276">이 값은 표준 오류 데이터를 저장하는 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-276">This is a variable to store the standard error data.</span></span>
   10. <span data-ttu-id="49b76-277">**오류 출력 처리** 섹션 바로 아래에 WriteBuildError 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-277">Add a WriteBuildError activity just below the **Handle Error Output** section.</span></span> <span data-ttu-id="49b76-278">Message='data'로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-278">Set the Message='data'.</span></span> <span data-ttu-id="49b76-279">그러면 스크립트의 표준 오류가 빌드 오류 출력에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-279">This ensures the standard errors of the script will get written to the build error output.</span></span>
   11. <span data-ttu-id="49b76-280">파란색 느낌표가 표시된 오류를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-280">Correct any errors, indicated by blue exclamation marks.</span></span> <span data-ttu-id="49b76-281">오류에 대한 힌트를 얻으려면 느낌표를 마우스로 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-281">Hover over the exclamation marks to get a hint about the error.</span></span> <span data-ttu-id="49b76-282">오류를 지우려면 워크플로를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-282">Save the workflow to clear errors.</span></span>

   <span data-ttu-id="49b76-283">게시 워크플로 작업의 최종 결과는 디자이너에 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-283">The final result of the publish workflow activities will look like this in the designer:</span></span>

   ![워크플로 작업][5]

   <span data-ttu-id="49b76-285">게시 워크플로 작업의 최종 결과는 XAML로 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-285">The final result of the publish workflow activities will look like this in XAML:</span></span>

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
8. <span data-ttu-id="49b76-286">빌드 프로세스 템플릿 워크플로를 저장하고 이 파일을 체크 인합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-286">Save the build process template workflow and Check In this file.</span></span>
9. <span data-ttu-id="49b76-287">빌드 정의를 편집하고(이미 열려 있는 경우 닫기), 프로세스 템플릿 목록에 새 템플릿이 표시되지 않으면 **새로 만들기** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-287">Edit the build definition (close it if it is already open), and select the **New** button if you do not yet see the new template in the list of Process Templates.</span></span>
10. <span data-ttu-id="49b76-288">기타 섹션에서 매개 변수 속성 값을 다음과 같이 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-288">Set the parameter property values in the Misc section as follows:</span></span>

    1. <span data-ttu-id="49b76-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *이 값의 파생 위치: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span><span class="sxs-lookup"><span data-stu-id="49b76-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *This value is derived from: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span></span>
    2. <span data-ttu-id="49b76-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *이 값의 파생 위치: ($PublishDir)($ProjectName).cspkg*</span><span class="sxs-lookup"><span data-stu-id="49b76-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *This value is derived from: ($PublishDir)($ProjectName).cspkg*</span></span>
    3. <span data-ttu-id="49b76-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span><span class="sxs-lookup"><span data-stu-id="49b76-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span></span>
    4. <span data-ttu-id="49b76-292">ServiceName = 'mycloudservicename' *여기에 적절한 클라우드 서비스 이름 사용*</span><span class="sxs-lookup"><span data-stu-id="49b76-292">ServiceName = 'mycloudservicename' *Use the appropriate cloud service name here*</span></span>
    5. <span data-ttu-id="49b76-293">Environment = 'Staging'</span><span class="sxs-lookup"><span data-stu-id="49b76-293">Environment = 'Staging'</span></span>
    6. <span data-ttu-id="49b76-294">StorageAccountName = 'mystorageaccountname' *여기에 적절한 저장소 계정 이름 사용*</span><span class="sxs-lookup"><span data-stu-id="49b76-294">StorageAccountName = 'mystorageaccountname' *Use the appropriate storage account name here*</span></span>
    7. <span data-ttu-id="49b76-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span><span class="sxs-lookup"><span data-stu-id="49b76-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span></span>
    8. <span data-ttu-id="49b76-296">SubscriptionName = 'default'</span><span class="sxs-lookup"><span data-stu-id="49b76-296">SubscriptionName = 'default'</span></span>

    ![매개 변수 속성 값][6]
11. <span data-ttu-id="49b76-298">변경 내용을 빌드 정의에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-298">Save the changes to the Build Definition.</span></span>
12. <span data-ttu-id="49b76-299">빌드를 큐에 대기시켜 패키지 빌드와 게시를 모두 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-299">Queue a Build to execute both the package build and publish.</span></span> <span data-ttu-id="49b76-300">트리거를 지속적인 통합으로 설정한 경우 이 동작이 체크 인할 때마다 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b76-300">If you have a trigger set to Continuous Integration, you will execute this behavior on every check-in.</span></span>

### <a name="publishcloudserviceps1-script-template"></a><span data-ttu-id="49b76-301">PublishCloudService.ps1 스크립트 템플릿</span><span class="sxs-lookup"><span data-stu-id="49b76-301">PublishCloudService.ps1 script template</span></span>
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy to $servicename",
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
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according to $alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
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

#main driver - publish & write progress to activity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a><span data-ttu-id="49b76-302">다음 단계</span><span class="sxs-lookup"><span data-stu-id="49b76-302">Next steps</span></span>
<span data-ttu-id="49b76-303">연속 배달을 사용하는 경우 원격 디버깅을 사용하려면 [연속 배달을 사용하여 Azure에 게시할 경우 원격 디버깅 사용](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49b76-303">To enable remote debugging when using continuous delivery, see [Enable remote debugging when using continuous delivery to publish to Azure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span></span>

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[the .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
