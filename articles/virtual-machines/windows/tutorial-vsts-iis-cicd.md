---
title: "Azure에서 Team Services를 사용하여 CI/CD 파이프라인 만들기 | Microsoft Docs"
description: "연속적인 통합 및 전달을 위해 Windows VM에서 웹앱을 IIS에 배포하는 Visual Studio Team Services 파이프라인을 만드는 방법에 대해 알아봅니다."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: a587f58fad2ec74c7633823c4d34f900e7c01f7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a><span data-ttu-id="c77dd-103">Visual Studio Team Services 및 IIS를 사용하여 연속 통합 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="c77dd-103">Create a continuous integration pipeline with Visual Studio Team Services and IIS</span></span>
<span data-ttu-id="c77dd-104">응용 프로그램 개발의 빌드, 테스트 및 배포 단계를 자동화하려면 CI/CD(연속 통합 및 배포) 파이프라인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-104">To automate the build, test, and deployment phases of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="c77dd-105">이 자습서에서는 Visual Studio Team Services 및 IIS를 실행하는 Azure의 Windows VM(가상 컴퓨터)를 사용하여 CI/CD 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-105">In this tutorial, you create a CI/CD pipeline using Visual Studio Team Services and a Windows virtual machine (VM) in Azure that runs IIS.</span></span> <span data-ttu-id="c77dd-106">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c77dd-107">Team Services 프로젝트에 ASP.NET 웹 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="c77dd-107">Publish an ASP.NET web application to a Team Services project</span></span>
> * <span data-ttu-id="c77dd-108">코드 커밋으로 트리거되는 빌드 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="c77dd-108">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="c77dd-109">Azure의 가상 컴퓨터에 IIS 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="c77dd-109">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="c77dd-110">Team Services의 배포 그룹에 IIS 인스턴스 추가</span><span class="sxs-lookup"><span data-stu-id="c77dd-110">Add the IIS instance to a deployment group in Team Services</span></span>
> * <span data-ttu-id="c77dd-111">새 웹 배포 패키지를 IIS에 게시하기 위한 릴리스 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="c77dd-111">Create a release definition to publish new web deploy packages to IIS</span></span>
> * <span data-ttu-id="c77dd-112">CI/CD 파이프라인 테스트</span><span class="sxs-lookup"><span data-stu-id="c77dd-112">Test the CI/CD pipeline</span></span>

