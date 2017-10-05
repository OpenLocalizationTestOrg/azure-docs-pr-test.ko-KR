---
title: "Azure 컨테이너 레지스트리 리포지토리 | Microsoft Docs"
description: "Docker 이미지에 Azure 컨테이너 레지스트리 리포지토리를 사용하는 방법"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: cristyg
ms.openlocfilehash: 1e5d5ea5b1ec121fe008abc48178b1d58f540ce1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-private-docker-container-registry-using-the-azure-powershell"></a><span data-ttu-id="e1730-103">Azure PowerShell을 사용하여 개인 Docker 컨테이너 레지스트리 만들기</span><span class="sxs-lookup"><span data-stu-id="e1730-103">Create a private Docker container registry using the Azure PowerShell</span></span>
<span data-ttu-id="e1730-104">[Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview)의 명령을 사용하여 Windows 컴퓨터에서 컨테이너 레지스트리를 만들고 설정을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-104">Use commands in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) to create a container registry and manage its settings from your Windows computer.</span></span> <span data-ttu-id="e1730-105">[Azure Portal](container-registry-get-started-portal.md), [Azure CLI](container-registry-get-started-azure-cli.md)을 사용하여 또는 Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376)를 사용하여 프로그래밍 방식으로 컨테이너 레지스트리를 만들고 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-105">You can also create and manage container registries using the [Azure portal](container-registry-get-started-portal.md), the [Azure CLI](container-registry-get-started-azure-cli.md), or programmatically with the Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="e1730-106">배경 지식 및 개념은 [개요](container-registry-intro.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1730-106">For background and concepts, see [the overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="e1730-107">지원되는 cmdlet의 전체 목록은 [Azure Container Registry 관리 Cmdlet](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1730-107">For a full list of supported cmdlets, see [Azure Container Registry Management Cmdlets](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e1730-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e1730-108">Prerequisites</span></span>
* <span data-ttu-id="e1730-109">**Azure PowerShell**: Azure PowerShell을 설치하고 시작하려면 [설치 지침](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1730-109">**Azure PowerShell**: To install and get started with Azure PowerShell, see the [installation instructions](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="e1730-110">`Login-AzureRMAccount`을 실행하여 Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-110">Log in to your Azure subscription by running `Login-AzureRMAccount`.</span></span> <span data-ttu-id="e1730-111">자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1730-111">For more information, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span></span>
* <span data-ttu-id="e1730-112">**리소스 그룹**: 컨테이너 레지스트리를 만들기 전에 [리소스 그룹](../azure-resource-manager/resource-group-overview.md#resource-groups)을 만들거나 기존 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="e1730-113">리소스 그룹이 Container Registry 서비스를 [사용할 수 있는](https://azure.microsoft.com/regions/services/) 위치에 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-113">Make sure the resource group is in a location where the Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="e1730-114">Azure PowerShell을 사용하여 리소스 그룹을 만들려면 [PowerShell 참조](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1730-114">To create a resource group using Azure PowerShell, see [the PowerShell reference](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span></span>
* <span data-ttu-id="e1730-115">**저장소 계정**(선택 사항): 동일한 위치의 컨테이너 레지스트리를 백업할 표준 Azure [저장소 계정](../storage/common/storage-introduction.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) to back the container registry in the same location.</span></span> <span data-ttu-id="e1730-116">`New-AzureRMContainerRegistry`를 사용하여 레지스트리를 만들 때 저장소 계정을 지정하지 않으면 명령에서 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-116">If you don't specify a storage account when creating a registry with `New-AzureRMContainerRegistry`, the command creates one for you.</span></span> <span data-ttu-id="e1730-117">PowerShell을 사용하여 저장소 계정을 만들려면 [PowerShell 참조](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1730-117">To create a storage account using PowerShell, see [the PowerShell reference](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span></span> <span data-ttu-id="e1730-118">Premium Storage는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="e1730-119">**서비스 주체**(선택 사항): PowerShell을 사용하여 레지스트리를 만들 때 기본적으로 액세스가 가능하도록 설정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-119">**Service principal** (optional): When you create a registry with PowerShell, by default it is not set up for access.</span></span> <span data-ttu-id="e1730-120">필요에 따라 레지스트리에 기존 Azure Active Directory 서비스 주체를 할당하거나 새 주체를 만들어서 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-120">Depending on your needs, you can assign an existing Azure Active Directory service principal to a registry or create and assign a new one.</span></span> <span data-ttu-id="e1730-121">또는 레지스트리의 관리 사용자 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-121">Alternatively, you can enable the registry's admin user account.</span></span> <span data-ttu-id="e1730-122">이 문서의 뒷부분에 나오는 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1730-122">See the sections later in this article.</span></span> <span data-ttu-id="e1730-123">레지스트리 액세스에 대한 자세한 내용은 [컨테이너 레지스트리로 인증](container-registry-authentication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1730-123">For more information about registry access, see [Authenticate with the container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="e1730-124">컨테이너 레지스트리 만들기</span><span class="sxs-lookup"><span data-stu-id="e1730-124">Create a container registry</span></span>
<span data-ttu-id="e1730-125">`New-AzureRMContainerRegistry` 명령을 실행하여 컨테이너 레지스트리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-125">Run the `New-AzureRMContainerRegistry` command to create a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="e1730-126">레지스트리를 만들 때 전역적으로 고유한 최상위 도메인 이름(문자 및 숫자만 포함)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-126">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="e1730-127">레지스트리 이름 예제가 `MyRegistry`이지만 자신만의 고유한 이름으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-127">The registry name in the examples is `MyRegistry`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="e1730-128">다음 명령은 미국 중남부 지역에 `MyResourceGroup`이라는 리소스 그룹의 `MyRegistry`라는 컨테이너 레지스트리를 만들기 위해 최소의 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-128">The following command uses the minimal parameters to create container registry `MyRegistry` in the resource group `MyResourceGroup` in the South Central US location:</span></span>

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* <span data-ttu-id="e1730-129">`-StorageAccountName` 는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-129">`-StorageAccountName` is optional.</span></span> <span data-ttu-id="e1730-130">지정하지 않으면 지정된 리소스 그룹에서 레지스트리 이름 및 타임스탬프로 구성된 이름으로 저장소 계정이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-130">If not specified, a storage account is created with a name consisting of the registry name and a timestamp in the specified resource group.</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="e1730-131">서비스 주체 할당</span><span class="sxs-lookup"><span data-stu-id="e1730-131">Assign a service principal</span></span>
<span data-ttu-id="e1730-132">PowerShell 명령을 사용하여 Azure Active Directory [서비스 주체](../azure-resource-manager/resource-group-authenticate-service-principal.md)를 레지스트리에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-132">Use PowerShell commands to assign an Azure Active Directory [service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md) to a registry.</span></span> <span data-ttu-id="e1730-133">이 예제의 경우 서비스 주체에 소유자 역할이 할당되어 있지만 필요하면 [다른 역할](../active-directory/role-based-access-control-configure.md)을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-133">The service principal in these examples is assigned the Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal"></a><span data-ttu-id="e1730-134">서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="e1730-134">Create a service principal</span></span>
<span data-ttu-id="e1730-135">다음 명령에서 새 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-135">In the following command, a new service principal is created.</span></span> <span data-ttu-id="e1730-136">`-Password` 매개 변수를 통해 강력한 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-136">Specify a strong password with the `-Password` parameter.</span></span>

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a><span data-ttu-id="e1730-137">새로운 서비스 주체 또는 기존 서비스 주체 할당</span><span class="sxs-lookup"><span data-stu-id="e1730-137">Assign a new or existing service principal</span></span>
<span data-ttu-id="e1730-138">레지스트리에 새 서비스 주체 또는 기존 서비스 주체를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-138">You can assign a new or an existing service principal to a registry.</span></span> <span data-ttu-id="e1730-139">레지스트리에 소유자 역할 액세스를 할당하려면 다음 예제와 유사한 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-139">To assign it Owner role access to the registry, run a command similar to the following example:</span></span>

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-to-the-registry-with-the-service-principal"></a><span data-ttu-id="e1730-140">서비스 주체를 사용하여 레지스트리에 로그인</span><span class="sxs-lookup"><span data-stu-id="e1730-140">Sign in to the registry with the service principal</span></span>
<span data-ttu-id="e1730-141">레지스트리에 서비스 주체를 할당한 후에 다음 명령을 사용하여 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-141">After assigning the service principal to the registry, you can sign in using the following command:</span></span>

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a><span data-ttu-id="e1730-142">관리자 자격 증명 관리</span><span class="sxs-lookup"><span data-stu-id="e1730-142">Manage admin credentials</span></span>
<span data-ttu-id="e1730-143">관리자 계정은 각 컨테이너 레지스트리에 대해 자동으로 생성되며 기본적으로 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-143">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="e1730-144">다음 예제는 컨테이너 레지스트리에 대한 관리자 자격 증명을 관리하는 PowerShell 명령을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e1730-144">The following examples show PowerShell commands to manage the admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="e1730-145">관리자 사용자 자격 증명 가져오기</span><span class="sxs-lookup"><span data-stu-id="e1730-145">Obtain admin user credentials</span></span>
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="e1730-146">기존 레지스트리에 대한 관리자 사용자 활성화</span><span class="sxs-lookup"><span data-stu-id="e1730-146">Enable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="e1730-147">기존 레지스트리에 대한 관리자 사용자 비활성화</span><span class="sxs-lookup"><span data-stu-id="e1730-147">Disable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a><span data-ttu-id="e1730-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e1730-148">Next steps</span></span>
* [<span data-ttu-id="e1730-149">Docker CLI를 사용하여 첫 번째 이미지 푸시</span><span class="sxs-lookup"><span data-stu-id="e1730-149">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
