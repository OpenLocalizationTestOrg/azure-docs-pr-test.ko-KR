---
title: "PowerShell을 사용하여 웹앱 복제"
description: "PowerShell을 사용하여 웹앱을 새 웹앱에 복제하는 방법에 대해 알아봅니다."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: f9a5cfa1-fbb0-41e6-95d1-75d457347a35
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: d47d5a2f7d2462525bf37718a234e222b4f64e6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a><span data-ttu-id="f66eb-103">PowerShell을 사용하여 Azure 앱 서비스 앱 복제</span><span class="sxs-lookup"><span data-stu-id="f66eb-103">Azure App Service App Cloning Using PowerShell</span></span>
<span data-ttu-id="f66eb-104">새 옵션이 New-AzureRMWebApp에 추가된 Microsoft Azure PowerShell 버전 1.1.0이 출시되어 사용자는 기존 웹앱을 다른 지역이나 동일한 지역에서 새로 만든 앱에 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-104">With the release of Microsoft Azure PowerShell version 1.1.0 a new option has been added to New-AzureRMWebApp that would give the user the ability to clone an existing Web App to a newly created app in a different region or in the same region.</span></span> <span data-ttu-id="f66eb-105">이를 통해 고객은 수많은 앱을 다른 지역에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-105">This will enable customers to deploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="f66eb-106">앱 복제는 현재 프리미엄 계층의 앱 서비스 계획에만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="f66eb-107">새로운 기능은 웹앱 백업 기능과 동일한 제한 사항을 사용합니다. [Azure App Service에서 웹앱 백업](web-sites-backup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f66eb-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="f66eb-108">Azure Resource Manager 기반 Azure PowerShell cmdlet을 사용하여 [Azure 웹앱용 Azure Resource Manager 기반 PowerShell 명령](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="f66eb-108">To learn about using Azure Resource Manager based Azure PowerShell cmdlets to manage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="cloning-an-existing-app"></a><span data-ttu-id="f66eb-109">기존 앱 복제</span><span class="sxs-lookup"><span data-stu-id="f66eb-109">Cloning an existing App</span></span>
<span data-ttu-id="f66eb-110">시나리오: 사용자가 미국 중남부 지역의 기존 웹앱의 콘텐츠를 미국 중북부 지역의 새 웹앱으로 복제하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-110">Scenario: An existing web app in South Central US region, the user would like to clone the contents to a new web app in North Central US region.</span></span> <span data-ttu-id="f66eb-111">이 작업은 SourceWebApp 옵션으로 새 웹앱을 만들기 위해 PowerShell cmdlet의 Azure Resource Manager 버전을 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-111">This can be accomplished by using the Azure Resource Manager version of the PowerShell cmdlet to create a new web app with the -SourceWebApp option.</span></span>

<span data-ttu-id="f66eb-112">원본 웹앱을 포함하는 리소스 그룹 이름을 알고 있으면 다음 PowerShell 명령을 사용하여 원본 웹앱의 정보를 가져올 수 있습니다(이 경우 이름은 source-webapp임).</span><span class="sxs-lookup"><span data-stu-id="f66eb-112">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="f66eb-113">새 앱 서비스 계획을 만들려면 다음 예제처럼 New-AzureRmAppServicePlan 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-113">To create a new App Service Plan, we can use New-AzureRmAppServicePlan command as in the following example</span></span>

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

<span data-ttu-id="f66eb-114">New-AzureRmWebApp 명령을 사용하여 미국 중북부 지역에서 새 웹앱을 만들어 기존 프리미엄 계층 앱 서비스 계획에 연결할 수 있으며 또한 원본 웹앱과 동일한 리소스 그룹을 사용하거나 다음과 같이 새 리소스 그룹을 정의할 수 있습니다. </span><span class="sxs-lookup"><span data-stu-id="f66eb-114">Using the New-AzureRmWebApp command, we can create the new web app in the North Central US region, and tie it to an existing premium tier App Service Plan, moreover we can use the same resource group as the source web app, or define a new resource group, the following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

<span data-ttu-id="f66eb-115">연결된 모든 배포 슬롯을 포함하여 기존 웹앱을 복제하려면 사용자는 IncludeSourceWebAppSlots 매개 변수를 사용해야 합니다. 다음 PowerShell 명령은 New-AzureRmWebApp 명령으로 해당 매개 변수를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-115">To clone an existing web app including all associated deployment slots, the user will need to use the IncludeSourceWebAppSlots parameter, the following PowerShell command demonstrates the use of that parameter with the New-AzureRmWebApp command:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

<span data-ttu-id="f66eb-116">동일한 지역 내에서 기존 웹앱을 복제하려면 사용자는 새 리소스 그룹 및 동일한 지역의 새 앱 서비스 계획을 만들고 다음 PowerShell 명령을 사용하여 웹앱을 복제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-116">To clone an existing web app within the same region, the user will need to create a new resource group and a new app service plan in the same region, and then using the following PowerShell command to clone the web app</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a><span data-ttu-id="f66eb-117">기존 앱을 앱 서비스 환경으로 복제</span><span class="sxs-lookup"><span data-stu-id="f66eb-117">Cloning an existing App to an App Service Environment</span></span>
<span data-ttu-id="f66eb-118">시나리오: 사용자가 기존 미국 중남부 지역의 웹앱의 콘텐츠를 기존 ASE(앱 서비스 환경)에 있는 새 웹앱으로 복제하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-118">Scenario: An existing web app in South Central US region, the user would like to clone the contents to a new web app to an existing App Service Environment (ASE).</span></span>

<span data-ttu-id="f66eb-119">원본 웹앱을 포함하는 리소스 그룹 이름을 알고 있으면 다음 PowerShell 명령을 사용하여 원본 웹앱의 정보를 가져올 수 있습니다(이 경우 이름은 source-webapp임).</span><span class="sxs-lookup"><span data-stu-id="f66eb-119">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="f66eb-120">ASE의 이름 및 ASE가 속한 리소스 그룹 이름을 알고 있으면 사용자는 New-AzureRmWebApp 명령을 사용하여 다음과 같이 기존 ASE에서 새 웹앱을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-120">Knowing the ASE's name, and the resource group name that the ASE belongs to, the user can use the New-AzureRmWebApp command to create the new web app in the existing ASE, the following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

<span data-ttu-id="f66eb-121">위치 매개 변수는 레거시 때문에 필요하지만 앱을 ASE에서 만드는 경우에는 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-121">The Location parameter is required due to legacy reason, but in the case of creating an app in an ASE it will be ignored.</span></span> 

## <a name="cloning-an-existing-app-slot"></a><span data-ttu-id="f66eb-122">기존 앱 슬롯 복제</span><span class="sxs-lookup"><span data-stu-id="f66eb-122">Cloning an existing App Slot</span></span>
<span data-ttu-id="f66eb-123">시나리오: 사용자가 기존 웹앱 슬롯을 새 웹앱이나 새 웹앱 슬롯에 복제하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-123">Scenario: The user would like to clone an existing Web App Slot to either a new Web App or a new Web App slot.</span></span> <span data-ttu-id="f66eb-124">새 웹앱은 원래 웹앱 슬롯과 동일한 지역이나 다른 지역에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-124">The new Web App can be in the same region as the original Web App slot or in a different region.</span></span>

<span data-ttu-id="f66eb-125">원본 웹앱을 포함한 리소스 그룹 이름을 알고 있으면 다음 PowerShell 명령을 사용하여 웹앱 source-webapp과 연결된 원본 웹앱 슬롯의 정보를 가져올 수 있습니다(이 경우 이름은 source-webappslot임).</span><span class="sxs-lookup"><span data-stu-id="f66eb-125">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app slot's information (in this case named source-webappslot) tied to Web App source-webapp:</span></span>

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

<span data-ttu-id="f66eb-126">다음에서는 새 웹앱에 원본 웹앱의 클론을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-126">The following demonstrates creating a clone of the source web app to a new web app:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a><span data-ttu-id="f66eb-127">앱을 복제하는 동한 트래픽 관리자 구성</span><span class="sxs-lookup"><span data-stu-id="f66eb-127">Configuring Traffic Manager while cloning a App</span></span>
<span data-ttu-id="f66eb-128">다중 지역 웹앱을 만들고 이러한 웹앱에 트래픽을 라우팅하도록 Azure 트래픽 관리자를 구성하는 것은 고객에게 높은 앱 가용성을 보장하기 위해 매우 중요한 시나리오입니다. 기존 웹앱을 복제할 때 두 웹앱을 새 트래픽 관리자 프로필에 연결할 수도 있고 기존 트래픽 관리자 프로필에 연결할 수도 있습니다. 단, 트래픽 관리자의 Azure Resource Manager 버전만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-128">Creating multi-region web apps and configuring Azure Traffic Manager to route traffic to all these web apps, is a n important scenario to insure that customers' apps are highly available, when cloning an existing web app you have the option to connect both web apps to either a new traffic manager profile or an existing one - note that only Azure Resource Manager version of Traffic Manager is supported.</span></span>

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a><span data-ttu-id="f66eb-129">앱을 복제하는 동안 새 트래픽 관리자 프로필 만들기</span><span class="sxs-lookup"><span data-stu-id="f66eb-129">Creating a new Traffic Manager profile while cloning a App</span></span>
<span data-ttu-id="f66eb-130">시나리오: 사용자가 두 웹앱을 모두 포함하는 Azure Resource Manager 트래픽 관리자 프로필을 구성하는 동안 다른 지역에 웹앱을 복제하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-130">Scenario: The user would like to clone an web app to another region, while configuring an Azure Resource Manager traffic manager profile that include both web apps.</span></span> <span data-ttu-id="f66eb-131">다음에서는 새 트래픽 관리자 프로필을 구성하는 동안 새 웹앱으로 원본 웹앱의 클론을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-131">The following demonstrates creating a clone of the source web app to a new web app while configuring a new Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-to-an-existing-traffic-manager-profile"></a><span data-ttu-id="f66eb-132">기존 트래픽 관리자 프로필에 복제된 새 웹앱 추가</span><span class="sxs-lookup"><span data-stu-id="f66eb-132">Adding new cloned Web App to an existing Traffic Manager profile</span></span>
<span data-ttu-id="f66eb-133">시나리오: 사용자가 두 웹앱을 끝점으로 추가하려고 하는 Azure Resource Manager 트래픽 관리자 프로필을 이미 가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-133">Scenario: The user already have an Azure Resource Manager traffic manager profile that he would like to add both web apps as endpoints.</span></span> <span data-ttu-id="f66eb-134">이를 수행하려면 먼저 기존 트래픽 관리자 프로필 ID를 어셈블해야 하며 구독 ID, 리소스 그룹 이름 및 기존 트래픽 관리자 프로필 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-134">To do so, we first need to assemble the existing traffic manager profile id, we will need the subscription id, resource group name and the existing traffic manager profile name.</span></span>

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

<span data-ttu-id="f66eb-135">트래픽 관리자 ID를 알게 된 후 다음에서는 원본 웹앱과 새 웹앱을 기존 트래픽 관리자 프로필에 추가하는 동안 원본 웹앱의 클론을 새 웹앱으로 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-135">After having the traffic manger id, the following demonstrates creating a clone of the source web app to a new web app while adding them to an existing Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a><span data-ttu-id="f66eb-136">현재 제한 사항</span><span class="sxs-lookup"><span data-stu-id="f66eb-136">Current Restrictions</span></span>
<span data-ttu-id="f66eb-137">이 기능은 현재 미리 보기 상태이며 점차 새 기능을 추가하기 위해 작업 중입니다. 다음 목록은 앱 복제의 현재 버전에 대해 알려진 제한 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-137">This feature is currently in preview, we are working to add new capabilities over time, the following list are the known restrictions on the current version of app cloning:</span></span>

* <span data-ttu-id="f66eb-138">자동 크기 설정은 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-138">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="f66eb-139">백업 일정 설정은 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-139">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="f66eb-140">VNET 설정은 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-140">VNET settings are not cloned</span></span>
* <span data-ttu-id="f66eb-141">App Insights는 대상 웹앱에서 자동으로 설치되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-141">App Insights are not automatically set up on the destination web app</span></span>
* <span data-ttu-id="f66eb-142">간편한 인증 설정은 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-142">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="f66eb-143">Kudu 확장은 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-143">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="f66eb-144">TiP 규칙은 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-144">TiP rules are not cloned</span></span>
* <span data-ttu-id="f66eb-145">데이터베이스 내용이 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f66eb-145">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="f66eb-146">참조</span><span class="sxs-lookup"><span data-stu-id="f66eb-146">References</span></span>
* [<span data-ttu-id="f66eb-147">Azure 웹앱용 Azure Resource Manager 기반 PowerShell 명령</span><span class="sxs-lookup"><span data-stu-id="f66eb-147">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="f66eb-148">Azure 포털을 사용하여 웹앱 복제</span><span class="sxs-lookup"><span data-stu-id="f66eb-148">Web App Cloning using Azure Portal</span></span>](app-service-web-app-cloning-portal.md)
* [<span data-ttu-id="f66eb-149">Azure 앱 서비스에서 웹앱 백업</span><span class="sxs-lookup"><span data-stu-id="f66eb-149">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="f66eb-150">Azure Traffic Manager에 대한 Azure Resource Manager 지원 미리 보기</span><span class="sxs-lookup"><span data-stu-id="f66eb-150">Azure Resource Manager support for Azure Traffic Manager Preview</span></span>](../traffic-manager/traffic-manager-powershell-arm.md)
* [<span data-ttu-id="f66eb-151">앱 서비스 환경 소개</span><span class="sxs-lookup"><span data-stu-id="f66eb-151">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="f66eb-152">Azure 리소스 관리자로 Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="f66eb-152">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

