---
title: "컨테이너 레지스트리 리포지토리 aaaAzure | Microsoft Docs"
description: "어떻게 Docker 이미지에 대 한 toouse Azure 컨테이너 레지스트리 리포지토리"
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
ms.openlocfilehash: 448fb812f537c9502041ce5fb372b0681a9dac4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-powershell"></a><span data-ttu-id="85c6a-103">Hello Azure PowerShell을 사용 하 여 개인 Docker 컨테이너 등록 만들기</span><span class="sxs-lookup"><span data-stu-id="85c6a-103">Create a private Docker container registry using hello Azure PowerShell</span></span>
<span data-ttu-id="85c6a-104">명령을 사용 하 여 [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate 컨테이너 레지스트리 및 Windows 컴퓨터에서 해당 설정을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-104">Use commands in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate a container registry and manage its settings from your Windows computer.</span></span> <span data-ttu-id="85c6a-105">또한 생성 하 고 컨테이너 레지스트리에 hello를 사용 하 여 관리 수 [Azure 포털](container-registry-get-started-portal.md), hello [Azure CLI](container-registry-get-started-azure-cli.md), 또는 프로그래밍 방식으로 컨테이너 레지스트리 hello [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376)합니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-105">You can also create and manage container registries using hello [Azure portal](container-registry-get-started-portal.md), hello [Azure CLI](container-registry-get-started-azure-cli.md), or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="85c6a-106">배경 및 개념에 대 한 참조 [hello 개요](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="85c6a-106">For background and concepts, see [hello overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="85c6a-107">지원되는 cmdlet의 전체 목록은 [Azure Container Registry 관리 Cmdlet](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85c6a-107">For a full list of supported cmdlets, see [Azure Container Registry Management Cmdlets](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="85c6a-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="85c6a-108">Prerequisites</span></span>
* <span data-ttu-id="85c6a-109">**Azure PowerShell**: tooinstall Azure PowerShell을 시작 하 고 hello를 참조 하십시오 [설치 지침](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)합니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-109">**Azure PowerShell**: tooinstall and get started with Azure PowerShell, see hello [installation instructions](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="85c6a-110">실행 하 여 Azure 구독 tooyour 로그인 `Login-AzureRMAccount`합니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-110">Log in tooyour Azure subscription by running `Login-AzureRMAccount`.</span></span> <span data-ttu-id="85c6a-111">자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85c6a-111">For more information, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span></span>
* <span data-ttu-id="85c6a-112">**리소스 그룹**: 컨테이너 레지스트리를 만들기 전에 [리소스 그룹](../azure-resource-manager/resource-group-overview.md#resource-groups)을 만들거나 기존 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="85c6a-113">컨테이너 레지스트리 서비스가 hello는 위치에는 hello 리소스 그룹이 있는지 확인 [사용 가능한](https://azure.microsoft.com/regions/services/)합니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-113">Make sure hello resource group is in a location where hello Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="85c6a-114">Azure PowerShell을 사용 하 여 리소스 그룹 toocreate 참조 [PowerShell 참조 hello](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group)합니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-114">toocreate a resource group using Azure PowerShell, see [hello PowerShell reference](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span></span>
* <span data-ttu-id="85c6a-115">**저장소 계정** (선택 사항): 표준 Azure 만들기 [저장소 계정](../storage/common/storage-introduction.md) tooback hello 컨테이너 레지스트리 hello에서 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) tooback hello container registry in hello same location.</span></span> <span data-ttu-id="85c6a-116">사용 하 여 레지스트리를 만들 때 저장소 계정을 지정 하지 않으면 `New-AzureRMContainerRegistry`, 솔루션이 hello 명령을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-116">If you don't specify a storage account when creating a registry with `New-AzureRMContainerRegistry`, hello command creates one for you.</span></span> <span data-ttu-id="85c6a-117">PowerShell을 사용 하 여 계정, 참조이 toocreate 저장소 [PowerShell 참조 hello](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount)합니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-117">toocreate a storage account using PowerShell, see [hello PowerShell reference](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span></span> <span data-ttu-id="85c6a-118">Premium Storage는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="85c6a-119">**서비스 주체**(선택 사항): PowerShell을 사용하여 레지스트리를 만들 때 기본적으로 액세스가 가능하도록 설정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-119">**Service principal** (optional): When you create a registry with PowerShell, by default it is not set up for access.</span></span> <span data-ttu-id="85c6a-120">필요에 따라 수는 기존 Azure Active Directory 서비스 보안 주체 tooa 레지스트리 할당 또는 만들고 새 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-120">Depending on your needs, you can assign an existing Azure Active Directory service principal tooa registry or create and assign a new one.</span></span> <span data-ttu-id="85c6a-121">또는 hello 레지스트리 관리자 사용자 계정을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-121">Alternatively, you can enable hello registry's admin user account.</span></span> <span data-ttu-id="85c6a-122">이 문서의 뒷부분에 나오는 hello 섹션을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="85c6a-122">See hello sections later in this article.</span></span> <span data-ttu-id="85c6a-123">레지스트리 액세스 하는 방법에 대 한 자세한 내용은 참조 [hello 컨테이너 레지스트리로 인증](container-registry-authentication.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-123">For more information about registry access, see [Authenticate with hello container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="85c6a-124">컨테이너 레지스트리 만들기</span><span class="sxs-lookup"><span data-stu-id="85c6a-124">Create a container registry</span></span>
<span data-ttu-id="85c6a-125">Hello 실행 `New-AzureRMContainerRegistry` 명령 toocreate 컨테이너 레지스트리 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-125">Run hello `New-AzureRMContainerRegistry` command toocreate a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="85c6a-126">레지스트리를 만들 때 전역적으로 고유한 최상위 도메인 이름(문자 및 숫자만 포함)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-126">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="85c6a-127">hello 예에서 hello 레지스트리 이름이 `MyRegistry`, 되지만 대신 사용자 고유의의 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-127">hello registry name in hello examples is `MyRegistry`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="85c6a-128">다음 명령을 사용 하 여 최소한의 매개 변수 toocreate 컨테이너 레지스트리 hello hello `MyRegistry` hello 리소스 그룹에 `MyResourceGroup` hello 미국 중남부 위치에서에서:</span><span class="sxs-lookup"><span data-stu-id="85c6a-128">hello following command uses hello minimal parameters toocreate container registry `MyRegistry` in hello resource group `MyResourceGroup` in hello South Central US location:</span></span>

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* <span data-ttu-id="85c6a-129">`-StorageAccountName` 는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-129">`-StorageAccountName` is optional.</span></span> <span data-ttu-id="85c6a-130">하지 않은 경우, 지정 된 저장소 계정을 hello 레지스트리 이름으로 된 이름을 만들어지고 타임 스탬프 hello에서 리소스 그룹을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-130">If not specified, a storage account is created with a name consisting of hello registry name and a timestamp in hello specified resource group.</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="85c6a-131">서비스 주체 할당</span><span class="sxs-lookup"><span data-stu-id="85c6a-131">Assign a service principal</span></span>
<span data-ttu-id="85c6a-132">PowerShell 명령 tooassign Azure Active Directory를 사용 하 여 [서비스 사용자](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa 레지스트리 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-132">Use PowerShell commands tooassign an Azure Active Directory [service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa registry.</span></span> <span data-ttu-id="85c6a-133">hello 이러한 예에서 서비스 사용자는 할당 hello 소유자 역할 되지만 할당할 수 있습니다 [다른 역할](../active-directory/role-based-access-control-configure.md) 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-133">hello service principal in these examples is assigned hello Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal"></a><span data-ttu-id="85c6a-134">서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="85c6a-134">Create a service principal</span></span>
<span data-ttu-id="85c6a-135">다음 명령을 hello, 새 서비스 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-135">In hello following command, a new service principal is created.</span></span> <span data-ttu-id="85c6a-136">Hello로 강력한 암호를 지정 `-Password` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-136">Specify a strong password with hello `-Password` parameter.</span></span>

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a><span data-ttu-id="85c6a-137">새로운 서비스 주체 또는 기존 서비스 주체 할당</span><span class="sxs-lookup"><span data-stu-id="85c6a-137">Assign a new or existing service principal</span></span>
<span data-ttu-id="85c6a-138">새 데이터베이스 또는 기존 서비스 보안 주체 tooa 레지스트리를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-138">You can assign a new or an existing service principal tooa registry.</span></span> <span data-ttu-id="85c6a-139">tooassign 것 소유자 역할 액세스 toohello 레지스트리, 다음 예제 명령은 비슷한 toohello 실행:</span><span class="sxs-lookup"><span data-stu-id="85c6a-139">tooassign it Owner role access toohello registry, run a command similar toohello following example:</span></span>

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-toohello-registry-with-hello-service-principal"></a><span data-ttu-id="85c6a-140">Hello 서비스 사용자를 사용 하 여 toohello 레지스트리에 로그인</span><span class="sxs-lookup"><span data-stu-id="85c6a-140">Sign in toohello registry with hello service principal</span></span>
<span data-ttu-id="85c6a-141">Hello 서비스 보안 주체 toohello 레지스트리를 할당 한 후 다음 명령을 hello를 사용 하 여 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-141">After assigning hello service principal toohello registry, you can sign in using hello following command:</span></span>

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a><span data-ttu-id="85c6a-142">관리자 자격 증명 관리</span><span class="sxs-lookup"><span data-stu-id="85c6a-142">Manage admin credentials</span></span>
<span data-ttu-id="85c6a-143">관리자 계정은 각 컨테이너 레지스트리에 대해 자동으로 생성되며 기본적으로 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="85c6a-143">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="85c6a-144">hello 다음 예제에서는 PowerShell 명령을 toomanage hello 컨테이너 레지스트리에 대 한 자격 증명 관리</span><span class="sxs-lookup"><span data-stu-id="85c6a-144">hello following examples show PowerShell commands toomanage hello admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="85c6a-145">관리자 사용자 자격 증명 가져오기</span><span class="sxs-lookup"><span data-stu-id="85c6a-145">Obtain admin user credentials</span></span>
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="85c6a-146">기존 레지스트리에 대한 관리자 사용자 활성화</span><span class="sxs-lookup"><span data-stu-id="85c6a-146">Enable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="85c6a-147">기존 레지스트리에 대한 관리자 사용자 비활성화</span><span class="sxs-lookup"><span data-stu-id="85c6a-147">Disable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a><span data-ttu-id="85c6a-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="85c6a-148">Next steps</span></span>
* [<span data-ttu-id="85c6a-149">Hello Docker CLI를 사용 하 여 첫 번째 이미지 강제</span><span class="sxs-lookup"><span data-stu-id="85c6a-149">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
