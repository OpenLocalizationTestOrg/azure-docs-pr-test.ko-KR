---
title: "Azure 웹 앱에 대 한 리소스 관리자 기반 크로스 플랫폼 명령줄 도구 aaaAzure | Microsoft Docs"
description: "어떻게 toouse hello 새 Azure 리소스 관리자 기반 크로스 플랫폼 명령줄 도구 toomanage Azure 웹 앱에 알아봅니다."
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
ms.openlocfilehash: 5f5e03edcb01154aef3bd220cd27358f69656ef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a><span data-ttu-id="5cb89-103">Azure App Service용 Azure Resource Manager 기반 XPlat CLI 사용</span><span class="sxs-lookup"><span data-stu-id="5cb89-103">Using Azure Resource Manager-Based XPlat CLI for Azure App Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5cb89-104">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5cb89-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="5cb89-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5cb89-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)

<span data-ttu-id="5cb89-106">Microsoft Azure 크로스 플랫폼 명령줄 도구 버전 0.10.5 hello 릴리스마다 새로운 명령이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-106">With hello release of Microsoft Azure Cross-platform Command-Line Tools version 0.10.5, new commands have been added.</span></span> <span data-ttu-id="5cb89-107">이 명령은 hello 사용자 hello 기능 toouse Azure 리소스 관리자 기반 PowerShell 명령을 toomanage 앱 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-107">These commands give hello user hello ability toouse Azure Resource Manager-based PowerShell commands toomanage App Service.</span></span>

