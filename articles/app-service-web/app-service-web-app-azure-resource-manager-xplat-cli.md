---
title: "Azure 웹앱용 Azure Resource Manager 기반 플랫폼 간 명령줄 도구 | Microsoft Docs"
description: "새 Azure Resource Manager 기반 플랫폼 간 명령줄 도구를 사용하여 Azure 웹앱을 관리하는 방법에 대해 알아봅니다."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: d415b195-4262-416f-b59f-7e1aef200054
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 7a03e1417617453c43edcc3787da10d171359757
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a><span data-ttu-id="ffd47-103">Azure App Service용 Azure Resource Manager 기반 XPlat CLI 사용</span><span class="sxs-lookup"><span data-stu-id="ffd47-103">Using Azure Resource Manager-Based XPlat CLI for Azure App Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ffd47-104">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ffd47-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="ffd47-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffd47-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)

<span data-ttu-id="ffd47-106">Microsoft Azure 플랫폼 간 명령줄 도구 버전 0.10.5 릴리스에서는 새로운 명령이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-106">With the release of Microsoft Azure Cross-platform Command-Line Tools version 0.10.5, new commands have been added.</span></span> <span data-ttu-id="ffd47-107">이러한 명령은 Azure Resource Manager 기반 PowerShell 명령을 사용하여 App Service를 관리하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-107">These commands give the user the ability to use Azure Resource Manager-based PowerShell commands to manage App Service.</span></span>

