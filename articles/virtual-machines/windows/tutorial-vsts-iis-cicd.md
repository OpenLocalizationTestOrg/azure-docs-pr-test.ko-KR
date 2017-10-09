---
title: "Team Services를 사용 하 여 Azure에서 CI/CD 파이프라인 aaaCreate | Microsoft Docs"
description: "연속 통합 및 Windows VM에서 웹 앱 tooIIS를 배포 하는 배달에 대 한 Visual Studio Team Services toocreate 파이프라인 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: b758a124c4742854dd3b543f747fd8700f954414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a><span data-ttu-id="d826d-103">Visual Studio Team Services 및 IIS를 사용하여 연속 통합 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="d826d-103">Create a continuous integration pipeline with Visual Studio Team Services and IIS</span></span>
<span data-ttu-id="d826d-104">tooautomate hello 빌드, 테스트 및 배포 응용 프로그램 개발 단계를 연속 통합 및 배포 (CI/CD) 파이프라인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-104">tooautomate hello build, test, and deployment phases of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="d826d-105">이 자습서에서는 Visual Studio Team Services 및 IIS를 실행하는 Azure의 Windows VM(가상 컴퓨터)를 사용하여 CI/CD 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-105">In this tutorial, you create a CI/CD pipeline using Visual Studio Team Services and a Windows virtual machine (VM) in Azure that runs IIS.</span></span> <span data-ttu-id="d826d-106">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d826d-107">ASP.NET 웹 응용 프로그램 tooa Team Services 프로젝트를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-107">Publish an ASP.NET web application tooa Team Services project</span></span>
> * <span data-ttu-id="d826d-108">코드 커밋으로 트리거되는 빌드 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="d826d-108">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="d826d-109">Azure의 가상 컴퓨터에 IIS 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="d826d-109">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="d826d-110">Team Services에서 hello IIS 인스턴스 tooa 배포 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-110">Add hello IIS instance tooa deployment group in Team Services</span></span>
> * <span data-ttu-id="d826d-111">릴리스 정의 toopublish 새로운 웹 배포 패키지 tooIIS</span><span class="sxs-lookup"><span data-stu-id="d826d-111">Create a release definition toopublish new web deploy packages tooIIS</span></span>
> * <span data-ttu-id="d826d-112">테스트 hello CI/CD 파이프라인</span><span class="sxs-lookup"><span data-stu-id="d826d-112">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="d826d-113">이 자습서는 Azure PowerShell 모듈 버전 3.6 이상 hello가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="d826d-114">실행 `Get-Module -ListAvailable AzureRM` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-114">Run `Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="d826d-115">Tooupgrade 필요한 경우 참조 [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="create-project-in-team-services"></a><span data-ttu-id="d826d-116">Team Services에서 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="d826d-116">Create project in Team Services</span></span>
<span data-ttu-id="d826d-117">Visual Studio Team Services를 사용하면 온-프레미스 코드 관리 솔루션을 유지 관리하지 않고도 손쉽게 공동 작업하고 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-117">Visual Studio Team Services allows for easy collaboration and development without maintaining an on-premises code management solution.</span></span> <span data-ttu-id="d826d-118">Team Services는 클라우드 코드 테스트, 빌드 및 응용 프로그램 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-118">Team Services provides cloud code testing, build, and application insights.</span></span> <span data-ttu-id="d826d-119">코드 개발에 가장 적합한 버전 제어 리포지토리 및 IDE를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-119">You can choose a version control repo and IDE that best fits your code development.</span></span> <span data-ttu-id="d826d-120">이 자습서에 대 한 무료 계정 toocreate 기본 ASP.NET 웹 응용 프로그램 및 CI/CD 파이프라인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-120">For this tutorial, you can use a free account toocreate a basic ASP.NET web app and CI/CD pipeline.</span></span> <span data-ttu-id="d826d-121">Team Services 계정이 없는 경우 [해당 계정을 만듭니다](http://go.microsoft.com/fwlink/?LinkId=307137).</span><span class="sxs-lookup"><span data-stu-id="d826d-121">If you do not already have a Team Services account, [create one](http://go.microsoft.com/fwlink/?LinkId=307137).</span></span>

<span data-ttu-id="d826d-122">toomanage hello 코드 커밋 프로세스를 빌드 정의 및 정의 해제, Team Services에서 다음과 같이 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-122">toomanage hello code commit process, build definitions, and release definitions, create a project in Team Services as follows:</span></span>

1. <span data-ttu-id="d826d-123">웹 브라우저에서 Team Services 대시보드를 열고 **새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-123">Open your Team Services dashboard in a web browser and choose **New project**.</span></span>
2. <span data-ttu-id="d826d-124">입력 *myWebApp* hello에 대 한 **프로젝트 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-124">Enter *myWebApp* for hello **Project name**.</span></span> <span data-ttu-id="d826d-125">다른 모든 기본 값 toouse 둡니다 *Git* 버전 제어 및 *Agile* 프로세스 작업 항목.</span><span class="sxs-lookup"><span data-stu-id="d826d-125">Leave all other default values toouse *Git* version control and *Agile* work item process.</span></span>
3. <span data-ttu-id="d826d-126">너무 hello 옵션을 선택**공유할** *팀원*을 선택한 후 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-126">Choose hello option too**Share with** *Team Members*, then select **Create**.</span></span>
5. <span data-ttu-id="d826d-127">프로젝트를 만든 후 hello 옵션을 너무 선택**추가 정보 또는 gitignore 초기화**, 다음 **초기화**합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-127">Once your project has been created, choose hello option too**Initialize with a README or gitignore**, then **Initialize**.</span></span>
6. <span data-ttu-id="d826d-128">새 프로젝트를 내부 선택 **대시보드** hello 위쪽 선택 **Visual Studio에서 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-128">Inside your new project, choose **Dashboards** across hello top, then select **Open in Visual Studio**.</span></span>


## <a name="create-aspnet-web-application"></a><span data-ttu-id="d826d-129">ASP.NET 웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="d826d-129">Create ASP.NET web application</span></span>
<span data-ttu-id="d826d-130">Hello 이전 단계에서 Team Services에서 프로젝트를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-130">In hello previous step, you created a project in Team Services.</span></span> <span data-ttu-id="d826d-131">hello 최종 단계는 Visual Studio에서 새 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-131">hello final step opens your new project in Visual Studio.</span></span> <span data-ttu-id="d826d-132">사용자 코드 커밋 hello에 관리 **팀 탐색기** 창.</span><span class="sxs-lookup"><span data-stu-id="d826d-132">You manage your code commits in hello **Team Explorer** window.</span></span> <span data-ttu-id="d826d-133">새 프로젝트의 로컬 복사본을 만든 다음 템플릿에서 다음과 같이 ASP.NET 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-133">Create a local copy of your new project, then create an ASP.NET web application from a template as follows:</span></span>

1. <span data-ttu-id="d826d-134">선택 **복제** toocreate Team Services 프로젝트의 로컬 git 리포지토리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-134">Select **Clone** toocreate a local git repo of your Team Services project.</span></span>
    
    ![Team Services 프로젝트에서 리포지토리 복제](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. <span data-ttu-id="d826d-136">**솔루션**에서 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-136">Under **Solutions**, select **New**.</span></span>

    ![웹 응용 프로그램 솔루션 만들기](media/tutorial-vsts-iis-cicd/new_solution.png)

3. <span data-ttu-id="d826d-138">선택 **웹** 템플릿 hello 선택 **ASP.NET 웹 응용 프로그램** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="d826d-138">Select **Web** templates, and then choose hello **ASP.NET Web Application** template.</span></span>
    1. <span data-ttu-id="d826d-139">같은 응용 프로그램에 대 한 이름을 입력 *myWebApp*에 대 한 hello 확인란의 선택을 취소 하 고 **솔루션용 디렉터리 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-139">Enter a name for your application, such as *myWebApp*, and uncheck hello box for **Create directory for solution**.</span></span>
    2. <span data-ttu-id="d826d-140">Hello 옵션을 사용할 수 있는 경우 확인란의 선택을 취소 hello 너무**Application Insights 추가 tooproject**합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-140">If hello option is available, uncheck hello box too**Add Application Insights tooproject**.</span></span> <span data-ttu-id="d826d-141">Application Insights 있습니다 tooauthorize Azure Application Insights를 사용한 웹 응용 프로그램 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-141">Application Insights requires you tooauthorize your web application with Azure Application Insights.</span></span> <span data-ttu-id="d826d-142">tookeep이이 자습서에서는 간단한 것이 프로세스를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-142">tookeep it simple in this tutorial, skip this process.</span></span>
    3. <span data-ttu-id="d826d-143">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-143">Select **OK**.</span></span>
4. <span data-ttu-id="d826d-144">선택 **MVC** hello 템플릿 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-144">Choose **MVC** from hello template list.</span></span>
    1. <span data-ttu-id="d826d-145">**인증 변경**을 선택하고 **인증 없음**을 선택한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-145">Select **Change Authentication**, choose **No Authentication**, then select **OK**.</span></span>
    2. <span data-ttu-id="d826d-146">선택 **확인** toocreate 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-146">Select **OK** toocreate your solution.</span></span>
5. <span data-ttu-id="d826d-147">Hello에 **팀 탐색기** 창 선택 **변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-147">In hello **Team Explorer** window, choose **Changes**.</span></span>

    ![TooTeam 서비스 git 리포지토리에 있는 로컬 변경 내용 커밋](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. <span data-ttu-id="d826d-149">Hello 커밋 텍스트 상자에를 입력 메시지와 같은 *초기 커밋*합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-149">In hello commit text box, enter a message such as *Initial commit*.</span></span> <span data-ttu-id="d826d-150">선택 **모든 커밋 및 동기화** hello 드롭 다운 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-150">Choose **Commit All and Sync** from hello drop-down menu.</span></span>


## <a name="create-build-definition"></a><span data-ttu-id="d826d-151">빌드 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="d826d-151">Create build definition</span></span>
<span data-ttu-id="d826d-152">Team Services 응용 프로그램을 작성 해야 하는 방법을 빌드 정의 toooutline를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-152">In Team Services, you use a build definition toooutline how your application should be built.</span></span> <span data-ttu-id="d826d-153">이 자습서에서는 코드 hello 솔루션을 빌드합니다 다음 웹을 만듭니다는 toorun hello 웹 응용 프로그램 IIS 서버에서 사용할 수 패키지를 배포 하는 기본 정의 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-153">In this tutorial, we create a basic definition that takes our source code, builds hello solution, then creates web deploy package we can use toorun hello web app on an IIS server.</span></span>

1. <span data-ttu-id="d826d-154">Team Services 프로젝트에서 선택 **빌드 및 릴리스** hello 위쪽 선택 **빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-154">In your Team Services project, choose **Build & Release** across hello top, then select **Builds**.</span></span>
3. <span data-ttu-id="d826d-155">**+ 새 정의**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-155">Select **+ New definition**.</span></span>
4. <span data-ttu-id="d826d-156">Hello 선택 **ASP.NET (미리 보기)** 템플릿과 선택 **적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-156">Choose hello **ASP.NET (PREVIEW)** template and select **Apply**.</span></span>
5. <span data-ttu-id="d826d-157">작업의 값 모두 hello 기본값을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-157">Leave all hello default task values.</span></span> <span data-ttu-id="d826d-158">아래 **원본을 가져올**, 해당 hello 확인 *myWebApp* 리포지토리 및 *마스터* 분기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-158">Under **Get sources**, ensure that hello *myWebApp* repository and *master* branch are selected.</span></span>

    ![Team Services 프로젝트에서 빌드 정의 만들기](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. <span data-ttu-id="d826d-160">Hello에 **트리거** 탭에 대 한 hello 슬라이더를 이동, **이 트리거를 사용 하도록 설정** 너무*Enabled*합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-160">On hello **Triggers** tab, move hello slider for **Enable this trigger** too*Enabled*.</span></span>
7. <span data-ttu-id="d826d-161">Hello 빌드 정 및 큐를 선택 하 여 새 빌드 저장 **저장 후 큐** , 다음 **저장 후 큐** 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-161">Save hello build definition and queue a new build by selecting **Save & queue** , then **Save & queue** again.</span></span> <span data-ttu-id="d826d-162">선택한 hello 기본값 그대로 두고 **큐**합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-162">Leave hello defaults and select **Queue**.</span></span>

<span data-ttu-id="d826d-163">조사식은 hello 빌드 호스트 된 에이전트에서 예약 된 다음 toobuild을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-163">Watch as hello build is scheduled on a hosted agent, then begins toobuild.</span></span> <span data-ttu-id="d826d-164">hello 비슷한 toohello 다음은 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="d826d-164">hello output is similar toohello following example:</span></span>

![성공적인 Team Services 프로젝트 빌드](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a><span data-ttu-id="d826d-166">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="d826d-166">Create virtual machine</span></span>
<span data-ttu-id="d826d-167">플랫폼 toorun tooprovide ASP.NET 웹 응용 프로그램 IIS를 실행 하는 Windows 가상 컴퓨터 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-167">tooprovide a platform toorun your ASP.NET web app, you need a Windows virtual machine that runs IIS.</span></span> <span data-ttu-id="d826d-168">Team Services 코드를 커밋합니다 및 빌드 트리거되는으로 hello IIS 인스턴스와 에이전트 toointeract를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-168">Team Services uses an agent toointeract with hello IIS instance as you commit code and builds are triggered.</span></span>

<span data-ttu-id="d826d-169">[이 스크립트 샘플](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json)을 사용하여 Windows Server 2016 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-169">Create a Windows Server 2016 VM using [this script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span></span> <span data-ttu-id="d826d-170">Hello 스크립트 toorun 몇 분 정도 걸리며 hello VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-170">It takes a few minutes for hello script toorun and create hello VM.</span></span> <span data-ttu-id="d826d-171">Hello VM을 만든 후에 웹 트래픽에 대해 포트 80을 열고 [추가 AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-171">Once hello VM has been created, open port 80 for web traffic with [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) as follows:</span></span>

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

<span data-ttu-id="d826d-172">tooconnect tooyour VM을 hello와 공용 IP 주소를 가져올 [Get AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-172">tooconnect tooyour VM, obtain hello public IP address with [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) as follows:</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

<span data-ttu-id="d826d-173">원격 데스크톱 세션 tooyour VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-173">Create a remote desktop session tooyour VM:</span></span>

```cmd
mstsc /v:<publicIpAddress>
```

<span data-ttu-id="d826d-174">Hello VM에서 열고는 **관리자 PowerShell** 명령 프롬프트입니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-174">On hello VM, open an **Administrator PowerShell** command prompt.</span></span> <span data-ttu-id="d826d-175">다음과 같이 IIS 및 필요한 .NET 기능을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-175">Install IIS and required .NET features as follows:</span></span>

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a><span data-ttu-id="d826d-176">배포 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="d826d-176">Create deployment group</span></span>
<span data-ttu-id="d826d-177">hello 웹 아웃 toopush 패키지 toohello IIS 서버를 배포 하 고 Team Services에서 배포 그룹을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-177">toopush out hello web deploy package toohello IIS server, you define a deployment group in Team Services.</span></span> <span data-ttu-id="d826d-178">이 그룹을 커밋하 코드 tooTeam 서비스 및 빌드 완료 된 서버를 새 빌드 hello 대상 toospecify가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-178">This group allows you toospecify which servers are hello target of new builds as you commit code tooTeam Services and builds are completed.</span></span>

1. <span data-ttu-id="d826d-179">Team Services에서 **빌드 및 릴리스**를 선택한 다음 **배포 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-179">In Team Services, choose **Build & Release** and then select **Deployment groups**.</span></span>
2. <span data-ttu-id="d826d-180">**배포 그룹 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-180">Choose **Add Deployment group**.</span></span>
3. <span data-ttu-id="d826d-181">같은 hello 그룹에 대 한 이름을 입력 *myIIS*을 선택한 후 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-181">Enter a name for hello group, such as *myIIS*, then select **Create**.</span></span>
4. <span data-ttu-id="d826d-182">Hello에 **컴퓨터 등록** 섹션에서 확인 *Windows* 을 선택 하면 hello 확인란 너무**hello 스크립트의 개인용 액세스 토큰을 사용 하 여 인증에 대 한**합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-182">In hello **Register machines** section, ensure *Windows* is selected, then check hello box too**Use a personal access token in hello script for authentication**.</span></span>
5. <span data-ttu-id="d826d-183">선택 **스크립트 tooclipboard 복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-183">Select **Copy script tooclipboard**.</span></span>


### <a name="add-iis-vm-toohello-deployment-group"></a><span data-ttu-id="d826d-184">IIS VM toohello 배포 그룹 추가</span><span class="sxs-lookup"><span data-stu-id="d826d-184">Add IIS VM toohello deployment group</span></span>
<span data-ttu-id="d826d-185">Hello 배포 그룹을 만든에 각 IIS 인스턴스 toohello 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-185">With hello deployment group created, add each IIS instance toohello group.</span></span> <span data-ttu-id="d826d-186">다운로드 하 고 새 웹을 수신 하는 VM을 배포 하는 hello에 에이전트를 구성 하는 스크립트를 생성 하는 team Services를 패키지 한 다음 tooIIS 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-186">Team Services generates a script that downloads and configures an agent on hello VM that receives new web deploy packages then applies it tooIIS.</span></span>

1. <span data-ttu-id="d826d-187">Hello에 다시 **관리자 PowerShell** 세션 VM에 붙여 넣고 Team Services에서 복사 하는 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-187">Back in hello **Administrator PowerShell** session on your VM, paste and run hello script copied from Team Services.</span></span>
2. <span data-ttu-id="d826d-188">Hello 에이전트에 대 한 증명된 tooconfigure 태그 선택 하는 경우 *Y* 입력 *웹*합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-188">When prompted tooconfigure tags for hello agent, choose *Y* and enter *web*.</span></span>
3. <span data-ttu-id="d826d-189">Hello 사용자 계정에 대 한 메시지가 표시 되 면 키를 눌러 *반환* tooaccept hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-189">When prompted for hello user account, press *Return* tooaccept hello defaults.</span></span>
4. <span data-ttu-id="d826d-190">메시지와 함께 hello 스크립트 toofinish 대기 *서비스 vstsagent.account.computername 성공적으로 시작*합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-190">Wait for hello script toofinish with a message *Service vstsagent.account.computername started successfully*.</span></span>
5. <span data-ttu-id="d826d-191">Hello에 **배포 그룹** hello 페이지 **빌드 및 릴리스** 메뉴를 열고 hello *myIIS* 배포 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-191">In hello **Deployment groups** page of hello **Build & Release** menu, open hello *myIIS* deployment group.</span></span> <span data-ttu-id="d826d-192">Hello에 **컴퓨터** 탭 VM이 나열 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-192">On hello **Machines** tab, verify that your VM is listed.</span></span>

    ![VM은 tooTeam 서비스 배포 그룹을 성공적으로 추가](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a><span data-ttu-id="d826d-194">릴리스 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="d826d-194">Create release definition</span></span>
<span data-ttu-id="d826d-195">toopublish Team Services에서 릴리스 정의 만든 빌드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-195">toopublish your builds, you create a release definition in Team Services.</span></span> <span data-ttu-id="d826d-196">응용 프로그램을 성공적으로 빌드하면 이 정의가 자동으로 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-196">This definition is triggered automatically by a successful build of your application.</span></span> <span data-ttu-id="d826d-197">Hello 배포 그룹 toopush 웹 배포 패키지를, 선택한 hello 적절 한 IIS 설정을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-197">You choose hello deployment group toopush your web deploy package to, and define hello appropriate IIS settings.</span></span>

1. <span data-ttu-id="d826d-198">**빌드 및 릴리스**를 선택한 다음 **빌드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-198">Choose **Build & Release**, then select **Builds**.</span></span> <span data-ttu-id="d826d-199">이전 단계에서 만든 hello 빌드 정의 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-199">Choose hello build definition created in a previous step.</span></span>
2. <span data-ttu-id="d826d-200">아래 **최근에 완료 된**를 hello 최신 빌드를 선택한 다음 선택 **릴리스**합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-200">Under **Recently completed**, choose hello most recent build, then select **Release**.</span></span>
3. <span data-ttu-id="d826d-201">선택 **예** toocreate 릴리스 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-201">Choose **Yes** toocreate a release definition.</span></span>
4. <span data-ttu-id="d826d-202">Hello 선택 **빈** 서식 파일을 다음 선택 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-202">Choose hello **Empty** template, then select **Next**.</span></span>
5. <span data-ttu-id="d826d-203">프로젝트를 프로젝트 및 소스 빌드 정의 hello 채워져 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-203">Verify hello project and source build definition are populated with your project.</span></span>
6. <span data-ttu-id="d826d-204">선택 hello **연속 배포** 확인란을 선택한 다음 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-204">Select hello **Continuous deployment** check box, then select **Create**.</span></span>
7. <span data-ttu-id="d826d-205">다음 너무 hello 드롭다운 상자를 선택**작업 추가 +** 선택 *배포 그룹 단계 추가*합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-205">Select hello drop-down box next too**+ Add tasks** and choose *Add a deployment group phase*.</span></span>
    
    ![Team Services에서 작업 toorelease 정의 추가 합니다.](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. <span data-ttu-id="d826d-207">선택 **추가** 다음 너무**IIS 웹 응용 프로그램 Deploy(Preview)**을 선택한 후 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-207">Choose **Add** next too**IIS Web App Deploy(Preview)**, then select **Close**.</span></span>
9. <span data-ttu-id="d826d-208">선택 hello **배포 그룹에서 실행** 부모 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-208">Select hello **Run on deployment group** parent task.</span></span>
    1. <span data-ttu-id="d826d-209">에 대 한 **배포 그룹**선택, hello 배포 그룹 등 이전에 만든 *myIIS*합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-209">For **Deployment Group**, select hello deployment group you created earlier, such as *myIIS*.</span></span>
    2. <span data-ttu-id="d826d-210">Hello에 **태그 컴퓨터** 상자 선택 **추가** hello 선택 *웹* 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-210">In hello **Machine tags** box, select **Add** and choose hello *web* tag.</span></span>
    
    ![IIS용 정의 배포 그룹 작업 릴리스](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. <span data-ttu-id="d826d-212">선택 hello **배포: IIS 웹 응용 프로그램 배포** 작업 tooconfigure IIS 설정을 다음과 같이 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="d826d-212">Select hello **Deploy: IIS Web App Deploy** task tooconfigure your IIS instance settings as follows:</span></span>
    1. <span data-ttu-id="d826d-213">**웹 사이트 이름**에서 *기본 웹 사이트*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-213">For **Website Name**, enter *Default Web Site*.</span></span>
    2. <span data-ttu-id="d826d-214">모든 hello 다른 기본 설정을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-214">Leave all hello other default settings.</span></span>
12. <span data-ttu-id="d826d-215">**저장**을 선택한 다음 **확인**을 두 번 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-215">Choose **Save**, then select **OK** twice.</span></span>


## <a name="create-a-release-and-publish"></a><span data-ttu-id="d826d-216">릴리스 만들기 및 게시</span><span class="sxs-lookup"><span data-stu-id="d826d-216">Create a release and publish</span></span>
<span data-ttu-id="d826d-217">이제 웹 배포 패키지를 새 릴리스로 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-217">You can now push your web deploy package as a new release.</span></span> <span data-ttu-id="d826d-218">이 단계는 hello 배포 그룹의 일부인, hello 웹 푸시 각 인스턴스에서 hello 에이전트와 통신 패키지를 배포한 다음 IIS toorun 업데이트 hello 웹 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-218">This step communicates with hello agent on each instance that is part of hello deployment group, pushes hello web deploy package, then configures IIS toorun hello updated web application.</span></span>

1. <span data-ttu-id="d826d-219">릴리스 정의에서 **+ 릴리스**를 선택한 다음 **릴리스 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-219">In your release definition, select **+ Release**, then choose **Create Release**.</span></span>
2. <span data-ttu-id="d826d-220">와 함께 hello 최신 빌드 hello 드롭 다운 목록에서 선택 되어 있는지 확인 **자동 배포: 릴리스 생성 이후**합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-220">Verify that hello latest build is selected in hello drop-down list, along with **Automated deployment: After release creation**.</span></span> <span data-ttu-id="d826d-221">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-221">Select **Create**.</span></span>
3. <span data-ttu-id="d826d-222">작은 배너를 표시 하려면 릴리스 정의의 hello 위쪽와 같은 *' 릴리스 1' 릴리스를 만든*합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-222">A small banner appears across hello top of your release definition, such as *Release 'Release-1' has been created*.</span></span> <span data-ttu-id="d826d-223">선택 hello 릴리스 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-223">Select hello release link.</span></span>
4. <span data-ttu-id="d826d-224">열기 hello **로그** toowatch hello 릴리스 진행률을 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-224">Open hello **Logs** tab toowatch hello release progress.</span></span>
    
    ![성공적인 Team Services 릴리스 및 웹 배포 패키지 푸시](media/tutorial-vsts-iis-cicd/successful_release.png)

5. <span data-ttu-id="d826d-226">Hello 릴리스 완료 되 면 웹 브라우저를 열고 하 고 VM의 hello 공용 IIP 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-226">After hello release is complete, open a web browser and enter hello public IIP address of your VM.</span></span> <span data-ttu-id="d826d-227">ASP.NET 웹 응용 프로그램이 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-227">Your ASP.NET web application is running.</span></span>

    ![IIS VM에서 실행 중인 ASP.NET 웹앱](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-hello-whole-cicd-pipeline"></a><span data-ttu-id="d826d-229">테스트 hello 전체 CI/CD 파이프라인</span><span class="sxs-lookup"><span data-stu-id="d826d-229">Test hello whole CI/CD pipeline</span></span>
<span data-ttu-id="d826d-230">IIS에서 실행 중인 웹 응용 프로그램을 지금 hello 전체 CI/CD 파이프라인을 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d826d-230">With your web application running on IIS, now try hello whole CI/CD pipeline.</span></span> <span data-ttu-id="d826d-231">Visual Studio와 다음 업데이트 된 웹 릴리스를 트리거하는 코드를 빌드 트리거되는 커밋 변경한 후 배포 패키지 tooIIS:</span><span class="sxs-lookup"><span data-stu-id="d826d-231">After you make a change in Visual Studio and commit your code, a build is triggered which then triggers a release of your updated web deploy package tooIIS:</span></span>

1. <span data-ttu-id="d826d-232">Visual Studio에서 열고 hello **솔루션 탐색기** 창.</span><span class="sxs-lookup"><span data-stu-id="d826d-232">In Visual Studio, open hello **Solution Explorer** window.</span></span>
2. <span data-ttu-id="d826d-233">Tooand 열기 이동 *myWebApp | 뷰 | 홈 | Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="d826d-233">Navigate tooand open *myWebApp | Views | Home | Index.cshtml*</span></span>
3. <span data-ttu-id="d826d-234">6 행 tooread를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-234">Edit line 6 tooread:</span></span>

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. <span data-ttu-id="d826d-235">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-235">Save hello file.</span></span>
5. <span data-ttu-id="d826d-236">열기 hello **팀 탐색기** 창, 선택 hello *myWebApp* 프로젝트를 선택한 다음 선택 **변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-236">Open hello **Team Explorer** window, select hello *myWebApp* project, then choose **Changes**.</span></span>
6. <span data-ttu-id="d826d-237">커밋 메시지를 같은 입력 *테스트 CI/CD 파이프라인*를 눌러 **커밋 모든 및 동기화** hello 드롭 다운 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-237">Enter a commit message, such as *Testing CI/CD pipeline*, then choose **Commit All and Sync** from hello drop-down menu.</span></span>
7. <span data-ttu-id="d826d-238">Team Services 작업 영역에서 새 빌드 hello 코드 커밋이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-238">In Team Services workspace, a new build is triggered from hello code commit.</span></span> 
    - <span data-ttu-id="d826d-239">**빌드 및 릴리스**를 선택한 다음 **빌드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-239">Choose **Build & Release**, then select **Builds**.</span></span> 
    - <span data-ttu-id="d826d-240">차례로 hello를 선택한 다음 빌드 정의 선택 **실행 및 큐 대기** hello로 빌드 toowatch 빌드 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-240">Choose your build definition, then select hello **Queued & running** build toowatch as hello build progresses.</span></span>
9. <span data-ttu-id="d826d-241">Hello 빌드에 성공 후 새 릴리스가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-241">Once hello build is successful, a new release is triggered.</span></span>
    - <span data-ttu-id="d826d-242">선택 **빌드 및 릴리스**, 다음 **릴리스** toosee hello 웹 배포 패키지 tooyour IIS VM 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-242">Choose **Build & Release**, then **Releases** toosee hello web deploy package pushed tooyour IIS VM.</span></span> 
    - <span data-ttu-id="d826d-243">선택 hello **새로 고침** 아이콘 tooupdate hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-243">Select hello **Refresh** icon tooupdate hello status.</span></span> <span data-ttu-id="d826d-244">Hello 때 *환경* 열에 녹색 확인 표시가 표시, hello 릴리스가 tooIIS 성공적으로 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-244">When hello *Environments* column shows a green check mark, hello release has successfully deployed tooIIS.</span></span>
11. <span data-ttu-id="d826d-245">toosee 변경 내용을 적용 되며, 브라우저에서 IIS 웹 사이트를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-245">toosee your changes applied, refresh your IIS website in a browser.</span></span>

    ![CI/CD 파이프라인을 통해 IIS VM을 실행 중인 ASP.NET 웹앱](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a><span data-ttu-id="d826d-247">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d826d-247">Next steps</span></span>

<span data-ttu-id="d826d-248">이 자습서에서는 Team Services에서 ASP.NET 웹 응용 프로그램을 생성 하 고 구성 된 빌드 및 릴리스 정의 toodeploy 새 웹 배포 패키지 tooIIS 각 코드 커밋에 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-248">In this tutorial, you created an ASP.NET web application in Team Services and configured build and release definitions toodeploy new web deploy packages tooIIS on each code commit.</span></span> <span data-ttu-id="d826d-249">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d826d-250">ASP.NET 웹 응용 프로그램 tooa Team Services 프로젝트를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-250">Publish an ASP.NET web application tooa Team Services project</span></span>
> * <span data-ttu-id="d826d-251">코드 커밋으로 트리거되는 빌드 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="d826d-251">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="d826d-252">Azure의 가상 컴퓨터에 IIS 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="d826d-252">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="d826d-253">Team Services에서 hello IIS 인스턴스 tooa 배포 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-253">Add hello IIS instance tooa deployment group in Team Services</span></span>
> * <span data-ttu-id="d826d-254">릴리스 정의 toopublish 새로운 웹 배포 패키지 tooIIS</span><span class="sxs-lookup"><span data-stu-id="d826d-254">Create a release definition toopublish new web deploy packages tooIIS</span></span>
> * <span data-ttu-id="d826d-255">테스트 hello CI/CD 파이프라인</span><span class="sxs-lookup"><span data-stu-id="d826d-255">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="d826d-256">다음 자습서 toolearn toohello 어떻게 발전 toosecure 웹 서버 SSL 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d826d-256">Advance toohello next tutorial toolearn how toosecure a web server with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d826d-257">SSL로 웹 서버 보안</span><span class="sxs-lookup"><span data-stu-id="d826d-257">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)