<span data-ttu-id="5cb89-108">리소스 그룹을 관리 하는 방법에 대 한 toolearn 참조 [hello Azure CLI toomanage Azure를 사용 하 여 리소스 및 리소스 그룹](../azure-resource-manager/xplat-cli-azure-resource-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-108">toolearn about managing Resource Groups, see [Use hello Azure CLI toomanage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span></span> 

> [!NOTE] 
> <span data-ttu-id="5cb89-109">또한 사용해 [Azure CLI 2.0](https://github.com/Azure/azure-cli), 차세대 CLI hello 리소스 관리 배포 모델에 대 한 Python으로 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-109">Also, try out [Azure CLI 2.0](https://github.com/Azure/azure-cli), a next-generation CLI written in Python for hello resource management deployment model.</span></span>
>
>

## <a name="managing-app-service-plans"></a><span data-ttu-id="5cb89-110">앱 서비스 계획 관리</span><span class="sxs-lookup"><span data-stu-id="5cb89-110">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="5cb89-111">앱 서비스 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="5cb89-111">Create an App Service Plan</span></span>
<span data-ttu-id="5cb89-112">앱 서비스 계획을 toocreate hello를 사용 하 여 **azure appserviceplan 만들** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-112">toocreate an app service plan, use hello **azure appserviceplan create** command.</span></span>

<span data-ttu-id="5cb89-113">다음은 hello 다른 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="5cb89-113">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="5cb89-114">**-리소스 그룹**: 새로 만든 hello 앱 서비스 계획을 포함 하는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-114">**--resource-group**: resource group that includes hello newly created app service plan.</span></span>
* <span data-ttu-id="5cb89-115">**-이름**: hello 앱 서비스 계획의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-115">**--name**: name of hello app service plan.</span></span>
* <span data-ttu-id="5cb89-116">**--location**: App Service 계획 위치</span><span class="sxs-lookup"><span data-stu-id="5cb89-116">**--location**: app service plan location.</span></span>
* <span data-ttu-id="5cb89-117">**-sku**: hello 필요한 가격 책정 sku (hello 옵션은: F1 (Free).</span><span class="sxs-lookup"><span data-stu-id="5cb89-117">**--sku**:  hello desired pricing sku (hello options are: F1 (Free).</span></span> <span data-ttu-id="5cb89-118">D1(공유)</span><span class="sxs-lookup"><span data-stu-id="5cb89-118">D1 (Shared).</span></span> <span data-ttu-id="5cb89-119">B1(Basic Small), B2(Basic Medium), B3(Basic Large)</span><span class="sxs-lookup"><span data-stu-id="5cb89-119">B1 (Basic Small), B2 (Basic Medium), and B3 (Basic Large).</span></span> <span data-ttu-id="5cb89-120">S1(Standard Small), S2(Standard Medium), S3(Standard Large)</span><span class="sxs-lookup"><span data-stu-id="5cb89-120">S1 (Standard Small), S2 (Standard Medium), and S3 (Standard Large).</span></span> <span data-ttu-id="5cb89-121">P1(Premium Small), P2(Premium Medium), P3(Premium Large)</span><span class="sxs-lookup"><span data-stu-id="5cb89-121">P1 (Premium Small), P2 (Premium Medium), and P3 (Premium Large).)</span></span>
* <span data-ttu-id="5cb89-122">**-인스턴스**: (기본값은 1) hello 앱 서비스 계획의 작업자 수가 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-122">**--instances**: hello number of workers in hello app service plan (Default value is 1).</span></span>

<span data-ttu-id="5cb89-123">예제 toouse이이 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5cb89-123">Example toouse this cmdlet:</span></span>

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="5cb89-124">Linux App Service 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="5cb89-124">Create a Linux App Service Plan</span></span>

<span data-ttu-id="5cb89-125">동일한 hello를 사용 하 여 **azure appserviceplan 만들** hello로 명령을 추가 매개 변수 **-islinux true**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-125">Using hello same **azure appserviceplan create** command, with hello extra parameter **--islinux true**.</span></span> <span data-ttu-id="5cb89-126">Hello 제한 사항 및 지역에 설명 된 유의 [소개 tooApp linux 서비스](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="5cb89-126">Note hello restrictions and regions outlined in [Introduction tooApp Service on Linux](app-service-linux-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="5cb89-127">기존 앱 서비스 계획 나열</span><span class="sxs-lookup"><span data-stu-id="5cb89-127">List Existing App Service Plans</span></span>
<span data-ttu-id="5cb89-128">toolist hello 기존 앱 서비스 계획을 사용 하 여 **azure appserviceplan 목록** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-128">toolist hello existing app service plans, use **azure appserviceplan list** command.</span></span>

<span data-ttu-id="5cb89-129">toolist 특정 리소스 그룹 아래의 모든 앱 서비스 계획을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-129">toolist all app service plans under a specific resource group, use:</span></span>

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="5cb89-130">tooget 특정 앱 서비스 계획을 사용 하 여 **azure appserviceplan 표시** 명령:</span><span class="sxs-lookup"><span data-stu-id="5cb89-130">tooget a specific app service plan, use **azure appserviceplan show** command:</span></span>

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="5cb89-131">기존 앱 서비스 계획 구성</span><span class="sxs-lookup"><span data-stu-id="5cb89-131">Configure an existing App Service Plan</span></span>
<span data-ttu-id="5cb89-132">기존 앱 서비스 계획에 대 한 toochange hello 설정을 사용 하 여 hello **azure appserviceplan config** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-132">toochange hello settings for an existing app service plan, use hello **azure appserviceplan config** command.</span></span> <span data-ttu-id="5cb89-133">Hello sku 및 hello 작업자 수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-133">You can change hello sku, and hello number of workers</span></span> 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="5cb89-134">앱 서비스 계획 크기 조정</span><span class="sxs-lookup"><span data-stu-id="5cb89-134">Scaling an App Service Plan</span></span>
<span data-ttu-id="5cb89-135">tooscale는 기존 앱 서비스 계획을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-135">tooscale an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-hello-sku-of-an-app-service-plan"></a><span data-ttu-id="5cb89-136">앱 서비스 계획의 SKU hello 변경</span><span class="sxs-lookup"><span data-stu-id="5cb89-136">Changing hello SKU of an App Service Plan</span></span>
<span data-ttu-id="5cb89-137">기존 앱 서비스 계획을 사용 하 여의 toochange hello sku:</span><span class="sxs-lookup"><span data-stu-id="5cb89-137">toochange hello sku of an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="5cb89-138">기존 앱 서비스 계획 삭제</span><span class="sxs-lookup"><span data-stu-id="5cb89-138">Delete an existing App Service Plan</span></span>
<span data-ttu-id="5cb89-139">기존 앱 서비스 계획 toodelete 모두 할당 됨 앱 필요 toobe 이동 하거나 먼저 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-139">toodelete an existing app service plan, all assigned apps need toobe moved or deleted first.</span></span> <span data-ttu-id="5cb89-140">그런 다음 hello를 사용 하 여 **azure webapp 삭제** 명령 hello 앱 서비스 계획을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-140">Then using hello **azure webapp delete** command you can delete hello app service plan.</span></span>

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a><span data-ttu-id="5cb89-141">App Service 앱 관리</span><span class="sxs-lookup"><span data-stu-id="5cb89-141">Managing App Service apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="5cb89-142">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="5cb89-142">Create a web app</span></span>
<span data-ttu-id="5cb89-143">toocreate 웹 응용 프로그램에서 사용 하 여 hello **azure webapp 만들** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-143">toocreate a web app, use hello **azure webapp create** command.</span></span>

<span data-ttu-id="5cb89-144">다음은 hello 다른 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="5cb89-144">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="5cb89-145">**-이름**: hello 웹 앱에 대 한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-145">**--name**: name for hello web app.</span></span>
* <span data-ttu-id="5cb89-146">**-계획**: toohost hello 웹 응용 프로그램을 사용 하는 hello 서비스 계획에 대 한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-146">**--plan**: name for hello service plan used toohost hello web app.</span></span>
* <span data-ttu-id="5cb89-147">**-리소스 그룹**: hello 앱 서비스 계획을 호스팅하는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-147">**--resource-group**: resource group that hosts hello App service plan.</span></span>
* <span data-ttu-id="5cb89-148">**-위치**: 웹 앱 위치의 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-148">**--location**: hello web app location.</span></span>

<span data-ttu-id="5cb89-149">예제 toouse이이 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5cb89-149">Example toouse this cmdlet:</span></span>

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a><span data-ttu-id="5cb89-150">기존 앱 삭제</span><span class="sxs-lookup"><span data-stu-id="5cb89-150">Delete an existing app</span></span>
<span data-ttu-id="5cb89-151">기존 앱 toodelete hello를 사용할 수 있습니다 **azure webapp 삭제** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-151">toodelete an existing app, you can use hello **azure webapp delete** command.</span></span> <span data-ttu-id="5cb89-152">Hello 앱 toospecify hello 이름과 hello 리소스 그룹 이름은 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-152">You need toospecify hello name of hello app and hello resource group name.</span></span>

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a><span data-ttu-id="5cb89-153">기존 앱 목록</span><span class="sxs-lookup"><span data-stu-id="5cb89-153">List existing apps</span></span>
<span data-ttu-id="5cb89-154">toolist hello 기존 응용 프로그램을 사용 하 여 hello **azure webapp 목록** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-154">toolist hello existing apps, use hello **azure webapp list** command.</span></span>

<span data-ttu-id="5cb89-155">toolist 특정 리소스 그룹에서 모든 앱을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-155">toolist all apps in a specific resource group, use:</span></span>

    azure webapp list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="5cb89-156">특정 앱 tooget hello를 사용 하 여 **azure webapp 표시** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-156">tooget a specific app, use hello **azure webapp show** command.</span></span>

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a><span data-ttu-id="5cb89-157">기존 앱 구성</span><span class="sxs-lookup"><span data-stu-id="5cb89-157">Configure an existing app</span></span>
<span data-ttu-id="5cb89-158">toochange hello 설정 및 기존 응용 프로그램에 대 한 구성을 사용 하 여 hello **azure webapp 구성 집합** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-158">toochange hello settings and configurations for an existing app, use hello **azure webapp config set** command.</span></span>

<span data-ttu-id="5cb89-159">응용 프로그램의 hello php 버전을 변경 하는 예 (1):</span><span class="sxs-lookup"><span data-stu-id="5cb89-159">Example (1): change hello php version of a app</span></span> 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

<span data-ttu-id="5cb89-160">예 (2): 앱 설정 추가 또는 변경</span><span class="sxs-lookup"><span data-stu-id="5cb89-160">Example (2): add or change app settings</span></span>

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

<span data-ttu-id="5cb89-161">tooknow 다른 구성을 변경할 수 있습니다를 사용 하 여 hello **azure webapp 구성 집합-h** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-161">tooknow what other configuration can be changed, use hello **azure webapp config set -h** command.</span></span>

### <a name="change-hello-state-of-an-existing-app"></a><span data-ttu-id="5cb89-162">기존 앱의 hello 상태 변경</span><span class="sxs-lookup"><span data-stu-id="5cb89-162">Change hello state of an existing app</span></span>
#### <a name="restart-an-app"></a><span data-ttu-id="5cb89-163">앱 다시 시작</span><span class="sxs-lookup"><span data-stu-id="5cb89-163">Restart an app</span></span>
<span data-ttu-id="5cb89-164">응용 프로그램 toorestart, hello 응용 프로그램의 hello 이름과 리소스 그룹을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-164">toorestart an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a><span data-ttu-id="5cb89-165">앱 중지</span><span class="sxs-lookup"><span data-stu-id="5cb89-165">Stop an app</span></span>
<span data-ttu-id="5cb89-166">응용 프로그램 toostop, hello 응용 프로그램의 hello 이름과 리소스 그룹을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-166">toostop an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a><span data-ttu-id="5cb89-167">앱 시작</span><span class="sxs-lookup"><span data-stu-id="5cb89-167">Start an app</span></span>
<span data-ttu-id="5cb89-168">응용 프로그램 toostart, hello 응용 프로그램의 hello 이름과 리소스 그룹을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-168">toostart an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a><span data-ttu-id="5cb89-169">앱의 게시 프로필 관리</span><span class="sxs-lookup"><span data-stu-id="5cb89-169">Manage publishing profiles of an app</span></span>
<span data-ttu-id="5cb89-170">각 응용 프로그램 코드를 사용 하는 toopublish 일 수 있는 게시 프로필에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-170">Each app has a publishing profile that can be used toopublish your code.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="5cb89-171">게시 프로필 가져오기</span><span class="sxs-lookup"><span data-stu-id="5cb89-171">Get Publishing Profile</span></span>
<span data-ttu-id="5cb89-172">tooget hello를 사용 하 여 응용 프로그램에 대 한 프로필 게시:</span><span class="sxs-lookup"><span data-stu-id="5cb89-172">tooget hello publishing profile for a app, use:</span></span>

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

<span data-ttu-id="5cb89-173">이 명령은 hello 게시 프로필 사용자 이름 및 암호 toohello 명령줄에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-173">This command echoes hello publishing profile username and password toohello command line.</span></span>

### <a name="manage-app-hostnames"></a><span data-ttu-id="5cb89-174">앱 호스트 관리</span><span class="sxs-lookup"><span data-stu-id="5cb89-174">Manage app hostnames</span></span>
<span data-ttu-id="5cb89-175">응용 프로그램에 대 한 호스트 이름 바인딩을 toomanage hello를 사용 하 여 **azure webapp config hostnames** 명령</span><span class="sxs-lookup"><span data-stu-id="5cb89-175">toomanage hostname bindings for your app, use hello **azure webapp config hostnames** command</span></span>  

#### <a name="list-hostname-bindings"></a><span data-ttu-id="5cb89-176">호스트 이름 바인딩 나열</span><span class="sxs-lookup"><span data-stu-id="5cb89-176">List hostname bindings</span></span>
<span data-ttu-id="5cb89-177">응용 프로그램에 대 한 tooget hello 현재 호스트 이름 바인딩을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-177">tooget hello current hostname bindings for an app, use:</span></span>

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a><span data-ttu-id="5cb89-178">호스트 이름 바인딩 추가</span><span class="sxs-lookup"><span data-stu-id="5cb89-178">Add hostname bindings</span></span>
<span data-ttu-id="5cb89-179">tooadd 호스트 이름 바인딩 tooan 앱을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="5cb89-179">tooadd hostname bindings tooan app, use:</span></span>

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a><span data-ttu-id="5cb89-180">호스트 이름 바인딩 삭제</span><span class="sxs-lookup"><span data-stu-id="5cb89-180">Delete hostname bindings</span></span>
<span data-ttu-id="5cb89-181">toodelete 호스트 이름 바인딩을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb89-181">toodelete hostname bindings, use:</span></span>

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a><span data-ttu-id="5cb89-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5cb89-182">Next Steps</span></span>
* <span data-ttu-id="5cb89-183">Azure 리소스 관리자 CLI 지원에 대 한 toolearn 참조 [hello Azure CLI toomanage Azure를 사용 하 여 리소스 및 리소스 그룹입니다.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="5cb89-183">toolearn about Azure Resource Manager CLI support, see [Use hello Azure CLI toomanage Azure resources and resource groups.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span></span>
* <span data-ttu-id="5cb89-184">PowerShell을 사용 하는 응용 프로그램 서비스를 관리 하는 방법에 대 한 toolearn 참조 [Using Azure Resource Manager-Based PowerShell tooManage Azure 웹 앱입니다.](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="5cb89-184">toolearn about managing App Service using PowerShell, see [Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span></span>
* <span data-ttu-id="5cb89-185">linux에서 Azure 앱 서비스에 대 한 toolearn 참조 [소개 tooApp linux 서비스](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="5cb89-185">toolearn about Azure App Service on Linux, see [Introduction tooApp Service on Linux](app-service-linux-intro.md)</span></span>
