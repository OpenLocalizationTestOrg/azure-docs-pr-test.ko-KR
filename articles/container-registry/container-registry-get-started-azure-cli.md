---
title: "개인 Docker 컨테이너 레지스트리 만들기 - Azure CLI | Microsoft Docs"
description: "Azure CLI 2.0을 사용하여 개인 Docker 컨테이너 레지스트리 만들기 및 관리 시작"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2875f4089231ed12a0312b2c2e077938440365c6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-private-docker-container-registry-using-the-azure-cli-20"></a><span data-ttu-id="16106-103">Azure CLI 2.0을 사용하여 개인 Docker 컨테이너 레지스트리 만들기</span><span class="sxs-lookup"><span data-stu-id="16106-103">Create a private Docker container registry using the Azure CLI 2.0</span></span>
<span data-ttu-id="16106-104">[Azure CLI 2.0](https://github.com/Azure/azure-cli)의 명령을 사용하여 Linux, Mac 또는 Windows 컴퓨터에서 컨테이너 레지스트리를 만들고 설정을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="16106-104">Use commands in the [Azure CLI 2.0](https://github.com/Azure/azure-cli) to create a container registry and manage its settings from your Linux, Mac, or Windows computer.</span></span> <span data-ttu-id="16106-105">[Azure Portal](container-registry-get-started-portal.md)을 사용하여 또는 Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376)를 사용하여 프로그래밍 방식으로 컨테이너 레지스트리를 만들고 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16106-105">You can also create and manage container registries using the [Azure portal](container-registry-get-started-portal.md) or programmatically with the Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="16106-106">배경 지식 및 개념은 [개요](container-registry-intro.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16106-106">For background and concepts, see [the overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="16106-107">Container Registry CLI 명령(`az acr` 명령)에 대한 도움말을 보려면, 모든 명령에 `-h` 매개 변수를 전달하세요.</span><span class="sxs-lookup"><span data-stu-id="16106-107">For help on Container Registry CLI commands (`az acr` commands), pass the `-h` parameter to any command.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="16106-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="16106-108">Prerequisites</span></span>
* <span data-ttu-id="16106-109">**Azure CLI 2.0**: CLI 2.0을 설치하고 시작하려면 [설치 지침](/cli/azure/install-azure-cli)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16106-109">**Azure CLI 2.0**: To install and get started with the CLI 2.0, see the [installation instructions](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="16106-110">`az login`을 실행하여 Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="16106-110">Log in to your Azure subscription by running `az login`.</span></span> <span data-ttu-id="16106-111">자세한 내용은 [CLI 2.0 시작](/cli/azure/get-started-with-azure-cli)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16106-111">For more information, see [Get started with the CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="16106-112">**리소스 그룹**: 컨테이너 레지스트리를 만들기 전에 [리소스 그룹](../azure-resource-manager/resource-group-overview.md#resource-groups)을 만들거나 기존 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="16106-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="16106-113">리소스 그룹이 Container Registry 서비스를 [사용할 수 있는](https://azure.microsoft.com/regions/services/) 위치에 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16106-113">Make sure the resource group is in a location where the Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="16106-114">CLI 2.0을 사용하여 리소스 그룹을 만들려면 [CLI 2.0 참조](/cli/azure/group)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16106-114">To create a resource group using the CLI 2.0, see [the CLI 2.0 reference](/cli/azure/group).</span></span>
* <span data-ttu-id="16106-115">**저장소 계정**(선택 사항): 동일한 위치의 컨테이너 레지스트리를 백업할 표준 Azure [저장소 계정](../storage/common/storage-introduction.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="16106-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) to back the container registry in the same location.</span></span> <span data-ttu-id="16106-116">`az acr create`를 사용하여 레지스트리를 만들 때 저장소 계정을 지정하지 않으면 명령에서 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="16106-116">If you don't specify a storage account when creating a registry with `az acr create`, the command creates one for you.</span></span> <span data-ttu-id="16106-117">CLI 2.0을 사용하여 저장소 계정을 만들려면 [CLI 2.0 참조](/cli/azure/storage/account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16106-117">To create a storage account using the CLI 2.0, see [the CLI 2.0 reference](/cli/azure/storage/account).</span></span> <span data-ttu-id="16106-118">Premium Storage는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16106-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="16106-119">**서비스 주체**(선택 사항): CLI를 사용하여 레지스트리를 만들 때 기본적으로 액세스가 가능하도록 설정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16106-119">**Service principal** (optional): When you create a registry with the CLI, by default it is not set up for access.</span></span> <span data-ttu-id="16106-120">필요에 따라 레지스트리에 기존 Azure Active Directory 서비스 주체를 할당하거나(또는 새 주체를 만들어서 할당하거나) 레지스트리의 관리자 사용자 계정을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16106-120">Depending on your needs, you can assign an existing Azure Active Directory service principal to a registry (or create and assign a new one), or enable the registry's admin user account.</span></span> <span data-ttu-id="16106-121">이 문서의 뒷부분에 나오는 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16106-121">See the sections later in this article.</span></span> <span data-ttu-id="16106-122">레지스트리 액세스에 대한 자세한 내용은 [컨테이너 레지스트리로 인증](container-registry-authentication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16106-122">For more information about registry access, see [Authenticate with the container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="16106-123">컨테이너 레지스트리 만들기</span><span class="sxs-lookup"><span data-stu-id="16106-123">Create a container registry</span></span>
<span data-ttu-id="16106-124">`az acr create` 명령을 실행하여 컨테이너 레지스트리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="16106-124">Run the `az acr create` command to create a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="16106-125">레지스트리를 만들 때 전역적으로 고유한 최상위 도메인 이름(문자 및 숫자만 포함)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="16106-125">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="16106-126">레지스트리 이름 예제가 `myRegistry1`이지만 자신만의 고유한 이름으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="16106-126">The registry name in the examples is `myRegistry1`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="16106-127">다음 명령은 최소 매개 변수를 사용하여 `myResourceGroup` 리소스 그룹에 `myRegistry1` 컨테이너 레지스트리를 만들고 *기본* SKU를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="16106-127">The following command uses the minimal parameters to create container registry `myRegistry1` in the resource group `myResourceGroup`, and using the *Basic* sku:</span></span>

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* <span data-ttu-id="16106-128">`--storage-account-name` 는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="16106-128">`--storage-account-name` is optional.</span></span> <span data-ttu-id="16106-129">지정하지 않으면 지정된 리소스 그룹에서 레지스트리 이름 및 타임스탬프로 구성된 이름으로 저장소 계정이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="16106-129">If not specified, a storage account is created with a name consisting of the registry name and a timestamp in the specified resource group.</span></span>

<span data-ttu-id="16106-130">레지스트리를 만들면 출력은 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="16106-130">When the registry is created, the output is similar to the following:</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T18:36:29.124842+00:00",
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry
/registries/myRegistry1",
  "location": "southcentralus",
  "loginServer": "myregistry1.azurecr.io",
  "name": "myRegistry1",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "myregistry123456789"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}

```


<span data-ttu-id="16106-131">특별 고려 사항:</span><span class="sxs-lookup"><span data-stu-id="16106-131">Take special note:</span></span>

* <span data-ttu-id="16106-132">`id` - 구독 내 레지스트리에 대한 식별자이며, 서비스 주체를 할당하려는 경우 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="16106-132">`id` - Identifier for the registry in your subscription, which you need if you want to assign a service principal.</span></span>
* <span data-ttu-id="16106-133">`loginServer` - [레지스트리에 로그인](container-registry-authentication.md)하기 위해 지정하는 정규화된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="16106-133">`loginServer` - The fully qualified name you specify to [log in to the registry](container-registry-authentication.md).</span></span> <span data-ttu-id="16106-134">이 예제의 경우 해당 이름은 `myregistry1.exp.azurecr.io`(모두 소문자)입니다.</span><span class="sxs-lookup"><span data-stu-id="16106-134">In this example, the name is `myregistry1.exp.azurecr.io` (all lowercase).</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="16106-135">서비스 주체 할당</span><span class="sxs-lookup"><span data-stu-id="16106-135">Assign a service principal</span></span>
<span data-ttu-id="16106-136">CLI 2.0 명령을 사용하여 Azure Active Directory 서비스 주체를 레지스트리에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="16106-136">Use CLI 2.0 commands to assign an Azure Active Directory service principal to a registry.</span></span> <span data-ttu-id="16106-137">이 예제의 경우 서비스 주체에 소유자 역할이 할당되어 있지만 필요하면 [다른 역할](../active-directory/role-based-access-control-configure.md)을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16106-137">The service principal in these examples is assigned the Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal-and-assign-access-to-the-registry"></a><span data-ttu-id="16106-138">서비스 주체를 만들고 레지스트리에 대한 액세스 할당</span><span class="sxs-lookup"><span data-stu-id="16106-138">Create a service principal and assign access to the registry</span></span>
<span data-ttu-id="16106-139">다음 명령에서는 새 서비스 주체에 `--scopes` 매개 변수를 통해 전달된 레지스트리 식별자에 대한 소유자 역할 액세스가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="16106-139">In the following command, a new service principal is assigned Owner role access to the registry identifier passed with the `--scopes` parameter.</span></span> <span data-ttu-id="16106-140">`--password` 매개 변수를 통해 강력한 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="16106-140">Specify a strong password with the `--password` parameter.</span></span>

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a><span data-ttu-id="16106-141">기존 서비스 주체 할당</span><span class="sxs-lookup"><span data-stu-id="16106-141">Assign an existing service principal</span></span>
<span data-ttu-id="16106-142">이미 존재하는 서비스 주체에 레지스트리에 대한 소유자 역할 액세스를 할당하려면 다음 예제와 유사한 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="16106-142">If you already have a service principal and want to assign it Owner role access to the registry, run a command similar to the following example.</span></span> <span data-ttu-id="16106-143">서비스 주체 앱 ID는 `--assignee` 매개 변수를 사용하여 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="16106-143">You pass the service principal app ID using the `--assignee` parameter:</span></span>

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a><span data-ttu-id="16106-144">관리자 자격 증명 관리</span><span class="sxs-lookup"><span data-stu-id="16106-144">Manage admin credentials</span></span>
<span data-ttu-id="16106-145">관리자 계정은 각 컨테이너 레지스트리에 대해 자동으로 생성되며 기본적으로 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="16106-145">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="16106-146">다음 예제는 컨테이너 레지스트리에 대한 관리자 자격 증명을 관리하는 `az acr` CLI 명령을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="16106-146">The following examples show `az acr` CLI commands to manage the admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="16106-147">관리자 사용자 자격 증명 가져오기</span><span class="sxs-lookup"><span data-stu-id="16106-147">Obtain admin user credentials</span></span>
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="16106-148">기존 레지스트리에 대한 관리자 사용자 활성화</span><span class="sxs-lookup"><span data-stu-id="16106-148">Enable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="16106-149">기존 레지스트리에 대한 관리자 사용자 비활성화</span><span class="sxs-lookup"><span data-stu-id="16106-149">Disable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a><span data-ttu-id="16106-150">이미지 및 태그 나열</span><span class="sxs-lookup"><span data-stu-id="16106-150">List images and tags</span></span>
<span data-ttu-id="16106-151">리포지토리의 이미지 및 태그를 쿼리하려면 `az acr` CLI 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="16106-151">Use the `az acr` CLI commands to query the images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="16106-152">현재 Container Registry는 `docker search` 명령으로 이미지 및 태그를 쿼리하도록 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16106-152">Currently, Container Registry does not support the `docker search` command to query for images and tags.</span></span>


### <a name="list-repositories"></a><span data-ttu-id="16106-153">리포지토리 나열</span><span class="sxs-lookup"><span data-stu-id="16106-153">List repositories</span></span>
<span data-ttu-id="16106-154">다음 예제는 레지스트리의 리포지토리를 JSON(JavaScript Object Notation) 형식으로 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="16106-154">The following example lists the repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="16106-155">태그 나열</span><span class="sxs-lookup"><span data-stu-id="16106-155">List tags</span></span>
<span data-ttu-id="16106-156">다음 예제는 **samples/nginx** 리포지토리의 태그를 JSON 형식으로 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="16106-156">The following example lists the tags on the **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="16106-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="16106-157">Next steps</span></span>
* [<span data-ttu-id="16106-158">Docker CLI를 사용하여 첫 번째 이미지 푸시</span><span class="sxs-lookup"><span data-stu-id="16106-158">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
