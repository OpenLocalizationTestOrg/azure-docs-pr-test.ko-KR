---
title: "Azure 웹앱에 대한 Azure Resource Manager 기반 PowerShell 명령 | Microsoft Docs"
description: "새 Azure Resource Manager 기반 PowerShell 명령을 사용하여 Azure 웹앱을 관리하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 8d574f051a327ba0409e6f25a5886af673d3d5e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-powershell-to-manage-azure-web-apps"></a><span data-ttu-id="d34a2-103">Azure Resource Manager 기반 PowerShell을 사용하여 Azure 웹앱 관리</span><span class="sxs-lookup"><span data-stu-id="d34a2-103">Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d34a2-104">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d34a2-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="d34a2-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d34a2-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

<span data-ttu-id="d34a2-106">Microsoft Azure PowerShell 버전 1.0.0에서는 사용자에게 Azure Resource Manager 기반 PowerShell 명령을 사용하여 웹앱을 관리하는 기능을 제공하는 새로운 명령이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-106">With Microsoft Azure PowerShell version 1.0.0 new commands have been added, that give the user the ability to use Azure Resource Manager-based PowerShell commands to manage Web Apps.</span></span>

<span data-ttu-id="d34a2-107">리소스 그룹 관리에 대해 알아보려면 [Azure Resource Manager로 Azure PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d34a2-107">To learn about managing Resource Groups, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span> 

<span data-ttu-id="d34a2-108">PowerShell cmdlet에 대한 매개 변수 및 옵션의 전체 목록에 대해 알아보려면 [웹앱 Azure Resource Manager 기반 PowerShell Cmdlet의 전체 Cmdlet 참조](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="d34a2-108">To learn about the full list of parameters and options for the PowerShell cmdlets, see the [full Cmdlet Reference of Web App Azure Resource Manager-based PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>

## <a name="managing-app-service-plans"></a><span data-ttu-id="d34a2-109">앱 서비스 계획 관리</span><span class="sxs-lookup"><span data-stu-id="d34a2-109">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="d34a2-110">앱 서비스 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="d34a2-110">Create an App Service Plan</span></span>
<span data-ttu-id="d34a2-111">앱 서비스 계획을 만들려면 **New-AzureRmAppServicePlan** cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-111">To create an app service plan, use the **New-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="d34a2-112">다음은 서로 다른 매개 변수의 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-112">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="d34a2-113">**Name**: 앱 서비스 계획의 이름.</span><span class="sxs-lookup"><span data-stu-id="d34a2-113">**Name**: name of the app service plan.</span></span>
* <span data-ttu-id="d34a2-114">**Location**: 서비스 계획 위치.</span><span class="sxs-lookup"><span data-stu-id="d34a2-114">**Location**: service plan location.</span></span>
* <span data-ttu-id="d34a2-115">**ResourceGroupName**: 새로 만든 앱 서비스 계획을 포함하는 리소스 그룹.</span><span class="sxs-lookup"><span data-stu-id="d34a2-115">**ResourceGroupName**: resource group that includes the newly created app service plan.</span></span>
* <span data-ttu-id="d34a2-116">**Tier**: 원하는 가격 책정 계층(기본값은 Free, 다른 옵션은 Shared, Basic, Standard 및 Premium)</span><span class="sxs-lookup"><span data-stu-id="d34a2-116">**Tier**:  the desired pricing tier (Default is Free, other options are Shared, Basic, Standard, and Premium.)</span></span>
* <span data-ttu-id="d34a2-117">**WorkerSize**: 작업자의 크기(Tier 매개 변수가 Basic, Standard 또는 Premium으로 지정된 경우 기본값은 Small입니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-117">**WorkerSize**: the size of workers (Default is small if the Tier parameter was specified as Basic, Standard, or Premium.</span></span> <span data-ttu-id="d34a2-118">다른 옵션은 Medium 및 Large입니다.)</span><span class="sxs-lookup"><span data-stu-id="d34a2-118">Other options are Medium, and Large.)</span></span>
* <span data-ttu-id="d34a2-119">**NumberofWorkers**: 앱 서비스 계획에서 작업자의 수(기본값은 1).</span><span class="sxs-lookup"><span data-stu-id="d34a2-119">**NumberofWorkers**: the number of workers in the app service plan (Default value is 1).</span></span> 

<span data-ttu-id="d34a2-120">이 cmdlet을 사용하는 예제:</span><span class="sxs-lookup"><span data-stu-id="d34a2-120">Example to use this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a><span data-ttu-id="d34a2-121">앱 서비스 환경에서 앱 서비스 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="d34a2-121">Create an App Service Plan in an App Service Environment</span></span>
<span data-ttu-id="d34a2-122">ASE(App Service Environment)에서 새 App Service 계획을 만들려면 동일한 **New-AzureRmAppServicePlan** 명령과 추가 매개 변수를 사용하여 ASE 이름과 ASE 리소스 그룹 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-122">To create an app service plan in an app service environment, use the same command **New-AzureRmAppServicePlan** command with extra parameters to specify the ASE's name and ASE's resource group name.</span></span>

<span data-ttu-id="d34a2-123">이 cmdlet을 사용하는 예제:</span><span class="sxs-lookup"><span data-stu-id="d34a2-123">Example to use this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

<span data-ttu-id="d34a2-124">앱 서비스 환경에 대해 자세히 알아보려면 [앱 서비스 환경 소개](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="d34a2-124">To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="d34a2-125">기존 앱 서비스 계획 나열</span><span class="sxs-lookup"><span data-stu-id="d34a2-125">List Existing App Service Plans</span></span>
<span data-ttu-id="d34a2-126">기존 앱 서비스 계획을 나열하려면 **Get-AzureRmAppServicePlan** cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-126">To list the existing app service plans, use **Get-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="d34a2-127">구독에서 모든 앱 서비스 계획을 목록화하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-127">To list all app service plans under your subscription, use:</span></span> 

    Get-AzureRmAppServicePlan

<span data-ttu-id="d34a2-128">특정 리소스 그룹에서 모든 앱 서비스 계획을 나열하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-128">To list all app service plans under a specific resource group, use:</span></span>

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="d34a2-129">특정 앱 서비스 계획을 가져오려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-129">To get a specific app service plan, use:</span></span>

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="d34a2-130">기존 앱 서비스 계획 구성</span><span class="sxs-lookup"><span data-stu-id="d34a2-130">Configure an existing App Service Plan</span></span>
<span data-ttu-id="d34a2-131">기존 앱 서비스 계획의 설정을 변경하려면 **Set-AzureRmAppServicePlan** cmdlet를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-131">To change the settings for an existing app service plan, use the **Set-AzureRmAppServicePlan** cmdlet.</span></span> <span data-ttu-id="d34a2-132">계층, 작업자 크기 및 작업자의 수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-132">You can change the tier, worker size, and the number of workers</span></span> 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="d34a2-133">앱 서비스 계획 크기 조정</span><span class="sxs-lookup"><span data-stu-id="d34a2-133">Scaling an App Service Plan</span></span>
<span data-ttu-id="d34a2-134">기존 앱 서비스 계획을 크기 조정하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-134">To scale an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-the-worker-size-of-an-app-service-plan"></a><span data-ttu-id="d34a2-135">앱 서비스 계획의 작업자 크기 변경</span><span class="sxs-lookup"><span data-stu-id="d34a2-135">Changing the worker size of an App Service Plan</span></span>
<span data-ttu-id="d34a2-136">기존 앱 서비스 계획에서 작업자의 크기를 변경하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-136">To change the size of workers in an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-the-tier-of-an-app-service-plan"></a><span data-ttu-id="d34a2-137">앱 서비스 계획의 계층 변경</span><span class="sxs-lookup"><span data-stu-id="d34a2-137">Changing the Tier of an App Service Plan</span></span>
<span data-ttu-id="d34a2-138">기존 앱 서비스 계획에서 계층을 변경하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-138">To change the tier of an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="d34a2-139">기존 앱 서비스 계획 삭제</span><span class="sxs-lookup"><span data-stu-id="d34a2-139">Delete an existing App Service Plan</span></span>
<span data-ttu-id="d34a2-140">기존 App Service 계획을 삭제하려면 할당된 모든 웹앱을 먼저 이동하거나 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-140">To delete an existing app service plan, all assigned web apps need to be moved or deleted first.</span></span> <span data-ttu-id="d34a2-141">그런 후 **Remove-AzureRmAppServicePlan** cmdlet을 사용하여 App Service 계획을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-141">Then using the **Remove-AzureRmAppServicePlan** cmdlet you can delete the app service plan.</span></span>

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a><span data-ttu-id="d34a2-142">앱 서비스 웹앱 관리</span><span class="sxs-lookup"><span data-stu-id="d34a2-142">Managing App Service Web Apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="d34a2-143">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="d34a2-143">Create a Web App</span></span>
<span data-ttu-id="d34a2-144">웹앱을 만들려면 **New-AzureRmWebApp** cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-144">To create a web app, use the **New-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="d34a2-145">다음은 서로 다른 매개 변수의 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-145">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="d34a2-146">**Name**: 웹앱에 대한 이름.</span><span class="sxs-lookup"><span data-stu-id="d34a2-146">**Name**: name for the web app.</span></span>
* <span data-ttu-id="d34a2-147">**AppServicePlan**: 웹앱을 호스트하는 데 사용되는 서비스 계획에 대한 이름.</span><span class="sxs-lookup"><span data-stu-id="d34a2-147">**AppServicePlan**: name for the service plan used to host the web app.</span></span>
* <span data-ttu-id="d34a2-148">**ResourceGroupName**: 앱 서비스 계획을 호스트하는 리소스 그룹.</span><span class="sxs-lookup"><span data-stu-id="d34a2-148">**ResourceGroupName**: resource group that hosts the App service plan.</span></span>
* <span data-ttu-id="d34a2-149">**Location**: 웹앱 위치.</span><span class="sxs-lookup"><span data-stu-id="d34a2-149">**Location**: the web app location.</span></span>

<span data-ttu-id="d34a2-150">이 cmdlet을 사용하는 예제:</span><span class="sxs-lookup"><span data-stu-id="d34a2-150">Example to use this cmdlet:</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a><span data-ttu-id="d34a2-151">App Service Environment에서 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="d34a2-151">Create a Web App in an App Service Environment</span></span>
<span data-ttu-id="d34a2-152">ASE(App Service Environment)에서 웹앱을 만들려면</span><span class="sxs-lookup"><span data-stu-id="d34a2-152">To create a web app in an App Service Environment (ASE).</span></span> <span data-ttu-id="d34a2-153">동일한 **New-AzureRmWebApp** 명령과 추가 매개 변수를 지정하여 ASE가 속하는 ASE 이름 및 리소스 그룹 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-153">Use the same **New-AzureRmWebApp** command with extra parameters to specify the ASE name and the resource group name that the ASE belongs to.</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

<span data-ttu-id="d34a2-154">앱 서비스 환경에 대해 자세히 알아보려면 [앱 서비스 환경 소개](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="d34a2-154">To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="delete-an-existing-web-app"></a><span data-ttu-id="d34a2-155">기존 웹앱 삭제</span><span class="sxs-lookup"><span data-stu-id="d34a2-155">Delete an existing Web App</span></span>
<span data-ttu-id="d34a2-156">기존 웹앱을 삭제하려면 **Remove-AzureRmWebApp** cmdlet을 사용할 수 있으며 웹앱의 이름 및 리소스 그룹 이름을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-156">To delete an existing web app you can use the **Remove-AzureRmWebApp** cmdlet, you need to specify the name of the web app and the resource group name.</span></span>

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a><span data-ttu-id="d34a2-157">기존 웹앱 나열</span><span class="sxs-lookup"><span data-stu-id="d34a2-157">List existing Web Apps</span></span>
<span data-ttu-id="d34a2-158">기존 웹앱을 나열하려면 **Get-AzureRmWebApp** cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-158">To list the existing web apps, use the **Get-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="d34a2-159">구독에서 모든 웹앱을 나열하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-159">To list all web apps under your subscription, use:</span></span>

    Get-AzureRmWebApp

<span data-ttu-id="d34a2-160">특정 리소스 그룹에서 모든 웹앱을 나열하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-160">To list all web apps under a specific resource group, use:</span></span>

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="d34a2-161">특정 웹앱을 가져오려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-161">To get a specific web app, use:</span></span>

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a><span data-ttu-id="d34a2-162">기존 웹앱 구성</span><span class="sxs-lookup"><span data-stu-id="d34a2-162">Configure an existing Web App</span></span>
<span data-ttu-id="d34a2-163">기존 웹앱에 대한 설정 및 구성을 변경하려면 **Set-AzureRmWebApp** cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-163">To change the settings and configurations for an existing web app, use the **Set-AzureRmWebApp** cmdlet.</span></span> <span data-ttu-id="d34a2-164">매개 변수의 전체 목록은 [Cmdlet 참조 링크](https://msdn.microsoft.com/library/mt652487.aspx)</span><span class="sxs-lookup"><span data-stu-id="d34a2-164">For a full list of parameters, check the [Cmdlet reference link](https://msdn.microsoft.com/library/mt652487.aspx)</span></span>

<span data-ttu-id="d34a2-165">예 (1): 이 cmdlet을 사용하여 연결 문자열 변경</span><span class="sxs-lookup"><span data-stu-id="d34a2-165">Example (1): use this cmdlet to change connection strings</span></span>

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

<span data-ttu-id="d34a2-166">예 (2): 앱 설정 추가 또는 변경</span><span class="sxs-lookup"><span data-stu-id="d34a2-166">Example (2): add or change app settings</span></span>

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


<span data-ttu-id="d34a2-167">예 (3): 64비트 모드에서 실행되도록 웹앱 설정</span><span class="sxs-lookup"><span data-stu-id="d34a2-167">Example (3):  set the web app to run in 64-bit mode</span></span>

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-the-state-of-an-existing-web-app"></a><span data-ttu-id="d34a2-168">기존 웹앱의 상태 변경</span><span class="sxs-lookup"><span data-stu-id="d34a2-168">Change the state of an existing Web App</span></span>
#### <a name="restart-a-web-app"></a><span data-ttu-id="d34a2-169">웹앱 다시 시작</span><span class="sxs-lookup"><span data-stu-id="d34a2-169">Restart a web app</span></span>
<span data-ttu-id="d34a2-170">웹앱을 다시 시작하려면 웹앱의 이름 및 리소스 그룹을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-170">To restart a web app, you must specify the name and resource group of the web app.</span></span>

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a><span data-ttu-id="d34a2-171">웹앱 중지</span><span class="sxs-lookup"><span data-stu-id="d34a2-171">Stop a web app</span></span>
<span data-ttu-id="d34a2-172">웹앱을 중지하려면 웹앱의 이름 및 리소스 그룹을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-172">To stop a web app, you must specify the name and resource group of the web app.</span></span>

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a><span data-ttu-id="d34a2-173">웹앱 시작</span><span class="sxs-lookup"><span data-stu-id="d34a2-173">Start a web app</span></span>
<span data-ttu-id="d34a2-174">웹앱을 시작하려면 웹앱의 이름 및 리소스 그룹을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-174">To start a web app, you must specify the name and resource group of the web app.</span></span>

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a><span data-ttu-id="d34a2-175">웹앱 게시 프로필 관리</span><span class="sxs-lookup"><span data-stu-id="d34a2-175">Manage Web App Publishing profiles</span></span>
<span data-ttu-id="d34a2-176">각 웹앱은 앱을 게시하는 데 사용할 수 있는 게시 프로필을 가지며 게시 프로필에서 다양한 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-176">Each web app has a publishing profile that can be used to publish your apps, several operations can be executed on publishing profiles.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="d34a2-177">게시 프로필 가져오기</span><span class="sxs-lookup"><span data-stu-id="d34a2-177">Get Publishing Profile</span></span>
<span data-ttu-id="d34a2-178">웹앱에 대한 게시 프로필을 가져오려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-178">To get the publishing profile for a web app, use:</span></span>

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

<span data-ttu-id="d34a2-179">이 명령은 게시 프로필을 명령줄로 반향할 뿐만 아니라 게시 프로필을 텍스트 파일로 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-179">This command echoes the publishing profile to the command line as well output the publishing profile to a text file.</span></span>

#### <a name="reset-publishing-profile"></a><span data-ttu-id="d34a2-180">게시 프로필 다시 설정</span><span class="sxs-lookup"><span data-stu-id="d34a2-180">Reset Publishing Profile</span></span>
<span data-ttu-id="d34a2-181">FTP에 대한 게시 암호 및 웹앱에 대한 웹 배포를 다시 설정하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d34a2-181">To reset both the publishing password for FTP and web deploy for a web app, use:</span></span>

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a><span data-ttu-id="d34a2-182">웹앱 인증서 관리</span><span class="sxs-lookup"><span data-stu-id="d34a2-182">Manage Web App Certificates</span></span>
<span data-ttu-id="d34a2-183">웹앱 인증서를 관리하는 방법에 대해 알아보려면 [PowerShell을 사용하여 SSL 인증서 바인딩](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="d34a2-183">To learn about how to manage web app certificates, see [SSL Certificates binding using PowerShell](app-service-web-app-powershell-ssl-binding.md)</span></span>

### <a name="next-steps"></a><span data-ttu-id="d34a2-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d34a2-184">Next Steps</span></span>
* <span data-ttu-id="d34a2-185">Azure Resource Manager PowerShell 지원에 대해 알아보려면 [Azure Resource Manager로 Azure PowerShell 사용](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="d34a2-185">To learn about Azure Resource Manager PowerShell support, see [Using Azure PowerShell with Azure Resource Manager.](../powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="d34a2-186">앱 서비스 환경에 대해 알아보려면 [앱 서비스 환경 소개](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="d34a2-186">To learn about App Service Environments, see [Introduction to App Service Environment.](app-service-app-service-environment-intro.md)</span></span>
* <span data-ttu-id="d34a2-187">PowerShell을 사용하여 앱 서비스 SSL 인증서 관리에 대해 알아보려면 [PowerShell을 사용하여 SSL 인증서 바인딩](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="d34a2-187">To learn about managing App Service SSL certificates using PowerShell, see [SSL Certificates binding using PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span></span>
* <span data-ttu-id="d34a2-188">Azure 웹앱에 대한 Azure Resource Manager 기반 PowerShell cmdlet의 전체 목록에 대해 알아보려면 [웹앱 Azure Resource Manager PowerShell Cmdlet의 전체 Cmdlet 참조](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="d34a2-188">To learn about the full list of Azure Resource Manager-based PowerShell cmdlets for Azure Web Apps, see [Azure Cmdlet Reference of Web Apps Azure Resource Manager PowerShell Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>
* * <span data-ttu-id="d34a2-189">CLI를 사용하여 App Service를 관리하는 방법에 대한 자세한 내용은 [Azure Web App에 Azure Resource Manager 기반 플랫폼 간 CLI 사용](app-service-web-app-azure-resource-manager-xplat-cli.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d34a2-189">To learn about managing App Service using CLI, see [Using Azure Resource Manager-Based XPlat CLI for Azure Web App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span></span>

