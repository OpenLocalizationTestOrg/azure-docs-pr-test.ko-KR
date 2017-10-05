---
title: "Azure Container Registry에서 Azure Container Instances에 배포 | Azure Docs"
description: "Azure Container Registry에서 Azure Container Instances에 배포"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: aa1c4ea379c10dff246e2f924a345f9fa444aa64
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-to-azure-container-instances-from-the-azure-container-registry"></a><span data-ttu-id="6a516-103">Azure Container Registry에서 Azure Container Instances에 배포</span><span class="sxs-lookup"><span data-stu-id="6a516-103">Deploy to Azure Container Instances from the Azure Container Registry</span></span>

<span data-ttu-id="6a516-104">Azure Container Registry는 Docker 컨테이너 이미지를 위한 Azure 기반의 개인 레지스트리입니다.</span><span class="sxs-lookup"><span data-stu-id="6a516-104">The Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="6a516-105">이 문서에서는 Azure Container Registry에 저장된 컨테이너 이미지를 Azure Container Instances에 배포하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6a516-105">This article covers how to deploy container images stored in the Azure Container Registry to Azure Container Instances.</span></span>

## <a name="using-the-azure-cli"></a><span data-ttu-id="6a516-106">Azure CLI 사용</span><span class="sxs-lookup"><span data-stu-id="6a516-106">Using the Azure CLI</span></span>

<span data-ttu-id="6a516-107">Azure CLI에는 Azure Container Instances에서 컨테이너를 만들고 관리하는 명령이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a516-107">The Azure CLI includes commands for creating and managing containers in Azure Container Instances.</span></span> <span data-ttu-id="6a516-108">`create` 명령에서 개인 이미지를 지정하는 경우 컨테이너 레지스트리를 사용하여 인증하는 데 필요한 이미지 레지스트리 암호를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a516-108">If you specify a private image in the `create` command, you can also specify the image registry password required to authenticate with the container registry.</span></span>

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

<span data-ttu-id="6a516-109">`create` 명령은 `registry-login-server` 및 `registry-username`도 지정하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6a516-109">The `create` command also supports specifying the `registry-login-server` and `registry-username`.</span></span> <span data-ttu-id="6a516-110">그러나 Azure Container Registry의 로그인 서버는 단순히 *registryname*.azurecr.io이며 사용자 이름은 *registryname*입니다. 따라서 이러한 값을 명시적으로 제공하지 않으면 이미지 이름에서 유추됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a516-110">However, the login server for the Azure Container Registry is always *registryname*.azurecr.io and the default username is *registryname*, so these values are inferred from the image name if not explicitly provided.</span></span>

## <a name="using-an-azure-resource-manager-template"></a><span data-ttu-id="6a516-111">Azure Resource Manager 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="6a516-111">Using an Azure Resource Manager template</span></span>

<span data-ttu-id="6a516-112">컨테이너 그룹 정의에 `imageRegistryCredentials` 속성을 포함하여 Azure Resource Manager 템플릿에서 Azure Container Registry 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a516-112">You can specify the properties of your Azure Container Registry in an Azure Resource Manager template by including the `imageRegistryCredentials` property in the container group definition:</span></span>

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

<span data-ttu-id="6a516-113">템플릿에서 바로 컨테이너 레지스트리 암호를 저장하지 않도록 하려면 [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md)에 비밀로 저장하고 [Azure Resource Manager 및 Key Vault 간의 네이티브 통합](../azure-resource-manager/resource-manager-keyvault-parameter.md)을 사용하여 템플릿에서 참조하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6a516-113">To avoid storing your container registry password directly in the template, we recommend that you store it as a secret in [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) and reference it in the template using the [native integration between the Azure Resource Manager and Key Vault](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span>

## <a name="using-the-azure-portal"></a><span data-ttu-id="6a516-114">Azure Portal 사용</span><span class="sxs-lookup"><span data-stu-id="6a516-114">Using the Azure portal</span></span>

<span data-ttu-id="6a516-115">Azure Container Registry에서 컨테이너 이미지를 유지할 경우 Azure Portal을 사용하여 Azure Container Instances에 컨테이너를 쉽게 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a516-115">If you maintain container images in the Azure Container Registry, you can easily create a container in Azure Container Instances using the Azure portal.</span></span>

1. <span data-ttu-id="6a516-116">Azure Portal에서 컨테이너 레지스트리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6a516-116">In the Azure portal, navigate to your container registry.</span></span>

2. <span data-ttu-id="6a516-117">리포지토리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6a516-117">Choose Repositories.</span></span>

    ![Azure Portal의 Azure Container Registry 메뉴][acr-menu]

3. <span data-ttu-id="6a516-119">배포하려는 리포지토리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6a516-119">Choose the repository that you want to deploy from.</span></span>

4. <span data-ttu-id="6a516-120">배포하려는 컨테이너 이미지의 태그를 오른쪽 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a516-120">Right-click the tag for the container image you want to deploy.</span></span>

    ![Azure Container Instances를 사용하여 컨테이너를 시작하기 위한 상황에 맞는 메뉴][acr-runinstance-contextmenu]

5. <span data-ttu-id="6a516-122">컨테이너에 대한 이름과 리소스 그룹에 대한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6a516-122">Enter a name for the container and a name for the resource group.</span></span> <span data-ttu-id="6a516-123">원하는 경우 기본값을 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a516-123">You can also change the default values if you wish.</span></span>

    ![Azure Container Instances의 만들기 메뉴][acr-create-deeplink]

6. <span data-ttu-id="6a516-125">배포가 완료되면 알림 창에서 컨테이너 그룹으로 이동하여 해당 IP 주소 및 기타 속성을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a516-125">Once the deployment completes, you can navigate to the container group from the notifications pane to find its IP address and other properties.</span></span>

    ![Azure Container Instances 컨테이너 그룹의 세부 정보 보기][aci-detailsview]

## <a name="next-steps"></a><span data-ttu-id="6a516-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6a516-127">Next steps</span></span>

<span data-ttu-id="6a516-128">컨테이너를 빌드하고 개인 컨테이너 레지스트리에 푸시하고 [자습서를 완료](container-instances-tutorial-prepare-app.md)하여 Azure Container Instances를 배포하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6a516-128">Learn how to build containers, push them to a private container registry, and deploy them to Azure Container Instances by [completing the tutorial](container-instances-tutorial-prepare-app.md).</span></span>

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
