---
title: "Azure 웹 앱에 대 한 리소스 관리자 기반 PowerShell aaaAzure 명령을 | Microsoft Docs"
description: "어떻게 toouse hello 새 Azure 리소스 관리자 기반 PowerShell 명령을 toomanage Azure 웹 앱에 알아봅니다."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 4231fbba-61e5-4f92-b958-531c066fb87f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: bbb821e89daa315280436e84e11316217bb644d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-powershell-toomanage-azure-web-apps"></a><span data-ttu-id="98137-103">Azure Resource Manager-Based PowerShell tooManage Azure 웹 앱을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="98137-103">Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="98137-104">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="98137-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="98137-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="98137-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

<span data-ttu-id="98137-106">Microsoft Azure powershell 버전 1.0.0 새로운 명령이 추가 된 hello 사용자 hello 기능 toouse Azure 리소스 관리자 기반 PowerShell 명령을 toomanage 웹 응용 프로그램을 제공 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="98137-106">With Microsoft Azure PowerShell version 1.0.0 new commands have been added, that give hello user hello ability toouse Azure Resource Manager-based PowerShell commands toomanage Web Apps.</span></span>

<span data-ttu-id="98137-107">리소스 그룹을 관리 하는 방법에 대 한 toolearn 참조 [Azure PowerShell 사용 하 여 Azure 리소스 관리자와](../powershell-azure-resource-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="98137-107">toolearn about managing Resource Groups, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span> 

<span data-ttu-id="98137-108">매개 변수 및 hello PowerShell cmdlet에 대 한 옵션의 전체 목록 hello에 대 한 toolearn hello 참조 [전체 웹 앱 Azure 리소스 관리자 기반 PowerShell Cmdlet의 Cmdlet 참조](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="98137-108">toolearn about hello full list of parameters and options for hello PowerShell cmdlets, see hello [full Cmdlet Reference of Web App Azure Resource Manager-based PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>

## <a name="managing-app-service-plans"></a><span data-ttu-id="98137-109">앱 서비스 계획 관리</span><span class="sxs-lookup"><span data-stu-id="98137-109">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="98137-110">앱 서비스 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="98137-110">Create an App Service Plan</span></span>
<span data-ttu-id="98137-111">앱 서비스 계획을 toocreate hello를 사용 하 여 **새로 AzureRmAppServicePlan** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="98137-111">toocreate an app service plan, use hello **New-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="98137-112">다음은 hello 다른 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="98137-112">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="98137-113">**이름**: hello 앱 서비스 계획의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="98137-113">**Name**: name of hello app service plan.</span></span>
* <span data-ttu-id="98137-114">**Location**: 서비스 계획 위치.</span><span class="sxs-lookup"><span data-stu-id="98137-114">**Location**: service plan location.</span></span>
* <span data-ttu-id="98137-115">**ResourceGroupName**: 새로 만든 hello 앱 서비스 계획을 포함 하는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="98137-115">**ResourceGroupName**: resource group that includes hello newly created app service plan.</span></span>
* <span data-ttu-id="98137-116">**계층**: hello 가격 책정 계층을 원하는 (기본값은 무료, 공유, Basic, Standard 및 Premium 다른 옵션은)</span><span class="sxs-lookup"><span data-stu-id="98137-116">**Tier**:  hello desired pricing tier (Default is Free, other options are Shared, Basic, Standard, and Premium.)</span></span>
* <span data-ttu-id="98137-117">**WorkerSize**: hello (기본값은 작은 경우 Basic, Standard 또는 Premium으로 hello 계층 매개 변수가 지정 되었습니다 작업자의 크기.</span><span class="sxs-lookup"><span data-stu-id="98137-117">**WorkerSize**: hello size of workers (Default is small if hello Tier parameter was specified as Basic, Standard, or Premium.</span></span> <span data-ttu-id="98137-118">다른 옵션은 Medium 및 Large입니다.)</span><span class="sxs-lookup"><span data-stu-id="98137-118">Other options are Medium, and Large.)</span></span>
* <span data-ttu-id="98137-119">**작업자**: (기본값은 1) hello 앱 서비스 계획의 작업자 수가 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="98137-119">**NumberofWorkers**: hello number of workers in hello app service plan (Default value is 1).</span></span> 

<span data-ttu-id="98137-120">예제 toouse이이 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="98137-120">Example toouse this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a><span data-ttu-id="98137-121">앱 서비스 환경에서 앱 서비스 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="98137-121">Create an App Service Plan in an App Service Environment</span></span>
<span data-ttu-id="98137-122">앱 서비스 환경에 toocreate 앱 서비스 계획, 사용 하 여 hello 동일 명령 **새로 AzureRmAppServicePlan** toospecify hello ASE의 추가 매개 변수 이름과 ASE의 리소스 그룹 이름을 가진 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="98137-122">toocreate an app service plan in an app service environment, use hello same command **New-AzureRmAppServicePlan** command with extra parameters toospecify hello ASE's name and ASE's resource group name.</span></span>

<span data-ttu-id="98137-123">예제 toouse이이 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="98137-123">Example toouse this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

<span data-ttu-id="98137-124">앱 서비스 환경을 검사 하는 방법에 대 한 자세한 toolearn [소개 tooApp 서비스 환경](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="98137-124">toolearn more about app service environment, check [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="98137-125">기존 앱 서비스 계획 나열</span><span class="sxs-lookup"><span data-stu-id="98137-125">List Existing App Service Plans</span></span>
<span data-ttu-id="98137-126">toolist hello 기존 앱 서비스 계획을 사용 하 여 **Get AzureRmAppServicePlan** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="98137-126">toolist hello existing app service plans, use **Get-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="98137-127">toolist 모든 앱 서비스 계획에서 구독을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98137-127">toolist all app service plans under your subscription, use:</span></span> 

    Get-AzureRmAppServicePlan

<span data-ttu-id="98137-128">toolist 특정 리소스 그룹 아래의 모든 앱 서비스 계획을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98137-128">toolist all app service plans under a specific resource group, use:</span></span>

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="98137-129">tooget 특정 앱 서비스 계획을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98137-129">tooget a specific app service plan, use:</span></span>

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="98137-130">기존 앱 서비스 계획 구성</span><span class="sxs-lookup"><span data-stu-id="98137-130">Configure an existing App Service Plan</span></span>
<span data-ttu-id="98137-131">기존 앱 서비스 계획에 대 한 toochange hello 설정을 사용 하 여 hello **집합 AzureRmAppServicePlan** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="98137-131">toochange hello settings for an existing app service plan, use hello **Set-AzureRmAppServicePlan** cmdlet.</span></span> <span data-ttu-id="98137-132">Hello 계층, 작업자 크기 및 hello 작업자 수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98137-132">You can change hello tier, worker size, and hello number of workers</span></span> 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="98137-133">앱 서비스 계획 크기 조정</span><span class="sxs-lookup"><span data-stu-id="98137-133">Scaling an App Service Plan</span></span>
<span data-ttu-id="98137-134">tooscale는 기존 앱 서비스 계획을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98137-134">tooscale an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-hello-worker-size-of-an-app-service-plan"></a><span data-ttu-id="98137-135">앱 서비스 계획의 hello 작업자 크기를 변경</span><span class="sxs-lookup"><span data-stu-id="98137-135">Changing hello worker size of an App Service Plan</span></span>
<span data-ttu-id="98137-136">기존 앱 서비스 계획을 사용 하 여 작업자의 toochange hello 크기:</span><span class="sxs-lookup"><span data-stu-id="98137-136">toochange hello size of workers in an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-hello-tier-of-an-app-service-plan"></a><span data-ttu-id="98137-137">앱 서비스 계획의 계층 hello 변경</span><span class="sxs-lookup"><span data-stu-id="98137-137">Changing hello Tier of an App Service Plan</span></span>
<span data-ttu-id="98137-138">기존 앱 서비스 계획을 사용 하 여의 toochange hello 계층:</span><span class="sxs-lookup"><span data-stu-id="98137-138">toochange hello tier of an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="98137-139">기존 앱 서비스 계획 삭제</span><span class="sxs-lookup"><span data-stu-id="98137-139">Delete an existing App Service Plan</span></span>
<span data-ttu-id="98137-140">기존 앱 서비스 계획 toodelete 모두 할당 됨 웹 앱 필요 toobe 이동 하거나 먼저 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="98137-140">toodelete an existing app service plan, all assigned web apps need toobe moved or deleted first.</span></span> <span data-ttu-id="98137-141">그런 다음 hello를 사용 하 여 **제거 AzureRmAppServicePlan** cmdlet hello 앱 서비스 계획을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98137-141">Then using hello **Remove-AzureRmAppServicePlan** cmdlet you can delete hello app service plan.</span></span>

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a><span data-ttu-id="98137-142">앱 서비스 웹앱 관리</span><span class="sxs-lookup"><span data-stu-id="98137-142">Managing App Service Web Apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="98137-143">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="98137-143">Create a Web App</span></span>
<span data-ttu-id="98137-144">toocreate 웹 응용 프로그램에서 사용 하 여 hello **새로 AzureRmWebApp** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="98137-144">toocreate a web app, use hello **New-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="98137-145">다음은 hello 다른 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="98137-145">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="98137-146">**이름**: hello 웹 앱에 대 한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="98137-146">**Name**: name for hello web app.</span></span>
* <span data-ttu-id="98137-147">**AppServicePlan**: toohost hello 웹 응용 프로그램을 사용 하는 hello 서비스 계획에 대 한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98137-147">**AppServicePlan**: name for hello service plan used toohost hello web app.</span></span>
* <span data-ttu-id="98137-148">**ResourceGroupName**: hello 앱 서비스 계획을 호스팅하는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="98137-148">**ResourceGroupName**: resource group that hosts hello App service plan.</span></span>
* <span data-ttu-id="98137-149">**위치**: 웹 앱 위치의 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="98137-149">**Location**: hello web app location.</span></span>

<span data-ttu-id="98137-150">예제 toouse이이 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="98137-150">Example toouse this cmdlet:</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a><span data-ttu-id="98137-151">App Service Environment에서 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="98137-151">Create a Web App in an App Service Environment</span></span>
<span data-ttu-id="98137-152">앱 서비스 환경 (ASE)에서 웹 앱 toocreate 합니다.</span><span class="sxs-lookup"><span data-stu-id="98137-152">toocreate a web app in an App Service Environment (ASE).</span></span> <span data-ttu-id="98137-153">사용 하 여 hello 동일 **새로 AzureRmWebApp** 명령에 추가 매개 변수 toospecify hello ASE 이름 및 hello ASE에 속하는 hello 리소스 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="98137-153">Use hello same **New-AzureRmWebApp** command with extra parameters toospecify hello ASE name and hello resource group name that hello ASE belongs to.</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

<span data-ttu-id="98137-154">앱 서비스 환경을 검사 하는 방법에 대 한 자세한 toolearn [소개 tooApp 서비스 환경](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="98137-154">toolearn more about app service environment, check [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="delete-an-existing-web-app"></a><span data-ttu-id="98137-155">기존 웹앱 삭제</span><span class="sxs-lookup"><span data-stu-id="98137-155">Delete an existing Web App</span></span>
<span data-ttu-id="98137-156">toodelete hello를 사용할 수는 기존 웹 응용 프로그램 **제거 AzureRmWebApp** cmdlet toospecify hello hello 웹 응용 프로그램의 이름과 hello 리소스 그룹 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="98137-156">toodelete an existing web app you can use hello **Remove-AzureRmWebApp** cmdlet, you need toospecify hello name of hello web app and hello resource group name.</span></span>

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a><span data-ttu-id="98137-157">기존 웹앱 나열</span><span class="sxs-lookup"><span data-stu-id="98137-157">List existing Web Apps</span></span>
<span data-ttu-id="98137-158">toolist hello 기존 웹 응용 프로그램을 사용 하 여 hello **Get AzureRmWebApp** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="98137-158">toolist hello existing web apps, use hello **Get-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="98137-159">toolist 구독 아래의 모든 웹 앱을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98137-159">toolist all web apps under your subscription, use:</span></span>

    Get-AzureRmWebApp

<span data-ttu-id="98137-160">toolist 특정 리소스 그룹 아래의 모든 웹 앱을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98137-160">toolist all web apps under a specific resource group, use:</span></span>

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="98137-161">tooget 특정 웹 앱을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98137-161">tooget a specific web app, use:</span></span>

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a><span data-ttu-id="98137-162">기존 웹앱 구성</span><span class="sxs-lookup"><span data-stu-id="98137-162">Configure an existing Web App</span></span>
<span data-ttu-id="98137-163">toochange hello 설정 및 기존 웹 응용 프로그램에 대 한 구성을 사용 하 여 hello **집합 AzureRmWebApp** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="98137-163">toochange hello settings and configurations for an existing web app, use hello **Set-AzureRmWebApp** cmdlet.</span></span> <span data-ttu-id="98137-164">매개 변수 전체 목록을 확인 hello [Cmdlet 참조 링크](https://msdn.microsoft.com/library/mt652487.aspx)</span><span class="sxs-lookup"><span data-stu-id="98137-164">For a full list of parameters, check hello [Cmdlet reference link](https://msdn.microsoft.com/library/mt652487.aspx)</span></span>

<span data-ttu-id="98137-165">이 cmdlet toochange 연결 문자열을 사용 하는 예 (1):</span><span class="sxs-lookup"><span data-stu-id="98137-165">Example (1): use this cmdlet toochange connection strings</span></span>

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

<span data-ttu-id="98137-166">예 (2): 앱 설정 추가 또는 변경</span><span class="sxs-lookup"><span data-stu-id="98137-166">Example (2): add or change app settings</span></span>

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


<span data-ttu-id="98137-167">예 (3): 64 비트 모드에서 웹 앱 toorun hello 설정</span><span class="sxs-lookup"><span data-stu-id="98137-167">Example (3):  set hello web app toorun in 64-bit mode</span></span>

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-hello-state-of-an-existing-web-app"></a><span data-ttu-id="98137-168">기존 웹 앱의 hello 상태 변경</span><span class="sxs-lookup"><span data-stu-id="98137-168">Change hello state of an existing Web App</span></span>
#### <a name="restart-a-web-app"></a><span data-ttu-id="98137-169">웹앱 다시 시작</span><span class="sxs-lookup"><span data-stu-id="98137-169">Restart a web app</span></span>
<span data-ttu-id="98137-170">웹 앱 toorestart hello 웹 앱의 hello 이름과 리소스 그룹을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98137-170">toorestart a web app, you must specify hello name and resource group of hello web app.</span></span>

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a><span data-ttu-id="98137-171">웹앱 중지</span><span class="sxs-lookup"><span data-stu-id="98137-171">Stop a web app</span></span>
<span data-ttu-id="98137-172">웹 앱 toostop hello 웹 앱의 hello 이름과 리소스 그룹을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98137-172">toostop a web app, you must specify hello name and resource group of hello web app.</span></span>

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a><span data-ttu-id="98137-173">웹앱 시작</span><span class="sxs-lookup"><span data-stu-id="98137-173">Start a web app</span></span>
<span data-ttu-id="98137-174">웹 앱 toostart hello 웹 앱의 hello 이름과 리소스 그룹을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98137-174">toostart a web app, you must specify hello name and resource group of hello web app.</span></span>

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a><span data-ttu-id="98137-175">웹앱 게시 프로필 관리</span><span class="sxs-lookup"><span data-stu-id="98137-175">Manage Web App Publishing profiles</span></span>
<span data-ttu-id="98137-176">각 웹 응용 프로그램에 사용 되는 toopublish 일 수 있는 게시 프로필 앱, 게시 프로필에 몇 가지 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98137-176">Each web app has a publishing profile that can be used toopublish your apps, several operations can be executed on publishing profiles.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="98137-177">게시 프로필 가져오기</span><span class="sxs-lookup"><span data-stu-id="98137-177">Get Publishing Profile</span></span>
<span data-ttu-id="98137-178">tooget hello를 사용 하 여 웹 응용 프로그램에 대 한 프로필 게시:</span><span class="sxs-lookup"><span data-stu-id="98137-178">tooget hello publishing profile for a web app, use:</span></span>

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

<span data-ttu-id="98137-179">이 명령은 hello 프로필 toohello 명령줄도 게시 프로필 tooa 텍스트 파일을 게시 하는 hello 출력에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="98137-179">This command echoes hello publishing profile toohello command line as well output hello publishing profile tooa text file.</span></span>

#### <a name="reset-publishing-profile"></a><span data-ttu-id="98137-180">게시 프로필 다시 설정</span><span class="sxs-lookup"><span data-stu-id="98137-180">Reset Publishing Profile</span></span>
<span data-ttu-id="98137-181">tooreset 둘 다 hello를 사용 하 여 웹 응용 프로그램에 대 한 FTP 및 웹 배포 게시 암호:</span><span class="sxs-lookup"><span data-stu-id="98137-181">tooreset both hello publishing password for FTP and web deploy for a web app, use:</span></span>

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a><span data-ttu-id="98137-182">웹앱 인증서 관리</span><span class="sxs-lookup"><span data-stu-id="98137-182">Manage Web App Certificates</span></span>
<span data-ttu-id="98137-183">toolearn toomanage 응용 프로그램 인증서를 웹 하는 방법에 대 한 참조 [PowerShell을 사용 하 여 SSL 인증서 바인딩](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="98137-183">toolearn about how toomanage web app certificates, see [SSL Certificates binding using PowerShell](app-service-web-app-powershell-ssl-binding.md)</span></span>

### <a name="next-steps"></a><span data-ttu-id="98137-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="98137-184">Next Steps</span></span>
* <span data-ttu-id="98137-185">Azure 리소스 관리자 PowerShell 지원에 대 한 toolearn 참조 [Azure PowerShell 사용 하 여 Azure 리소스 관리자와 함께 합니다.](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="98137-185">toolearn about Azure Resource Manager PowerShell support, see [Using Azure PowerShell with Azure Resource Manager.](../powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="98137-186">앱 서비스 환경에 대 한 toolearn 참조 [소개 tooApp 서비스 환경입니다.](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="98137-186">toolearn about App Service Environments, see [Introduction tooApp Service Environment.](app-service-app-service-environment-intro.md)</span></span>
* <span data-ttu-id="98137-187">PowerShell을 사용 하는 응용 프로그램 서비스 SSL 인증서를 관리 하는 방법에 대 한 toolearn 참조 [PowerShell을 사용 하 여 SSL 인증서 바인딩.](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="98137-187">toolearn about managing App Service SSL certificates using PowerShell, see [SSL Certificates binding using PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span></span>
* <span data-ttu-id="98137-188">Azure 웹 앱에 대 한 Azure 리소스 관리자 기반 PowerShell cmdlet의 전체 목록 hello에 대 한 toolearn 참조 [웹 앱 Azure 리소스 관리자 PowerShell Cmdlet의 Azure Cmdlet 참조 합니다.](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="98137-188">toolearn about hello full list of Azure Resource Manager-based PowerShell cmdlets for Azure Web Apps, see [Azure Cmdlet Reference of Web Apps Azure Resource Manager PowerShell Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>
* * <span data-ttu-id="98137-189">toolearn CLI를 사용 하 여 응용 프로그램 서비스를 관리 하는 방법에 대 한 참조 [Using Azure Resource Manager-Based XPlat CLI Azure 웹 앱에 대 한 합니다.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span><span class="sxs-lookup"><span data-stu-id="98137-189">toolearn about managing App Service using CLI, see [Using Azure Resource Manager-Based XPlat CLI for Azure Web App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span></span>