<span data-ttu-id="c77dd-113">이 자습서에는 Azure PowerShell 모듈 버전 3.6 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="c77dd-114">`Get-Module -ListAvailable AzureRM`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-114">Run `Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="c77dd-115">업그레이드해야 하는 경우 [Azure PowerShell 모듈 설치](/powershell/azure/install-azurerm-ps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c77dd-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="create-project-in-team-services"></a><span data-ttu-id="c77dd-116">Team Services에서 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="c77dd-116">Create project in Team Services</span></span>
<span data-ttu-id="c77dd-117">Visual Studio Team Services를 사용하면 온-프레미스 코드 관리 솔루션을 유지 관리하지 않고도 손쉽게 공동 작업하고 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-117">Visual Studio Team Services allows for easy collaboration and development without maintaining an on-premises code management solution.</span></span> <span data-ttu-id="c77dd-118">Team Services는 클라우드 코드 테스트, 빌드 및 응용 프로그램 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-118">Team Services provides cloud code testing, build, and application insights.</span></span> <span data-ttu-id="c77dd-119">코드 개발에 가장 적합한 버전 제어 리포지토리 및 IDE를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-119">You can choose a version control repo and IDE that best fits your code development.</span></span> <span data-ttu-id="c77dd-120">이 자습서에서는 체험 계정을 사용하여 기본 ASP.NET 웹앱 및 CI/CD 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-120">For this tutorial, you can use a free account to create a basic ASP.NET web app and CI/CD pipeline.</span></span> <span data-ttu-id="c77dd-121">Team Services 계정이 없는 경우 [해당 계정을 만듭니다](http://go.microsoft.com/fwlink/?LinkId=307137).</span><span class="sxs-lookup"><span data-stu-id="c77dd-121">If you do not already have a Team Services account, [create one](http://go.microsoft.com/fwlink/?LinkId=307137).</span></span>

<span data-ttu-id="c77dd-122">코드 커밋 프로세스를 관리하고, 정의를 빌드하고 릴리스하려면 다음과 같이 Team Services에서 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-122">To manage the code commit process, build definitions, and release definitions, create a project in Team Services as follows:</span></span>

1. <span data-ttu-id="c77dd-123">웹 브라우저에서 Team Services 대시보드를 열고 **새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-123">Open your Team Services dashboard in a web browser and choose **New project**.</span></span>
2. <span data-ttu-id="c77dd-124">**프로젝트 이름**에서 *myWebApp*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-124">Enter *myWebApp* for the **Project name**.</span></span> <span data-ttu-id="c77dd-125">다른 모든 기본값은 그대로 두고 *Git* 버전 제어 및 *Agile* 작업 항목 프로세스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-125">Leave all other default values to use *Git* version control and *Agile* work item process.</span></span>
3. <span data-ttu-id="c77dd-126">***팀 구성원*과 공유** 옵션을 선택한 다음 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-126">Choose the option to **Share with** *Team Members*, then select **Create**.</span></span>
5. <span data-ttu-id="c77dd-127">프로젝트가 만들어지면 **추가 정보나 gitignore를 사용하여 초기화** 옵션을 선택한 다음 **초기화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-127">Once your project has been created, choose the option to **Initialize with a README or gitignore**, then **Initialize**.</span></span>
6. <span data-ttu-id="c77dd-128">새 프로젝트에서 위쪽의 **대시보드**를 선택한 다음 **Visual Studio에서 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-128">Inside your new project, choose **Dashboards** across the top, then select **Open in Visual Studio**.</span></span>


## <a name="create-aspnet-web-application"></a><span data-ttu-id="c77dd-129">ASP.NET 웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="c77dd-129">Create ASP.NET web application</span></span>
<span data-ttu-id="c77dd-130">이전 단계에서는 Team Services에서 프로젝트를 만들었으며,</span><span class="sxs-lookup"><span data-stu-id="c77dd-130">In the previous step, you created a project in Team Services.</span></span> <span data-ttu-id="c77dd-131">마지막 단계에서는 Visual Studio에서 새 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-131">The final step opens your new project in Visual Studio.</span></span> <span data-ttu-id="c77dd-132">**팀 탐색기** 창에서 코드 커밋을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-132">You manage your code commits in the **Team Explorer** window.</span></span> <span data-ttu-id="c77dd-133">새 프로젝트의 로컬 복사본을 만든 다음 템플릿에서 다음과 같이 ASP.NET 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-133">Create a local copy of your new project, then create an ASP.NET web application from a template as follows:</span></span>

1. <span data-ttu-id="c77dd-134">**복제**를 선택하여 Team Services 프로젝트의 로컬 git 리포지토리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-134">Select **Clone** to create a local git repo of your Team Services project.</span></span>
    
    ![Team Services 프로젝트에서 리포지토리 복제](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. <span data-ttu-id="c77dd-136">**솔루션**에서 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-136">Under **Solutions**, select **New**.</span></span>

    ![웹 응용 프로그램 솔루션 만들기](media/tutorial-vsts-iis-cicd/new_solution.png)

3. <span data-ttu-id="c77dd-138">**웹** 템플릿을 선택한 다음 **ASP.NET 웹 응용 프로그램** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-138">Select **Web** templates, and then choose the **ASP.NET Web Application** template.</span></span>
    1. <span data-ttu-id="c77dd-139">*myWebApp*과 같은 응용 프로그램의 이름을 입력하고 **솔루션용 디렉터리 만들기** 확인란의 선택을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-139">Enter a name for your application, such as *myWebApp*, and uncheck the box for **Create directory for solution**.</span></span>
    2. <span data-ttu-id="c77dd-140">**프로젝트에 Application Insights 추가** 옵션을 사용할 수 있는 경우 이 확인란의 선택을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-140">If the option is available, uncheck the box to **Add Application Insights to project**.</span></span> <span data-ttu-id="c77dd-141">Application Insight에서는 Azure Application Insights를 통해 웹 응용 프로그램에 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-141">Application Insights requires you to authorize your web application with Azure Application Insights.</span></span> <span data-ttu-id="c77dd-142">이 자습서에서 간단하게 유지하려면 이 프로세스를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-142">To keep it simple in this tutorial, skip this process.</span></span>
    3. <span data-ttu-id="c77dd-143">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-143">Select **OK**.</span></span>
4. <span data-ttu-id="c77dd-144">템플릿 목록에서 **MVC**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-144">Choose **MVC** from the template list.</span></span>
    1. <span data-ttu-id="c77dd-145">**인증 변경**을 선택하고 **인증 없음**을 선택한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-145">Select **Change Authentication**, choose **No Authentication**, then select **OK**.</span></span>
    2. <span data-ttu-id="c77dd-146">솔루션을 만들려면 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-146">Select **OK** to create your solution.</span></span>
5. <span data-ttu-id="c77dd-147">**팀 탐색기** 창에서 **변경**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-147">In the **Team Explorer** window, choose **Changes**.</span></span>

    ![Team Services git 리포지토리에 로컬 변경 내용 커밋](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. <span data-ttu-id="c77dd-149">커밋 텍스트 상자에서 *초기 커밋*과 같은 메시지를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-149">In the commit text box, enter a message such as *Initial commit*.</span></span> <span data-ttu-id="c77dd-150">드롭다운 메뉴에서 **모두 커밋 후 동기화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-150">Choose **Commit All and Sync** from the drop-down menu.</span></span>


## <a name="create-build-definition"></a><span data-ttu-id="c77dd-151">빌드 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="c77dd-151">Create build definition</span></span>
<span data-ttu-id="c77dd-152">Team Services에서 빌드 정의를 사용하여 응용 프로그램을 빌드하는 방법을 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-152">In Team Services, you use a build definition to outline how your application should be built.</span></span> <span data-ttu-id="c77dd-153">이 자습서에서는 소스 코드를 가져와서 솔루션을 빌드한 다음 IIS 서버에서 웹앱을 실행하는 데 사용할 수 있는 웹 배포 패키지를 만드는 기본 정의를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-153">In this tutorial, we create a basic definition that takes our source code, builds the solution, then creates web deploy package we can use to run the web app on an IIS server.</span></span>

1. <span data-ttu-id="c77dd-154">Team Services 프로젝트에서 위쪽의 **빌드 및 릴리스**를 선택한 다음 **빌드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-154">In your Team Services project, choose **Build & Release** across the top, then select **Builds**.</span></span>
3. <span data-ttu-id="c77dd-155">**+ 새 정의**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-155">Select **+ New definition**.</span></span>
4. <span data-ttu-id="c77dd-156">**ASP.NET(미리 보기)** 템플릿을 선택하고 **적용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-156">Choose the **ASP.NET (PREVIEW)** template and select **Apply**.</span></span>
5. <span data-ttu-id="c77dd-157">모든 기본 작업 값은 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-157">Leave all the default task values.</span></span> <span data-ttu-id="c77dd-158">**원본 가져오기**에서 *myWebApp* 리포지토리와 *마스터* 분기가 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-158">Under **Get sources**, ensure that the *myWebApp* repository and *master* branch are selected.</span></span>

    ![Team Services 프로젝트에서 빌드 정의 만들기](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. <span data-ttu-id="c77dd-160">**트리거** 탭에서 **이 트리거 사용**에 대한 슬라이더를 *사용*으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-160">On the **Triggers** tab, move the slider for **Enable this trigger** to *Enabled*.</span></span>
7. <span data-ttu-id="c77dd-161">빌드 정의를 저장하고 **저장 및 큐**를 선택한 다음 **저장 및 큐**를 다시 선택하여 새 빌드를 큐에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-161">Save the build definition and queue a new build by selecting **Save & queue** , then **Save & queue** again.</span></span> <span data-ttu-id="c77dd-162">기본값은 그대로 두고 **큐**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-162">Leave the defaults and select **Queue**.</span></span>

<span data-ttu-id="c77dd-163">빌드가 호스트된 에이전트에 예약되어 있는지 확인한 다음 빌드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-163">Watch as the build is scheduled on a hosted agent, then begins to build.</span></span> <span data-ttu-id="c77dd-164">다음 예제와 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-164">The output is similar to the following example:</span></span>

![성공적인 Team Services 프로젝트 빌드](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a><span data-ttu-id="c77dd-166">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="c77dd-166">Create virtual machine</span></span>
<span data-ttu-id="c77dd-167">ASP.NET 웹앱을 실행할 플랫폼을 제공하려면 IIS를 실행하는 Windows 가상 컴퓨터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-167">To provide a platform to run your ASP.NET web app, you need a Windows virtual machine that runs IIS.</span></span> <span data-ttu-id="c77dd-168">코드를 커밋하고 빌드가 트리거될 때 Team Services에서 에이전트를 사용하여 IIS 인스턴스와 상호 작용합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-168">Team Services uses an agent to interact with the IIS instance as you commit code and builds are triggered.</span></span>

<span data-ttu-id="c77dd-169">[이 스크립트 샘플](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json)을 사용하여 Windows Server 2016 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-169">Create a Windows Server 2016 VM using [this script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span></span> <span data-ttu-id="c77dd-170">스크립트가 실행되어 VM을 만드는 데 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-170">It takes a few minutes for the script to run and create the VM.</span></span> <span data-ttu-id="c77dd-171">VM을 만들면 다음과 같이 [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup)를 사용하여 웹 트래픽용 80 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-171">Once the VM has been created, open port 80 for web traffic with [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) as follows:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $resourceGroup `
  -Name "myNetworkSecurityGroup" | `
Add-AzureRmNetworkSecurityRuleConfig `
  -Name "myNetworkSecurityGroupRuleWeb" `
  -Protocol "Tcp" `
  -Direction "Inbound" `
  -Priority "1001" `
  -SourceAddressPrefix "*" `
  -SourcePortRange "*" `
  -DestinationAddressPrefix "*" `
  -DestinationPortRange "80" `
  -Access "Allow" | `
Set-AzureRmNetworkSecurityGroup
```

<span data-ttu-id="c77dd-172">VM에 연결하려면 다음과 같이 [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)를 사용하여 공용 IP 주소를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-172">To connect to your VM, obtain the public IP address with [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) as follows:</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

<span data-ttu-id="c77dd-173">VM에 대한 원격 데스크톱 세션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-173">Create a remote desktop session to your VM:</span></span>

```cmd
mstsc /v:<publicIpAddress>
```

<span data-ttu-id="c77dd-174">VM에서 **관리자 PowerShell** 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-174">On the VM, open an **Administrator PowerShell** command prompt.</span></span> <span data-ttu-id="c77dd-175">다음과 같이 IIS 및 필요한 .NET 기능을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-175">Install IIS and required .NET features as follows:</span></span>

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a><span data-ttu-id="c77dd-176">배포 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="c77dd-176">Create deployment group</span></span>
<span data-ttu-id="c77dd-177">웹 배포 패키지를 IIS 서버로 푸시하려면 Team Services에서 배포 그룹을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-177">To push out the web deploy package to the IIS server, you define a deployment group in Team Services.</span></span> <span data-ttu-id="c77dd-178">이 그룹을 사용하면 Team Services에 코드를 커밋하고 빌드가 완료될 때 새 빌드 대상이 되는 서버를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-178">This group allows you to specify which servers are the target of new builds as you commit code to Team Services and builds are completed.</span></span>

1. <span data-ttu-id="c77dd-179">Team Services에서 **빌드 및 릴리스**를 선택한 다음 **배포 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-179">In Team Services, choose **Build & Release** and then select **Deployment groups**.</span></span>
2. <span data-ttu-id="c77dd-180">**배포 그룹 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-180">Choose **Add Deployment group**.</span></span>
3. <span data-ttu-id="c77dd-181">*myIIS*와 같은 그룹의 이름을 입력한 다음 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-181">Enter a name for the group, such as *myIIS*, then select **Create**.</span></span>
4. <span data-ttu-id="c77dd-182">**컴퓨터 등록** 섹션에서 *Windows*가 선택되어 있는지 확인한 다음 **인증에 스크립트의 개인용 액세스 토큰 사용** 확인란을 선택합니다 .</span><span class="sxs-lookup"><span data-stu-id="c77dd-182">In the **Register machines** section, ensure *Windows* is selected, then check the box to **Use a personal access token in the script for authentication**.</span></span>
5. <span data-ttu-id="c77dd-183">**클립보드에 스크립트 복사**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-183">Select **Copy script to clipboard**.</span></span>


### <a name="add-iis-vm-to-the-deployment-group"></a><span data-ttu-id="c77dd-184">배포 그룹에 IIS VM 추가</span><span class="sxs-lookup"><span data-stu-id="c77dd-184">Add IIS VM to the deployment group</span></span>
<span data-ttu-id="c77dd-185">만든 배포 그룹을 사용하여 각 IIS 인스턴스를 그룹에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-185">With the deployment group created, add each IIS instance to the group.</span></span> <span data-ttu-id="c77dd-186">Team Services는 새 웹 배포 패키지를 받는 VM에서 에이전트를 다운로드하고 구성하는 스크립트를 생성한 다음 IIS에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-186">Team Services generates a script that downloads and configures an agent on the VM that receives new web deploy packages then applies it to IIS.</span></span>

1. <span data-ttu-id="c77dd-187">VM의 **관리자 PowerShell** 세션으로 돌아가서 Team Services에서 복사한 스크립트를 붙여넣고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-187">Back in the **Administrator PowerShell** session on your VM, paste and run the script copied from Team Services.</span></span>
2. <span data-ttu-id="c77dd-188">에이전트에 대한 태그를 구성하도록 요구하는 메시지가 표시되면 *Y*를 선택하고 *웹*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-188">When prompted to configure tags for the agent, choose *Y* and enter *web*.</span></span>
3. <span data-ttu-id="c77dd-189">사용자 계정을 요구하는 메시지가 표시되면 *Enter* 키를 눌러 기본값을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-189">When prompted for the user account, press *Return* to accept the defaults.</span></span>
4. <span data-ttu-id="c77dd-190">*vstsagent.account.computername 서비스가 성공적으로 시작되었습니다.* 메시지와 함께 스크립트가 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-190">Wait for the script to finish with a message *Service vstsagent.account.computername started successfully*.</span></span>
5. <span data-ttu-id="c77dd-191">**빌드 및 릴리스** 메뉴의 **배포 그룹** 페이지에서 *myIIS* 배포 그룹을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-191">In the **Deployment groups** page of the **Build & Release** menu, open the *myIIS* deployment group.</span></span> <span data-ttu-id="c77dd-192">**컴퓨터** 탭에서 VM이 나열되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-192">On the **Machines** tab, verify that your VM is listed.</span></span>

    ![Team Services 배포 그룹에 VM이 성공적으로 추가되었습니다.](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a><span data-ttu-id="c77dd-194">릴리스 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="c77dd-194">Create release definition</span></span>
<span data-ttu-id="c77dd-195">빌드를 게시하려면 Team Services에서 릴리스 정의를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-195">To publish your builds, you create a release definition in Team Services.</span></span> <span data-ttu-id="c77dd-196">응용 프로그램을 성공적으로 빌드하면 이 정의가 자동으로 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-196">This definition is triggered automatically by a successful build of your application.</span></span> <span data-ttu-id="c77dd-197">웹 배포 패키지를 푸시할 배포 그룹을 선택하고 적절한 IIS 설정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-197">You choose the deployment group to push your web deploy package to, and define the appropriate IIS settings.</span></span>

1. <span data-ttu-id="c77dd-198">**빌드 및 릴리스**를 선택한 다음 **빌드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-198">Choose **Build & Release**, then select **Builds**.</span></span> <span data-ttu-id="c77dd-199">이전 단계에서 만든 빌드 정의를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-199">Choose the build definition created in a previous step.</span></span>
2. <span data-ttu-id="c77dd-200">**최근 완료됨**에서 가장 최근의 빌드를 선택한 다음 **릴리스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-200">Under **Recently completed**, choose the most recent build, then select **Release**.</span></span>
3. <span data-ttu-id="c77dd-201">릴리스 정의를 만들려면 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-201">Choose **Yes** to create a release definition.</span></span>
4. <span data-ttu-id="c77dd-202">**빈** 템플릿을 선택한 후 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-202">Choose the **Empty** template, then select **Next**.</span></span>
5. <span data-ttu-id="c77dd-203">프로젝트 및 소스 빌드 정의가 프로젝트로 채워졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-203">Verify the project and source build definition are populated with your project.</span></span>
6. <span data-ttu-id="c77dd-204">**연속 배포** 확인란을 선택한 다음 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-204">Select the **Continuous deployment** check box, then select **Create**.</span></span>
7. <span data-ttu-id="c77dd-205">**+ 작업 추가** 옆에 있는 드롭다운 상자를 선택하고 *배포 그룹 단계 추가*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-205">Select the drop-down box next to **+ Add tasks** and choose *Add a deployment group phase*.</span></span>
    
    ![Team Services에서 정의를 릴리스하는 작업 추가](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. <span data-ttu-id="c77dd-207">**IIS 웹앱 배포(미리 보기)** 옆에 있는**추가**를 선택한 다음 **닫기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-207">Choose **Add** next to **IIS Web App Deploy(Preview)**, then select **Close**.</span></span>
9. <span data-ttu-id="c77dd-208">**배포 그룹에서 실행** 부모 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-208">Select the **Run on deployment group** parent task.</span></span>
    1. <span data-ttu-id="c77dd-209">**배포 그룹**에 대해 *myIIS*와 같이 이전에 만든 배포 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-209">For **Deployment Group**, select the deployment group you created earlier, such as *myIIS*.</span></span>
    2. <span data-ttu-id="c77dd-210">**컴퓨터 태그** 상자에서 **추가**를 선택하고 *웹* 태그를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-210">In the **Machine tags** box, select **Add** and choose the *web* tag.</span></span>
    
    ![IIS용 정의 배포 그룹 작업 릴리스](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. <span data-ttu-id="c77dd-212">**배포: IIS 웹앱 배포** 작업을 선택하여 다음과 같이 IIS 인스턴스 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-212">Select the **Deploy: IIS Web App Deploy** task to configure your IIS instance settings as follows:</span></span>
    1. <span data-ttu-id="c77dd-213">**웹 사이트 이름**에서 *기본 웹 사이트*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-213">For **Website Name**, enter *Default Web Site*.</span></span>
    2. <span data-ttu-id="c77dd-214">다른 모든 기본 설정을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-214">Leave all the other default settings.</span></span>
12. <span data-ttu-id="c77dd-215">**저장**을 선택한 다음 **확인**을 두 번 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-215">Choose **Save**, then select **OK** twice.</span></span>


## <a name="create-a-release-and-publish"></a><span data-ttu-id="c77dd-216">릴리스 만들기 및 게시</span><span class="sxs-lookup"><span data-stu-id="c77dd-216">Create a release and publish</span></span>
<span data-ttu-id="c77dd-217">이제 웹 배포 패키지를 새 릴리스로 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-217">You can now push your web deploy package as a new release.</span></span> <span data-ttu-id="c77dd-218">이 단계에서는 배포 그룹에 속한 각 인스턴스의 에이전트와 통신하고, 웹 배포 패키지를 푸시한 다음, IIS에서 업데이트된 웹 응용 프로그램을 실행하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-218">This step communicates with the agent on each instance that is part of the deployment group, pushes the web deploy package, then configures IIS to run the updated web application.</span></span>

1. <span data-ttu-id="c77dd-219">릴리스 정의에서 **+ 릴리스**를 선택한 다음 **릴리스 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-219">In your release definition, select **+ Release**, then choose **Create Release**.</span></span>
2. <span data-ttu-id="c77dd-220">드롭다운 목록에서 **자동 배포: 릴리스를 만들 때**와 함께 최신 빌드가 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-220">Verify that the latest build is selected in the drop-down list, along with **Automated deployment: After release creation**.</span></span> <span data-ttu-id="c77dd-221">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-221">Select **Create**.</span></span>
3. <span data-ttu-id="c77dd-222">릴리스 정의의 위쪽에 *'Release-1' 릴리스를 만들었습니다.*와 같은 작은 배너가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-222">A small banner appears across the top of your release definition, such as *Release 'Release-1' has been created*.</span></span> <span data-ttu-id="c77dd-223">릴리스 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-223">Select the release link.</span></span>
4. <span data-ttu-id="c77dd-224">**로그** 탭을 열어 릴리스 진행 상황을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-224">Open the **Logs** tab to watch the release progress.</span></span>
    
    ![성공적인 Team Services 릴리스 및 웹 배포 패키지 푸시](media/tutorial-vsts-iis-cicd/successful_release.png)

5. <span data-ttu-id="c77dd-226">릴리스가 완료되면 웹 브라우저를 열고 VM의 공용 IP 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-226">After the release is complete, open a web browser and enter the public IIP address of your VM.</span></span> <span data-ttu-id="c77dd-227">ASP.NET 웹 응용 프로그램이 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-227">Your ASP.NET web application is running.</span></span>

    ![IIS VM에서 실행 중인 ASP.NET 웹앱](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-the-whole-cicd-pipeline"></a><span data-ttu-id="c77dd-229">전체 CI/CD 파이프라인 테스트</span><span class="sxs-lookup"><span data-stu-id="c77dd-229">Test the whole CI/CD pipeline</span></span>
<span data-ttu-id="c77dd-230">이제 IIS에서 실행 중인 웹 응용 프로그램을 사용하여 전체 CI/CD 파이프라인을 사용해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-230">With your web application running on IIS, now try the whole CI/CD pipeline.</span></span> <span data-ttu-id="c77dd-231">Visual Studio에서 변경하고 코드를 커밋하면, 빌드가 트리거되어 업데이트된 웹 배포 패키지의 릴리스를 IIS에 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-231">After you make a change in Visual Studio and commit your code, a build is triggered which then triggers a release of your updated web deploy package to IIS:</span></span>

1. <span data-ttu-id="c77dd-232">Visual Studio에서 **솔루션 탐색기** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-232">In Visual Studio, open the **Solution Explorer** window.</span></span>
2. <span data-ttu-id="c77dd-233">*myWebApp | 보기 | 홈 | Index.cshtml*로 차례로 이동하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-233">Navigate to and open *myWebApp | Views | Home | Index.cshtml*</span></span>
3. <span data-ttu-id="c77dd-234">다음을 읽으려면 6번째 줄을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-234">Edit line 6 to read:</span></span>

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. <span data-ttu-id="c77dd-235">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-235">Save the file.</span></span>
5. <span data-ttu-id="c77dd-236">**팀 탐색기** 창을 열고 *myWebApp* 프로젝트를 선택한 다음 **변경**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-236">Open the **Team Explorer** window, select the *myWebApp* project, then choose **Changes**.</span></span>
6. <span data-ttu-id="c77dd-237">*CI/CD 파이프라인 테스트*와 같은 커밋 메시지를 입력한 다음 드롭다운 메뉴에서 **모두 커밋 후 동기화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-237">Enter a commit message, such as *Testing CI/CD pipeline*, then choose **Commit All and Sync** from the drop-down menu.</span></span>
7. <span data-ttu-id="c77dd-238">Team Services 작업 영역에서 새 빌드가 코드 커밋에서 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-238">In Team Services workspace, a new build is triggered from the code commit.</span></span> 
    - <span data-ttu-id="c77dd-239">**빌드 및 릴리스**를 선택한 다음 **빌드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-239">Choose **Build & Release**, then select **Builds**.</span></span> 
    - <span data-ttu-id="c77dd-240">빌드 정의를 선택한 다음 **큐에 대기 및 실행** 빌드를 선택하여 빌드 진행 상황을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-240">Choose your build definition, then select the **Queued & running** build to watch as the build progresses.</span></span>
9. <span data-ttu-id="c77dd-241">빌드가 성공되면 새 릴리스가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-241">Once the build is successful, a new release is triggered.</span></span>
    - <span data-ttu-id="c77dd-242">**빌드 및 릴리스**, **릴리스**를 차례로 선택하여 IIS VM에 푸시된 웹 배포 패키지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-242">Choose **Build & Release**, then **Releases** to see the web deploy package pushed to your IIS VM.</span></span> 
    - <span data-ttu-id="c77dd-243">**새로 고침** 아이콘을 선택하여 상태를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-243">Select the **Refresh** icon to update the status.</span></span> <span data-ttu-id="c77dd-244">*환경* 열에 녹색 확인 표시가 있으면 해당 릴리스가 IIS에 성공적으로 배포되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-244">When the *Environments* column shows a green check mark, the release has successfully deployed to IIS.</span></span>
11. <span data-ttu-id="c77dd-245">변경 내용이 적용되었는지 확인하려면 브라우저에서 IIS 웹 사이트를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-245">To see your changes applied, refresh your IIS website in a browser.</span></span>

    ![CI/CD 파이프라인을 통해 IIS VM을 실행 중인 ASP.NET 웹앱](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a><span data-ttu-id="c77dd-247">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c77dd-247">Next steps</span></span>

<span data-ttu-id="c77dd-248">이 자습서에서는 Team Services에서 ASP.NET 웹 응용 프로그램을 만들고, 빌드 및 릴리스 정의를 구성하여 각 코드 커밋에서 새 웹 배포 패키지를 IIS에 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-248">In this tutorial, you created an ASP.NET web application in Team Services and configured build and release definitions to deploy new web deploy packages to IIS on each code commit.</span></span> <span data-ttu-id="c77dd-249">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c77dd-250">Team Services 프로젝트에 ASP.NET 웹 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="c77dd-250">Publish an ASP.NET web application to a Team Services project</span></span>
> * <span data-ttu-id="c77dd-251">코드 커밋으로 트리거되는 빌드 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="c77dd-251">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="c77dd-252">Azure의 가상 컴퓨터에 IIS 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="c77dd-252">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="c77dd-253">Team Services의 배포 그룹에 IIS 인스턴스 추가</span><span class="sxs-lookup"><span data-stu-id="c77dd-253">Add the IIS instance to a deployment group in Team Services</span></span>
> * <span data-ttu-id="c77dd-254">새 웹 배포 패키지를 IIS에 게시하기 위한 릴리스 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="c77dd-254">Create a release definition to publish new web deploy packages to IIS</span></span>
> * <span data-ttu-id="c77dd-255">CI/CD 파이프라인 테스트</span><span class="sxs-lookup"><span data-stu-id="c77dd-255">Test the CI/CD pipeline</span></span>

<span data-ttu-id="c77dd-256">SSL 인증서로 웹 서버를 보호하는 방법에 대해 알아보려면 다음 자습서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c77dd-256">Advance to the next tutorial to learn how to secure a web server with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c77dd-257">SSL로 웹 서버 보호</span><span class="sxs-lookup"><span data-stu-id="c77dd-257">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)