<span data-ttu-id="ffd47-108">리소스 그룹을 관리하는 방법에 대한 자세한 내용은 [Azure CLI를 사용하여 Azure 리소스 및 리소스 그룹 관리](../azure-resource-manager/xplat-cli-azure-resource-manager.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffd47-108">To learn about managing Resource Groups, see [Use the Azure CLI to manage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span></span> 

> [!NOTE] 
> <span data-ttu-id="ffd47-109">또한 Python으로 작성된 리소스 관리 배포 모델용 차세대 CLI인 [Azure CLI 2.0](https://github.com/Azure/azure-cli)도 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="ffd47-109">Also, try out [Azure CLI 2.0](https://github.com/Azure/azure-cli), a next-generation CLI written in Python for the resource management deployment model.</span></span>
>
>

## <a name="managing-app-service-plans"></a><span data-ttu-id="ffd47-110">앱 서비스 계획 관리</span><span class="sxs-lookup"><span data-stu-id="ffd47-110">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="ffd47-111">앱 서비스 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="ffd47-111">Create an App Service Plan</span></span>
<span data-ttu-id="ffd47-112">App Service 계획을 만들려면 **azure appserviceplan create** 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-112">To create an app service plan, use the **azure appserviceplan create** command.</span></span>

<span data-ttu-id="ffd47-113">다음은 서로 다른 매개 변수의 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-113">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="ffd47-114">**--resource-group**: 새로 만든 App Service 계획을 포함하는 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="ffd47-114">**--resource-group**: resource group that includes the newly created app service plan.</span></span>
* <span data-ttu-id="ffd47-115">**--name**: App Service 계획의 이름</span><span class="sxs-lookup"><span data-stu-id="ffd47-115">**--name**: name of the app service plan.</span></span>
* <span data-ttu-id="ffd47-116">**--location**: App Service 계획 위치</span><span class="sxs-lookup"><span data-stu-id="ffd47-116">**--location**: app service plan location.</span></span>
* <span data-ttu-id="ffd47-117">**--sku**: 원하는 가격 책정 SKU(옵션: F1(무료))</span><span class="sxs-lookup"><span data-stu-id="ffd47-117">**--sku**:  the desired pricing sku (The options are: F1 (Free).</span></span> <span data-ttu-id="ffd47-118">D1(공유)</span><span class="sxs-lookup"><span data-stu-id="ffd47-118">D1 (Shared).</span></span> <span data-ttu-id="ffd47-119">B1(Basic Small), B2(Basic Medium), B3(Basic Large)</span><span class="sxs-lookup"><span data-stu-id="ffd47-119">B1 (Basic Small), B2 (Basic Medium), and B3 (Basic Large).</span></span> <span data-ttu-id="ffd47-120">S1(Standard Small), S2(Standard Medium), S3(Standard Large)</span><span class="sxs-lookup"><span data-stu-id="ffd47-120">S1 (Standard Small), S2 (Standard Medium), and S3 (Standard Large).</span></span> <span data-ttu-id="ffd47-121">P1(Premium Small), P2(Premium Medium), P3(Premium Large)</span><span class="sxs-lookup"><span data-stu-id="ffd47-121">P1 (Premium Small), P2 (Premium Medium), and P3 (Premium Large).)</span></span>
* <span data-ttu-id="ffd47-122">**--instances**: App Service 계획의 작업자 수(기본값은 1)</span><span class="sxs-lookup"><span data-stu-id="ffd47-122">**--instances**: the number of workers in the app service plan (Default value is 1).</span></span>

<span data-ttu-id="ffd47-123">이 cmdlet을 사용하는 예제:</span><span class="sxs-lookup"><span data-stu-id="ffd47-123">Example to use this cmdlet:</span></span>

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="ffd47-124">Linux App Service 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="ffd47-124">Create a Linux App Service Plan</span></span>

<span data-ttu-id="ffd47-125">동일한 **azure appserviceplan create** 명령과 추가 매개 변수 **-islinux true** 사용</span><span class="sxs-lookup"><span data-stu-id="ffd47-125">Using the same **azure appserviceplan create** command, with the extra parameter **--islinux true**.</span></span> <span data-ttu-id="ffd47-126">[Linux의 App Service 소개](app-service-linux-intro.md)에 설명된 제한 사항 및 지역 참조</span><span class="sxs-lookup"><span data-stu-id="ffd47-126">Note the restrictions and regions outlined in [Introduction to App Service on Linux](app-service-linux-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="ffd47-127">기존 앱 서비스 계획 나열</span><span class="sxs-lookup"><span data-stu-id="ffd47-127">List Existing App Service Plans</span></span>
<span data-ttu-id="ffd47-128">기존 App Service 계획을 나열하려면 **azure appserviceplan list** 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-128">To list the existing app service plans, use **azure appserviceplan list** command.</span></span>

<span data-ttu-id="ffd47-129">특정 리소스 그룹에서 모든 앱 서비스 계획을 나열하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-129">To list all app service plans under a specific resource group, use:</span></span>

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="ffd47-130">특정 App Service 계획을 가져오려면 **azure appserviceplan show** 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-130">To get a specific app service plan, use **azure appserviceplan show** command:</span></span>

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="ffd47-131">기존 앱 서비스 계획 구성</span><span class="sxs-lookup"><span data-stu-id="ffd47-131">Configure an existing App Service Plan</span></span>
<span data-ttu-id="ffd47-132">기존 App Service 계획의 설정을 변경하려면 **azure appserviceplan config** 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-132">To change the settings for an existing app service plan, use the **azure appserviceplan config** command.</span></span> <span data-ttu-id="ffd47-133">SKU 및 작업자 수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-133">You can change the sku, and the number of workers</span></span> 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="ffd47-134">앱 서비스 계획 크기 조정</span><span class="sxs-lookup"><span data-stu-id="ffd47-134">Scaling an App Service Plan</span></span>
<span data-ttu-id="ffd47-135">기존 앱 서비스 계획을 크기 조정하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-135">To scale an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-the-sku-of-an-app-service-plan"></a><span data-ttu-id="ffd47-136">App Service 계획의 SKU 변경</span><span class="sxs-lookup"><span data-stu-id="ffd47-136">Changing the SKU of an App Service Plan</span></span>
<span data-ttu-id="ffd47-137">기존 App Service 계획의 SKU를 변경하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-137">To change the sku of an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="ffd47-138">기존 앱 서비스 계획 삭제</span><span class="sxs-lookup"><span data-stu-id="ffd47-138">Delete an existing App Service Plan</span></span>
<span data-ttu-id="ffd47-139">기존 App Service 계획을 삭제하려면 할당된 모든 앱을 먼저 이동하거나 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-139">To delete an existing app service plan, all assigned apps need to be moved or deleted first.</span></span> <span data-ttu-id="ffd47-140">그런 후 **azure webapp delete** 명령을 사용하여 App Service 계획을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-140">Then using the **azure webapp delete** command you can delete the app service plan.</span></span>

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a><span data-ttu-id="ffd47-141">App Service 앱 관리</span><span class="sxs-lookup"><span data-stu-id="ffd47-141">Managing App Service apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="ffd47-142">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="ffd47-142">Create a web app</span></span>
<span data-ttu-id="ffd47-143">웹앱을 만들려면 **azure webapp create** 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-143">To create a web app, use the **azure webapp create** command.</span></span>

<span data-ttu-id="ffd47-144">다음은 서로 다른 매개 변수의 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-144">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="ffd47-145">**--name**: 웹앱의 이름</span><span class="sxs-lookup"><span data-stu-id="ffd47-145">**--name**: name for the web app.</span></span>
* <span data-ttu-id="ffd47-146">**--plan**: 웹앱을 호스트하는 데 사용되는 서비스 계획의 이름</span><span class="sxs-lookup"><span data-stu-id="ffd47-146">**--plan**: name for the service plan used to host the web app.</span></span>
* <span data-ttu-id="ffd47-147">**--resource-group**: App Service 계획을 호스트하는 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="ffd47-147">**--resource-group**: resource group that hosts the App service plan.</span></span>
* <span data-ttu-id="ffd47-148">**--location**: 웹앱 위치</span><span class="sxs-lookup"><span data-stu-id="ffd47-148">**--location**: the web app location.</span></span>

<span data-ttu-id="ffd47-149">이 cmdlet을 사용하는 예제:</span><span class="sxs-lookup"><span data-stu-id="ffd47-149">Example to use this cmdlet:</span></span>

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a><span data-ttu-id="ffd47-150">기존 앱 삭제</span><span class="sxs-lookup"><span data-stu-id="ffd47-150">Delete an existing app</span></span>
<span data-ttu-id="ffd47-151">기존 앱을 삭제하려면 **azure webapp delete** 명령을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-151">To delete an existing app, you can use the **azure webapp delete** command.</span></span> <span data-ttu-id="ffd47-152">앱의 이름 및 리소스 그룹 이름을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-152">You need to specify the name of the app and the resource group name.</span></span>

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a><span data-ttu-id="ffd47-153">기존 앱 목록</span><span class="sxs-lookup"><span data-stu-id="ffd47-153">List existing apps</span></span>
<span data-ttu-id="ffd47-154">기존 앱을 나열하려면 **azure webapp list** 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-154">To list the existing apps, use the **azure webapp list** command.</span></span>

<span data-ttu-id="ffd47-155">특정 리소스 그룹의 모든 앱을 나열하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-155">To list all apps in a specific resource group, use:</span></span>

    azure webapp list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="ffd47-156">특정 앱을 가져오려면 **azure webapp show** 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-156">To get a specific app, use the **azure webapp show** command.</span></span>

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a><span data-ttu-id="ffd47-157">기존 앱 구성</span><span class="sxs-lookup"><span data-stu-id="ffd47-157">Configure an existing app</span></span>
<span data-ttu-id="ffd47-158">기존 앱에 대한 설정 및 구성을 변경하려면 **azure webapp config set** 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-158">To change the settings and configurations for an existing app, use the **azure webapp config set** command.</span></span>

<span data-ttu-id="ffd47-159">예 (1): 앱의 php 버전 변경</span><span class="sxs-lookup"><span data-stu-id="ffd47-159">Example (1): change the php version of a app</span></span> 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

<span data-ttu-id="ffd47-160">예 (2): 앱 설정 추가 또는 변경</span><span class="sxs-lookup"><span data-stu-id="ffd47-160">Example (2): add or change app settings</span></span>

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

<span data-ttu-id="ffd47-161">변경할 수 있는 기타 구성을 확인하려면 **azure webapp config set -h** 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-161">To know what other configuration can be changed, use the **azure webapp config set -h** command.</span></span>

### <a name="change-the-state-of-an-existing-app"></a><span data-ttu-id="ffd47-162">기존 앱의 상태 변경</span><span class="sxs-lookup"><span data-stu-id="ffd47-162">Change the state of an existing app</span></span>
#### <a name="restart-an-app"></a><span data-ttu-id="ffd47-163">앱 다시 시작</span><span class="sxs-lookup"><span data-stu-id="ffd47-163">Restart an app</span></span>
<span data-ttu-id="ffd47-164">앱을 다시 시작하려면 앱의 이름 및 리소스 그룹을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-164">To restart an app, you must specify the name and resource group of the app.</span></span>

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a><span data-ttu-id="ffd47-165">앱 중지</span><span class="sxs-lookup"><span data-stu-id="ffd47-165">Stop an app</span></span>
<span data-ttu-id="ffd47-166">앱을 중지하려면 앱의 이름 및 리소스 그룹을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-166">To stop an app, you must specify the name and resource group of the app.</span></span>

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a><span data-ttu-id="ffd47-167">앱 시작</span><span class="sxs-lookup"><span data-stu-id="ffd47-167">Start an app</span></span>
<span data-ttu-id="ffd47-168">앱을 시작하려면 앱의 이름 및 리소스 그룹을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-168">To start an app, you must specify the name and resource group of the app.</span></span>

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a><span data-ttu-id="ffd47-169">앱의 게시 프로필 관리</span><span class="sxs-lookup"><span data-stu-id="ffd47-169">Manage publishing profiles of an app</span></span>
<span data-ttu-id="ffd47-170">각 앱에는 코드를 게시하는 데 사용할 수 있는 게시 프로필이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-170">Each app has a publishing profile that can be used to publish your code.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="ffd47-171">게시 프로필 가져오기</span><span class="sxs-lookup"><span data-stu-id="ffd47-171">Get Publishing Profile</span></span>
<span data-ttu-id="ffd47-172">앱에 대한 게시 프로필을 가져오려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-172">To get the publishing profile for a app, use:</span></span>

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

<span data-ttu-id="ffd47-173">이 명령은 게시 프로필 사용자 이름 및 암호를 명령줄에 에코합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-173">This command echoes the publishing profile username and password to the command line.</span></span>

### <a name="manage-app-hostnames"></a><span data-ttu-id="ffd47-174">앱 호스트 관리</span><span class="sxs-lookup"><span data-stu-id="ffd47-174">Manage app hostnames</span></span>
<span data-ttu-id="ffd47-175">앱에 대한 호스트 이름 바인딩을 관리하려면 **azure webapp config hostnames** 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-175">To manage hostname bindings for your app, use the **azure webapp config hostnames** command</span></span>  

#### <a name="list-hostname-bindings"></a><span data-ttu-id="ffd47-176">호스트 이름 바인딩 나열</span><span class="sxs-lookup"><span data-stu-id="ffd47-176">List hostname bindings</span></span>
<span data-ttu-id="ffd47-177">앱에 대한 현재 호스트 이름 바인딩을 가져오려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-177">To get the current hostname bindings for an app, use:</span></span>

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a><span data-ttu-id="ffd47-178">호스트 이름 바인딩 추가</span><span class="sxs-lookup"><span data-stu-id="ffd47-178">Add hostname bindings</span></span>
<span data-ttu-id="ffd47-179">앱에 호스트 이름 바인딩을 추가하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-179">To add hostname bindings to an app, use:</span></span>

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a><span data-ttu-id="ffd47-180">호스트 이름 바인딩 삭제</span><span class="sxs-lookup"><span data-stu-id="ffd47-180">Delete hostname bindings</span></span>
<span data-ttu-id="ffd47-181">호스트 이름 바인딩을 삭제하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd47-181">To delete hostname bindings, use:</span></span>

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a><span data-ttu-id="ffd47-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ffd47-182">Next Steps</span></span>
* <span data-ttu-id="ffd47-183">Azure Resource Manager CLI 지원에 대한 자세한 내용은 [Azure CLI를 사용하여 Azure 리소스 및 리소스 그룹 관리](../azure-resource-manager/xplat-cli-azure-resource-manager.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffd47-183">To learn about Azure Resource Manager CLI support, see [Use the Azure CLI to manage Azure resources and resource groups.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span></span>
* <span data-ttu-id="ffd47-184">PowerShell을 사용하여 App Service를 관리하는 방법에 대한 자세한 내용은 [Azure Resource Manager 기반 PowerShell을 사용하여 Azure 웹앱 관리](app-service-web-app-azure-resource-manager-powershell.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffd47-184">To learn about managing App Service using PowerShell, see [Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span></span>
* <span data-ttu-id="ffd47-185">Linux의 Azure App Service에 대해 알아보려면 [Linux의 Azure App Service 소개](app-service-linux-intro.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffd47-185">To learn about Azure App Service on Linux, see [Introduction to App Service on Linux](app-service-linux-intro.md)</span></span>
